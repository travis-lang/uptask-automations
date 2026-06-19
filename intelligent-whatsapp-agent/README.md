# Intelligent WhatsApp Customer Agent

**An AI-powered customer service agent that responds to WhatsApp inquiries in real-time, qualifies leads, and schedules appointments automatically.**

Stop losing customers because you can't respond fast enough. This workflow turns WhatsApp into a 24/7 sales and support machine.

---

## 📊 What It Does (In 60 Seconds)

```
Customer texts you on WhatsApp
         ↓
n8n receives the message
         ↓
Groq AI processes the inquiry intelligently
         ↓
Responds with product info / answers questions / asks qualifying questions
         ↓
If customer wants to proceed → Automatically creates appointment in Google Calendar
         ↓
Customer books a time, your team is notified
```

**Result**: Customers get instant responses. You get qualified leads. No manual work.

---

## 🎯 Real-World Use Cases

### Real Estate Agent
**Before:** Miss 40% of inquiries because you're showing a property
**After:** WhatsApp agent qualifies buyers while you're busy
- Asks: Budget? Bedrooms? Preferred area?
- Shows matching listings
- Books viewing appointments
- You handle only serious buyers → +40% close rate

### E-Commerce Store Owner
**Before:** Customer asks a question at 9 PM, leaves because you don't respond until morning
**After:** AI answers instantly, customer buys same night
- Customer: "Is this available in blue?"
- Agent: "Yes! Shipping takes 2 days. Want me to add to cart?"
- Customer books follow-up call to pay
- You wake up to a sale

### SACCO/Credit Union Manager
**Before:** Members call, leave voicemails, wait days for callbacks
**After:** Instant responses, automatic appointment booking
- Member: "How do I apply for a loan?"
- Agent: "Tell me your income range"
- Member provides info → Auto-scheduled meeting with loan officer
- You focus on approvals, not answering phones

### Service Business (Plumber, Electrician, etc.)
**Before:** Missed calls = missed revenue
**After:** Every inquiry is captured and qualified
- Customer: "Do you do urgent repairs?"
- Agent: "Yes! What's the issue?"
- Customer describes problem → Agent books emergency slot
- You dispatch crew with full info upfront

---

## 🔧 How It Works (Technical Overview)

### Architecture

```
Meta WhatsApp API
       ↓
n8n Webhook (receives messages)
       ↓
Parse Message (extract customer text + phone)
       ↓
Groq AI (llama-3.1-8b: understand intent, respond)
       ↓
Simple Memory (remember conversation history)
       ↓
Send WhatsApp Reply (respond to customer)
       ↓
Google Calendar Tool (if appointment is mentioned)
       ↓
Appointment Created (customer sees booking options)
```

### Key Components

| Component | What It Does | Why It Matters |
|-----------|-------------|-----------------|
| **Webhook (GET)** | Verifies your connection with Meta | Security — prevents fake messages |
| **Webhook (POST)** | Receives actual customer messages | Core trigger for the workflow |
| **Parse Message** | Extracts customer text, phone, session ID | So AI knows who's talking |
| **Groq AI** | Understands intent, generates smart responses | Fast + accurate (cheaper than OpenAI) |
| **Simple Memory** | Remembers previous messages in conversation | Context awareness (customer feels heard) |
| **Google Calendar** | Auto-creates appointments | Saves 5+ minutes per booking |
| **Send WhatsApp Reply** | Responds to customer instantly | The payoff — customer gets instant answer |

---

## 💰 Expected Results

| Metric | Before | After | Impact |
|--------|--------|-------|--------|
| Response time | 2-4 hours (missed calls) | Instant | +30-50% conversation → sale rate |
| Customer satisfaction | Low (slow response) | High (instant answers) | More 5-star reviews |
| Time spent on support | 20+ hrs/week | 5 hrs/week | 15 hours back in your week |
| Qualified leads captured | 60% (rest move on) | 95% (automatic) | +50% lead volume |
| Appointment no-shows | 30% | 10% (confirmed in calendar) | More meetings happen |

---

## 🚀 Setup Guide (30 minutes)

### Step 1: Get Your Credentials (10 minutes)

