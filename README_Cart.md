# 🛒 AI Abandoned Cart Intelligence Engine
### Week 15 — Haus of Intelligence Cohort

Runs every 15 minutes. Reads every abandoned cart. Picks the best recovery approach. Sends personalized email + Telegram. Learns from every outcome. Recovers lost revenue automatically — while you sleep.

---

## 🎯 What It Does

Every D2C brand loses 20-30% of revenue to abandoned carts. Klaviyo charges ₹40K/month to solve this. This system does it for ₹0 — with multi-touch intelligence Klaviyo doesn't have.

---

## ⚡ Every 15 Minutes, Automatically

1. **Reads all abandoned carts** from Google Sheets
2. **Reads customer history** — LTV, orders, tier, preferred channel, past abandons
3. **Reads recovery log** — enforces 24-hour cooldown, learns from past outcomes
4. **Filters smartly** — only carts abandoned 15 mins to 48 hours ago
5. **💎 VIP Customer Detector** — scores customers by LTV, orders, tier — routes VIPs to PREMIUM approach
6. **💰 Dynamic Discount Engine** — calculates optimal discount % based on cart value + tier + history
7. **AI Strategist picks from 6 recovery approaches:**
   - URGENCY — stock scarcity messaging
   - DISCOUNT — personalized % offer
   - SOCIAL PROOF — community validation
   - WIN_BACK — aggressive offer for repeat abandoners
   - PREMIUM — no discount, brand story for VIPs
   - FOMO — time-limited offer
8. **Writes personalized HTML recovery email** in brand voice
9. **Sends Telegram alert** to customer
10. **📊 Recovery Performance Summary** — tracks recovery rate, estimated revenue recovered
11. **Logs every attempt** with outcome for future learning
12. **Alerts owner** with full performance brief on Telegram
13. **Marks cart as Sent** — prevents duplicate messages

---

## 🏗️ Architecture (25 nodes)

```
15-Min Trigger → Read Carts → Read Customer History → Read Recovery Log →
Filter & Enrich → Any Pending? → Build Strategist Prompt →
Agent1: Recovery Strategist → Parse + Prep →
VIP Customer Detector → Apply VIP Routing →
Dynamic Discount Engine → Fan Out per Cart →
Build Recovery HTML → Should Send Email? → Send Recovery Email →
Should Send Telegram? → Send Recovery Telegram →
Log Recovery Attempt → Mark Cart as Sent →
Build Owner Alert → Recovery Performance Summary →
Build Performance Alert → Should Alert Owner? → Send Owner Alert (Telegram)
```

---

## 🤖 6 Recovery Approaches

| Approach | When Used | Discount |
|----------|-----------|---------|
| PREMIUM | VIP customers (LTV > ₹10K) | None |
| WIN_BACK | 3+ abandons, 0 recoveries | 20-25% |
| DISCOUNT | Standard recovery | 10-20% scaled to cart value |
| URGENCY | Stock scarcity signal | 5% nudge |
| FOMO | Time-limited sale | 5% nudge |
| SOCIAL_PROOF | First-time abandoners | None |

---

## 💎 VIP Scoring System

| Signal | Points |
|--------|--------|
| LTV > ₹10,000 | +3 |
| LTV > ₹5,000 | +2 |
| Orders > 5 | +2 |
| Premium tier | +2 |
| Past recoveries > 1 | +1 |
| **VIP threshold** | **4+** |

---

## ⚙️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation + Scheduler | n8n (self-hosted) |
| Recovery Strategist | Gemini 2.5 Flash |
| Cart + Customer Data | Google Sheets |
| Recovery Memory | Google Sheets |
| Email Delivery | Gmail API |
| Alerts | Telegram Bot |

---

## 🔧 Setup

1. Import `AI_Abandoned_Cart_Intelligence.json` into n8n
2. Configure credentials:
   - **Google Gemini** — Query Auth with Gemini API key
   - **Gmail** — OAuth2
   - **Google Sheets** — OAuth2
   - **Telegram** — Bot token + your Chat ID
3. Create Google Sheet: **"AI Abandoned Cart Intelligence"** with 3 tabs:

**Tab 1: `Abandoned_Carts_Tab`**
`Cart ID, Customer Email, Customer Phone, Customer Name, Products, Cart Value, Currency, Abandoned At, Last Viewed Product, Time on Site Mins, Status, Source`

**Tab 2: `Customer_History_Tab`**
`Email, Phone, Lifetime Orders, Lifetime Value, Avg Order Value, Days Since Last Order, Past Abandons, Past Recoveries, Favorite Category, Last Discount Used, Tier, Preferred Channel`

**Tab 3: `Recovery_log_tab`**
`Send At, Cart ID, Customer Name, Customer Email, Cart Value, Approach Used, Channel, Discount %, Tone, Subject, Expected Recovery %, AI Reasoning, Customer Tier, Returning, Mins Since Abandon, Outcome, Recovered Value`

4. Update Telegram Chat ID in both Telegram nodes
5. Workflow runs every 15 minutes automatically

---

## 💡 Business Case

- Industry average cart abandonment rate: 70%
- Recovery rate with smart sequencing: 15-25%
- **For a brand doing ₹10L/month:** recovers ₹1.5-2.5L monthly
- Klaviyo equivalent: ₹40,000/month
- **This system: ₹0**

---

## 🎬 Demo Data

GlowVeda skincare brand — 8 abandoned carts including Priya (premium VIP, ₹1,599 cart), Rahul (win-back candidate, 4 past abandons), and 6 others across Web, Instagram, and Google sources.

---

## 👤 Author

**Ram** — AI Automation Agency founder  
Building done-for-you AI systems for D2C brands and service businesses  
[GitHub](https://github.com/Ram-cyber-dev)
