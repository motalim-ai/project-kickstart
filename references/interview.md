# Interview guide

## Contents
1. Principles
2. Adaptive rules (what to skip)
3. Question bank A–H
4. Handling "I don't know": patterns and examples
5. Reflecting back and the project brief

---

## 1. Principles

- **Batches of 3–5 questions.** Multiple-choice where possible, with your recommendation first. Free text for the idea itself.
- **Why before what.** If a question might confuse, add one line on why you ask ("I'm asking about the server so I size memory correctly, not because of traffic").
- **Use what you already saw.** If you studied their site or files, ask to confirm ("I see 15 branches on your site, correct?") instead of asking from scratch.
- **Write down every answer immediately** into your working notes; they become the brief and the docs.
- **Stop when you know enough.** You don't need every answer to start; unknowns go to `OPEN-QUESTIONS.md` with the phase that needs them.

## 2. Adaptive rules

First determine the **project type** (question A3), then skip what doesn't apply:

| Type | Skip | Emphasize |
|---|---|---|
| Public website / marketing site / store | — | E (SEO, languages, pixels), B (brand), G (domain, hosting) |
| Web app / SaaS with accounts | E2–E4 if not public | D (roles), F (privacy), G (deploys) |
| Internal tool / dashboard for staff | E (SEO, pixels) | D (roles), F, H |
| Mobile app | E1 SEO (keep app-store listing), G2 domain | C (offline? push notifications?), G (app stores) |
| API / backend only | B, E | F, G, testing |
| Script / automation / prototype | most of D, E, F, G | A, C, H (size S) |

Always ask A, C, and H1–H2. Ask G1 only if the project will be deployed.

## 3. Question bank

Wording below is a guide. Rephrase naturally in the person's language. Arabic examples are given for the trickiest ones.

### A. The idea
- **A1.** In one or two sentences, what are we building and what problem does it solve? *(free text)*
- **A2.** Who uses it? Customers, staff, partners, the public? About how many at the start, and in a year?
- **A3.** What kind of thing is it? Website / web app with accounts / mobile app / internal tool / API / automation / not sure. *(If not sure: describe each in one line with an example and recommend.)*
- **A4.** Is there anything similar you like or dislike? Links or names help a lot.
- **A5.** What does success look like in 3 months? (orders per day, time saved, signups, ranking on Google…)