#### A. Get Groq API Key (Free)
1. Go to https://console.groq.com
2. Sign up (free account)
3. Click "API Keys" → Create new key
4. Copy the key (you'll need this in n8n)

#### B. Set Up Meta WhatsApp Business Account
1. Go to https://www.facebook.com/business
2. Create Business Account (free)
3. Add WhatsApp app
4. Get your:
   - Phone Number ID
   - Business Account ID
   - Verify Token (create your own: any random string like "mytoken123")
   - Access Token (from Facebook Developer Dashboard)

#### C. Connect Google Calendar
1. In n8n, click Credentials → Add "Google Calendar OAuth2"
2. Authenticate with your Google account
3. n8n will request permission to manage calendar

### Step 2: Import the Workflow (5 minutes)

1. Open n8n dashboard
2. Click "New Workflow"
3. Click "Import from file"
4. Select `WhatsApp_Real_Estate_AI_Agent.json`
5. Click Import

### Step 3: Add Your Credentials (10 minutes)

1. In the imported workflow, find these nodes:
   - **Groq Model** → Click → Add credentials (paste your Groq API key)
   - **Send whatsapp reply** → Click → Add credentials (paste Meta Access Token)
   - **Create an event in Google Calendar** → Click → Select your Google account

2. Update these hardcoded values:
   - **Webhook GET (Meta Verify)** → `Verify Meta Token` node: change `mytoken123` to YOUR verify token
   - **Send whatsapp reply** → Change phone number ID to YOUR phone number ID
   - **Groq Model** → Verify model is set to `llama-3.1-8b-instant` ✓

### Step 4: Customize the AI Personality (10 minutes, optional)

In the **AI Agent** node, modify the system prompt:

**Current (Real Estate Example):**
```
You are Maya, a warm and professional real estate consultant at Uptask Realty Kenya.
```

**Customize for your business:**
- E-commerce: `You are Alex, a friendly e-commerce specialist at [Your Store Name]`
- SACCO: `You are Grace, a helpful loan officer at [Your SACCO Name]`
- Services: `You are Chris, a professional plumber serving [Your City]`

Update the "Available listings" section with YOUR actual offerings.

### Step 5: Test (5 minutes)

1. Click "Execute Workflow"
2. Send a test message to your WhatsApp number
3. You should get a response within 2 seconds
4. Test an appointment booking: "I want to book a viewing"
5. Check your Google Calendar — appointment should appear

### Step 6: Deploy

1. Click "Save"
2. Toggle "Active" to ON
3. Your WhatsApp agent is live 24/7

---

## 🎛️ Customization Tips

### Change the AI Model
Want a different AI? Replace **Groq Model** with:
- OpenAI (GPT-4) — More powerful but costs $0.03 per message
- Ollama (local) — Free but slower
- Anthropic Claude — Balanced power + cost

Just swap the node and add credentials.

### Add WhatsApp Message Buttons
Instead of text responses, send clickable buttons:
```
Customer sees: "What would you like help with?"
Options:
  ✓ Product info
  ✓ Pricing
  ✓ Book appointment
```

Add a **WhatsApp Interactive Message** node before "Send whatsapp reply"

### Integrate with CRM
Want appointments in HubSpot/Salesforce instead of Google Calendar?

Replace the **Google Calendar** node with:
- HubSpot (create deal)
- Salesforce (create task)
- Airtable (add row)
- Any CRM via webhook

### Track Conversation Quality
Add a **Google Sheets** node after "Send whatsapp reply" to log:
- Customer phone
- Their question
- AI response
- Timestamp

### Add Human Handoff
If AI can't answer, pass to human:
```
If customer says "talk to a human"
  → Send message: "Connecting you to my team"
  → Post to Slack (your team responds)
  → Customer gets human help
```

---

## 🛡️ Troubleshooting

| Problem | Solution |
|---------|----------|
| Messages not being received | Check webhook URL is correct in Meta Dashboard |
| Groq API errors | Verify API key, check you haven't hit rate limit (30/min free tier) |
| Google Calendar not creating events | Re-authenticate Google Calendar credentials |
| Responses are slow | Increase n8n execution timeout, or switch to faster model |
| AI is giving wrong answers | Refine the system prompt with more specific instructions |

---

## 📈 Optimization Ideas

### Phase 1 (Week 1): Launch Basic Agent
- Handle common questions
- Auto-schedule appointments
- Log metrics

### Phase 2 (Week 2-3): Add Integrations
- Connect to your CRM (HubSpot, Salesforce)
- Send leads to Slack for your team
- Create tasks in your project management tool

### Phase 3 (Month 2): Expand Vertically
- Add another WhatsApp business account (for a second business)
- Create different agents for different departments
- Build a dashboard to track performance

### Phase 4 (Month 3+): Monetize
- Sell this service to other businesses ($500-2K setup)
- Charge maintenance retainers ($200-500/month)
- Build a SaaS on top

---

## 📊 Metrics to Track

Set up a Google Sheet to log:

```
| Date | Customer | Question | Response Time | Booked? | Outcome |
|------|----------|----------|----------------|---------|---------|
| Jun 18 | +254712... | Property inquiry | 2s | Yes | Viewing scheduled |
| Jun 18 | +254713... | Budget question | 1s | Yes | Lead captured |
```

**Key KPIs:**
- Response time (should be <5 seconds)
- Booking rate (% that schedule appointments)
- Customer satisfaction (rate responses manually)
- Time saved (hours/week no longer spent on WhatsApp)

---

## 🔐 Security Notes

- **Never hardcode API keys** — use n8n Credentials
- **Verify webhook token** — prevents fake messages
- **Store conversation data safely** — GDPR compliance if EU customers
- **Encrypt sensitive data** — customer info in Google Sheets should be access-restricted

---

## 💡 Advanced: Multi-Language Support

Want to respond in Swahili, Spanish, or French?

Update the system prompt:
```
You are Maya, a bilingual real estate consultant.
Respond in the same language the customer used.
If they write in Swahili, respond in Swahili.
```

Groq supports 100+ languages automatically.

---

## 🚀 Next Steps

1. **Get your Groq API key** (2 minutes)
2. **Set up Meta Business account** (10 minutes)
3. **Import this workflow into n8n** (5 minutes)
4. **Add your credentials** (10 minutes)
5. **Customize AI personality** (10 minutes)
6. **Test & deploy** (10 minutes)

**Total time to live: 47 minutes**

Then watch your response rate, booking rate, and customer satisfaction skyrocket.

---

## 📚 Resources

- [n8n Documentation](https://docs.n8n.io)
- [Groq Console](https://console.groq.com)
- [Meta WhatsApp API Docs](https://developers.facebook.com/docs/whatsapp/)
- [Google Calendar API](https://developers.google.com/calendar)

---

**Built to save you hours every week and turn WhatsApp into your best salesperson.**

*Questions? Customize this workflow for your business, deploy, and start capturing leads.*

---

## File Reference

- `workflow.json` — The complete n8n workflow (import this)
- This README — Setup + customization guide
