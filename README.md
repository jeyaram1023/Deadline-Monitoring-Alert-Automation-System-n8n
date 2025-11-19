# User Deadline Monitoring & Alert Automation System

---

## 🟦 1. Project Overview

A smart automation system to **track user deadlines (e.g., students, employees, research team members)**, monitor real-time submissions, and **send instant Telegram alerts** when deadlines are missed.  
Leverages **n8n automation**, **Supabase** for cloud database, and a customizable **HTML submission portal** for a seamless, hands-off experience.

---

## 🟦 2. System Architecture Diagram


<img width="1854" height="771" alt="Screenshot 2025-11-19 214124" src="https://github.com/user-attachments/assets/0fcd7092-673d-4be3-93ae-3564101e5eb2" />
<img width="1568" height="594" alt="Screenshot 2025-11-20 003347" src="https://github.com/user-attachments/assets/cc0b7884-f0fd-46fb-851b-4228f7f7c4ee" />


---

## 🟦 3. Technology Stack

- **n8n**: Automation/Workflow Engine
- **Supabase**: PostgreSQL Database + REST API
- **Telegram Bot API**: Alert delivery
- **HTML / CSS / JavaScript**: Submission portal for users
- **GitHub Pages / Vercel**: Static portal hosting

---

## 🟦 4. Features

- Admin can add users and assign unique deadlines
- User-facing form for easy online submissions
- Submissions timestamped and stored in Supabase
- n8n workflow checks each deadline vs latest submission
- Sends Telegram alerts only to users who miss or are late
- Links to web portal included in all reminders
- Runs automatically on schedule (daily/hourly)
- Highly scalable (10,000+ users supported)

---

## 🟦 5. Sample Data: `local_data_table_sample.csv`

This CSV is used to load all users into your n8n Data Table. **You must create, edit, or import this when setting up the system!**

**Required columns:**
- `user_id` (e.g., USER001)
- `user_name`
- `telegram_chat_id` (from @userinfobot)
- `allowed_time` (deadline, ISO e.g., 2025-12-01T17:00:00Z)
- `email` (optional)
- `phone` (optional)

**Sample Table:**

<img width="72" height="44" alt="Screenshot 2025-11-19 214028" src="https://github.com/user-attachments/assets/38d92fc8-ae4e-40c0-89b6-96ebd06f2e08" />


**How to use in n8n:**
1. Go to “Data Tables” in n8n.
2. Create a new table (e.g., `user_deadlines`).
3. Add fields: user_id, user_name, telegram_chat_id, allowed_time, (optionally email, phone).
4. Click "**Import CSV**" and select your `local_data_table_sample.csv`.
5. Confirm all users appear in the table with correct data.

---

## 🟦 6. HTML Submission Portal

- **Users** access a simple form with fields for user ID, name, upload, etc.
- **Configuration:**  
  - Add your Supabase URL and Anon key in the HTML/JS.
  - Set table name for submission records.
  - Add form validation if needed.
- **Deployment:**  
  - Host via GitHub Pages, Vercel, or Netlify—just upload and deploy!
- **Internal flow:**  
  - Form POSTs directly to Supabase REST API; data saved to `submissions` table.

---

## 🟦 7. Supabase Setup

- Create `submissions` table with fields: id, user_id, created_at, report_link, uploaded_file, status
- Enable RLS for insert/select (frontend users), disable for backend (n8n)
- Use Project URL and Anon key for public/portal access; use Service key with n8n (never expose this in HTML)

---

## 🟦 8. n8n Setup

1. Install/Access n8n (Cloud, Docker, Desktop app supported)
2. Import the workflow JSON file
3. Create Data Table as above, load sample data
4. Add Supabase credentials (Project URL, Service Key in n8n)
5. Add Telegram credentials (Bot token)
6. Set up Cron schedule (daily/hourly as desired)
7. Map nodes/fields as per guide

---

## 🟦 9. Telegram Bot Setup

- Create bot using [@BotFather](https://t.me/botfather), save the token
- Add Telegram credential in n8n workflow node
- For each user, obtain chat ID using [@userinfobot](https://t.me/userinfobot)
- Test the bot by sending yourself a message

---

## 🟦 10. Workflow Execution Step-by-Step

1. **Admin**: Loads/imports users into Data Table using `local_data_table_sample.csv`
2. **User**: Submits a report via the HTML portal
3. **Supabase**: Stores submission, auto-timestamps row
4. **n8n Cron**: Scheduled check runs, fetches user list and recent submissions
5. **Logic**: Compares each user’s latest submission with their deadline
6. **Alert**: If missed/late, Telegram sends a custom, dynamic alert to that user
7. **Admin**: Optionally reviews data in Supabase or n8n

---

## 🟦 11. Testing Guide

- Add your own chat ID with a past deadline, run workflow manually—should receive alert in Telegram.
- Submit a file, run the workflow again—should NOT receive alert if submitted on time.
- Test missing chat ID, wrong API key, and CORS errors for troubleshooting.

---

## 🟦 12. Error Handling

- **Telegram “can't parse entities”**: Set parse mode to “None” in Telegram node
- **Supabase CORS**: Add portal origin to Supabase CORS allowed list
- **Workflow not running**: Workflow may not be active or Cron misconfigured
- **Missing fields**: Confirm Data Table matches sample CSV headings
- **Key issues**: Use Service Role Key for n8n, never in frontend/portal

---

## 🟦 13. Security Guidelines

- **Never expose Service Key** in frontend/HTML
- **Protect all secrets**: Use n8n Credentials/Environment variables
- **Lock down CORS and RLS** in Supabase
- **Always use HTTPS** for your submission portal and Supabase API

---

## 🟦 14. Example Alert
Hi Neha Patel,

You have not submitted your research report before the deadline (2025-12-01T17:00:00Z).
Reason: No submission found before deadline

Please submit as soon as possible: Submission Portal

Best,
Deadline Monitoring Bot


---

## 🟦 15. Future Upgrades

- Add email alert/reminders
- Build an admin dashboard for submissions
- Support PDF/file uploads and analytics
- Pre-deadline “reminder” alerts, department logic

---

## 🟦 16. Credits

- **Developer:** Jeyaram Reddy (replace with your name/username)
- **Tools:** n8n, Supabase, Telegram Bot API, GitHub Pages, HTML/CSS/JS
- **License:** MIT

---

## ⭐ Quickstart

1. **Fork & clone** this repo
2. **Create** and import your user data with `local_data_table_sample.csv`
3. **Set up** n8n, Supabase, Telegram credentials
4. **Deploy** the portal on GitHub Pages/Vercel
5. **Test** with your data—Go live!

---

Ready to automate deadline monitoring?  
**Deploy, add users, and get started today!**

---


