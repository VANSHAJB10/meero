# Delta AI Academy — Website Content

All visible copy on the site, grouped by page and section, in the order a visitor meets it. Each section notes the source file so edits can be traced back to the code.

**How to read this file**

- `{price}` means the country-aware plan price: **₹999** for India, **AED 99** for everywhere else.
- Text in *italics inside brackets* describes things that aren't copy (images, layout) so the section makes sense.
- Dynamic text (countdowns, dates, counts) is described in brackets with how it is produced.
- The "recently enrolled" popup that used to appear on marketing pages has been removed and is not part of this file.
- Items that need a decision are listed at the end under **Items to review**.

**Contents**

1. [Site-wide](#1-site-wide)
2. [Home page](#2-home-page)
3. [Curriculum page](#3-curriculum-page-course)
4. [Free seminar page](#4-free-seminar-page-seminar)
5. [Free episode page](#5-free-episode-page-watch)
6. [Order / checkout](#6-order--checkout-order)
7. [Beginner ad landing page](#7-beginner-ad-landing-page)
8. [Course area (signed-in)](#8-course-area-signed-in-learn)
9. [Blog](#9-blog-blog)
10. [404 page](#10-404-page)
11. [Items to review](#11-items-to-review)

---

## 1. Site-wide

### 1.1 Page metadata (`app/layout.tsx`, `lib/site.ts`)

- **Site name:** Delta AI Academy
- **Page title:** Delta AI Academy — Build AI powered applications
- **Description:** Build AI powered applications even if you've never coded before. Learn React, React Native, Python FastAPI and MongoDB with AI tools like Codex, Claude Code and Lovable, and ship four real projects on one all-inclusive plan.
- **Programme name** (used on the pricing card, enrol bar, checkout, invoice, certificate): Master Software Development with AI
- **Contact phone:** +91 85900 26442 (call and WhatsApp)
- **Site URL:** https://www.deltaaiacademy.ai

### 1.2 Launch-price banner (`components/offer-banner.tsx`)

Pinned above the nav on every marketing page. Shown only while the offer is live and hidden once the deadline passes, and hidden for signed-in users and inside the course.

- **Badge:** {discount}% OFF *(calculated from the struck-through price)*
- **Text:** Launch price ends {deadline date, e.g. "Wed, 30 Sept"}
- **Countdown:** days / hours / minutes / seconds ticking down. On phones the label reads "Ends in".
- **Deadline in code:** 30 September 2026, 23:59:59 IST (`lib/offer-deadline.ts`)

### 1.3 Navigation (`components/site-header.tsx`, `components/mobile-nav.tsx`)

- What you'll learn → `/#learn`
- Projects → `/#projects`
- Curriculum → `/course`
- Pricing → `/#pricing`
- Blog → `/blog`
- **Brochure** (opens the PDF)
- **Join now** (→ `/order`). For signed-in users, or right after payment, this button reads **Start course** (→ `/learn`).
- Mobile menu: aria labels "Open menu" / "Close menu".

### 1.4 Intro preloader (`components/preloader.tsx`)

Home page only, about 3 seconds. Four stacked badges that read: **Let's** · **Build** · **AI powered** · **Applications**

### 1.5 Entry popups (`components/site-popups.tsx`)

Shown in sequence on marketing pages (not on checkout, seminar, watch, learn or admin; not for signed-in users).

**Popup 1 — free webinar** (appears 3 seconds after load, if a session is scheduled)

- *Poster image for the next session* (`/seminar/free-website.jpg`)
- Image description: Free live webinar — {session title}, {date} at {time}, with {speaker}
- **Button:** Book your free slot (→ `/seminar`)
- **Dismiss link:** Maybe later — it's on {date}

**Popup 2 — free episode** (appears after popup 1 is closed)

- Uses the free-episode dialog (see [5. Free episode page](#5-free-episode-page-watch)). Link text: Open full page.

### 1.6 Chat widget — "Ask Delta AI" (`components/ai-chat-widget.tsx`, `lib/faq-bot.ts`)

A preset-answer bot (no AI model behind it).

- **Header:** Ask Delta AI — Instant answers, no waiting
- **Greeting:** Hi! I can answer common questions about the programme instantly. Tap one below, or type your own.
- **Starter questions:**
  - What will I build during the programme?
  - Do I need any coding experience to join?
  - What does it cost?
  - How is the course structured?
- **Fallback when nothing matches:** I don't have a preset answer for that one — tap a question below, or use "Join now" / "Get the brochure" to ask the team directly.
- **When someone asks to enrol:** Great — you can enrol right here. Pop in your details below and I'll take you straight to payment.
- **User message when tapping enrol:** I'd like to enrol.
- **In-chat enrol form:** placeholders "Full name", "Phone number", a country selector; button **Continue to payment** (shows "Preparing your payment…" while sending). Validation: "Enter your name." / "Enter a valid email address." / "Enter a valid phone number." Error: "Could not start checkout. Please try again."

**Full list of preset answers**

| Question | Answer |
|---|---|
| Do I need any coding experience to join? | The programme is built for complete beginners and assumes no prior AI or development experience. You start with AI assisted tools from day one and learn the underlying concepts as you build. |
| What will I build during the programme? | Four complete applications: an AI portfolio website, an ecommerce storefront, a social media web app, and the same social product as a mobile app in React Native with Expo. Every one is deployed and yours to keep. |
| Which technologies will I learn? | React.js for the web, React Native with Expo for mobile, Python FastAPI for backend APIs, and MongoDB Atlas for data. You will also learn version control with GitHub. |
| Which AI tools will I work with? | Twelve tools in total. The core building agents are ChatGPT Codex, Claude Code, Lovable, Google AI Studio and Kimi — alongside research tools like Perplexity, automation with n8n, and others such as Cursor, GitHub Copilot, v0, Replit and Windsurf. |
| How does the teaching actually work? | You don't write code by hand. You describe the app you want, an AI agent builds it, and you review, direct and refine the result. The skill you're building is judgement and direction, not memorising syntax. |
| Will my applications actually go live? | Every project is deployed to production using Vercel, Hostinger VPS and Cloudflare, so it ends up at a real URL you can share with employers or clients. |
| What does it cost? | One plan, {price} total — every project, every tool, every skill area. No tiers, no subscriptions. |
| What will I have at the end? | A portfolio of real web and mobile applications, a working understanding of AI powered development, production deployment experience, and the confidence to build your own ideas. |
| How do I join? | Tap "Join now" anywhere on the page to get started, or "Get the brochure" if you'd rather read the details first. |
| How is the course structured? | 4 modules, 26 topics: Introduction to AI, AI-Assisted Design, Full-Stack Web Development, Application Development Fundamentals. See the full breakdown, topic by topic, on the Curriculum page. |
| What does the AI fundamentals module cover? | Module 1 covers how AI actually works — what a model is, tokens and context windows, why AI hallucinates, traditional development versus AI-powered development, and prompt engineering fundamentals. |
| What do I learn in the design module? | Module 2 covers AI-assisted design — finding design references, designing with Figma Stitch, then actually building and hosting a landing page and a portfolio website with Git and Vercel. |
| What's in the full-stack development module? | Module 3 covers full-stack web development — how frontend, backend and database fit together, comparing different tech stacks, planning a project properly, then building and hosting it with a custom domain. |
| Does the course cover mobile app development? | Module 4 covers application development fundamentals — website versus mobile, choosing the right technology stack, planning an application, and how backend architecture actually works. |
| What language are classes conducted in? | Classes are conducted in English, with live support also available in Malayalam if you'd prefer it. |
| How can I pay? | Pay the {price} in full at enrolment, by card or through Razorpay. We don't offer Tabby or Tamara instalments. |

### 1.7 Sticky enrol bar (`components/enroll-bar.tsx`)

Appears while scrolling on marketing pages (not for signed-in users or in the course).

- Programme name: Master Software Development with AI
- Price: {price} · struck-through original price · {discount}% off
- **Button:** Enroll now (→ `/order`). On the order page it reads **Complete order** and scrolls to the form.

### 1.8 Contact dialog — "Talk to our team" (`components/contact-dialog.tsx`)

- **Heading:** Join Delta AI Academy
- **Intro:** Leave your details and our team will get back to you about the programme.
- **Fields:** Full name (placeholder "Your name"), email (placeholder "you@example.com"), Phone number (placeholder "+971 50 000 0000")
- **Payment preference:** "How would you like to pay?" — Pay in full / Razorpay
- **Button:** Send my details ("Sending…" while submitting)
- **Success message:** We have your details and will get back to you shortly.
- **Errors:** Please enter your name. / Please enter a valid email address. / Please enter a valid phone number. / Something went wrong. Please try again.

### 1.9 Footer (`components/site-footer.tsx`)

- **Headline:** Build AI powered applications
- **Buttons:** Download brochure · Join the program
- **Talk to us:** +91 85900 26442 · WhatsApp
- **Link columns**
  - *Program:* What you'll learn · Projects you'll build · AI tools
  - *Outcomes:* What you'll achieve · Portfolio
  - *Stack:* React.js · React Native · Python FastAPI · MongoDB Atlas
  - *Deployment:* Vercel · Hostinger VPS · Cloudflare
  - *Academy:* About · Brochure · Contact
  - *Join:* Enrol now · Talk to our team
- *Oversized wordmark along the bottom:* DELTA AI ACADEMY
- *Legal links (Privacy policy, Accessibility, Terms of service) and the © line are in the code but currently commented out, so they do not show.*

---

## 2. Home page

Section order follows `app/page.tsx`.

### 2.1 Hero (`components/hero.tsx`)

- **Headline:** BUILD WEBSITES AND APPS IN MINUTES WITH AI
- **Sub-headline:** Even if you've never coded before. We make AI development simple and accessible for beginners.
- **Webinar call-to-action:** a countdown to the next free webinar and a booking button (see [4. Free seminar page](#4-free-seminar-page-seminar)). Shown only while a session is scheduled.
- **Phone-only strip:**
  - Buttons: Join now · Get the brochure
  - Three facts: **4** projects · **12** AI tools · **{price}** one plan
- **Card 1 — Start building today**
  - Join the program and build real applications from your very first week, with no prior AI experience.
  - Button: Join now
- **Card 2 — Talk to our team**
  - Not sure where to start? We'll walk you through the program and what you'll build.
  - Button: Get the brochure

### 2.2 AI tools (`components/ai-tools.tsx`)

- **Label:** AI tools
- **Headline:** Modern developers use AI tools to build faster and more efficiently
- **Scrolling logo strip (12 tools):** Lovable · ChatGPT Codex · Claude · Google AI Studio · Cursor · GitHub Copilot · v0 · Replit · Windsurf · Perplexity · n8n · Hugging Face

### 2.3 Pricing (`components/pricing-section.tsx`)

- **Label:** Pricing
- **Headline:** One plan. Everything included.

**How to join (three steps)**

1. **Tell us you're in** — Tap "Join now" and leave your name, email and phone — takes under a minute.
2. **Choose how to pay** — Pay by card or through Razorpay — right there in the same form.
3. **Get your payment link, fast** — The team follows up with the right link for the method you picked — no back-and-forth to figure it out.

**Banner — "Learn. Build. Ship."** (`components/free-fifty-banner.tsx`)

- **Tag:** Learn. Build. Ship.
- **Headline:** YOU DON'T NEED A BIG COURSE TO BECOME A DEVELOPER.
- **Line:** Everything you need to build is here.
- **Counter** (only shown once the enrolment count reaches 25): "{number} already building with us" — see Items to review.

**Class preview**

- *Looping video card.* Text: **See a class before you join**. Clicking it plays the free episode. Accessible label: Watch a class — play the free episode.

**Price card**

- Programme name: Master Software Development with AI
- Price: {price}, with the struck-through original (₹10,000 or AED 440) and a "{discount}% off" tag
- **Text:** One price for the whole programme every project, every tool, every skill area. No tiers to compare.
- **What's included**
  - Four complete applications, web and mobile
  - Five skill areas: full stack, mobile, backend, database, deployment
  - Production deployment on Vercel, Hostinger VPS and Cloudflare
  - No prior coding experience needed
  - Live support in English and Malayalam
- **Buttons:** Join now · Talk to our team
- **Payment line:** Pay in full, or split it at enrolment — Razorpay

### 2.4 Certificate (`components/certificate-section.tsx`)

- **Label:** Certificate
- **Headline:** Finish with a certificate, not just a folder of code
- **Text:** Every graduate gets a Delta AI Academy certificate of completion — proof you shipped four real, deployed applications, not just watched tutorials.
- *Sample certificate card:*
  - Ribbon: Delta official certificate
  - "Your Name successfully completed"
  - Title: Master Software Development with AI
  - Body: By completing this programme, the learner has demonstrated practical skills in AI-assisted software development and shipped four deployed applications across full-stack, mobile, backend and database work.
  - Course length: 26 lessons
  - Date of issue: 15 June 2026 *(sample)*
  - Certificate ID: DAA-2026-4C81-7F30-92B5 *(sample)*
  - Signature caption: Delta AI Academy
- **Caption:** Sample certificate — yours is issued with your name, date and a unique certificate ID on completion.

### 2.5 How we teach (`components/vibe-coding.tsx`)

- **Label:** How we teach
- **Headline:** We don't teach you to write code. We teach you to build with AI.
- **Text:** No syntax drills, no memorising APIs. You work the way developers actually work now — describing what you want and directing an AI agent until it is built and live.
- **Three steps**
  1. **Describe it** — You explain the app you want in plain language — the screens, the data, what it should do. No syntax, no boilerplate.
  2. **The agent builds it** — Codex, Claude Code, Lovable, AI Studio or Kimi writes the code and wires it together while you watch it take shape.
  3. **You direct and ship it** — You review what it produced, tell it what to change, and push the result live. Judgement is the skill — not typing.
- **The agents you build with:** ChatGPT Codex · Claude Code · Lovable · Google AI Studio · Kimi
- **Closing line:** You still finish with four deployed applications and a portfolio — you just get there by directing agents rather than writing every line yourself.

### 2.6 Curriculum preview (`components/curriculum-preview.tsx`)

- **Label:** Curriculum
- **Headline:** The curriculum, at a glance
- **Text:** 4 modules, 26 topics — every one of them included in the one {price} plan.
- **Four cards**, each showing the module number, topic count, title, the first two topics and "+N more":
  - Module 01 · 7 topics — Introduction to AI — *What is AI? + How AI works* · *What is an AI model? + the three types of AI models* · +5 more
  - Module 02 · 7 topics — AI-Assisted Design — *Identifying typical AI design patterns* · *How to find design references* · +5 more
  - Module 03 · 6 topics — Full-Stack Web Development — *Frontend, backend & database explained* · *Understanding different tech stacks* · +4 more
  - Module 04 · 6 topics — Application Development Fundamentals — *Website vs mobile application* · *Application development fundamentals* · +4 more
- **Link:** See the full curriculum (→ `/course`)

### 2.7 Projects (`components/projects-section.tsx`)

- **Headline:** During the program, you will build real applications
- **Text:** Four complete products, not exercises — web and mobile, each one deployed and yours to show.
- Each project card also has a **See the brief** button and a preview video or image.

**Project 01 — AI Portfolio Website**
- A portfolio site with a modern UI, built with AI assisted coding and shipped to a live URL.
- *Tags:* React.js · AI assisted workflow · Vercel
- *Your tasks:* 1. Design and build your own layout 2. Add your projects and case studies 3. Deploy it to a live URL you can share

**Project 02 — Ecommerce Application**
- A full storefront — browse, add to cart, place an order — backed by a real database.
- *Tags:* Listing & search · Cart & orders · MongoDB Atlas
- *Your tasks:* 1. Build the product catalogue and search 2. Implement the cart and checkout flow 3. Wire orders through to the database

**Project 03 — Social Media Application**
- A social app with real accounts, a live feed, and everything running on your own backend.
- *Tags:* Profiles & auth · Posts, likes, comments · Python FastAPI
- *Your tasks:* 1. Build sign up, login and profiles 2. Create the feed with posts and comments 3. Add image upload and deploy the app

**Project 04 — Mobile Social App**
- The same social product as a real mobile app — built with React Native and Expo, running on your own phone.
- *Tags:* React Native · Expo · iOS & Android
- *Your tasks:* 1. Set up the Expo project and navigation 2. Build the feed and profile screens 3. Run and test it on your own phone

### 2.8 Why choose Delta (`components/why-delta.tsx`)

- **Label:** Our approach
- **Headline:** Why choose Delta AI Academy

**The traditional way**
- Most routes into software start with months of theory before you build anything anyone can use.
- ✗ Months of syntax and theory before your first real project
- ✗ Tutorials you follow along with but never ship
- ✗ You learn the tools, not how to build a product
- ✗ Nothing at the end you can actually show someone

**How you learn at Delta**
- You build from the first week. AI assisted tools carry the heavy lifting while you learn what you are actually shipping.
- ✓ Build a real application from week one
- ✓ AI tools do the heavy lifting, you stay in control
- ✓ Four complete products, web and mobile
- ✓ Every project deployed to a URL you can share

**What you study**

| # | Area | Tools |
|---|---|---|
| 01 | Full stack | React.js |
| 02 | Mobile | React Native, Expo |
| 03 | Backend | Python FastAPI |
| 04 | Database | MongoDB Atlas |
| 05 | Deployment | Vercel, Hostinger VPS, Cloudflare |

- **Link:** See the full curriculum, module by module (→ `/course`)

### 2.9 Mentors (`components/mentors-section.tsx`)

- **Label:** Mentors
- **Headline:** You build it. Someone experienced is watching over your shoulder.
- **Text:** You learn from people who ship production software for a living — not from a pre-recorded course that cannot answer you back.

**Abshar** — Academic Head — *AWS Certified Developer*
4+ years of experience in software development, with expertise in 45+ web and mobile applications, IT hosting, and AWS cloud technologies.

**Shan** — Chief Mentor
2+ years of experience in software development and AI technologies, specializing in AI tools, automation, and modern development workflows.

**Support**
- Live weekly sessions, plus your questions answered between them
- Code and project reviews on what you actually build
- Support in English and Malayalam

**Buttons:** Talk to a mentor (WhatsApp) · Call now

### 2.10 Testimonials (`components/testimonials.tsx`)

- **Label:** Testimonials
- **Headline:** Hear from our students
- Scrolling cards, each with a photo, name and the role "Cohort 2026". *The file marks these quotes as sample text — see Items to review.*
  - **Jazeem:** "I had never written a line of code before I started. By the third week my portfolio site was live at my own URL."
  - **Riziwin:** "The AI tools do the heavy lifting, but you still understand what you are shipping. That was the part I did not expect."
  - **Sajjin:** "I finished with four applications deployed and a GitHub history I could actually show people."
  - **Nithin:** "The backend was the part I was dreading. Building the API alongside the app made it far less abstract than I expected."
  - **Thazim:** "Every project ends at a real URL. That is what made the difference when I started showing my work to people."

### 2.11 FAQs (`components/faq-section.tsx`)

**Headline:** FAQs *(first question opens by default)*

1. **Do I need any coding experience to join?**
   No. The programme is built for beginners and assumes no prior AI or development experience. You start with AI assisted tools from day one and learn the underlying concepts as you build.
2. **What will I build during the programme?**
   Four complete applications: an AI portfolio website, an ecommerce storefront, a social media web app, and the same social product as a mobile app in React Native with Expo. Every one is deployed and yours to keep.
3. **Which technologies will I learn?**
   React.js for the web, React Native with Expo for mobile, Python FastAPI for backend APIs, and MongoDB Atlas for data. You will also learn version control with GitHub.
4. **Which AI tools will I work with?**
   Lovable, ChatGPT Codex, Claude and Google AI Studio for building, alongside AI research and summarization tools, speech to text workflows such as Whisper, and automation tools that speed up development tasks.
5. **Will my applications actually go live?**
   Yes. You deploy to production using Vercel, Hostinger VPS and Cloudflare, so each project ends up at a real URL you can share with employers or clients.
6. **What will I have at the end?**
   A portfolio of real web and mobile applications, a working understanding of AI powered development, production deployment experience, and the confidence to build your own ideas.
7. **What language are classes conducted in?**
   Classes are conducted in English, with live support also available in Malayalam if you'd prefer it.
8. **How can I pay?**
   Pay the {price} in full at enrolment, by card or through Razorpay.

### 2.12 Closing call-to-action (`components/closing-cta.tsx`)

- *Row of six student photos:* Jazeem, Riziwin, Sajjin, Abshar, Nithin, Thazim
- **Headline:** Start building. No coding experience needed.
- **Text:** One plan at {price}, four applications you deploy yourself, five skill areas and twelve AI tools.
- **Buttons:** Join now · Get the brochure

> **Not shown on the home page:** `components/learn-section.tsx` ("Your path to building with AI") and `components/outcomes-section.tsx` exist in the code but are not placed on any page. The "What you'll learn" nav link points to `/#learn`, which has no matching section on the page right now. The learn-section copy is listed in the appendix below in case you want it back.

---

## 3. Curriculum page (`/course`)

(`app/course/page.tsx`, `lib/curriculum.ts`)

- **Page title:** Full Curriculum
- **Meta description:** Every module and topic in the Delta AI Academy programme — 4 modules, 26 topics, from how AI models work to shipping a deployed full-stack application.
- **Label:** Full curriculum
- **Headline:** Everything you'll learn, module by module
- **Text:** 4 modules, 26 topics — from how AI models actually work through to a deployed full-stack application, on the one {price} plan.
- **Language note:** Taught in English & Malayalam , with live support in Malayalam

### Module 01 — Introduction to AI (7 topics)
The concepts every later module assumes you already have — what a model actually is, why it sometimes gets things wrong, and how to talk to one.
1. What is AI? + How AI works
2. What is an AI model? + the three types of AI models
3. What are tokens? + context windows + AI hallucination
4. Traditional development vs AI-powered development
5. AI tools overview
6. Six important things to know before you start
7. Prompt engineering fundamentals

### Module 02 — AI-Assisted Design (7 topics)
From a blank page to a shipped landing page and portfolio site — finding references, generating designs, and getting a real project live.
1. Identifying typical AI design patterns
2. How to find design references
3. Creating designs using Figma Stitch
4. Claude Code: explanation
5. Building a landing page
6. Building a portfolio website
7. Git fundamentals & hosting with Vercel

### Module 03 — Full-Stack Web Development (6 topics)
What frontend, backend and database actually mean in practice, then planning and building a full product from scratch.
1. Frontend, backend & database explained
2. Understanding different tech stacks
3. Project planning phase
4. Starting the development process
5. Hosting frontend & backend
6. Adding custom domains

### Module 04 — Application Development Fundamentals (6 topics)
Where mobile diverges from web — choosing a stack, planning an app, and understanding the backend architecture behind it.
1. Website vs mobile application
2. Application development fundamentals
3. Choosing the right technology stack
4. Planning an application
5. Starting the development process
6. Backend architecture explained

### Closing block
- **Headline:** Same curriculum, one price
- **Text:** Every module above is included in the {price} plan — no tiers, nothing locked behind an upgrade.
- **Buttons:** Join now · Get the brochure
- **Small print:** Pay in full by card or through Razorpay at enrolment.

---

## 4. Free seminar page (`/seminar`)

(`app/seminar/page.tsx`, `components/seminar-form.tsx`, `lib/next-webinar.ts`)

**Scheduled session in the code**
- **Title:** Build a website in minutes, free
- **Speaker:** Muhammed Shan
- **Start:** 15 September 2026, 7:30 PM IST, 60 minutes, live on Google Meet
- *Poster image:* `/seminar/free-website.jpg`
- Once all sessions are in the past, nothing is advertised.

**Page metadata**
- *With a session:* "{title} — free live seminar" / "{date} at {time}, live on Google Meet with {speaker}. Free — no card needed."
- *Without:* "Free live seminar" / "Book a free seat at the next Delta AI Academy live seminar. Build a website in minutes with AI — no coding experience needed."

**Page body (when a session exists)**
- *Poster, then a bullet list:*
  - Build and publish a real website during the session
  - No coding experience needed — you direct the AI
  - Live on Google Meet, with your questions answered
  - Free, and the recording is not the point — come live

**Booking form**
- **Heading:** Book your free seat
- **Sub-line:** {date} · {time} — live on Google Meet
- **Fields:** Full name ("Your name") · Email ("you@example.com") with the hint "Your calendar invite goes here — use the address your calendar is on." · Phone number ("+971 50 000 0000") · Country ("Select your country")
- **Button:** Book my free seat ("Booking your seat…" while sending)
- **Small print:** Free, no card needed. We'll send the joining link and a calendar invite.
- **Errors:** Please enter your name. / Please enter a valid email address. / Please enter a valid phone number. / Something went wrong. Please try again. / Could not reach the server. Check your connection and try again.

**After booking**
- **Heading:** Your seat is booked *(or "You're already booked")*
- {date and time}. A Google Calendar invitation is on its way to your email — accept it and the joining link sits in your calendar, with a reminder before we start.
- Automatic redirect: Taking you to the WhatsApp community in {n}… · button "Stay here" · link "Join the WhatsApp community"

**When no session is scheduled**
- **Heading:** No seminar scheduled right now
- The next date isn't announced yet. Check back soon, or join the programme and start today.

**On small screens (under 1024px wide):** the booking form also opens as a popup one second after the page loads.

---

## 5. Free episode page (`/watch`)

(`app/watch/page.tsx`, `lib/episode.ts`)

- **Page title:** Watch episode 1 free
- **Meta description:** The full opening class of the Delta AI Academy programme, free to watch in Malayalam or English.
- **Label:** Free episode
- **Episode title:** Episode 1 — watch the full class, free
- **Description:** The opening class of the programme, start to finish. No sign-up, no card — pick your language and press play.
- **Language options:** English (EN) · Malayalam (ML)
- **Buttons:** Book the free webinar · Join the programme

---

## 6. Order / checkout (`/order`)

(`app/order/page.tsx`, `components/order-form.tsx`)

- **Page title:** Join the programme
- **Meta description:** Confirm your details and how you'd like to pay to join Delta AI Academy.
- *(Page is hidden from search engines.)*

**Summary panel**
- "Learn. Build. Ship." banner (same as in section 2.3, Pricing)
- Programme name: Master Software Development with AI
- Price with the struck-through original, "{discount}% off" and the launch countdown *(only shown next to a discounted price)*
- With a coupon applied: the new price, or **FREE**
- **Coupon code:** field placeholder "Enter code" · button Apply ("Checking…") · after applying: "{n}% off" / "{currency} {n} off" / "free access" with a Remove button · error "Invalid coupon code." / "Could not check that code. Please try again."
- *Preview video of a class*
- **Included:** Four complete applications, web and mobile · Five skill areas: full stack, mobile, backend, database, deployment · Production deployment on Vercel, Hostinger VPS and Cloudflare · No prior coding experience needed

**Details form**
- **Heading:** Your details
- **Link:** Already enrolled? Start the course
- **Fields:** Full name ("Your name") · Email ("you@example.com") · Phone ("+971 50 000 0000") · Country (with the hint "Sets your price and which payment methods are available.")
- **Payment method:** radio buttons — Razorpay · Card (Stripe) · Abzer Pay *(Abzer Pay appears only for UAE, Saudi Arabia, Oman, Kuwait, Qatar and Bahrain)*
- **Countries in the picker:** United Arab Emirates, Saudi Arabia, India, Oman, Kuwait, Qatar, Bahrain, Other
- **Buttons:** pay button ("Preparing…" while loading) · "Claim free access" when a coupon makes it free
- **Trust line:** Secure checkout
- **Messages:** "We've got your details. {method} isn't connected to a live payment link yet — the team will reach out with how to complete payment." · "Could not start checkout. Please try again." · "Could not complete free enrolment. Please try again." · "Something went wrong. Please try again."
- **Validation:** Please enter your name. / Please enter a valid email address. / Please enter a valid phone number.

**Already enrolled (automatic redirect):** You're already enrolled — opening your course…

### 6.1 Pricing rules (`lib/pricing.ts`)

| Visitor | Price | Struck-through "was" price | Payment methods |
|---|---|---|---|
| India | ₹999 | ₹10,000 | Razorpay, Card (Stripe) |
| UAE, Saudi Arabia, Oman, Kuwait, Qatar, Bahrain | AED 99 | AED 440 | Razorpay, Abzer Pay, Card (Stripe) |
| Everywhere else | AED 99 | AED 440 | Razorpay, Card (Stripe) |

The visitor's country is detected automatically and can be changed on the order form.

### 6.2 Thank-you page (`/order/thank-you`)

- **Page title:** Payment successful
- **Heading:** Payment successful
- **Text:** Welcome to Delta AI Academy! Your invoice and the full course details are on their way to your email.
- **Phone prompt:** One last thing — your phone number · So we can reach you about your sessions and send your class reminders on WhatsApp. · after saving: "Thanks — we've got your number." · errors: "Please enter a valid phone number." / "Could not save that just now."
- **Buttons:** Start the course · Download invoice

### 6.3 Payment return page (`/order/payment-return`)

- Checking: Confirming your payment… — This only takes a moment.
- Pending: **Still confirming** — Your payment is still being confirmed. This can take a few minutes — you'll get an email with your invoice as soon as it's done. Feel free to close this page.
- Not found: **We couldn't find that order** — If you completed a payment, it's still being processed and you'll get a confirmation email shortly. If something went wrong, please contact us.

---

## 7. Beginner ad landing page

`/ai-development-course-for-beginners` — a separate page with its own header, footer and theme, and none of the site banner, popups or chat widget. (`app/ai-development-course-for-beginners/page.tsx`)

**Metadata**
- **Title:** AI Development Course for Beginners | Delta AI Academy
- **Description:** Start learning AI development from scratch. Build real websites and apps with AI tools through practical projects, mentor support and beginner-friendly lessons.
- **Keywords:** AI development course for beginners · AI course for beginners · AI coding course for beginners · AI development for beginners · learn AI development for beginners · AI programming course for beginners · beginner AI development course · learn software development with AI · AI app development for beginners
- *Structured data:* an FAQ block and a Course block (price ₹999 INR).

**Top bar:** Delta AI Academy wordmark · **Start learning** (→ `/order`)

### 7.1 Hero
- *Photo of the mentor (Shan).*
- **Tag:** No prior AI experience required
- **Headline:** AI Development Course for Beginners
- Learn how to build websites and applications with AI-assisted development — while understanding the technology behind what you're building.
- Delta AI Academy is designed for beginners who want to move from simply using AI tools to actually building with them.
- **Buttons:** Start learning with AI · Join the free AI class

### 7.2 Trust strip
*Photo of a social app built in the programme, with four chips:*
- Beginner Friendly — Yes
- Real Applications — 4
- AI Tools — 12+
- Live Mentor Support — Weekly

### 7.3 Section 01 — Do You Need to Know Coding Before Learning AI Development?
- **No.**
- One of the biggest barriers for beginners is believing they need to become an experienced programmer before they can start building.
- AI-assisted development gives beginners another way to approach software development.
- You can describe what you want to build, work with AI tools to generate and modify code, review the result, understand the concepts involved and gradually develop your technical understanding.
- The goal isn't to skip learning. **The goal is to make the learning process more practical.**

### 7.4 Section 02 — Start With an Idea — Not With Hundreds of Lines of Syntax
- Instead of beginning with endless syntax exercises, you'll learn through application development.
- You can start by describing:
  1. What your application should do
  2. What screens it needs
  3. What information it should store
  4. How users should interact with it
  5. What features it should include
- Then you'll learn how AI-assisted development can help turn those requirements into an application.

### 7.5 Section 03 — What Will Beginners Learn?
- **AI Fundamentals** — Understand what AI is, how AI models work and how AI is being used in software development.
- **AI-Assisted Design** — Learn how AI can help with application ideas, design references and interface development.
- **Web Development** — Learn the fundamentals of building modern web applications.
- **Full-Stack Development** — Understand how frontend, backend and database systems work together.
- **Mobile Development** — Explore mobile application development using React Native and Expo.
- **Backend Development** — Work with Python and FastAPI.
- **Databases** — Understand how applications work with data using MongoDB Atlas.
- **Deployment** — Learn how applications can be deployed using platforms such as Vercel, Hostinger VPS and Cloudflare.

### 7.6 Section 04 — What Can a Beginner Build? You'll work toward four real applications.
- **01 AI Portfolio Website** — Create and deploy a personal portfolio website.
- **02 Ecommerce Application** — Build a storefront with products, search, cart and orders.
- **03 Social Media Application** — Build an application with profiles, authentication, posts, likes and comments.
- **04 Mobile Social App** — Build a mobile version using React Native and Expo.

### 7.7 Section 05 — AI Tools Beginners Can Learn. You don't need to master every tool at once.
- The program introduces: Lovable · ChatGPT Codex · Claude · Google AI Studio · Cursor · GitHub Copilot · Replit · Windsurf · Perplexity · Hugging Face
- The objective is to understand where these tools can fit into an AI-assisted development workflow.

### 7.8 Section 06 — What If I Get Stuck?
- You won't have to rely entirely on trial and error.
- The program includes:
  - **Live Weekly Sessions** — Learn directly and ask questions.
  - **Code Reviews** — Get feedback on your implementation.
  - **Project Reviews** — Review what you're actually building.
  - **Between-Session Questions** — Get support while working through the program.
  - **English + Malayalam Support** — Get support in both languages.

### 7.9 Section 07 — Who Is This Beginner AI Course For?
- This course is suitable for: Complete beginners · Students · Non-programmers · Aspiring developers · Entrepreneurs · Creators · Professionals exploring AI development
- **Not sure if you're ready?** You don't need to know everything before starting. You need the willingness to learn, follow the program and build.
- **Link:** See the beginner-friendly curriculum (→ `/course`)

### 7.10 Section 08 — Your Beginner Learning Path
1. Understand AI.
2. Learn AI-assisted design.
3. Start building web applications.
4. Understand backend and databases.
5. Explore mobile development.
6. Deploy your applications.
7. Review and improve your work.

### 7.11 Section 09 — What You'll Have After the Program. You'll have practical experience across:
- AI-assisted development · Full-stack development · Mobile development · Backend · Database · Deployment · AI development tools
- You'll also have four applications that you worked on and deployed.

### 7.12 Section 10 — Start Your AI Development Journey
- **₹999** ~~₹4,000~~ **75% off**
- **Buttons:** Start learning for ₹999 · Watch free AI class

### 7.13 FAQ — Frequently Asked Questions
1. **Can I learn AI development if I don't know coding?** Yes. The program is designed for beginners and does not require prior AI or development experience.
2. **Is this AI course suitable for complete beginners?** Yes. The program starts with AI fundamentals and introduces development concepts while you build applications.
3. **Do I need to know Python before joining?** No prior Python experience is required. Python and FastAPI are introduced as part of the development stack.
4. **Do I need to know React?** No. React.js is part of the technologies covered in the program.
5. **Will AI write all the code for me?** AI tools are used to assist with development, but the program also focuses on understanding, directing, reviewing and improving what you're building.
6. **Can I build an app without being a professional developer?** AI-assisted development can make the development process more accessible, but building useful applications still requires learning the fundamentals, understanding the tools and reviewing the output.
7. **What projects will I build as a beginner?** You'll work on a portfolio website, ecommerce application, social media application and mobile social application.
8. **Will I have someone to help me?** Yes. The program includes live weekly sessions, questions support, code reviews and project reviews.
9. **Is Malayalam support available?** Yes. Support is available in English and Malayalam.
10. **How much does the beginner course cost?** The current launch price is ₹999.

### 7.14 Final call-to-action
- **Headline:** You Don't Have to Be an Expert to Start Building
- Start learning AI-assisted development by building real applications.
- **Buttons:** Start learning with AI · Join the free AI class

### 7.15 Footer
- Delta AI Academy wordmark · **Start learning**
- **Programme:** Curriculum · Free AI class · Enrol
- **Contact:** +91 85900 26442 · WhatsApp · deltaaiacademy.ai
- © {year} Delta AI Academy. All rights reserved.

---

## 8. Course area (signed-in, `/learn`)

(`app/learn/*`, `components/learn/*`)

**Page title:** Your course

**Sign-in (email one-time code)**
- **Headings:** Sign in to your course · Already enrolled? Sign in · Sign in to watch
- **Email step:** Email address ("you@example.com") · button **Send code** ("Sending…") · error "Could not send the code."
- **Code step:** Six-digit code ("123456") · button **Sign in** ("Checking…") · error "That code didn't work." · link "Use a different email"
- **New device:** **One more step** — This is a new device, so it needs a quick approval before it can play the course. We've let the team know — you'll be able to sign in here as soon as they approve it. Signed in on your usual device already? Use that one.
- **Device limit:** **Two devices already** — You're already set up on two devices, which is the limit. Ask the team to remove one of them, then sign in here again.
- **Wrong account:** Enrolled under a different email? Sign out and use that one instead.

**Course home**
- **Button:** Continue watching
- **Error:** Something went wrong reaching the course. Refresh the page, and if it keeps happening let us know.
- Language toggle: "Course language" (English / Malayalam)
- Episode rows are tagged **Free**, **English only** or **Malayalam only** where relevant.

**Episode page**
- **Links:** Back to the course · Course contents · previous / next episode
- **Not enrolled:** **This episode is part of the programme** — Join to unlock all {n} episodes across {n} modules. (button to `/order`)
- **Fallback-language notice:** the chosen language isn't available for that episode yet — "you're watching the {English/Malayalam} version."
- **Playback error:** The connection dropped on the way. Your place in the course is safe — try again. · button **Try again**
- **Unknown episode:** No such episode

---

## 9. Blog (`/blog`)

(`app/blog/page.tsx`, `app/blog/[slug]/page.tsx`, `lib/blog.ts`)

- **Intro:** Notes on building with AI — what the tools can do, where they fall short, and how to ship real software with them.
- **Empty state:** No posts yet — the first one is on its way.
- Each card shows the title, excerpt, date and "{n} min read".
- **Post content is not in the code.** Posts are written in the admin panel (`/admin/blog`) and stored in the database, so they are not included here.

---

## 10. 404 page

(`app/not-found.tsx`)

- **404**
- **This page doesn't exist**
- The link may be out of date, or the address mistyped.
- Taking you to the home page in {3, 2, 1}… *(redirects automatically)*
- **Button:** Go to the home page

---

## 11. Items to review

These came up while collecting the copy. None were changed in this file, so the file matches the live site.

1. **Inflated student counter.** The "{number} already building with us" line on the pricing banner shows the real enrolment count **plus 1,036** (`displayed + 1036` in `components/free-fifty-banner.tsx`). The number shown is therefore higher than the real count. Worth deciding whether that offset should stay.
2. **Sample testimonials.** `components/testimonials.tsx` says the quotes are sample text, written to describe the programme, and must be replaced with what each student actually said, with their permission, before launch. They are still the sample quotes.
3. **Inconsistent "was" price.** The main site shows ₹999 against ₹10,000 (about 90% off). The beginner landing page shows ₹999 against ₹4,000 (75% off). The AED plan shows AED 99 against AED 440.
4. **Expired offer.** The launch-price deadline is 30 September 2026, which has passed, so the banner and countdown are now hidden. Pages still show the struck-through original price and the "% off" tag, and the landing-page FAQ still calls ₹999 "the current launch price".
5. **Past webinar.** The only scheduled webinar was on 15 September 2026 and has passed, so the hero countdown, popup and booking form now show the "no seminar scheduled" state.
6. **Links that go nowhere.** "See the brief" on each project points to `#`. In the main footer, every link in the columns except "Brochure" points to `#` (What you'll learn, Projects you'll build, AI tools, What you'll achieve, Portfolio, React.js, React Native, Python FastAPI, MongoDB Atlas, Vercel, Hostinger VPS, Cloudflare, About, Contact, Enrol now, Talk to our team). The Privacy policy, Accessibility and Terms of service links and the © line are commented out in the code, so no legal pages are linked anywhere on the main site.
7. **Dead nav link.** "What you'll learn" points to `/#learn`, but the section it targets is not on the home page.
8. **Placeholder certificate data.** The sample certificate uses a placeholder name, date (15 June 2026) and ID.
9. **Instalment wording.** The pricing card says "Pay in full, or split it at enrolment" but only Razorpay is shown, and the FAQ and chat bot say instalments (Tabby/Tamara) are not offered.
10. **Tool count.** The site says "12 AI tools", while the Claude Code and Kimi agents appear in the "How we teach" section but not in the 12-tool strip, so the lists differ.

---

## Appendix — Unused section copy (not currently on any page)

**Learn section — "Your path to building with AI"** (`components/learn-section.tsx`)
- At Delta AI Academy, we make AI development simple and accessible for beginners.
- **Full stack** (React.js) — Learn how to build modern web applications using React.js and AI assisted coding tools.
- **Mobile** (React Native · Expo) — Create mobile applications using React Native and Expo so your apps run on real iOS and Android phones.
- **Backend** (Python FastAPI) — Build backend APIs using Python FastAPI to handle logins, bookings, and application logic.
- **Database** (MongoDB Atlas) — Learn how to store and manage application data using MongoDB Atlas Cluster.
- **Deployment** (Vercel · Cloudflare) — Deploy applications to production using Vercel, Hostinger VPS, and Cloudflare. You will also learn version control using GitHub.
