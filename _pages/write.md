---
layout: page
title: Text Editor
permalink: /write
---

> Write: A text editor in C++
>
> January 2020
>
> [https://github.com/pmusgrave/write](https://github.com/pmusgrave/write)

Based on this list of [challenging projects every programmer should try](http://web.eecs.utk.edu/~azh/blog/challengingprojects.html), I started playing around with text editors and thinking about the data structure challenges involved in making a performant text editor. As a side note, my approach to working on learning projects is to try to think about them on my own completely from first principles without coloring my approach with existing solutions. So, I didn't read what the article says about text editor data structures and just dove right into it. After I've gotten into the details of a project, then I like to do a little research and see what else is out there. I just feel like I learn more by working on the problem in isolation and it results in a stronger learning experience.

The main challenge in writing a text editor is in how to store text in memory in a way that it can be modified at any arbitrary cursor position. To illustrate, one could naively store a text file as a character buffer array and increment a pointer when each new character is inserted. However, this approach has poor performance in most situations because inserting anything into the middle of the buffer requires shifting every following element by one. In the worst case, therefore, this approach is O(n) for every single character insertion.

My approach to this was to use a linked list instead of an array to allow O(1) insertion and deletion. However, I didn't just use a simple linked list for the entire buffer because this results in poor performance for a lot of situations other than inserting/deleting. Instead, I created a new linked list for every newline in the buffer, and then I store the head pointers in a C++ std::vector. With this approach, moving the cursor left/right is equivalent to advancing through the linked list, and moving the cursor up/down is equivalent to iterating through the line vector. This approach felt like a good balance between simplicity and performance. It's not the most performant solution to this problem, because you might be dealing with a large text buffer that has no newlines for instance. But I felt like the approach I came up with struck a good balance between ease of use in the API on the one hand and performance on the other.

{% include google_analytics.html %}