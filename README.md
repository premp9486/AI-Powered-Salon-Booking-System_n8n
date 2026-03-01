# 🤖 AI-Powered Salon Booking System (Telegram Demo)

An AI booking assistant that handles salon appointments through natural conversation.
Built using n8n, OpenAI, Google Sheets, and Google Calendar.

> ⚠️ For testing and demo, Telegram is used.
> The same logic can be connected to Instagram, WhatsApp, and Facebook Messenger.

---

# 🚨 Problem

Salons usually handle bookings through calls and WhatsApp chats.

This creates problems:

* Staff manually reply to every message
* Double bookings happen
* No centralized system
* Customers wait for replies
* No tracking of staff assignments
* No booking outside business hours

There is no automation. Everything depends on humans.

---

# ✅ Solution

An AI-powered booking assistant.

It:

* Talks naturally with customers
* Understands free text like “haircut friday 5pm”
* Collects missing details step-by-step
* Checks availability rules
* Assigns staff automatically
* Creates Google Calendar event
* Saves booking in Google Sheets
* Sends confirmation instantly
* Works 24/7

No forms. Just conversation.

---

# 🛠️ Tools Used

### Core Stack

* **n8n** – workflow automation engine
* **OpenAI (GPT-4o)** – conversation intelligence
* **Telegram Bot API** – demo interface
* **Google Sheets** – booking database
* **Google Calendar** – scheduling + conflict control

### Logic Components

* AI Agent with memory
* Session tracking using Telegram user ID
* Date-time formatter (ISO 8601)
* JavaScript nodes for parsing + staff assignment
* Round-robin staff distribution

---

# 🏗️ Architecture

### High-Level Flow

1. Customer sends message on Telegram
2. User data extracted
3. Services loaded
4. Current time injected
5. AI Agent processes conversation
6. If booking ready → booking flow
7. Parse details
8. Assign staff
9. Format date-time
10. Create Google Calendar event
11. Save to Google Sheet
12. Send confirmation

---

# 📊 Architecture Diagram (Simple)

```
Customer (Telegram)
        │
        ▼
Telegram Trigger
        │
        ▼
Extract User Data
        │
        ▼
Load Services + Add Time
        │
        ▼
AI Agent (OpenAI + Memory)
        │
        ▼
Check If Ready?
     │           │
     │Yes        │No
     ▼           ▼
Parse Details   Continue Chat
     │
     ▼
Assign Staff
     │
     ▼
Format DateTime
     │
     ▼
Create Google Calendar Event
     │
     ▼
Save to Google Sheets
     │
     ▼
Send Confirmation
```

---

# 🧠 Architecture (Detailed Logic)

### Conversation Layer

* Extract Telegram userId
* Load salon services
* Add current time for validation

### AI Processing

* GPT model understands intent
* Memory stores last messages
* Ensures service + date + time + phone collected

### Decision Routing

If AI says:

> “I’m creating your booking now”

Then booking workflow triggers.

Otherwise, conversation continues.

### Booking Engine

* Parse structured data
* Assign staff (round-robin)
* Format time to ISO 8601
* Create calendar event
* Update sheet
* Notify customer + salon

---

# 🚀 How to Run

### 1. Setup n8n

Use Docker or Cloud version.

### 2. Create Telegram Bot

* Message @BotFather
* Use `/newbot`
* Copy bot token

### 3. Add Credentials in n8n

* OpenAI API Key
* Telegram Bot Token
* Google OAuth2

### 4. Create Google Sheet

Columns:

```
Booking ID
Customer Name
Phone
Service
Price
Duration
Date
Time
Status
Staff Assigned
Created At
User ID
Calendar Event ID
```

### 5. Create Google Calendar

Create one calendar per staff member.

### 6. Import Workflow

Import your n8n JSON workflow.

### 7. Activate Workflow

Turn on the workflow.

---

# 🧪 Testing (Telegram Demo)

Send:

```
hello
i need haircut
hair cut men friday 5pm
9876543210
```

You should see:

* Booking confirmation
* Google Sheet updated
* Calendar event created

---

# 📸 Sample Result

### Conversation Example

Customer:

```
i need hair cut kids on 2 march 5pm
```

Bot:

```
Please share your phone number.
```

Customer:

```
9873031144
```

Bot:

```
Booking Confirmed!

Service: Hair Cut - Kids
Date: 2 March
Time: 5:00 PM
Staff: Priya
Booking ID: BK1709876543210
```

---

### Google Sheet Entry

| Booking ID      | Name | Phone      | Service       | Date    | Time | Staff | Status    |
| --------------- | ---- | ---------- | ------------- | ------- | ---- | ----- | --------- |
| BK1709876543210 | John | 9873031144 | Hair Cut Kids | 2 March | 5 PM | Priya | Confirmed |

---

### Google Calendar Event

Title:

```
Hair Cut Kids - John
```

Time:

```
5:00 PM – 5:30 PM
```

Description includes:

* Phone
* Booking ID
* Staff name

---

# 🔄 Multi-Platform Support

Currently used:

* ✅ Telegram (for testing & demo)

Can be connected to:

* WhatsApp (via WATI / Meta API)
* Instagram DM
* Facebook Messenger
* Web chat widget

Only trigger node changes.
Core booking logic remains the same.

---

# ✨ Key Features

* Natural language understanding
* Memory-based conversation
* Multi-staff scheduling
* Conflict prevention
* Automatic confirmation
* Real-time calendar sync
* 24/7 availability


