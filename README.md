<p align="center">
  <a href="https://github.com/liurenju/AiBase">
    <img src="images/logo.svg" alt="AiBase Logo" width="100" height="100">
  </a>
</p>

<h1 align="center" style="border-bottom: none;">AiBase</h1>
<h2 align="center">Backend-as-a-Service for AI Applications</h2>

<p align="center">
  Build AI apps without backend headaches. 
  <br />
  <em>Community-driven, open, and built for developers.</em>
</p>

---

## Key Features

- **Flexible Billing & Usage Tracking:** Manage usage-based subscriptions, one-time credits, and real-time usage metrics automatically.
- **Unified LLM API:** Streamlined prompt handling with support for multiple models, streaming session resuming, conversation history and AI credits deduction.
- **Real-Time Analytics:** Visual dashboards to monitor user behavior, model popularity, revenue and more.
- **Open Source & Community-Driven:** Transparent, collaborative, and shaped by contributors.

---

## How It Works

AiBase condenses the entire backend workflow for AI apps into three simple steps:

### 1. Configure Billing Plans

Define subscriptions or credit packages in minutes. AiBase automates payments, tracks usage, and deducts credits—no manual work required.

#### Configure Billing Plans
*Set up credit packages and pricing tiers.*

```http
POST /api/pricing-plans
Authorization: Bearer sk_test_abc123456789
Content-Type: application/json

[
  {
    "name": "Free",
    "description": "Basic Free Plan",
    "monthly_price": 0,
    "yearly_price": 0,
    "ai_credits": 100
  },
  {
    "name": "Pro",
    "description": "For teams and growing businesses",
    "monthly_price": 50,
    "yearly_price": 500,
    "ai_credits": 10000
  }
]
```

#### Customer Purchase Flow
*A seamless credit package purchasing experience for your users.*

```javascript
const { purchasePlan } = useAiBase();

<Button
  onClick={async () => {
    const result = await purchasePlan({
      planId: "pro",
      customerId: "cus_abc123456789"
    });
    window.location.href = result.url;
  }}
/>
```

---

### 2. Connect and Use LLMs

Send prompts and parameters to your preferred LLMs through AiBase's API. Streaming, session resuming, history management, and credits deduction are all handled for you.

#### Real-time AI Streaming
*See LLM responses stream live and credits update instantly.*

```javascript
const response = await fetch("/api/llm/complete", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer sk_test_abc123456789"
  },
  body: JSON.stringify({
    model: "anthropic-claude-4-sonnet",
    messages: [
      { role: "system", content: "You are an AI software engineer." },
      { role: "user", content: "Plan and create a data pipeline for me." },
    ],
    model_kwargs: {
      temperature: 0.4,
      max_tokens: 2048
    }
    streaming: true,
    input_token_per_credit: 10000,
    output_token_per_credit: 5000,
    customer_id: "cus_abc123",
    tracing_tags: ["agent1"]
  })
})
```

#### Resume Conversations
*Seamlessly continue interrupted sessions for a better user experience.*

```javascript
const response = await fetch("/api/llm/stream/resume", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer sk_test_abc123456789"
  },
  body: JSON.stringify({
    session_id: "sess_1234567890"
  })
});
```

#### Conversation History
*Access and manage previous conversations easily.*

```javascript
const customerId = "cus_abc123";
const limit = 20;
const offset = 0;
const sessionId = "sess_1234567890";

const params = new URLSearchParams({
  customer_id: customerId,
  limit: limit,
  offset: offset,
  session_id: sessionId
});

const response = await fetch(
  `/api/history?${params}`,
  {
    headers: {
      Authorization: "Bearer sk_test_abc123456789"
    }
  }
);
```

---

### 3. Track & Optimize

Monitor your AI app's performance in real time. Get actionable insights into user behavior, model popularity, and revenue. All from your dashboard.

#### User Behavior Analytics
*Track how users interact with your AI features.*
<p align="center">
  <img src="images/analysis/user-behavior.png" alt="User behavior analytics" width="700"/>
</p>

#### AI Assisted Analysis
*Ask our AI assistant anything about user performance and behavior.*
<p align="center">
  <img src="images/analysis/ai-user-behavior.png" alt="AI user behavior insights" width="700"/>
</p>

---

## Roadmap

We're building AiBase in the open, with the community. Here's what's coming up:

- **Full Auth Support:** Comprehensive authentication and authorization for users and teams.
- **Long-Term Memory Store:** Persistent storage for conversations and user data.
- **RAG/Knowledge Base Integrations:** Support for Retrieval-Augmented Generation and knowledge base.
- **Serverless Function Runtime:** Run custom backend logic and webhooks with ease.
- **Community Feature Requests:** Top requests from users prioritized for future releases.

Want something? [Open an issue](https://github.com/liurenju/AiBase/issues) or upvote your favorites!

---

## Getting Started

Coming soon.

---

## Contributing

We welcome contributions! Whether it's bug fixes, feature suggestions, or documentation, your input helps shape AiBase. Fork the repo and submit a pull request, or start a discussion in the issues.

---

## Who's Using AiBase

AiBase is already powering production AI applications:

- **[SellToSky](https://www.selltosky.com)** – Automatically build shopping storefronts from products with AiBase's scalable backend and analytics.

---

## License

Distributed under the Apache License. See [`LICENSE`](./LICENSE) for details.