[README.md](https://github.com/user-attachments/files/27487533/README.md)
# Nikki Patel — Meeting Booking Page

A customer-facing scheduling page for booking 60-minute meetings with Nikki Patel (NetDocuments). Customers pick two preferred time slots and submit their details, which generates a pre-filled email to Nikki so she can confirm a time and send a Teams invite.

---

## What It Does

- Displays next week's available time slots (Monday–Friday, 9 AM – 5 PM Eastern)
- Blocks 9–10 AM daily (no availability in that window)
- Lets customers select a **1st choice** and optional **2nd choice** time slot
- Collects customer details: Company Name, Your Name, Email, Purpose of Meeting
- On submit, opens a pre-filled email to `nikki.patel@netdocuments.com` with all details
- Meeting title follows the format: `Company Name | ND - Purpose of Meeting`
- Timezone selector: Eastern (EDT), Central (CDT), Pacific (PDT)

---

## Files

| File | Description |
|------|-------------|
| `index.html` | The entire booking page — one self-contained file, no dependencies |

---

## Hosting on GitHub Pages

1. Create a new **public** GitHub repository
2. Upload `index.html` to the root of the repo
3. Go to **Settings → Pages**
4. Under *Source*, select **Deploy from a branch** → `main` / `root` → **Save**
5. Your page will be live at `https://yourusername.github.io/your-repo-name`

---

## Sending to Customers

Paste the GitHub Pages URL directly into an email:

> *"You can use this link to request a meeting time with me next week: [your link here]"*

---

## How the Submission Works

When a customer submits the form, their browser opens a pre-filled email addressed to Nikki with:

- Customer name, company, and email
- Purpose of the meeting
- 1st and 2nd choice time slots (in their selected timezone)
- A suggested Teams meeting title

Nikki reviews the request, picks one of the times, and manually sends a Teams calendar invite to the customer.

---

## Important Notes

**No live calendar sync.** This is a static page — it does not connect to Outlook or any calendar system. All time slots will always appear as available. Nikki should check her actual calendar before confirming a time from the customer's request.

**Timezone offsets are set for May 2026 (Daylight Saving Time).** If you reuse this page in winter months (November–March), update the UTC offsets in the `TZ` config block near the top of the `<script>` section:

```js
// Summer (DST) — May–November
const TZ = {
  EST: { off: -4, label: 'Eastern (EDT)' },
  CST: { off: -5, label: 'Central (CDT)' },
  PST: { off: -7, label: 'Pacific (PDT)' }
};

// Winter (Standard Time) — November–March
const TZ = {
  EST: { off: -5, label: 'Eastern (EST)' },
  CST: { off: -6, label: 'Central (CST)' },
  PST: { off: -8, label: 'Pacific (PST)' }
};
```

**The page always shows "next week."** The date range updates automatically based on when the customer visits — no manual edits needed week to week.

---

## Customization

All key settings are in the `CONFIG` block at the top of the `<script>` section in `index.html`:

| Constant | Default | Description |
|----------|---------|-------------|
| `HOST_NAME` | `Nikki Patel` | Name shown in the header |
| `HOST_EMAIL` | `nikki.patel@netdocuments.com` | Email that receives the request |
| `WORK_H_S` | `13` | Work day start in UTC (9 AM EDT) |
| `WORK_H_E` | `21` | Work day end in UTC (5 PM EDT) |
| `MEET_MIN` | `60` | Meeting length in minutes |
| `BUF_MIN` | `30` | Buffer around blocked times in minutes |
