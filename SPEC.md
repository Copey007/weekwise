# WeekWise — Workflow Intelligence

## The Concept

**Problem:** Sales and revenue people spend 40%+ of their week on repetitive tasks that could be automated — but they don't know what to prioritize or where to start.

**Solution:** A browser extension that tracks work patterns, shows where time goes, identifies automation opportunities, and seamlessly transitions users to the full AI Sales Agent when they're ready.

**Positioning:** "Know where your week goes, discover what to automate, upgrade when you're ready."

---

## The Product

### 1. Browser Extension (Chrome)
- **Installs in 1 click** from Chrome Web Store
- **Tracks in background:** active tab, time spent, clicks, workflow patterns
- **No screenshots, no surveillance** — just category + duration + event data
- **Daily dashboard in popup:** "Today you spent 3.2 hrs in email, clicked 47 times, did 8 repetitive tasks"

### 2. Web Dashboard
- Weekly/monthly work breakdown
- Tool usage patterns (which apps, when, how long)
- **Click and workflow tracking** (not just time)
- "Workflow score" — how repetitive vs varied is the week
- **Automation recommendations** based on actual repetitive clicks
- Week-over-week comparison

### 3. Freemium Model

**Free tier:**
- 7 day tracking history
- Daily summary (time + clicks)
- 3 workflow insights
- Basic categories

**Pro ($9/mo):**
- Unlimited history
- Full automation recommendations (based on click patterns)
- Export data
- Priority support

**A-Gent Upsell:**
- "We noticed you manually enter data into HubSpot 22x/week — our AI agent does that for you"
- Direct link to sales agent demo/trial
- **The workflow data is the sales pitch** — we already know what they need automated

---

## Key Features

### Extension Features
- [x] Active tab tracking (what site/app)
- [x] Time categorization (email, crm, chat, docs, web, other)
- [ ] Click tracking within apps (Salesforce, HubSpot, Gmail, etc.)
- [ ] Workflow pattern detection (repetitive sequences)
- [x] Daily popup summary
- [ ] Manual log entry (for offline work)
- [ ] Distraction detection ("You checked email 47 times today")

### Dashboard Features
- [ ] Weekly heat map (activity by hour/day)
- [ ] Category breakdown chart
- [ ] Tool usage ranking
- [ ] **Click frequency analysis**
- [ ] **Repetitive workflow detection**
- [ ] **Automation opportunity score** (based on click patterns)
- [ ] Week-over-week comparison

### Upgrade Flow
- [ ] "Unlock with Pro" prompts at key data points
- [ ] "See what we can automate" CTA
- [ ] **A-Gent recommendation engine** (uses workflow data)
- [ ] Smooth transition to sales agent onboarding

---

## Workflow Data Model

```javascript
// What we track per user
User {
  id: uuid,
  email: string,
  created_at: timestamp,
  plan: 'free' | 'pro'
}

// Session = time on a tab
Session {
  id: uuid,
  user_id: uuid,
  start_time: timestamp,
  end_time: timestamp,
  category: string,  // 'email', 'crm', 'chat', 'docs', 'web', 'other'
  tool_name: string,
  domain: string,
  click_count: number  // clicks during this session
}

// WorkflowEvent = specific action within an app
WorkflowEvent {
  id: uuid,
  user_id: uuid,
  session_id: uuid,
  timestamp: timestamp,
  domain: string,
  action_type: string,  // 'form_submit', 'button_click', 'page_view', 'data_entry'
  action_detail: string, // 'updated_contact', 'sent_email', 'created_task'
  repetition_count: number  // how many times this week
}

// AutomationOpportunity (computed from workflow data)
AutomationOpportunity {
  user_id: uuid,
  action: string,  // 'Manually update Salesforce contact'
  frequency: string,  // '22x per week'
  category: string,  // 'crm'
  recommendation: string,  // 'We can automate this for $49/mo'
  agent_upgrade: boolean  // qualifies for A-Gent upsell
}
```

---

## Data That Enables A-Gent Upsell

When a user upgrades to A-Gent, we already know:

- ✅ Which CRM they use (Salesforce vs HubSpot vs none)
- ✅ How many times/week they manually enter data
- ✅ Which tools they're weakest at (low time, high clicks = struggle)
- ✅ What their typical workday looks like (pattern analysis)
- ✅ Where the time sinks are

**The sales pitch is pre-built:** "We tracked your workflow for 2 weeks. You spend 4.5 hours/week on manual data entry into Salesforce. We can automate that."

---

## User Flow

```
User installs extension (Chrome Web Store)
         ↓
Email capture → Tracking starts
         ↓
Day 1: "Today: 3.2 hrs tracked, 47 clicks, 5 workflows"
         ↓
Day 7: Weekly dashboard (free) — "You do 18 repetitive tasks/week"
         ↓
Pro prompt: "Unlock automation recommendations"
         ↓
Pays $9/mo → Sees full insights + specific automation opportunities
         ↓
Clicks "Automate this" on repetitive task
         ↓
A-Gent recommendation: "We automate exactly this workflow"
         ↓
A-Gent trial/demo → Convert to $99/mo subscription
```

---

## MVP Scope (First 2 Weeks)

### Week 1: Extension + Basic Tracking
- [x] Chrome extension scaffold
- [x] Track active tab + duration
- [x] Store in local storage
- [x] Daily popup summary
- [x] Basic categories
- [ ] Click counting infrastructure

### Week 2: Dashboard + Freemium
- [ ] Web dashboard with charts
- [ ] Email capture (free tier)
- [ ] 7-day history limit (free)
- [ ] Pro upgrade flow (Stripe)
- [ ] Automation recommendations engine

### Week 3+: Workflow Intelligence
- [ ] Content scripts for major apps (Salesforce, HubSpot, Gmail)
- [ ] Click pattern detection
- [ ] A-Gent recommendation engine
- [ ] Integration with sales agent backend

---

## Branding

- **Name:** WeekWise (or suggest alternatives)
- **Colors:** Match GTM Revolution — dark text, pink accent (#d44a9a)
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

**Differentiation:** Not just tracking — click patterns + automation recommendations + path to AI agent is the unique value prop.

---

## Success Metrics

- Install rate (target: 100 installs in week 1)
- Free → Pro conversion (target: 3-5%)
- Pro → A-Gent upgrade (target: 10% of Pro)
- Time to first automation booked

---

## Next Steps

1. Create Chrome Web Store developer account ($5 one-time)
2. Build extension scaffold (DONE)
3. Deploy to Chrome Web Store (review takes 1-3 days)
4. Launch with blog post / social
5. Track metrics, iterate