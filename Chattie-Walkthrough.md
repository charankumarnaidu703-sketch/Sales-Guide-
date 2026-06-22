# 🌿 Chattie: AI-Powered Customer Service Dashboard for Landscaping Businesses
## Project Walkthrough and Strategic Analysis

---

## 1. The Problem: The Administrative Burnout of the Solo Tradesperson

Independent landscapers (*hoveniers*) are artists and builders. They spend their days doing heavy, creative physical labor outdoors—planting gardens, laying stone patios, constructing fences, and shaping lawns. 

However, running a modern landscaping business requires a massive amount of customer communication. A typical customer journey requires a long "qualification" phase: getting the customer's home address, understanding their design wishes (e.g., modern paving, English country garden, child-friendly play lawn), measuring the garden dimensions, collecting photos of the current space, and securing a reliable email address. 

Because potential clients expect fast responses, solo operators face a painful dilemma. They must either interrupt their physical work during the day to answer WhatsApp messages and emails, or spend their evenings typing out the same standard questions to dozens of leads. If they don't respond quickly, the customer moves on to a competitor. If they spend hours typing replies, they lose their personal time, leading to exhaustion and operational bottleneck.

**A Typical Scenario:**
Imagine Jan, a solo landscaper in Utrecht. After nine hours of laying heavy concrete paving stones in the cold rain, he sits down at 7:00 PM with a cup of coffee. He opens his phone to find twelve unread WhatsApp messages and eight new emails. Some are asking basic questions, others are sending vague requests like *"Can you look at my yard?"* 
Before Jan can even think about writing an estimate, he must ask every single person for their address, what services they need, and for photos of their current garden. By 10:00 PM, he is finally done typing the same repetitive questions, exhausted, having spent his entire evening on administrative chores instead of resting or spending time with his family.

---

## 2. The Solution: A Virtual Office Manager for the Garden

**Chattie** solves this problem by acting as Jan's digital office manager, working twenty-four hours a day, seven days a week. It bridges the gap between client communication channels and business operations.

When a client sends a message to Jan's business WhatsApp or email address, Chattie's automated system immediately replies in natural, friendly Dutch. The system understands the context and systematically guides the client through a polite qualification flow, collecting their address, specific wishes, garden dimensions, and photo uploads. 

All of this collected data is structured and saved in real-time to a clean, easy-to-use CRM (Customer Relationship Management) dashboard. 

If a client asks a general question (such as *"Do you lay artificial grass?"* or *"What is your hourly rate?"*), the system references the business's custom knowledge base to provide an accurate answer. 

If Jan wants to reply personally, he can click a button on his dashboard to **pause** the automated system. He is now in complete manual control and can chat directly with the customer. When he is done, he can hand control back to the automation with one tap.

By the time Jan sits down in the evening, he doesn't face a wall of unread inquiries. Instead, he opens his Chattie dashboard and sees a list of fully qualified leads, complete with addresses, list of wishes, dimensions, and high-resolution photos of the gardens. He can review the qualified dossiers in ten minutes, make a quick callback to close the deal, and enjoy the rest of his evening.

---

## 3. What Makes This Different: The Competitive Standouts

While there are many generic chat tools and standard business software platforms, Chattie stands out in three distinct ways:

*   **Multi-Step, Multi-Channel Automated Qualification:** Standard CRM software (like Jobber or Service Autopilot) only provides static, boring contact forms that customers rarely fill out on mobile. Chattie engages customers in active, conversational qualification over both WhatsApp and Email, asking relevant follow-ups to gather necessary data without human intervention.
*   **Human-in-the-Loop Takeover (Pause & Resume):** Most chatbots fail because they get stuck in loops, frustrating the customer. Chattie solves this by giving the business owner absolute control. Jan can pause the AI agent at any moment to chat manually. The dashboard clearly highlights manual messages in a distinct color with a "Manual" label, so the owner can instantly distinguish what the AI said versus what they said.
*   **Multi-Media Trade Intake:** Unlike traditional tools that only accept text, Chattie is built for visual trades. It prompts WhatsApp users to send photos of their current garden and uploads them directly to the client's file in the CRM, displaying them in a swipeable photo gallery modal optimized for mobile viewing.
*   **Deep Dutch Trade Localization:** The platform is localized specifically for the Dutch landscaping market (*hoveniersbedrijven*). It supports localized greetings (e.g., *Goedemorgen*, *Goedemiddag*), understands Dutch dimensions (square meters), and filters inquiries based on the custom service regions specified by the business.

