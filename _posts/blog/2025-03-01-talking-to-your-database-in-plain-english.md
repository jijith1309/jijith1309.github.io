---
title: "Talking to Your Database in Plain English"
date: 2025-03-01
layout: post
categories: [blog]
tags: [dotnet, ai, sql, agents, natural-language]
description: "Using .NET and Azure AI to convert natural language questions into SQL queries and execute them"
---

"Show me all users who signed up last month and haven't logged in yet."

Your product manager asks this. You translate it to SQL in 30 seconds because you know the schema. But what if they could ask it directly, without going through you?

That's what the `6-agentic-sql` project does: take a plain English question, convert it to SQL, execute it, and return results. The code is in my [AI Apps Collection](https://github.com/jijith1309/ai-apps-collection).

## The Core Loop

The tricky part isn't generating SQL — models are decent at that. The real challenges are:

1. The model needs to know your database schema
2. Generated SQL should be validated before running
3. If it fails, you need to retry with the error as feedback

I went with a straightforward approach: inject the schema into the system prompt, generate SQL, execute it, and if it fails, send the error back and ask for a fix.

```csharp
var systemPrompt = $"""
    You are a SQL query generator for SQL Server.
    Given a plain English question, write a valid SQL SELECT query.

    Database schema:
    {schemaDescription}

    Return only the SQL query. No explanation, no markdown.
    """;

var sql = await GenerateSqlAsync(userQuestion, systemPrompt);
var result = await ExecuteSafelyAsync(sql);
```

## The "Safely" Part Is Not Optional

The sample runs queries in read-only mode. `DELETE`, `UPDATE`, `DROP` — none of that runs. This is non-negotiable for anything beyond a personal experiment. Even in read-only mode, you want to validate the SQL before execution, not after.

Restricting to SELECT queries or running against a read replica are both good approaches depending on your setup.

## Where This Is Actually Useful

Internal tooling. Give your support team or analysts a natural language interface to query data without needing SQL knowledge. It won't replace proper dashboards for structured reporting, but for ad-hoc questions — "how many users from Kerala signed up this week?" — it works well and saves back-and-forth with the dev team.

The sample is minimal. Extending it with your actual schema and proper access controls is the next step for real deployment.
