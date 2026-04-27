# Zintro Pricing Workflow Interview

A single-page web app that pairs a Vapi voice agent (Alex) with a synchronized visual display of three RFQs being reviewed in a pricing workflow interview.

## How to Run

You need to serve the file over HTTP (not `file://`) because the Vapi SDK and microphone access require a proper origin.

### Option 1 — Python (quickest)

```bash
cd /Users/stuartlewtan/.openclaw/workspace/tools/pricing-interview
python3 -m http.server 8080
```

Then open: **http://localhost:8080**

### Option 2 — Node (if you have `npx`)

```bash
npx serve /Users/stuartlewtan/.openclaw/workspace/tools/pricing-interview
```

### Option 3 — Any static host

Drop `index.html` onto Netlify Drop, Vercel, or any web server. No build step needed — it's fully self-contained.

---

## How It Works

1. Click **Start Interview** — the browser will request mic permission, then connect to the Vapi assistant.
2. Alex (the voice agent) leads a mock pricing workflow walkthrough covering three RFQs.
3. As Alex speaks, keyword detection automatically highlights the relevant RFQ card.
4. When Alex reveals an outcome ("We sent a proposal" / "We passed on this one"), the outcome badge on the active card is revealed.

---

## Updating Vapi Config

Open `index.html` and find the config block near the top of the `<script>` section:

```js
const VAPI_PUBLIC_KEY   = 'deec25d8-9e0e-48e1-a203-c2c940d638a1';
const VAPI_ASSISTANT_ID = '50138eea-64fb-45ab-a8e7-fe002830a8f3';
```

Replace either value as needed. The public key is tied to your Vapi project; the assistant ID is the specific assistant you want to use.

---

## Keyword Sync Logic

RFQ cards are activated when Alex says any of these keywords:

| RFQ | Keywords |
|-----|----------|
| #1 Key Lime Interactive | "Key Lime", "AI Admin", "ServiceNow", "first one" |
| #2 TriVoca Health | "TriVoca", "Lab Director", "proprietary panel", "second one" |
| #3 CMB | "CMB", "asset management", "financial advisor", "third one" |

Outcome badges are revealed when Alex says:
- "We sent a proposal" / "proposal was sent" → ✅ Proposal Sent
- "We passed on this one" / "we declined" → ❌ Declined

---

## Files

```
pricing-interview/
├── index.html   ← the entire app (self-contained)
└── README.md    ← this file
```
