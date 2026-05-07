# Nikki Patel — Meeting Scheduler

A single-file scheduling page that lets customers pick time slots and submit meeting requests. When submitted, an email is **automatically sent** to `nikki.patel@netdocuments.com` with all the customer's details and preferred times. No manual steps required.

Hosted on GitHub Pages. No backend required.

---

## ⚡ One-Time Setup: Activate Email Sending

Email sending is powered by **Web3Forms** (free, no account signup required beyond entering your email).

### Step 1: Get Your Access Key

1. Go to **[https://web3forms.com](https://web3forms.com)**
2. Enter `nikki.patel@netdocuments.com` and click **Get Access Key**
3. Check your inbox — they'll email you a free access key instantly

### Step 2: Add the Key to index.html

Open `index.html` and find this line near the top of the `<script>` section:

```js
const WEB3FORMS_KEY = 'YOUR_WEB3FORMS_ACCESS_KEY';
```

Replace `YOUR_WEB3FORMS_ACCESS_KEY` with your actual key:

```js
const WEB3FORMS_KEY = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx';
```

Save and push to GitHub — email sending is now live. Every form submission will automatically email Nikki.

---

## 📬 What the Email Looks Like

When a customer submits the form, Nikki receives:

```
Subject: Meeting Request: Acme Corp | ND - AI Profiling

Hi Nikki,

You have a new meeting request.

CUSTOMER DETAILS
Name:        Jane Smith
Company:     Acme Corp
Email:       jsmith@acme.com
Purpose:     AI Profiling

PREFERRED TIMES
1st Choice:  Monday, May 11, 2026, 10:00 AM – 11:00 AM EDT
2nd Choice:  Tuesday, May 12, 2026, 2:30 PM – 3:30 PM EDT

Please confirm one of the times and send Jane Smith a Teams invite at jsmith@acme.com.
Suggested title: Acme Corp | ND - AI Profiling
```

Hitting **Reply** goes directly to the customer's email.

---

## 🚀 Deploying to GitHub Pages

1. Push `index.html` and `README.md` to your GitHub repo
2. Go to **Settings → Pages**
3. Set source to your main branch, root folder → **Save**
4. Your page will be live at `https://yourusername.github.io/repo-name/`

---

## 🗓 Updating Availability

Real calendar busy blocks are hard-coded in the `CALENDAR_DATA` object in `index.html`. Update this each week with your actual Outlook events (busy only, UTC times):

```js
const CALENDAR_DATA = {
  '2026-05-11': [
    { s: '2026-05-11T15:30:00Z', e: '2026-05-11T16:00:00Z' },  // GCX Sync
    { s: '2026-05-11T16:00:00Z', e: '2026-05-11T17:00:00Z' },  // Lunch
  ],
  // ... etc
};
```

**Rules:**
- All times in **UTC**. EDT = UTC−4, so 9 AM EDT = `13:00Z`.
- Work hours are 9 AM–5 PM EDT (13:00–21:00 UTC).
- Only include `showAs: busy` events. Skip declined or free/OOO blocks.
- The 9–10 AM EDT block is applied automatically every day — don't add it.
- A 30-minute buffer is auto-applied around each meeting when computing open slots.

---

## What It Does

- Shows real availability based on your Outlook calendar for next week (Mon–Fri, 9 AM–5 PM EDT)
- Customers pick a 1st choice and optional 2nd choice time slot
- Timezone switcher: Eastern, Central, Pacific
- Form collects: Company, Name, Email, Purpose of Meeting
- On submit → email fires automatically to `nikki.patel@netdocuments.com`
- Confirmation screen shown to the customer after submit
- Fully responsive, zero dependencies, single HTML file

---

## Customization

Key settings at the top of the `<script>` section in `index.html`:

| Constant | Default | Description |
|----------|---------|-------------|
| `HOST_NAME` | `Nikki Patel` | Name shown in the header |
| `HOST_EMAIL` | `nikki.patel@netdocuments.com` | Recipient of the request email |
| `WEB3FORMS_KEY` | *(your key)* | Web3Forms access key for email sending |
| `WORK_H_S` | `13` | Work day start in UTC (9 AM EDT) |
| `WORK_H_E` | `21` | Work day end in UTC (5 PM EDT) |
| `MEET_MIN` | `60` | Meeting length in minutes |
| `BUF_MIN` | `30` | Buffer around blocked times in minutes |

**Timezone note:** Offsets are set for EDT (May–November, UTC−4). If reusing in winter, update the `TZ` block to EST (UTC−5), CST (UTC−6), PST (UTC−8).
