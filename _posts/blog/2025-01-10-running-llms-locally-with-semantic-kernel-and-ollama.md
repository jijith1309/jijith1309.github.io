---
title: "Running LLMs Locally with Semantic Kernel and Ollama"
date: 2025-01-10
layout: post
categories: [blog]
tags: [semantic-kernel, ollama, dotnet, ai]
description: "How I set up a local LLM workflow using Semantic Kernel and Ollama in .NET — no cloud, no costs."
---

There's something satisfying about running an LLM entirely on your own machine. No API keys to rotate, no billing surprises at the end of the month, no rate limits during experiments. When I started building AI features, I wanted a local setup first before touching any cloud endpoints. That's where Ollama came in.

Ollama is a tool that lets you pull and run open-source models — Llama 3, Mistral, Gemma — locally. It exposes a simple HTTP endpoint, so connecting it to .NET is straightforward.

## Setting It Up

Install Ollama from [ollama.com](https://ollama.com), then pull a model:

```bash
ollama pull llama3.2
```

In your .NET project, connect via Semantic Kernel:

```csharp
var kernel = Kernel.CreateBuilder()
    .AddOllamaChatCompletion("llama3.2", new Uri("http://localhost:11434"))
    .Build();

var result = await kernel.InvokePromptAsync("Explain REST APIs in 2 sentences.");
Console.WriteLine(result);
```

That's basically it for a working setup.

## Why Semantic Kernel Instead of Direct HTTP?

You could hit the Ollama endpoint directly with `HttpClient`. It works. But Semantic Kernel gives you a consistent abstraction — when you eventually move to Azure OpenAI or any other provider, the builder config changes but the rest of the code stays the same. That portability is worth something when you're prototyping.

## What I Actually Used This For

Mostly testing prompt templates without burning Azure credits during development. Write a prompt locally against Llama, iterate until it works well, then test on the actual cloud model before committing. It saved me a fair bit on my Azure bill and made the feedback loop much faster.

The smaller 7B models aren't GPT-4. For complex reasoning tasks, the gap shows. But for structured data extraction, summarization, or classification? More than enough for development.

## One Thing That Caught Me Out

Make sure Ollama is actually running before you start the .NET app. If it's not, you get a connection refused error and spend 10 minutes wondering what's broken. Speaking from experience there.

Full code is in my [ai-apps-collection](https://github.com/jijith1309/ai-apps-collection) repo under `1_semantic-kernel-ollama-connection`.
