---
name: claude-agent-sdk-reference
displayName: Claude Agent SDK Reference
description: Comprehensive reference for Claude Agent SDK - TypeScript and Python SDKs for building AI agents
version: "1.0.0"
author: iyein
tags:
  - agent
  - sdk
  - typescript
  - python
  - claude
  - anthropic
keywords:
  - agent
  - agent sdk
  - anthropic
  - claude
  - 에이전트
  - sdk
triggers:
  - pattern: "agent"
    scope: keyword
  - pattern: "sdk"
    scope: keyword
  - pattern: "에이전트"
    scope: semantic
  - pattern: "anthropic"
    scope: keyword
  - pattern: "claude.*sdk"
    scope: semantic
context7_libraries:
  - name: "@anthropic-ai/sdk"
    version: "latest"
  - name: "@anthropic-ai/agent-sdk"
    version: "latest"
---

# Agent SDK Comprehensive Reference

## Overview

The Claude Agent SDK provides powerful tools for building AI agents with Claude. It includes official SDKs for TypeScript and Python, enabling developers to create intelligent agents with tool use, memory, and complex reasoning capabilities.

---

## Documentation Links

### Main Documentation

| Section | Link | Description |
|---------|------|-------------|
| **Agent SDK Overview** | https://docs.anthropic.com/en/docs/agent-sdk/overview | Introduction to Agent SDK concepts and architecture |
| **Quickstart** | https://docs.anthropic.com/en/docs/agent-sdk/quickstart | Get started with Agent SDK in minutes |

---

### TypeScript SDK

| Section | Link | Description |
|---------|------|-------------|
| **TypeScript SDK** | https://docs.anthropic.com/en/docs/agent-sdk/typescript | Official TypeScript Agent SDK documentation |
| **TypeScript V2 (Preview)** | https://docs.anthropic.com/en/docs/agent-sdk/typescript-v2-preview | Next-generation TypeScript SDK (preview) |

---

### Python SDK

| Section | Link | Description |
|---------|------|-------------|
| **Python SDK** | https://docs.anthropic.com/en/docs/agent-sdk/python | Official Python Agent SDK documentation |

---

### Migration Guide

| Section | Link | Description |
|---------|------|-------------|
| **Migration Guide** | https://docs.anthropic.com/en/docs/agent-sdk/migration-guide | Migrate from older SDK versions |

---

### Guides

| Section | Link | Description |
|---------|------|-------------|
| **Guides** | https://docs.anthropic.com/en/docs/agent-sdk/guides | Comprehensive guides for common use cases |

---

## Quick Reference

### TypeScript SDK Setup

```bash
# Install TypeScript SDK
npm install @anthropic-ai/sdk

# Or with Yarn
yarn add @anthropic-ai/sdk

# Or with pnpm
pnpm add @anthropic-ai/sdk
```

### Python SDK Setup

```bash
# Install Python SDK
pip install anthropic

# Or with pipenv
pipenv install anthropic

# Or with poetry
poetry add anthropic
```

---

## Code Examples

### TypeScript - Basic Agent

```typescript
import { Anthropic } from '@anthropic-ai/sdk';

const client = new Anthropic({
  apiKey: process.env.ANTHROPIC_API_KEY,
});

async function basicAgent() {
  const message = await client.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 1024,
    messages: [{
      role: 'user',
      content: 'Hello, Claude!'
    }]
  });

  console.log(message.content[0].text);
}
```

### Python - Basic Agent

```python
import anthropic

client = anthropic.Anthropic(
    api_key=os.environ["ANTHROPIC_API_KEY"]
)

def basic_agent():
    message = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        messages=[
            {"role": "user", "content": "Hello, Claude!"}
        ]
    )

    print(message.content[0].text)
```

---

### TypeScript - Agent with Tools

