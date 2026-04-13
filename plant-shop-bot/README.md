# 🌿 Plant Shop Bot — Marmelstein Nursery

WhatsApp customer service automation bot for Marmelstein Nursery built on **n8n**.

---

## 📋 Features

- 💬 **Text Messages** — AI-powered replies via OpenAI Assistant
- 🎤 **Voice Messages** — Auto transcription + AI reply
- 📸 **Image Messages** — Forwarded to expert WhatsApp group
- 📧 **Auto Emails** — Supplier & accounting emails generated automatically
- 📊 **Google Sheets** — Full chat history & customer tracking
- 🔀 **Smart Routing** — Classifier decides: reply / send to group / send email

---

## 🏗️ Architecture

```
WhatsApp (GreenAPI)
       ↓
   Webhook (n8n)
       ↓
  [Filter: not group chat]
       ↓
  ┌────────────────────────────┐
  │  Text Message?             │→ OpenAI Assistant → Reply → Update Sheet → Classifier
  │  Audio Message?            │→ Transcribe → OpenAI → Reply → Update Sheet → Classifier
  │  Image Message?            │→ Forward to Expert Group → Update Sheet
  └────────────────────────────┘
       ↓
   Classifier (GPT-4o)
       ↓
  ┌────────────────────────────┐
  │  sendtogroup               │→ Summary → WhatsApp Group → Set Chat Mode = Manual
  │  suppliermail              │→ Email to Michal (accounting)
  │  accountingmail            │→ Email to accounting dept
  │  none                      │→ Continue bot conversation
  └────────────────────────────┘
```

---

## ⚙️ Setup Instructions

### 1. Import Workflow
1. Open your **n8n** instance
2. Go to **Workflows** → **Import from File**
3. Upload `workflow/plant-shop-bot.json`

### 2. Configure Credentials (REQUIRED)

After import, update the following credentials:

| Credential | Used For | Where to Update |
|---|---|---|
| `OpenAi -- Logit` | Main AI Assistant + Classifier | All `Message a model*` nodes |
| `Tal ChatGpt` | Audio Transcription | `Transcribe a recording2` node |
| `pant sheet samad` | Google Sheets | All `Get/Update/Append row` nodes |
| `Rohit Gmail account` | Sending emails | All `Send a message*` nodes |

### 3. Update GreenAPI Settings

In all **HTTP Request** nodes that send WhatsApp messages, update:
```
URL: https://YOUR_INSTANCE.api.greenapi.com/waInstanceXXXXXXXX/sendMessage/YOUR_API_TOKEN
```

Replace:
- `7103` → your GreenAPI instance number
- `7103242575` → your WhatsApp instance ID
- `3d98966d04804dadb930d30b0f4affadbb0852d38b274aedb1` → your API token

### 4. Update WhatsApp Group Chat ID

In nodes that send to the expert group, change:
```
923070650940@c.us  →  YOUR_WHATSAPP_GROUP_ID@g.us
```

Nodes to update:
- `HTTP Request47`
- `HTTP Request51`
- `HTTP Request50`
- `HTTP Request APi Post` (caption + chatId)

### 5. Update Google Sheets

Replace the spreadsheet ID in all Google Sheets nodes:
```
1hfyzxeTQs0yODvu-uQMVZZJJaPbd_HTSk4JepncgRUg  →  YOUR_SHEET_ID
```

Your sheet must have these columns:
| Name | Number | Thread Id | Chat History | Chat Mode |

### 6. Update OpenAI Assistant ID

In all `Message a model*` (assistant type) nodes, update:
```
asst_WGbxqmCg1rA70ZkPqd0k6fQd  →  YOUR_ASSISTANT_ID
```

### 7. Update Email Addresses

In all Gmail nodes, change:
```
samad125612@gmail.com  →  YOUR_ACCOUNTING_EMAIL
```

### 8. Activate Webhook

1. Open the `Webhook` node
2. Copy the webhook URL
3. Set it as your GreenAPI notification URL

---

## 📁 File Structure

```
plant-shop-bot/
├── README.md                          ← You are here
├── workflow/
│   └── plant-shop-bot.json            ← n8n workflow (import this)
└── docs/
    ├── bot-script-hebrew.md           ← Full bot conversation script (Hebrew)
    └── setup-checklist.md            ← Quick setup checklist
```

---

## 🤖 Bot Menu (Hebrew)

```
1️⃣ ייעוץ מקצועי
2️⃣ הזמנות, בדיקת מלאי, הצעות מחיר
3️⃣ טיפול בהזמנה קיימת
4️⃣ מתנות ומארזים
5️⃣ הנהלת חשבונות
6️⃣ שעות פתיחה וכתובת
```

---

## 🔁 Classifier Actions

| Action | Trigger |
|---|---|
| `none` | Keep bot conversation going |
| `sendtogroup` | Human expert needed — send summary to WhatsApp group |
| `suppliermail` | Supplier inquiry — generate & send email to Michal |
| `accountingmail` | Customer billing issue — generate & send accounting email |

---

## 📞 Support

Built for **Marmelstein Nursery** — מושב גני טל (צמוד לגדרה)  
Website: https://mermel-nursery.co.il/
