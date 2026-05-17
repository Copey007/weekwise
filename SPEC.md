# WeekWise — Workflow Intelligence

## The Concept

**Problem:** Sales and revenue people spend 40%+ of their week on repetitive tasks that could be automated — but they don't know what to prioritize or where to start.

**Solution:** A browser extension that tracks work patterns, shows where time goes, identifies automation opportunities, and seamlessly transitions users to the full AI Sales Agent when they're ready.

**Positioning:** "Know where your week goes, discover what to automate, upgrade when you're ready."

---

## The Product

### 1. Browser Extension (Chrome)
- **Installs in 1 click** from Chrome Web Store
- **Tracks in background:** active tab, time spent, app switches
- **No screenshots, no surveillance** — just category + duration data
- **Daily dashboard in popup:** "Today you spent 3.2 hrs in email, 1.1 hrs in Slack, 0.8 hrs in Salesforce"

### 2. Web Dashboard
- Weekly/monthly work breakdown
- Tool usage patterns (which apps, when, how long)
- "Workflow score" — how repetitive vs varied is the week
- Top time-wasters identified
- Automation recommendations based on patterns

### 3. Freemium Model

**Free tier:**
- 7 day tracking history
- Daily summary
- 3 workflow insights
- Basic categories

**Pro ($9/mo):**
- Unlimited history
- Full automation recommendations
- Export data
- Priority support

**AI Agent Upsell:**
- "We noticed you manually enter data into HubSpot 4x/day — our AI agent does that for you"
- Direct link to sales agent demo/trial
- Commission on sales conversions

---

## Key Features

### Extension Features
- [ ] Active tab tracking (what site/app)
- [ ] Time categorization (email, crm, chat, docs, web)
- [ ] Daily popup summary
- [ ] Manual log entry (for offline work)
- [ ] Distraction detection ("You checked email 47 times today")

### Dashboard Features
- [ ] Weekly heat map (activity by hour/day)
- [ ] Category breakdown chart
- [ ] Tool usage ranking
- [ ] Repetitive task detection
- [ ] Automation opportunity score
- [ ] Week-over-week comparison

### Upgrade Flow
- [ ] "Unlock with Pro" prompts at key data points
- [ ] "See what we can automate" CTA
- [ ] Smooth transition to sales agent onboarding

---

## Tech Stack

- **Extension:** Chrome Extension API (Manifest V3), JavaScript
- **Backend:** Node.js + Express (same Mac mini hosting)
- **Database:** SQLite (simple, local, no setup)
- **Dashboard:** Static HTML + API calls (same as gtm-revolution-web)
- **Auth:** Simple email capture (Mailchimp or CSV for MVP)

---

## Data Model

```javascript
// What we track per user
User {
  id: uuid,
  email: string,
  created_at: timestamp,
  plan: 'free' | 'pro'
}

Session {
  id: uuid,
  user_id: uuid,
  start_time: timestamp,
  end_time: timestamp,
  category: string,  // 'email', 'crm', 'chat', 'docs', 'web', 'other'
  tool_name: string, // 'gmail', 'salesforce', 'slack', 'etc'
  domain: string      // 'mail.google.com'
}

// Aggregated weekly data (for dashboard)
WeeklyReport {
  user_id: uuid,
  week_start: date,
  total_hours: number,
  top_tools: [{tool, hours, percentage}],
  automation_opportunities: [string],
  workflow_score: number // 0-100
}
```

---

## User Flow

```
User installs extension (Chrome Web Store)
         ↓
Sees popup: "Tracking started! Check back tomorrow for insights"
         ↓
Day 1 complete → Daily summary in popup
         ↓
Day 7 → Sees weekly dashboard (free tier)
         ↓
Sees "Upgrade to see automation recommendations"
         ↓
Pays $9/mo → Sees full insights + automation opportunities
         ↓
Clicks "Automate this" on repetitive task
         ↓
Redirected to sales agent trial/demo
         ↓
Sales agent converts → commission or subscription
```

---

## MVP Scope (First 2 Weeks)

### Week 1: Extension + Basic Tracking
- [ ] Chrome extension scaffold
- [ ] Track active tab + duration
- [ ] Store in local SQLite
- [ ] Daily popup summary
- [ ] Basic categories

### Week 2: Dashboard + Freemium
- [ ] Web dashboard with charts
- [ ] Email capture (free tier)
- [ ] 7-day history limit (free)
- [ ] Pro upgrade flow (Stripe)
- [ ] Automation recommendations

### Week 3+: Sales Agent Integration
- [ ] "What we can automate" section
- [ ] Link to sales agent demo
- [ ] Track conversions

---

## Branding

- **Name:** WeekWise (or suggest alternatives)
- **Colors:** Match GTM Revolution — dark text, pink accent
- **Font:** Caveat for logo, Inter for UI
- **Positioning:** "Workflow intelligence for revenue teams"

---

## Competitors

| Product | What | Price |
|---------|------|-------|
| RescueTime | Full time tracking | $6-12/mo |
| Toggl | Time tracking | $9-18/mo |
| Clockify | Free time tracker | Free |
| Wave | Email tracking | $6/mo |

**Differentiation:** Not just tracking — the automation recommendations and path to AI agent is the unique value prop.

---

## Success Metrics

- Install rate (target: 100 installs in week 1)
- Free → Pro conversion (target: 3-5%)
- Pro → Agent upgrade (target: 10% of Pro)
- Time to first automation booked

---

## Next Steps

1. Create Chrome Web Store developer account ($5 one-time)
2. Build extension scaffold
3. Deploy to Chrome Web Store (review takes 1-3 days)
4. Launch with blog post / social
5. Track metrics, iterate

---

**Questions to answer:**
- Email capture at install or first dashboard view?
- Stripe for payments or PayPal?
- Single user or team-based pricing?
- Chrome only or also Firefox/Safari?