```typescript
import { Anthropic } from '@anthropic-ai/sdk';

const client = new Anthropic({
  apiKey: process.env.ANTHROPIC_API_KEY,
});

const tools = [
  {
    name: 'get_weather',
    description: 'Get the current weather in a given location',
    input_schema: {
      type: 'object',
      properties: {
        location: {
          type: 'string',
          description: 'The city and state, e.g. San Francisco, CA'
        },
        unit: {
          type: 'string',
          enum: ['celsius', 'fahrenheit'],
          description: 'The temperature unit'
        }
      },
      required: ['location']
    }
  }
];

async function agentWithTools() {
  const message = await client.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 1024,
    tools: tools,
    messages: [{
      role: 'user',
      content: 'What is the weather in Seoul?'
    }]
  });

  // Handle tool use
  console.log(message.content);
}
```

### Python - Agent with Tools

```python
import anthropic

client = anthropic.Anthropic(api_key=os.environ["ANTHROPIC_API_KEY"])

tools = [
    {
        "name": "get_weather",
        "description": "Get the current weather in a given location",
        "input_schema": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "The city and state, e.g. San Francisco, CA"
                },
                "unit": {
                    "type": "string",
                    "enum": ["celsius", "fahrenheit"],
                    "description": "The temperature unit"
                }
            },
            "required": ["location"]
        }
    }
]

def agent_with_tools():
    message = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        tools=tools,
        messages=[
            {"role": "user", "content": "What is the weather in Seoul?"}
        ]
    )

    print(message.content)
```

---

### TypeScript - Streaming Agent

```typescript
import { Anthropic } from '@anthropic-ai/sdk';

const client = new Anthropic({
  apiKey: process.env.ANTHROPIC_API_KEY,
});

async function streamingAgent() {
  const stream = await client.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 1024,
    stream: true,
    messages: [{
      role: 'user',
      content: 'Count from 1 to 10'
    }]
  });

  for await (const event of stream) {
    if (event.type === 'content_block_delta') {
      process.stdout.write(event.delta.text);
    }
  }
}
```

### Python - Streaming Agent

```python
import anthropic

client = anthropic.Anthropic(api_key=os.environ["ANTHROPIC_API_KEY"])

def streaming_agent():
    with client.messages.stream(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        messages=[{"role": "user", "content": "Count from 1 to 10"}]
    ) as stream:
        for text in stream.text_stream:
            print(text, end="", flush=True)
```

---

## Agent SDK Features

### Core Capabilities

| Feature | Description |
|---------|-------------|
| **Tool Use** | Enable Claude to call external functions and APIs |
| **Streaming** | Real-time token streaming for responsive UX |
| **Multi-turn Conversations** | Maintain conversation context across messages |
| **System Prompts** | Set agent behavior and personality |
| **Image Analysis** | Process and analyze images with vision |
| **JSON Mode** | Get structured JSON output |

### Available Models

| Model | Description | Max Tokens |
|-------|-------------|------------|
| `claude-3-5-sonnet-20241022` | Most capable model for complex tasks | 200K |
| `claude-3-5-haiku-20241022` | Fast, efficient model for simple tasks | 200K |
| `claude-3-opus-20240229` | Previous generation flagship | 200K |

---

## Common Use Cases

### 1. Building a Chatbot

```typescript
// TypeScript
const chatHistory = [];

async function chat(userMessage: string) {
  chatHistory.push({ role: 'user', content: userMessage });

  const response = await client.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 1024,
    messages: chatHistory
  });

  const assistantMessage = response.content[0].text;
  chatHistory.push({ role: 'assistant', content: assistantMessage });

  return assistantMessage;
}
```

```python
# Python
chat_history = []

def chat(user_message: str) -> str:
    chat_history.append({"role": "user", "content": user_message})

    response = client.messages.create(
        model="claude-3-5-sonnet-20241022",
        max_tokens=1024,
        messages=chat_history
    )

    assistant_message = response.content[0].text
    chat_history.append({"role": "assistant", "content": assistant_message})

    return assistant_message
```

### 2. Function Calling

```typescript
// Define your tool
const searchTool = {
  name: 'search_database',
  description: 'Search the product database',
  input_schema: {
    type: 'object',
    properties: {
      query: { type: 'string', description: 'Search query' }
    },
    required: ['query']
  }
};

// Claude will request to use this tool when needed
```

### 3. Document Analysis

