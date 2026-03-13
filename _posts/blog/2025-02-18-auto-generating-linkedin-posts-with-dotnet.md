---
title: "Auto-generating LinkedIn Posts with .NET — Lazy or Smart?"
date: 2025-02-18
layout: post
categories: [blog]
tags: [dotnet, ai, linkedin, content-generation]
description: "Using .NET and AI to generate LinkedIn post drafts from topics or article links"
---

I'll be honest: I'm bad at posting on LinkedIn. I have things to share, but sitting down to write the post — the opening line, the hashtags, that particular LinkedIn tone — I keep putting it off until the moment has passed.

So I built something to handle the annoying part.

The `4-social-post-generation` project in my [AI Apps Collection](https://github.com/jijith1309/ai-apps-collection) generates LinkedIn post drafts from a topic or article URL. You give it input, it returns a ready-to-edit draft.

## What It Generates

- An opening line that doesn't start with "I'm excited to share..."
- The main insight or takeaway in 2-3 short paragraphs
- A question or call-to-action at the end
- 3-5 relevant hashtags

## The Prompt Matters More Than the Code

```csharp
var prompt = $"""
    Write a LinkedIn post about: {input}

    Requirements:
    - Start with a hook — a question, a surprising fact, or a direct statement
    - Keep it under 300 words
    - Write like a developer sharing a genuine insight, not a press release
    - End with a question or call to action
    - Include 3-5 relevant hashtags at the end
    - Do not start with "I'm excited to", "Thrilled to announce", or similar
    """;
```

I spent more time on the prompt than on the code itself. Generic instructions produce generic LinkedIn-speak. Being specific about tone and including explicit anti-examples cuts down specific failure modes.

## Is This Actually Useful?

It depends on how you use it. Publishing the raw output without reading it is probably not a good idea — the posts come out slightly flat. But as a starting point to edit from, it solves the blank-page problem.

My workflow: take the draft, rewrite 2-3 sentences to make it sound like me, post. Takes 5 minutes instead of 30, and I actually do it instead of skipping it.

For teams that need to share product updates or release notes regularly, this kind of automation is genuinely useful. The code is simple enough to adapt for any content type — blog posts, event announcements, product releases.