---

## 4. How It All Works: Architecture in Plain English

Rather than a complex stack of code, think of Chattie as a well-designed house with three main rooms:

```
┌────────────────────────────────────────────────────────┐
│             THE COMMAND CENTER (Next.js Dashboard)     │
│  - Jan's view: tracks stats, reads messages, logs calls│
└──────────────────────────┬─────────────────────────────┘
                           │  Real-time updates
┌──────────────────────────▼─────────────────────────────┐
│             THE SECURE VAULT (Supabase Database)       │
│  - Stores customer contacts, message history, & photos │
└──────────────────────────┬─────────────────────────────┘
                           │  Listens & Orchestrates
┌──────────────────────────▼─────────────────────────────┐
│             THE ENGINE (n8n Workflows & AI Brain)      │
│  - Connects WhatsApp/Gmail, classifies, & replies      │
└────────────────────────────────────────────────────────┘
```

1.  **The Command Center (The Next.js Frontend):** This is the visual dashboard Jan opens on his phone or computer. It is designed to feel like a premium mobile app. It displays incoming alerts, allows Jan to read chat streams, log phone calls, edit his business information, and toggle the AI bot on or off.
2.  **The Secure Vault (The Supabase Database):** This is where all business data is safely stored—customer profiles, chat histories, email threads, follow-up dates, and uploaded garden photos. The vault is equipped with "Realtime" sensors. The moment a customer sends a message or a photo on WhatsApp, the database pushes it to Jan's screen instantly without requiring him to refresh the page.
3.  **The Engine (The n8n Workflows & AI Brain):** This is the coordinator operating behind the scenes. Built using **n8n** (an automation designer), it acts like an office assistant. When a message arrives via WhatsApp (linked via Unipile) or Gmail, the engine catches it, runs it through the AI Brain to extract details or classify the email category (e.g., distinguishing a real customer from a supplier invoice or spam), updates the vault, and fires back a response.

---

## 5. Full Walkthrough of Pages & Features

This guided tour explains every feature currently working in Chattie, following the path of a user:

### 1. Operations Dashboard
This is the homepage Jan sees when logging in. It features:
*   **Dynamic Greeting:** Displays a friendly greeting localized to the time of day (*Good morning / Good afternoon / Good evening*) alongside a localized date.
*   **Welcome Banner:** A collapsible onboarding card that guides new users through the key modules.
*   **Bento Stats Grid:** Four high-contrast statistics showing:
    *   *Leads Today:* The number of contacts who completed qualification today.
    *   *Emails:* Volume of customer emails processed in the past week.
    *   *Bot Active:* Number of conversations currently handled by the AI.
    *   *Paused:* Number of active chats currently paused for manual control.
*   **Attention Required Alert:** Urgently highlights any customer conversation where the AI has been paused, with a one-click button to enter the chat and resume control.
*   **Recent Activity Stream:** A live feed showing system operations as they happen (e.g., *"WhatsApp message received,"* *"Gmail draft created"*), styled with color-coded emojis.

### 2. WhatsApp Conversations
This is the messaging dashboard:
*   **Filterable Chat List:** Jan can search for a contact by name or phone number and filter conversations by status (*All, Active, Paused, Qualified*).
*   **Interactive Chat Room:** Clicking a chat opens a real-time messaging interface. It displays the full conversation history. Jan's own manual messages appear in a distinct dark purple color with a "Manual" label, separating them from the green AI messages.
*   **Pause/Resume Control:** A prominent button at the top allows Jan to pause the AI to type a message. The text input bar is locked while the bot is active to prevent accidental interruptions, opening only when paused.
*   **Live Qualification Progress Panel:** Displays a visual 5-step checklist (Address, Wishes, Dimensions, Photos, Email) indicating what information the AI has successfully collected so far.
*   **Swipeable Photo Gallery Modal:** Under the lead's dossier, Jan can click *"View photos"* to open a full-screen, swipe-friendly gallery of the customer's uploaded garden photos.

