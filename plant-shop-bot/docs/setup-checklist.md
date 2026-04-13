# ✅ Setup Checklist — Plant Shop Bot

Quick checklist before going live.

---

## Step 1 — Import
- [ ] Upload `workflow/plant-shop-bot.json` to n8n

## Step 2 — Credentials
- [ ] Add **OpenAI API Key** → name it `OpenAi -- Logit`
- [ ] Add **second OpenAI key** (or same) → name it `Tal ChatGpt`
- [ ] Connect **Google Sheets OAuth2** → name it `pant sheet samad`
- [ ] Connect **Gmail OAuth2** → name it `Rohit Gmail account`

## Step 3 — GreenAPI (WhatsApp)
- [ ] Update instance URL in all HTTP Request nodes
- [ ] Update WhatsApp Group Chat ID (`923070650940@c.us` → your group)

## Step 4 — Google Sheet
- [ ] Create sheet with columns: `Name | Number | Thread Id | Chat History | Chat Mode`
- [ ] Copy Sheet ID → replace in all Google Sheets nodes

## Step 5 — OpenAI Assistant
- [ ] Create Assistant in OpenAI platform with bot script
- [ ] Copy Assistant ID → replace `asst_WGbxqmCg1rA70ZkPqd0k6fQd`

## Step 6 — Email
- [ ] Update `samad125612@gmail.com` to real accounting email in all Gmail nodes

## Step 7 — Go Live
- [ ] Activate workflow in n8n
- [ ] Copy webhook URL
- [ ] Set webhook URL in GreenAPI notification settings
- [ ] Send test message to WhatsApp number
- [ ] Verify response received ✓

---

## 🔑 Values to Replace

| Placeholder | Replace With |
|---|---|
| `7103` | Your GreenAPI instance |
| `7103242575` | Your WhatsApp instance ID |
| `3d98966d04804...` | Your GreenAPI API token |
| `923070650940@c.us` | Your expert WhatsApp group ID |
| `1hfyzxeTQs0yODvu...` | Your Google Sheet ID |
| `asst_WGbxqmCg1rA70ZkPqd0k6fQd` | Your OpenAI Assistant ID |
| `samad125612@gmail.com` | Your accounting email |
| `rNjm517Ey2CKNLo3` | Will auto-update with new credentials |
| `kFDxtbPhnBTQa5eL` | Will auto-update with new credentials |
| `62IiiQVdsIGUQMiN` | Will auto-update with new credentials |
