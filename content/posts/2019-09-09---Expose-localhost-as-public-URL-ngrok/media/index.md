---
title: Expose localhost as a public URL and debug using ngrok
date: "2019-09-09T23:46:37.121Z"
template: "post"
draft: false
slug: "Expose-localhost-as-public-URL-ngrok"
category: ".NET Core"
tags:
  - "ngrok"
  - "localhost tunneling to internet"
description: "ngrok is an awesome open-source tool that will expose your local port as a public URL through SSL which you can copy from the CLI. It provides secure tunnels to your localhost server."
socialImage: "/media/title.jpeg"
---

![ngrok](/media/title.jpeg)

ngrok is an awesome open-source tool that will expose your local port as a public URL through SSL which you can copy from the CLI. It provides secure tunnels to your localhost server. This means that your localhost web server will receive the request through public URL which is very handy if you need to share or demo or debug integration environments where it accepts only public URL. Let’s walk through it!

### Ngrok set up
1. Login to the official web site and register yourself
2. Download the tool (which is a single exe or dmg file)
3. Set up auth token on your local machine
4. You are ready to expose your local port to public

![ngrok](/media/setup-installation.png)

### Expose localhost REST API to a public URL and debug
This is very useful in integration where other pieces can only accept a public URL and you want to debug your REST API and see how it works. An example of this use case is Alexa Skill debugging .

The Alexa skill developer console needs a publicly accessible endpoint to process the request. Using ngrok, you can expose your localhost to a public URL and use it in Alexa developer console and debug it.

The below example exposes an Azure function to make publicly accessible. This avoids deploying it to Azure for integration testing,

1. Create an Azure function
2. Run the function and check the port that it is running on.

![ngrok](/media/az-function-running.png)

3. Open the command with your tool path and run the below command to expose your local port

```
ngrok http 7071
```
![ngrok](/media/ngrok-run.png)

Now I can configure this in the Alexa dev console and test it and share it out to the world as needed.

### Expose localhost as a web server to a public URL and debug
This is very useful if you are looking for a temporary public URL for your localhost. You can share this public URL to demo it and you can also use to test integration environments. And the best part is you can debug it. This is how you do it.

1. Create a web app and run it locally. I am using .NET Core Web app. Check the port that it is running on.

![ngrok](/media/browser-run.png)

2.  Open the command with your tool path and run the below command to expose your local port

```
ngrok http -host-header="localhost:57142" 57142
```

![ngrok](/media/ngrok-cmd-run.png)

3. Run with public address and share it with the world as needed.

![ngrok](/media/browser-run-ngrok.png)

### Troubleshooting ngrok
If ngrok is not working, it could be one of below reasons.

1. If you are behind the proxy check your proxy and firewall settings.
2. Always expose HTTP port and ngrok will give you HTTPS and redirect properly.
3. The free account will give you one URL only.

### Is ngrok safe and secure?
There is lot of debate out there about security concerns. It is open source and would monitor in/outs of your traffic. I use it only for development testing with non-sensitive data. If it worries your more, use it in docker with non-sensitive data.