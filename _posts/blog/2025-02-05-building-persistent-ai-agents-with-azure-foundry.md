---
title: "Building Persistent AI Agents with Azure AI Foundry"
date: 2025-02-05
layout: post
categories: [blog]
tags: [azure-ai, agents, dotnet, ai-foundry]
description: "Creating server-side AI agents that maintain state across conversations using the Azure AI Agents SDK"
---

Most AI demos show a single-turn exchange: user sends a message, model replies, done. Real applications are messier. Users ask follow-up questions, agents need context from earlier in the conversation, and sessions last longer than one message.

Azure AI Foundry's agent service handles this with a server-side thread model. Your agent runs in Azure, state is maintained there, and you communicate with it over simple API calls. The `3-agent-foundry-model-basic` project shows how this works.

## How the Thread Model Works

You create an agent once with instructions and a model. For each user session, you create a thread. Messages go into the thread, and the agent processes them with full conversation history available.

```csharp
var agentsClient = new AgentsClient(endpoint, new DefaultAzureCredential());

// Create the agent (do this once, reuse the ID)
var agent = await agentsClient.CreateAgentAsync(
    model: "gpt-4o",
    name: "DevAssistant",
    instructions: "You are a helpful assistant for software developers.");

// One thread per user session
var thread = await agentsClient.CreateThreadAsync();

// Add a message and run
await agentsClient.CreateMessageAsync(thread.Value.Id, MessageRole.User, "What is dependency injection?");
var run = await agentsClient.CreateRunAsync(thread.Value.Id, agent.Value.Id);
```

## What's Different from Regular Chat Completions

With regular chat completions, you manage the conversation history yourself — sending the full message list on every request. With agents and threads, Azure manages that for you. It also handles tool calls, file retrieval, and code execution if you enable those capabilities.

For simple back-and-forth chat, the difference is mostly architectural. For multi-step tasks where an agent needs to call tools and track progress across turns, the thread model is significantly cleaner.

## Where It Gets Interesting

Once the basics are working, you can add tools — functions the agent can call, files it can search, code it can run. The sample in the repo stays minimal, but it's the right foundation to build on.

If you're building a support bot or an internal task automation agent, this is production-viable architecture. You're offloading thread storage, concurrency, and tool orchestration to Azure, which is one less infrastructure concern.

The agent ID persists across restarts, so you create it once and store the ID. Thread IDs map to user sessions. It's a clean model once you get your head around it.
