🧠 Project Explanation
---

Welth is a full-stack AI-powered personal finance platform I built using Next.js 15, React 19, Prisma, Supabase, Clerk, Gemini AI, Inngest, Arcjet, and Shadcn UI.
The platform allows users to manage their finances intelligently: they can track and categorize transactions, analyze spending patterns, scan receipts with AI, set budgets, and receive automated monthly insights and alerts — all in a modern, production-grade SaaS environment.

I approached this project as if I were building a real product. It combines modern frontend frameworks, a typed backend with Prisma and Supabase, AI capabilities for data extraction and summarization, background job automation, and enterprise-level authentication and security.

![image alt](https://github.com/rahimrehann/Wealth/blob/e4b6fdc478eb25569e690ec799e840c72389b33b/main%20page%20photo.png)


🧭 How It Works (End-to-End)
---

1. Authentication (Clerk)
Users sign in using Clerk’s secure auth system. It handles sessions, JWTs, and organization management, allowing me to focus on the app’s core features while ensuring production-grade security.

2. Accounts & Transactions (Prisma + Supabase)
Each user can create multiple accounts (e.g., credit card, chequing). Transactions are stored in a Supabase Postgres database using Prisma ORM. I designed the schema with proper indexing, foreign keys, and cent-based amounts to avoid floating-point errors.

3. Dashboard Visualization (Next.js + Recharts)
The dashboard aggregates spending data in real time, showing KPIs like total monthly spend, remaining budget, top merchants, and more. I built bar and pie charts using Recharts, with all data fetched through optimized SQL queries via Prisma.

4. AI Receipt Scanning (Gemini API)
One of the most powerful features is the AI receipt scanner:

Users upload a receipt image. The backend uses Gemini’s Vision model to perform OCR and extract raw text. Then, the LLM is prompted with a strict Zod schema to return structured JSON (merchant, date, total, tax, items, etc). The result is validated, converted into a transaction, and saved automatically — turning messy receipts into structured finance data.

(Currently Working On this...)

![image alt](https://github.com/rahimrehann/Wealth/blob/3fd6c278ff0c189b0557b7747ca61643613b2d8a/dashboard%20pic.png)

5. Budgets & Alerts (Inngest)
Users can set monthly budgets. Inngest cron jobs run daily to check spending:

If spending exceeds 80% of the budget, an email alert is sent.

If spending passes the budget, a warning is issued.
These are background functions, so the user experience remains smooth.

6. Monthly Reports & AI Insights (Inngest + Gemini)
On the 1st of each month, an Inngest job aggregates last month’s spending, generates a narrative summary using Gemini, compiles charts, and emails a complete Monthly Report to the user. This turns raw transaction data into meaningful insights automatically.

7. Security & Rate Limiting (Arcjet)
All write and AI endpoints are protected by Arcjet. It applies sliding-window rate limiting per user/IP and bot protection on public pages. This ensures API stability and prevents abuse.


📡 APIs & Services Used
---

Service	Purpose
Clerk	Authentication, user sessions, SSR auth<br/>
Supabase Postgres	Main database for accounts, transactions, budgets<br/>
Prisma	Type-safe database access & schema migrations<br/>
Gemini API	Receipt OCR, structured data extraction, monthly insights generation<br/>
Inngest	Scheduled jobs (budget alerts, recurring txns, monthly reports)<br/>
Arcjet	API rate limiting & bot protection<br/>
Recharts	Data visualization (pie & bar charts)<br/>
Vercel	Deployment (to be done....)<br/>


🧠 What I Learned
---

Building this project pushed me to work at the intersection of frontend, backend, and AI — and it taught me more than just coding.<br/>
I learned how important it is to treat AI like an unreliable teammate: powerful, but only if you wrap it with strict validation, error handling, and clear instructions.<br/>
I saw firsthand how moving background work off the main thread (with Inngest) makes everything more stable and scalable.<br/>
Designing proper database schemas, using cents for money, adding indexes, securing endpoints, and rate limiting with Arcjet — all of these reinforced that real-world apps are built on strong foundations, not hacks.<br/>
I also learned to think like a system designer, not just a coder. Every service I integrated had a reason, a trade-off, and a role.<br/>
Most importantly, this project reminded me that you don’t need to wait for “someday” to build something ambitious. You just have to start. Every feature felt overwhelming at first — AI, cron jobs, rate limiting — but breaking it down piece by piece, I was able to build something I’m genuinely proud of.<br/>

💡 If you keep shipping, learning, and iterating, complex projects stop feeling impossible — they start feeling inevitable.