### 3. Email Leads
This page handles email communication:
*   **AI Email Classification:** Hitting the inbox, emails are automatically categ classified intoories: *CUSTOMER* (inquiries), *SUPPLIER* (bills/invoices), *SPAM* (junk), *INTERNAL* (staff), and *OTHER*.
*   **Threaded Email Viewer:** Displays conversations in a clean thread format, complete with search and filters (*All, New, Active, Qualified*).
*   **Gmail Draft Creator:** The system automatically drafts replies in Gmail based on the client's questions, allowing Jan to approve and send them. Hitting send or typing a reply in the dashboard automatically pauses the AI email assistant.

### 4. Call Notes Log
This screen serves as a quick logger for phone conversations:
*   **Note Logger Widget:** Jan can select a customer contact from a dropdown menu, write a brief summary of a phone call, and select an outcome badge (*Interested, Callback, Voicemail, No Answer, Not Interested*).
*   **Gmail Integration:** Hitting *"Save & Email"* writes the call log to the database and triggers a workflow that automatically emails a summary to Jan's inbox as a permanent record.
*   **Follow-up Scheduler:** Jan can set a specific follow-up date for a callback, which logs a reminder in the system.

### 5. Follow-ups Tracker
This screen prevents leads from slipping through the cracks:
*   **Stale Lead Monitor:** Scans the database for active qualification conversations that have had no response or update for more than 12 hours.
*   **Urgency Levels:** Stale conversations are flagged as:
    *   *Medium:* No activity for 12 to 24 hours.
    *   *High:* No activity for 24 to 72 hours.
    *   *Critical:* No activity for over 72 hours (marked in bold red).
*   **Pull-to-Refresh:** Optimized for mobile, Jan can pull down on the screen to refresh the status of his stale leads instantly.

### 6. Company Info (Knowledge Base Editor)
This settings screen controls the "brain" of the AI agent:
*   **Details Management:** Allows Jan to edit his company name, phone number, and website.
*   **Services List:** A text editor where Jan can detail what services he provides (e.g., *"We install wooden decking but we do not lay asphalt"*).
*   **Service Regions:** Jan defines his travel boundaries (e.g., *"Haarlem and within a 20km radius"*). If a lead lives outside this area, the AI politely declines the job.
*   **Price Indications:** Guidelines the AI uses to answer price questions (e.g., *"Garden renovation starts at €35 per square meter"*).
*   **Email Signature Template:** Jan can set up his formal signature for all automated email drafts.

---

## 6. Honest Constraints & Limitations

Every software has limits. To build trust, here are Chattie's current constraints:

*   **Third-Party API Dependency:** The system relies entirely on external services (Unipile for WhatsApp, Google for Gmail, and OpenAI/Anthropic for LLMs). If any of these services experience downtime, or if Gmail OAuth credentials expire, automated qualification will temporarily stop until re-authenticated.
*   **Intentional Response Delays (Debounce):** To prevent the AI from responding to every short message in a fragmented sentence (e.g., sending five separate messages: *"Hi"* -> *"My name is Jan"* -> *"I have a lawn"*), the engine has a built-in "debounce" delay. It waits for 1 to 2 minutes of silence from the customer before assembling their messages and passing them to the AI. This means the bot does not respond instantly, which is necessary for quality but may feel slow to a fast typer.
*   **Media Preview Restrictions:** While customers can upload video, audio, or document attachments via WhatsApp, and these files are successfully saved to the database, only image files (.png, .jpg) are supported by the swipeable photo gallery modal. Non-image files must be opened directly via database links.
*   **No Native Calendar Sync:** The dashboard allows logging follow-up dates in Call Notes and tracking stale leads, but it does not yet feature a calendar view or direct two-way sync with Google Calendar or Calendly in the interface.

---
---

## 7. Pricing Structure & Operational Costs

To deliver a fully customized, production-ready system, the pricing is divided into a one-time setup fee, third-party infrastructure requirements, and ongoing developer support.

### Cost Breakdown Overview

