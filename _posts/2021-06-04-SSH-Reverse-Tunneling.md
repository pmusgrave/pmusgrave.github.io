---
layout: post
title:  "SSH Reverse Tunneling"
date:   2021-06-04 05:11:09 -0500
categories: blog
---
If you've ever wanted to set up push notifications from an API using webhooks to a server running on your local machine, SSH reverse tunneling can make this relatively easy to do. In this example, I'll be using the Google Calendar API, a Google Cloud Compute Engine VM, and SSH. There are instructions elsewhere for how to set up a Google Cloud VM, so I'll assume you have a Compute Engine instance with SSH access already configured and ready to go. Really any public server with a static IP address and SSH access would work perfectly well for this, if you use another provider.

A lot of APIs offer push notifications using [webhooks](https://en.wikipedia.org/wiki/Webhook). Generally, to use a webhook, your application sends an HTTP request and registers a watch notification request on some resource, with a specified callback URL. Whenever that resource changes, the API server will send an HTTP request to whatever callback URL you gave them. 

This avoids the need to continually poll the API and see if anything changes, which has at least two main advantages. First, it reduces the amount of network requests and removes all the traffic involved with constant polling. Second, it removes the delay between when the resouce changes and when your application detects that change due to the polling frequency.

The problem I run into a lot of the time is that I have some server running on my local machine that I'd like to handle these webhooks. But there's no straightforward way to register a local machine as the callback URL, at least not without a static IP address. That's where the cloud VM and SSH reverse tunneling come in. The Google Cloud free tier includes a VM that you can SSH into, as well as static IP address assignment. 

The method I describe here can result in API push notifications without spending any money on a static IP address or ngrok or some other service, all while staying within the Google Cloud free tier limits.

#### Instructions
First, [we assign the VM a static IP](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address).

There will be some web server configuration involved on the VM, and this will vary depending on what web server you choose to use. In the case of the Google Calendar API specifically, the webhook address must use HTTPS, so the server must be configured to use SSL/TLS. Here's an example nginx configuration:
```
server {
    server_name <static_ip_address>;
    listen 443 ssl;
    ssl_certificate /path/to/ssl/certificate
    ssl_certificate_key /path/to/certificate/key

    location / {
        proxy_pass http://localhost:<tunnel_port>;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
    }
}
```

Then, we [register the webhook](https://developers.google.com/calendar/v3/push#creating-notification-channels) using that static IP address as the callback address.

Finally, we use SSH on our local machine to forward traffic from the VM to our local machine. Any requests that come into the VM will be tunneled to whatever port we specify on our local machine.

`ssh -R <remote_port>:localhost:<local_port>`

Some other flags that might be useful (copied from ssh(1)):
```
-f      Requests ssh to go to background just before command execution.  This is useful if ssh
             is going to ask for passwords or passphrases, but the user wants it in the background.
             This implies -n.  The recommended way to start X11 programs at a remote site is with
             something like ssh -f host xterm
-N      Do not execute a remote command.  This is useful for just forwarding ports.
-T      Disable pseudo-terminal allocation.
```

#### Example
To give a more concrete example, let's say you wanted to forward webhook traffic to your local machine on port 3000, via port 4000 on the remote server. You would set the `<tunnel_port>` option in the ngingx server configuration block above to 4000:

```proxy_pass http://localhost:4000;```

And then the SSH command on the local machine would look like this:

```ssh -R 4000:localhost:3000 -NTf```

{% include google_analytics.html %}
