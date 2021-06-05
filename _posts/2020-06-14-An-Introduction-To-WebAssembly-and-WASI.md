---
layout: post
title:  "An Introduction to WebAssembly and WASI"
date:   2020-06-14 14:53:38 -0500
categories: blog
---
These are mostly just notes that I'm taking on all the related technologies surrounding WebAssembly as I try to understand them all myself. There's a surprising amount to dig through, so I'm putting this out there in case anyone else finds it useful. A lot of this stuff is still actively being worked on and is in quite a bit of flux, so a lot of this should be considered a snapshot as of the time of writing.

First, it's important to understand that WebAssembly, despite its name, is not limited to uses cases on the web. That's where the technology was born, but it was created in such a way that it applies to many other domains. WebAssembly is a _binary instruction format_. This means source code in a number of different languages can be compiled to web assembly, similar to the way that source code is typically compiled to the machine code of whatever architecture you're targeting when you normally compile source code. 

So, just to cover the basics, typically you write source code in C or C++ for example, and then you use GCC or clang to compile your code to a specific target architecture, such as x86_64. At the end of that process, the instructions corresponding to the code you wrote are in a binary format (ELF or HEX, etc), and the resulting binary is only intelligible to a specific instruction set (also called an ISA), and thus only able to be executed on a machine that understands that ISA. 

WebAssembly is an alternative compile target. Instead of compiling to a specific ISA, you can compile to WebAssembly and end up with a .wasm file. Instead of binary instructions for a specific ISA, you would have binary instructions in a format specified by the WebAssembly spec. So, it's very crucial to understand that WebAssembly is binary instruction format and that it's a *compile target* for other programming languages.

Ok. So this is where the web comes in. To make a long story short, the majority of browsers have agreed to support WebAssembly in the browser. So, if you write code in C/C++ or Rust, etc., and compile to WebAssembly, you can call that code inside a browser.

But, WebAssembly also works outside the browser! Remember, it's *just* a binary instruction format. So if you can imagine some layer in between the WebAssembly binary and your machine's ISA, you would then be able to write source code in C/C++, compile to Wasm, and then run Wasm on any arbitrary machine that understands Wasm, as long as it can run Wasm code, even though you didn't have to target that arbitrary machine's architecture. This is the purpose of WASI, the WebAssembly System Interface specification. WASI is a specification for how Wasm code can interact with a host operating system. There are then *implementations* of the WASI spec, and there are multiple of these that exist already: wasmtime, wasmer, Lucet, and others. These are referred to as Wasm *runtimes*.

In other situations, you might not be able to run wasmtime or any of these other runtimes, such as in an embedded systems context where you don't have a full OS with a shell, or if you're doing serverless stuff, etc. In such scenarios, it's actually possible to host Wasm code inside another program. Wasmtime can be imported in a variety of languages. This could get confusing, but basically, you could run code that was written in one language, compiled to Wasm, then imported into a second language, which might be either interpreted or compiled to a different target altogether.

There's a lot more to go into, but I think that's enough to start with. There are a lot of moving pieces to this whole situation, so I hope that helps clarify the basics of these technologies.

##### References:
* [This tutorial](https://github.com/bytecodealliance/wasmtime/blob/master/docs/WASI-tutorial.md) probably helped the most
* [The Wasm spec](https://webassembly.github.io/spec/core/intro/introduction.html)
* [The WASI repository](https://github.com/WebAssembly/WASI)

{% include google_analytics.html %}