| Service / Component | Cost | Frequency | Details & Requirements |
| :--- | :--- | :--- | :--- |
| **Custom Dashboard & Automation Build** | **$500.00** | One-time | Building the Next.js CRM dashboard and tailoring n8n workflows to custom client requirements. |
| **Developer Support** | **$100.00** | Monthly | Ongoing maintenance, system health monitoring, and technical support. |
| **n8n Workflow Automation (VPS)** | **$6.00 – $7.00** | Monthly | Virtual Private Server hosting fee to run the self-hosted n8n engine. |
| **Database & Backend (Supabase)** | **$25.00** | Monthly | Supabase Pro plan for database hosting, backups, and real-time synchronization. |
| **Vercel Frontend Hosting** | **$0.00 / $20.00** | Monthly | Hobby plan is free. Optional Pro plan is $20/month for team features and enhanced bandwidth. |
| **Meta Developer Account (WhatsApp)** | **$0.00 + Usage** | Variable | Free setup and free within 24-hr windows. Template configuration costs **$2.00 – $4.00** per template. |
| **Google Cloud APIs (Gmail & Drive)** | **$0.00 + Usage** | Variable | Free for the first 3 months (requires credit card for signup). Pay-as-you-go based on usage thereafter. |
| **Google Gemini API Key (AI Engine)** | **Pay-as-you-go** | Variable | Configured via Google Cloud. Cost scale depends entirely on AI message traffic volume. |

---

### Detailed Fee Breakdown

#### 1. One-Time Setup & Development Fee ($500)
This covers the complete implementation of the solution tailored specifically to your business workflows. It includes:
*   Building and styling the Next.js operations dashboard.
*   Designing and deploying the database structure in Supabase.
*   Configuring custom automation pipelines (WhatsApp & Gmail classification) in n8n.
*   Integrating custom service regions, company info, and pricing rules into the AI knowledge base.

#### 2. Infrastructure & Tooling Costs (Client-Owned Accounts)
To ensure data privacy and long-term autonomy, the client registers their own developer accounts. The operational costs include:
*   **n8n Automation Engine:** Self-hosted on a Virtual Private Server (VPS) at **$6.00 to $7.00/month** to avoid high SaaS plan fees.
*   **Database (Supabase):** Run on the Pro plan at **$25.00/month** to guarantee resource safety, automated backups, and database stability.
*   **Frontend Hosting (Vercel):** Starts on the **Hobby (Free) plan**, which is sufficient for initial volumes. Can switch to the **Pro plan ($20.00/month)** for more robust usage requirements.
*   **WhatsApp API (Meta Developer Platform):** Meta does not charge a subscription fee for the WhatsApp Business API. Incoming messages and normal replies within a 24-hour window are free. Messages initiated outside the 24-hour window using template configurations incur a fee of **$2.00 to $4.00** depending on the specific template setup and volume.
*   **Google Cloud Platform & Workspace APIs:** Used for Gmail integration, Call Logs sync, and Gemini API keys. Google Cloud offers a **free tier and credits for the first 3 months** (credit card required for verification). After the trial period, billing is pay-as-you-go and generally negligible under standard business volumes.

#### 3. Monthly Maintenance & Developer Support ($100)
A recurring monthly support fee of **$100.00** covers:
*   General maintenance and monitoring of n8n automation stability.
*   Handling OAuth token refreshes (e.g., Google or WhatsApp connection updates).
*   Troubleshooting and assistance with minor prompt tuning or adjustments to the company knowledge base.

---



 Glossary of Terms

*   **API (Application Programming Interface):** A digital bridge that allows two different software programs to talk to each other. For example, Chattie uses an API to let its dashboard talk to WhatsApp.
*   **Database:** A secure digital storage vault where all of the business's information (leads, messages, settings, photos) is kept.
*   **Webhook:** A real-time notification system. When something happens in one app (like a customer sending a WhatsApp message), it fires a "webhook" to instantly tell another app (like n8n) to take action.
*   **n8n:** The automation software engine that coordinates behind-the-scenes workflows, moving data between WhatsApp, Gmail, the database, and the AI.
*   **Supabase:** The cloud service provider hosting Chattie's database, security credentials, and photo storage.
*   **Debounce:** An intentional delay that waits for a customer to finish typing multiple short messages before triggering the AI response, preventing the bot from responding repeatedly.

**Site Url:**http://chattie-9vo6.vercel.app/
