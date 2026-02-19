# 🚀 NOVA AI — Complete Deployment Guide
### Make Your AI Website Fully Live (Free!)

---

## 🔑 STEP 1: Get Your Anthropic API Key

An **API key** is like a password that lets your website talk to the AI brain.
It's free to get started!

1. Go to 👉 **https://console.anthropic.com/**
2. Click **"Sign Up"** and create a free account
3. After logging in, click **"API Keys"** in the left menu
4. Click **"Create Key"** → give it a name like "NOVA AI"
5. **Copy the key** — it looks like: `sk-ant-api03-xxxxxxxx...`
6. ⚠️ Save it somewhere safe — you'll need it in Step 3

---

## 📁 STEP 2: Create a GitHub Account (Free)

GitHub stores your website files online.

1. Go to 👉 **https://github.com/**
2. Click **"Sign Up"** → create a free account
3. After logging in, click the **"+"** icon → **"New Repository"**
4. Name it: `nova-ai-website`
5. Make sure it's set to **Public**
6. Click **"Create Repository"**
7. Click **"uploading an existing file"**
8. Upload the `nova-ai.html` file you downloaded
9. Click **"Commit Changes"**

---

## ⚙️ STEP 3: Add a Backend (For Live AI Chat)

Because API keys must be kept secret, you need a tiny backend.
We'll use **Netlify Functions** — it's free and easy!

### Create this folder structure:
```
nova-ai-website/
├── index.html          ← (rename nova-ai.html to this)
└── netlify/
    └── functions/
        └── chat.js     ← (create this new file)
```

### Contents of `netlify/functions/chat.js`:
```javascript
exports.handler = async (event) => {
  if (event.httpMethod !== 'POST') {
    return { statusCode: 405, body: 'Method Not Allowed' };
  }

  const { messages } = JSON.parse(event.body);

  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01'
    },
    body: JSON.stringify({
      model: 'claude-sonnet-4-20250514',
      max_tokens: 1000,
      system: 'You are NOVA AI, a friendly and intelligent AI assistant.',
      messages: messages
    })
  });

  const data = await response.json();
  return {
    statusCode: 200,
    headers: { 'Access-Control-Allow-Origin': '*' },
    body: JSON.stringify(data)
  };
};
```

### Update your `index.html` — change the fetch URL:
Find this line in nova-ai.html:
```
const response = await fetch('https://api.anthropic.com/v1/messages', {
```
Replace it with:
```
const response = await fetch('/.netlify/functions/chat', {
```
And **remove** the headers lines (x-api-key etc.) — the backend handles that now.

Upload both files to your GitHub repository.

---

## 🌐 STEP 4: Deploy on Netlify (Free)

1. Go to 👉 **https://netlify.com/**
2. Click **"Sign Up"** → sign in with your GitHub account
3. Click **"Add New Site"** → **"Import from Git"**
4. Choose **GitHub** → select your `nova-ai-website` repository
5. Click **"Deploy Site"** — Netlify builds it automatically!

---

## 🔐 STEP 5: Add Your API Key Securely

1. In Netlify, go to your site dashboard
2. Click **"Site Settings"** → **"Environment Variables"**
3. Click **"Add Variable"**
4. Key: `ANTHROPIC_API_KEY`
5. Value: paste your API key from Step 1 (e.g. `sk-ant-api03-xxx...`)
6. Click **"Save"**
7. Go to **"Deploys"** → click **"Trigger Deploy"** to restart

---

## ✅ DONE! Your Site is Live!

Netlify gives you a free URL like:
**`https://nova-ai-abc123.netlify.app`**

You can also buy a custom domain (e.g. `www.novaai.in`) from:
- **GoDaddy** (~₹799/year)
- **Namecheap** (~₹699/year)
And connect it in Netlify → Domain Settings.

---

## 💰 Cost Summary

| Item | Cost |
|------|------|
| GitHub | FREE |
| Netlify hosting | FREE |
| Anthropic API (first ~$5 credit) | FREE |
| Custom domain (optional) | ~₹700/year |

---

## 🆘 Need Help?

If you get stuck on any step, just message us and describe which step you're on!

---
*NOVA AI Deployment Guide — 2025*