```typescript
async function analyzeDocument(document: string) {
  const message = await client.messages.create({
    model: 'claude-3-5-sonnet-20241022',
    max_tokens: 4096,
    messages: [{
      role: 'user',
      content: `Analyze this document:\n\n${document}`
    }]
  });

  return message.content[0].text;
}
```

---

## API Reference

### Message Creation Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `model` | string | ✅ | Model ID to use |
| `max_tokens` | integer | ✅ | Maximum tokens to generate |
| `messages` | array | ✅ | Conversation history |
| `system` | string | ❌ | System prompt |
| `tools` | array | ❌ | Available tools |
| `stream` | boolean | ❌ | Enable streaming (default: false) |
| `temperature` | number | ❌ | Randomness (0-1) |

### Response Structure

```typescript
{
  id: string,
  type: "message",
  role: "assistant",
  content: [
    {
      type: "text",
      text: string
    }
  ],
  model: string,
  stop_reason: string,
  usage: {
    input_tokens: number,
    output_tokens: number
  }
}
```

---

## Best Practices

### 1. API Key Security

```typescript
// NEVER hardcode API keys
const client = new Anthropic({
  apiKey: process.env.ANTHROPIC_API_KEY,  // ✅ Good
});
```

```python
# Python
import os

client = anthropic.Anthropic(
    api_key=os.environ["ANTHROPIC_API_KEY"]  # ✅ Good
)
```

### 2. Error Handling

```typescript
try {
  const response = await client.messages.create({...});
} catch (error) {
  if (error instanceof Anthropic.APIError) {
    console.error('API Error:', error.message);
  } else {
    console.error('Unexpected error:', error);
  }
}
```

```python
try:
    response = client.messages.create(...)
except anthropic.APIError as e:
    print(f"API Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

### 3. Token Management

```typescript
// Monitor usage to control costs
const response = await client.messages.create({
  model: 'claude-3-5-sonnet-20241022',
  max_tokens: 1024,  // Set appropriate limit
  messages: [...]
});

console.log(`Input: ${response.usage.input_tokens} tokens`);
console.log(`Output: ${response.usage.output_tokens} tokens`);
```

---

## Migration Guide

### From V1 to V2 (TypeScript)

| V1 | V2 |
|----|----|
| `client.completions.create()` | `client.messages.create()` |
| `prompt` parameter | `messages` array |
| `stream: true` in options | Use `client.messages.stream()` |

### Example Migration

```typescript
// V1 (Old)
const completion = await client.completions.create({
  model: 'claude-2',
  prompt: 'Hello, world!',
  max_tokens_to_sample: 1024
});

// V2 (New)
const message = await client.messages.create({
  model: 'claude-3-5-sonnet-20241022',
  messages: [{ role: 'user', content: 'Hello, world!' }],
  max_tokens: 1024
});
```

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     Your Application                    │
│                  (TypeScript/Python)                    │
└───────────────────────┬─────────────────────────────────┘
                        │
                        │ SDK Calls
                        ▼
┌─────────────────────────────────────────────────────────┐
│                   Agent SDK (Client)                     │
│  • Message Creation  • Tool Management  • Streaming     │
└───────────────────────┬─────────────────────────────────┘
                        │
                        │ HTTP API
                        ▼
┌─────────────────────────────────────────────────────────┐
│                    Anthropic API                         │
│  • Claude Models  • Tool Execution  • Context Handling  │
└─────────────────────────────────────────────────────────┘
```

---

## Related Resources

| Resource | Link |
|----------|------|
| **Anthropic API Docs** | https://docs.anthropic.com/ |
| **Claude Models** | https://docs.anthropic.com/en/docs/about-claude/models |
| **Prompt Engineering** | https://docs.anthropic.com/en/docs/prompts |
| **Tool Use Guide** | https://docs.anthropic.com/en/docs/tool-use |

---

## Related Skills

- `moai-foundation-claude`: Claude Code authoring kit
- `moai-lang-typescript`: TypeScript development specialist
- `moai-lang-python`: Python development specialist

---

**Last Updated**: 2026-01-26
**SDK Version**: Latest
