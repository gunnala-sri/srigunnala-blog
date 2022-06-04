---
title: Build your first Alexa skill with Alexa.NET and Azure Functions
date: "2019-10-08T23:46:37.121Z"
template: "post"
draft: false
slug: "Custom-Alexa-Skill-with-Azure-Function"
category: "Alexa Custom Skill"
tags:
  - ".NET Core"
  - "Alexa Custom Skill with Azure Functions"
description: "I had a chance to play with Amazon Echo device and I was impressed by the quality of the voice interaction. It motivated me to start building a simple Alexa App. When I first heard the term Alexa Skill, I did not quite get it. Amazon came up with this creative term “Skill”, but it’s nothing but a Voice Assistance App."
socialImage: "/media/title.jpeg"
---

![Alexa Custom Skill with Azure Functions](/media/title.jpeg)

I had a chance to play with Amazon Echo device and I was impressed by the quality of the voice interaction. It motivated me to start building a simple Alexa App. When I first heard the term Alexa Skill, I did not quite get it. Amazon came up with this creative term “Skill”, but it’s nothing but a Voice Assistance App. You can build a wide verity of skills, and the most commonly used one is the custom skill. This includes things like ordering a pizza, booking a ride, or a shopping voice app.

### How do Alexa Skills Work?
Our voice request to an Alexa echo is streamed to the Alexa Could Service. This is where the actual magic happens. At Alexa Could Service, the voice stream is translated into text using ASR — Automated Speech Recognition. This text is broken up to identify user intent using NLP — Natural Language Processing. It structures user intent and passes it to the web service (REST API) which processes it and sends the response back. This response text is passed back to the echo device, and it will read it out for you using SSML — Speech Synthesis Markup Language

Here is the step by step guide to build a custom skill using Alexa.NET and Azure functions.

You need an Amazon developer account for this. If you don’t have one, create it <a href="https://developer.amazon.com/" target="_blank">here</a>.

### Build Your Custom Model First
1. Log in to your Amazon developer console and open the Alexa developer console. Locate the “Create Skill” button and click it

![Alexa Custom Skill with Azure Functions](/media/1-alexa-home.png)

2. Give a skill name (I chose “dot net”) and click on create

![Alexa Custom Skill with Azure Functions](/media/2-custom-skill.png)

3. Keep the default selection (“Start from scratch” template)

![Alexa Custom Skill with Azure Functions](/media/3-custom-skill.png)

4. You will be navigated to the Custom Model build page. Click on “Invocation” in the left pane and leave the name as is. This is the name that will be used to invoke our skill.

![Alexa Custom Skill with Azure Functions](/media/4-custom-skill.png)

5. Click on the “Add Intent” button. This carries the user intention to the back end service. It could be booking a ride, order a pizza etc. You will identify it in the back end and then process it. This one is going to be a basic one, so name it “Hello”.

![Alexa Custom Skill with Azure Functions](/media/5-custom-skill.png)

6. Click on the “Hello” intent and add utterances. When the user says these utterances, it will invoke the “Hello” Intent.

![Alexa Custom Skill with Azure Functions](/media/6-custom-skill.png)

Save the model before we move to the next step

### Build an Azure function to handle your Intents
Amazon highly recommends Lambda expressions to process voice commands. At the same time, it also supports the Microsoft ecosystem. Let’s do it with Azure functions.

1. Create an Azure function. Select “HTTP Triggers” and set “Access right” as anonymous

![Alexa Custom Skill with Azure Functions](/media/az-1.png)

2. Open your Azure function and install Alexa.NET nuget package

![Alexa Custom Skill with Azure Functions](/media/az-2.png)

3. Paste the below code into your Azure function

```cs
[FunctionName("dot-net-skill")]
public static async Task<IActionResult> Run(
            [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req,
            ILogger log)
{
    string json = await req.ReadAsStringAsync();
    var skillRequest = JsonConvert.DeserializeObject<SkillRequest>(json);
    return ProcessRequest(skillRequest);
}
private static IActionResult ProcessRequest(SkillRequest skillRequest)
{
    var requestType = skillRequest.GetRequestType();
    SkillResponse response = null;
    if (requestType == typeof(LaunchRequest))
    {
        response = ResponseBuilder.Tell("Welcome to dot net!");
        response.Response.ShouldEndSession = false;
    }
    else if (requestType == typeof(IntentRequest))
    {
        var intentRequest = skillRequest.Request as IntentRequest;
        if (intentRequest.Intent.Name == "Hello")
        {
            response = ResponseBuilder.Tell("Hi dot net Skill!");
            response.Response.ShouldEndSession = false;
        }
    }
    else if (requestType == typeof(SessionEndedRequest))
    {
        response = ResponseBuilder.Tell("See you next time!");
        response.Response.ShouldEndSession = true;
    }
    return new OkObjectResult(response);
}
```

### Integration
Now you can directly deploy this Azure function, but debugging would be tough. We will use ngrok to expose our port to a public URL and configure this in the dev console so we can debug. Follow my other post on ngrok and get the public URL for your Azure function by ngrok expose your local web server port to public . This will help you in testing before deploying it to Azure.

<a href="https://srigunnala.com/posts/2019-09-09---Expose-localhost-as-public-URL-ngrok/media/Expose-localhost-as-public-URL-ngrok" target="_blank">Expose localhost as a public URL and debug using ngrok</a>

2. Once you get the public exposed URL from ngrok, open a custom model configure endpoint in custom model.

![Alexa Custom Skill with Azure Functions](/media/az-3.png)

### Testing
Open the test console and test the skill. It would hit the debugger if you have any in Azure functions.

![Alexa Custom Skill with Azure Functions](/media/az-4.png)



