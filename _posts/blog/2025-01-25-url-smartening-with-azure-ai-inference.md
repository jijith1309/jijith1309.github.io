---
title: "Making URLs Smarter with Azure AI Inference"
date: 2025-01-25
layout: post
categories: [blog]
tags: [azure-ai, dotnet, seo, automation]
description: "Using Azure AI Inference to auto-generate SEO metadata from URLs in .NET"
---

At Socxo, we deal with a lot of URLs. Socxly handles link shortening and tracking, and one thing users always asked for was smarter metadata — better titles, descriptions, tags — without having to fill them in manually every time.

The `2-url-smartening` project in my [AI Apps Collection](https://github.com/jijith1309/ai-apps-collection) shows how to use Azure AI Inference to analyze a URL and return useful metadata automatically.

## The Basic Idea

You pass in a URL. The app fetches the page content, sends it to an Azure AI model, and gets back a structured response: title, description, relevant tags, topic category. The user can approve or edit it, but most of the time it's close enough to use directly.

```csharp
var client = new ChatCompletionsClient(
    new Uri(endpoint),
    new AzureKeyCredential(apiKey));

var response = await client.CompleteAsync(new ChatCompletionsOptions
{
    Messages = {
        new ChatRequestUserMessage(
            $"Analyze this URL content and return JSON with title, description, and tags:\n\n{pageContent}")
    },
    ResponseFormat = ChatCompletionsResponseFormat.JsonObject
});
```

## Getting Consistent Output

The part I spent the most time on was reliable structured output. Models don't always return valid JSON, especially with a loose prompt. I ended up using the `JsonObject` response format and validating the output before doing anything with it. When validation fails, the app falls back to simpler text extraction from the page's own meta tags.

That fallback is important. AI-generated output works most of the time, but "most of the time" isn't good enough for a production link tool.

## Why This Is Actually Useful

For a link management product, this is genuinely valuable. Users paste a URL, the app suggests metadata in under two seconds, they click approve. Compared to manually copying the page title and writing a description yourself, it's a noticeable improvement. Small features like this get disproportionately positive feedback.

## The Azure AI Inference SDK

If you're starting a new project and don't need the full Azure OpenAI SDK, the Azure AI Inference SDK is lighter and works well with models deployed through Azure AI Foundry. Worth knowing if you're greenfielding something.