### B. Ready materials
- **B1.** Do you have a brand identity: logo, colors, fonts, a style guide? Where are the files?
- **B2.** Is there an existing website, app or system we are replacing or extending? (Study it if yes.)
- **B3.** Do you have designs (Figma, images, sketches) or content (texts, photos, product lists, prices)?
- **B4.** Do you own a domain? Who is it registered with, and where is its DNS managed? *(Most people don't know the DNS part, which is fine. Offer to check it with a public DNS lookup.)*

### C. Features
- **C1.** What must exist at launch? List the 3–7 things without which launching makes no sense.
- **C2.** What can wait until after launch?
- **C3.** Anything explicitly *not* wanted (now or ever)?
- **C4.** Will users log in? Do they need accounts? (Explain: accounts add security work and privacy duties.)
- **C5.** Payments online? (If yes: which country and which gateway? Recommend local gateways.)
- **C6.** Notifications: email, SMS, WhatsApp, push? Which events trigger them?
- **C7.** Integrations: existing systems (POS, ERP, CRM, accounting, maps, delivery apps)?

### D. Users, roles, admin
- **D1.** Who manages the content or data day to day? Are they technical?
- **D2.** Do you need an admin dashboard? What should staff control without a developer? (Give examples: hide or show products, reorder, edit prices, receive orders.)
- **D3.** Different roles with different permissions? (e.g. admin, editor, order manager)

### E. Languages, markets, SEO, marketing
- **E1.** Should people find it on Google? *(If "I don't know", see §4: SEO.)* If yes: which searches matter (brand, local "near me", products, services)?
- **E2.** Languages? Which is the default? Right-to-left (Arabic) support needed?
- **E3.** Which countries or cities? (Matters for privacy laws, payments, local SEO.)
- **E4.** Will you run ads or measure marketing? Which platforms (TikTok, Snapchat, Meta, Google)? (Explain pixels and the consent banner.)
- **E5.** Is it a local business with branches? (Local SEO: a page per branch, Google Business Profile.)

### F. Data & privacy
- **F1.** What personal data will you collect? (names, phones, emails, addresses, IDs, payment info)
- **F2.** Which laws apply? Suggest based on E3: Saudi PDPL, UAE PDPL, Egypt PDPL, EU GDPR… and whether data must stay in-country.
- **F3.** How long should data be kept? (Recommend defaults: orders 3 years, messages 2 years, logs 30 days.)

### G. Hosting, domain, email, deploys
- **G1.** Where will it run? Your own server (VPS) / a managed platform (Vercel, Netlify, Railway, Render…) / app stores / not sure. *(If they have a server: with permission, inspect it read-only.)*
- **G2.** Who manages the domain and DNS now? Is Cloudflare an option? (Explain in one line: free speed and protection layer.)
- **G3.** Sending emails: from which address and service? Daily limit? (Domain mailboxes often allow ~100/day. Design around it.)
- **G4.** How should new versions go live? Automatically from GitHub, on request, or by a person or agent on the server? (Explain the security trade-off: whoever deploys needs access to the server.)
- **G5.** Backups: does anything exist? (Recommend nightly offsite + monthly restore test.)

### H. Team, tools, timeline, budget
- **H1.** Who will build it? You with AI agents / a developer / a team? Which AI tools (Claude Code, Cursor, Codex…)?
- **H2.** Do you have a GitHub account? (Details in Step 7. Just note the answer here.)
- **H3.** Timeline: any hard dates (launch, season, event)?
- **H4.** Monthly budget for services (hosting, email, domains)? "As low as possible" is a valid answer.
- **H5.** Who approves each phase? Who should the agent ask when stuck?

## 4. Handling "I don't know"

Pattern for every unknown:
1. **Normalize:** "عادي جدًا، دي حاجة تقنية وأنا هوضحها."
2. **Explain** in 2–3 lines with an analogy tied to their project.
3. **Options** with a clear recommendation and the reason.
4. **Default** if still unsure, then tell them it's recorded as an assumption in `OPEN-QUESTIONS.md` and can change.

### Example: SEO (Arabic, Egyptian)
> **مش فاهم يعني إيه SEO؟**
> SEO هو إن موقعك يطلع في جوجل لما حد يدوّر على حاجة بتقدمها. مثلًا لو حد كتب «كافيه قريب مني» ومحلك يطلع في أول النتايج.
> لو موقعك للعامة وعاوز عملاء جداد يلاقوك، يبقى محتاجينه، وده بيأثر على طريقة بناء الصفحات من أول يوم.
> لو التطبيق داخلي للموظفين بس، مش محتاجينه.
> **اقتراحي:** بما إن عندك فروع وعملاء من الشارع، نخليه أولوية.

### Example: hosting
> A VPS is like renting a whole apartment: full control, but you maintain it. A managed platform is like a hotel: they handle maintenance, you pay a bit more and accept their rules. For your project (admin dashboard + database, low traffic) I recommend the VPS you already have, because cost is fixed and you keep your data.

### Example: roles
> Roles are like keys in a building: the manager has a master key, the cashier only opens the register. Do your staff need different keys, or does everyone do everything?

### Example: "I don't know who manages my domain"
Offer to check: run a public DNS lookup (nameservers, A, MX records) and explain the result: "Your domain's DNS is at Hostinger, and your email is on Titan." No account access is needed.

### Example: budget
If they can't answer, propose a minimal tier ("about $0–20 per month using what you already have"), and list what would cost more later.

## 5. Reflecting back and the brief

After each batch, write 1–2 lines: "So far I understand: …. Correct?"

Before writing docs, present the **project brief** (in their language):

```
## ملخص المشروع
- **الفكرة:** …
- **لمين:** …
- **نوعه وحجمه:** … (S / M / L)
- **لازم يكون في الإطلاق:** …
- **بعد الإطلاق:** …
- **خارج النطاق:** …
- **الجاهز عندك:** … (هوية، محتوى، موقع حالي…)
- **اللغات:** … · **SEO:** نعم/لا (السبب) · **الدفع أونلاين:** …
- **الاستضافة:** … · **الدومين:** … · **الإيميل:** …
- **التقنيات المقترحة:** … (سطر لكل واحدة: ليه)
- **أسئلة مفتوحة:** … (هتتسجل في OPEN-QUESTIONS.md)
- **الملفات اللي هكتبها:** … (سطر لكل ملف: بيجاوب على إيه)
```

Wait for "yes" (or corrections) before Step 5.
