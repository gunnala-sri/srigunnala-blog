---
title: What is Deno.js and how it is different from Node
date: "2020-05-05"
template: "post"
draft: false
slug: "DenoJS-and-how-it-is-different-from-node"
category: "Node"
tags:
  - "NodeJS"
  - "DenoJS"
description: "Deno is a javascript runtime same as Node, reached its 1.0 release status on May 13, 2020. Deno was developed by Ryan Dahl, the same person who developed Node. Two Javascript run-times by same person."
socialImage: "/media/notebook.jpg"
---

![Welcome to Deno World!](/media/dino.jpg)

Deno is a javascript runtime same as Node, reached its 1.0 release status on May 13, 2020. Deno was developed by Ryan Dahl, the same person who developed Node. Two Javascript run-times by same person . This raises many questions — What made Ryan to develop another Javascript runtime? What is wrong with Node? Is Deno going to replace Node? Lets find answers to all of these.

### Why Deno.js ?

Node was designed in 2009 when Javascript was a much different language. Since then, through standards organisations like ECMA International, the Javascript has been improved continuously. For instance, there was no Promises or async/await when Node was developed. Node’s counterpart to promises was the EventEmitter which has back-pressure issue and later it was mitigated with extra code.

On other hand, out of necessity, Node had to invent concepts which were later taken up by the standards organisations and added to the language differently.

With continuous evolution of Javascript and new additions like TypeScript, building and managing Node project needed extra heavy lifting work. Since Node first release, Javascript and its eco system has changed enough to consider simplifying Node.

In a single line, Node has redesigned to Deno to fix it flaws.

If you are curious and wanting to understand the design mistakes of Node, check this out below video by Ryan Dahl — <a href="https://www.youtube.com/watch?v=M3BM9TB-8yA" target="_blank">Regret about Node.js</a>

### What is Deno ?
According to Deno official page, Deno is ‘A secure runtime for JavaScript and TypeScript’. This definition has very close match to Node except the terms security and Tyepscript. Lets understand this a bit more with a Deno sample and find out how it is different from Node.

### How to install Deno?
I am running windows, so I installed it using power shell. For all install options, look at <a href="https://github.com/denoland/deno_install" target="_blank">here.</a>

```
iwr https://deno.land/x/install/install.ps1 -useb | iex
```

![Power Sheel Run](/media/power-shell.png)

Run the command “deno -V” to confirm successful installation. This will give the current version (1.0 as of writing this) of deno.

### A simple Deno Code
Here is the simple typescript code in Deno.

![Sample Deno Code](/media/deno-code.png)

We are importing **serve** from a web resource, spinning up the server at port 8000 and listening to it. Run the code with below command.

```
deno run sample.ts
```

![Deno Run](/media/deno-run.png)

This will throw an error — Uncaught PermissionDenied error.

Before we fix the error, let’s dig deeper to understand how this code is different from Node.

### How Deno is different from Node

1. **Typescript** — If you look at the example, it is a typescript file. Yes, Out of the box, deno support Typescript as well without the need of manual compilation. The Typescript compiler is built into deno. You can write all the code in Typescript.
2. **Importing packages** — In deno, you don’t need to install any module to import them into code. Instead, you import from web server. In the example above, we imported server from web server url. When you run the code, it downloads all imports from web server, catches it locally so it doesn’t need to download them again when you run next time.
3. **Promises/async iterables** — In our sample code, the for loop was an infinite array of incoming data and events. Await command doesn’t need to be wrapped up in an async function, deno also supports top level await. We don’t need any wrapper around await.
4. **Secure runtime** — With node when we import third party packages, we don’t have much visibility and control over it. We are relying on the maintainers of the package and trusting them they don’t write any harmful code under the hood. With deno, we control which permissions we give to our script to execute them. By default, there will be no permissions. This is the reason why our sample got an error Uncaught PermissionDenied error. In our sample we need network access, so we need passing another flag to give those extra permissions. So, deno is considered to be highly secured than Node.

### Deno or Node?
Deno is alternative to Node. But it is very new, immature and it will have bugs. It has been in the development for 2 years now and there will be a lot of development in coming year. Deno initial release 1.0 is stable, however it might not be the right choice for everyone right now. Deno is not compatible with Node packages. All the functionality which is not yet ready for stabilisation has been hidden under the ‘- -unstable’ command line flag.

With all these, Node is not going any where. It is a huge ecosystem and lot of company still uses it. Deno will co-exist with Node and might play an important role in the future. But, it is still nice to dive in to start play around with it and do some experiments.