# PROJECT: WINGER — Persian Football Telegram Bot 

## 1. Your Role 

Act as a Senior Python Backend Engineer, Telegram Bot Developer, Software Architect, and Product Engineer. 

Your mission is to design, implement, test, and document a production-oriented Telegram bot named **Winger (وینگر)**. 

Build an actual working application, not merely a demonstration, pseudocode, or a static UI mockup. 

Work iteratively, implement features in logical phases, and keep the project runnable throughout development. 

All user-facing content must be written in natural, friendly Persian (Farsi), with proper right-to-left text presentation wherever supported by Telegram. 

## 2. Product Vision 

Winger is a personal football assistant for Persian-speaking football fans. 

Its primary value is helping users: 

- Discover today's and tomorrow's football fixtures. 
- Check match results. 
- Follow their favorite football teams. 
- Receive selected match reminders. 
- Discover relevant football news. 
- Answer a daily football question. 
- Browse football-themed bank card designs. 
- Access football games and competitions on the Wingeriha website. 

The business goal is to generate qualified traffic, registrations, and repeat participation in the Wingeriha football gaming platform. 

**Important product principle:** 

The bot must provide genuine utility independently of the website. 

Website promotion must be contextual, helpful, and non-intrusive. 

Avoid excessive advertising, unnecessary notifications, and repetitive promotional messages. 

## 3. Technical Stack 

Use the following preferred architecture: 

- Python 3.12 or newer 
- aiogram 3.x for Telegram Bot API integration 
- PostgreSQL for persistent application data 
- SQLAlchemy 2.x with async database sessions 
- Alembic for database migrations 
- Redis for caching and temporary state 
- APScheduler or a suitable persistent job scheduling solution 
- FastAPI for health checks, integrations, and administrative APIs 
- HTTPX for asynchronous external API requests 
- Pydantic Settings for configuration 
- Docker and Docker Compose for local deployment 
- pytest for automated tests 
- Ruff for code quality 

Choose maintained, compatible library versions and document them. 

Use a modular architecture that separates Telegram handlers, business logic, database models, background jobs, and external service integrations. 

Never hardcode credentials, tokens, or API keys. 

## 4. Supported Football Competitions 

The bot must cover exactly the following eight competitions in its initial product scope: 

1. Persian Gulf Pro League — Iran 
2. English Premier League — England 
3. La Liga — Spain 
4. Serie A — Italy 
5. Bundesliga — Germany 
6. UEFA Champions League 
7. UEFA Nations League 
8. AFC Champions League Elite 

Every football-related feature must respect this supported competition list, including: 

- Fixtures 
- Results 
- Match reminders 
- Football news 
- Team selection 
- Football statistics 
- Competition tables 

Use a centralized competition configuration containing internal IDs, Persian names, external provider identifiers, and active status. 

Avoid mixing similarly named competitions or accidentally including unsupported leagues. 

## 5. Football Data Integration 

Build a provider-independent football data integration layer. 

The system must support replacing the football data provider without rewriting Telegram handlers. 

Define interfaces for: 

- Get today's fixtures 
- Get tomorrow's fixtures 
- Get matches by competition 
- Get matches by team 
- Get match details 
- Get completed results 
- Get competition standings 
- Get available teams 
- Get recent team news 
- Get match statistics when available 

Choose an appropriate commercially licensed football API only after verifying that its coverage includes all eight required competitions. 

If no single provider covers everything, support multiple providers behind the same service interface. 

Do not invent live scores, scheduled matches, sports news, or statistics. 

Implement proper fallback behavior when live data is unavailable. 

Provide a realistic, clearly identified demo-data adapter for development and testing. 

Store provider timestamps in UTC and display match times in a configurable default timezone, initially Asia/Tehran. 

Do not automatically detect the user's local timezone or introduce automatic local-time display as a product feature. 

Use caching, rate-limit handling, retries, and scheduled synchronization to minimize API requests. 

## 6. Telegram Interface 

The bot must use Telegram's native interactive interfaces, including reply keyboards and inline keyboards. 

The main navigation should be easy to understand and accessible with minimal clicks. 

Create the following Persian main menu: 

⚽ بازی‌های امروز 
🏆 نتایج فوتبال 
🔔 بازی‌های من 
📰 اخبار تیم‌های من 
📊 جدول لیگ‌ها 
🧠 سؤال فوتبالی روز 
💳 فرم درخواست کارت 
🎮 لیگ وینگری‌ها 
👤 پروفایل من 
⚙️ تنظیمات 

Allow users to return to the main menu from every section. 

Implement loading states where appropriate, pagination for long lists, meaningful empty states, and clear error messages. 

Use concise messages rather than overwhelming the user with large blocks of text. 

## 7. User Registration and Profile 

On the first interaction with /start, welcome the user with a friendly Persian message: 

"سلام فوتبالی! ⚽ 
من وینگرم، رفیق فوتبالی تو. 
بیا اول یکم بیشتر با هم آشنا بشیم!" 

Create a step-by-step profile completion flow. 

Collect: 

1. Username or preferred display name 
2. Age 
3. Gender 
4. Favorite football team or teams 
5. Winger membership status 

For membership status, provide exactly these two primary options: 

- ✅ وینگری هستم 
- ❌ وینگری نیستم 

Do not assume that self-declared membership is verified. 

Store a separate verified membership status that can only be confirmed through an authorized Wingeriha integration. 

Age and gender should support privacy-friendly options such as "ترجیح می‌دهم نگویم", and users must be able to edit their profile later. 

Use Telegram's unique user ID as the primary account identifier. 

Allow users to manage favorite teams from the supported competitions. 

Support multiple favorite teams, but enforce a reasonable configurable maximum. 

Show the completed profile in a clean, visually structured Telegram message. 

Example: 

👤 پروفایل فوتبالی من 

نام کاربری: علی 
سن: ۲۵ 
جنسیت: مرد 
تیم محبوب: رئال مادرید 
وضعیت عضویت: وینگری هستم 

Include buttons for: 

- ویرایش پروفایل 
- تغییر تیم‌های محبوب 
- وضعیت عضویت وینگر 
- تنظیمات اعلان‌ها 
- اتصال حساب وینگری‌ها 

If the user is not registered on Wingeriha, provide a relevant registration link without forcing registration to use the bot. 

## 8. Today's Fixtures 

When users select "بازی‌های امروز", retrieve all available matches from the eight supported competitions. 

Group matches by competition. 

Each fixture should display: 

- Home team 
- Away team 
- Scheduled kickoff time 
- Competition name 
- Match status, if relevant 

Provide navigation buttons: 

- بازی‌های فردا 
- انتخاب لیگ 
- بازی‌های تیم‌های من 
- بازگشت به منو 

Only display real provider data in production mode. 

At the bottom of an appropriate fixtures list, show a contextual call to action: 

"فکر می‌کنی نتیجه این بازی‌ها چی می‌شه؟ ⚽" 

Button: 

"🎯 پیش‌بینی مسابقات در وینگری‌ها" 

The button must link to the relevant Wingeriha prediction page using an environment-configured URL. 

If an individual match has a valid prediction link, prioritize linking directly to that match. 

Do not show prediction CTAs for matches whose prediction opportunities have ended. 

Do not invent Wingeriha website routes. 

## 9. Match Results 

Create a "نتایج فوتبال" section. 

Allow users to explore: 

- Today's results 
- Yesterday's results 
- Results by competition 
- Results of favorite teams 

When supported by the provider, show: 

- Final score 
- Goal scorers 
- Match status 
- Important match events 

Avoid displaying unfinished matches as final results. 

Include a contextual link to upcoming predictions where relevant. 

## 10. My Matches and Reminders 

Create a personalized "بازی‌های من" section. 

Use saved favorite teams to discover their upcoming matches. 

Allow users to configure reminders such as: 

- One day before a match 
- One hour before a match 
- At kickoff 

These settings represent possible reminder preferences, not permission to send all three reminders. 

The notification policy defined below must always take priority over individual reminder preferences. 

Prevent duplicate reminders for the same match and event. 

Respect timezone configuration, match postponements, cancellations, and schedule changes. 

## 11. Notification Policy 

This is a critical product requirement. 

The bot must NOT overwhelm users with frequent messages. 

Default notification limit: 

**Maximum one proactive notification per user per calendar day.** 

Exceptional limit: 

**Maximum two proactive notifications per user per calendar day**, only when justified by relevant football events and allowed by user preferences. 

Never exceed two proactive notifications per calendar day. 

User-requested replies and active interactive conversations do not count as proactive notifications. 

Create a notification prioritization system. 

Suggested priority order: 

1. Important upcoming match involving a favorite team 
2. A relevant match reminder requested by the user 
3. An important football update related to a favorite team 
4. Daily football engagement content 
5. Promotional Wingeriha content 

Avoid sending multiple notifications when several favorite teams play on the same day. 

Instead, combine information into one concise digest when appropriate. 

Do not send notifications for every goal, yellow card, substitution, or minor news update. 

Support: 

- Enable/disable notifications 
- Match reminder preferences 
- Daily notification limits 
- Quiet hours 
- Notification history 
- Deduplication 
- Opt-out behavior 

Promotional messaging must remain secondary to football utility. 

Use persistent notification history and enforce limits transactionally so that multiple background workers cannot exceed the cap. 

## 12. Favorite Teams News 

Create the "اخبار تیم‌های من" section. 

Only show relevant news for selected favorite teams and the supported competitions. 

Prioritize: 

- Official transfers 
- Important injuries 
- Suspensions 
- Starting lineup announcements 
- Coaching changes 
- Major competition developments 

Provide a headline, short summary, source, publication time, and original link. 

Use licensed or appropriately permitted news sources. 

Never fabricate news. 

Avoid duplicate articles. 

Where appropriate, show a contextual Wingeriha prediction CTA for upcoming matches. 

## 13. Competition Standings 

Create a "جدول لیگ‌ها" section. 

Display standings for supported competitions when a meaningful standings format exists. 

For league-based competitions, show: 

- Position 
- Team 
- Matches played 
- Points 
- Goal difference 

Support competition-specific formats where applicable. 

For tournaments that do not have a single conventional season-long league table, show relevant group, league-phase, or knockout information instead. 

Do not create fictional tables to fill unavailable data. 

## 14. Daily Football Question 

Create a special section named: 

"🧠 سؤال فوتبالی روز" 

This feature must be linked to real football events from the current week. 

Every calendar day, publish exactly one new multiple-choice question. 

Questions should relate to relevant recent events such as: 

- An important match from the current week 
- A major player performance 
- A new record 
- A notable team achievement 
- An important development in one of the supported competitions 

Use four answer options. 

After the user chooses an answer: 

1. Reveal whether the answer was correct. 
2. Show the correct answer. 
3. Provide a short and interesting explanation. 
4. Offer a contextual promotional invitation to Wingeriha. 

Example CTA: 

"این فقط گرم‌کردن بود! 🔥 
اگه فکر می‌کنی فوتبالت خیلی خوبه، بیا توی مغز متفکر وینگری‌ها خودتو محک بزن!" 

Button: 

"🧠 ورود به مغز متفکر" 

Do not provide coins or rewards through the Telegram question unless a verified Wingeriha integration explicitly authorizes them. 

The daily question must primarily function as an engagement and promotional feature for the website rather than a separate competing game. 

Create an administrative workflow to draft, review, approve, and schedule daily questions. 

Questions must be verified against reliable sources before publication. 

If automated question generation is later enabled, generated questions must never be published without validation. 

Allow one recorded answer per user per daily question. 

Do not reveal the correct answer before a user answers. 

## 15. Bank Card Request Section 

Create a new main-menu feature: 

"💳 فرم درخواست کارت" 

When selected, show a visually organized selection menu with three categories: 

1. طرح تیم‌های ملی 
2. طرح تیم‌های باشگاهی 
3. طرح بازیکنان ستاره 

Each category must display available card designs using image previews and clearly labeled selection buttons. 

Card designs should be stored in a database and managed through an administrative interface or API. 

Each design must contain: 

- Unique design ID 
- Persian title 
- Category 
- Image 
- Availability status 
- Display order 
- Optional description 

Allow the user to: 

1. Select a category. 
2. Browse available designs. 
3. View a larger design preview. 
4. Select a preferred design. 
5. Confirm the selection. 
6. Continue to the official Winger card request process. 

Do not implement an unverified banking application, card issuance process, or collection of sensitive banking credentials inside Telegram. 

Use an approved external card request URL when provided. 

If no official card application integration or URL exists, implement a clearly labeled prototype workflow and preserve the selected card design locally without claiming that a bank card has been issued or requested successfully. 

Do not ask for bank account passwords, card PINs, CVV2, or SMS verification codes. 

Use only card design assets that the project is authorized to display, including approved national-team, club, and player imagery. 

## 16. Wingeriha Gaming Section 

Create a dedicated section: 

"🎮 لیگ وینگری‌ها" 

Its submenu should include: 

- پیش‌بینی مسابقات 
- مغز متفکر 
- بازی پا به توپ 
- بازی جفت‌چین 
- لیگ و مدال‌های من 
- جوایز و قرعه‌کشی 

Each button should navigate to a configured official website destination. 

Do not invent URLs. 

Create an integration layer for future Wingeriha account connection. 

Once an authenticated and authorized API is available, the bot should be able to display: 

- User's current league 
- Coin balance 
- Earned medals 
- Progress toward the next medal 
- Eligible upcoming gaming opportunities 

Never fabricate coins, medals, reward eligibility, membership verification, or prize information. 

If no integration is configured, show an appropriate website link or a clear "این قابلیت به‌زودی فعال می‌شود" message. 

For users who identify themselves as non-Winger members, offer contextual membership information without making it a prerequisite for normal football features. 

## 17. Additional Engagement Features 

Implement the following as optional modular features, with feature flags: 

### What Should I Watch Today? 

Recommend a small number of interesting matches from supported competitions based on favorite teams and relevant match significance. 

### Before the Match 

Provide brief factual pre-match information such as recent form, head-to-head records, and confirmed injuries, where reliable data is available. 

### Football Banter 

Generate short, friendly, non-abusive football banter messages that users can share with friends. 

Avoid hateful, discriminatory, or defamatory content. 

### On This Day in Football 

Show verified historical football moments with reliable dates and attribution. 

### My Football DNA 

Offer a short football-preference quiz. 

At the end, generate a shareable profile summary based on user answers. 

Do not infer sensitive demographic or psychological characteristics from quiz responses. 

These features should not delay completion of the core working bot. 

## 18. Website Integration and Analytics 

The bot must support measurable website referrals. 

Track important events such as: 

- Bot started 
- Profile completed 
- Favorite team selected 
- Fixtures viewed 
- Results viewed 
- Reminder enabled 
- Daily question answered 
- Card design viewed 
- Card design selected 
- Website CTA clicked 
- Wingeriha account connected 

Use privacy-conscious event tracking. 

Create a centralized link-building service with UTM parameters or equivalent tracking identifiers. 

Use safe, allowlisted website domains. 

Track the source section and campaign. 

Do not pass unnecessary personal information in URL parameters. 

Where backend data exists, expose aggregated analytics for: 

- Active bot users 
- Profile completion rate 
- Feature engagement 
- Website click-through rate 
- Conversion events from authorized integrations 
- Repeat engagement 

Do not claim completed website registrations without confirmed website-side data. 

## 19. Administration 

Build a simple secure administrative API or interface. 

Administrators should be able to: 

- Manage supported competitions 
- Manage card design catalogs 
- Manage external website URLs 
- Create and approve daily football questions 
- Review scheduled notifications 
- Manage feature flags 
- Review integration status 
- View basic aggregated analytics 

Use proper authentication and access controls. 

Keep administrative credentials separate from Telegram user authentication. 

## 20. Database Design 

Create an appropriate normalized schema. 

At minimum, model: 

- Users 
- User profiles 
- Membership status 
- Favorite teams 
- Competitions 
- Teams 
- Matches 
- Match results 
- News articles 
- Notification preferences 
- Notification history 
- Daily questions 
- Question answer options 
- User question responses 
- Card design categories 
- Card designs 
- Card selections 
- Website click events 
- External account links 
- Feature flags 

Add indexes and uniqueness constraints where needed. 

Use database migrations. 

Avoid storing unnecessary sensitive personal information. 

## 21. Security and Reliability 

Follow secure development practices. 

Requirements: 

- Environment-based secret management 
- Secure webhook verification 
- Input validation 
- Restricted administration 
- Rate limiting 
- Safe external URL handling 
- Protection against duplicate callback processing 
- Safe logging without exposing secrets 
- Proper error handling 
- Database transactions where required 
- External API timeout handling 
- Retry and backoff mechanisms 
- Idempotent background tasks 
- User data deletion support 
- Clear consent for notifications 
- Privacy-aware account linking 

Never expose Telegram bot tokens or external API keys in logs or source files. 

## 22. Visual and UX Direction 

The bot should feel like a modern football product, not a generic utility. 

Brand personality: 

- Friendly 
- Football-focused 
- Energetic 
- Clear 
- Helpful 
- Occasionally playful 

Use concise Persian copy and restrained football-related emojis. 

Brand colors for any generated cards, previews, or future Mini App components: 

- Primary purple: #5A469D 
- Deep purple: #4E3775 
- Accent purple: #742BD2 
- Light lavender: #C8BEEB 

Telegram's native chat buttons cannot be styled freely. Respect the platform's limitations instead of pretending full custom visual styling is available. 

Prioritize clarity and usability. 

## 23. Development Phases 

Implement the project in the following order. 

### Phase 1 — Functional Core 

- Project initialization 
- Configuration 
- Database 
- Telegram bot startup 
- Persian main menu 
- Profile registration 
- Membership status 
- Favorite teams 
- Fixtures 
- Results 
- Match reminders 
- Notification limits 
- Website prediction links 

### Phase 2 — Football Content 

- Favorite team news 
- Competition standings 
- Daily football questions 
- Question approval workflow 

### Phase 3 — Wingeriha Features 

- Bank card design catalog 
- Card selection flow 
- Wingeriha games menu 
- Configurable website links 
- Website referral analytics 
- Account linking interface 

### Phase 4 — Advanced Engagement 

- Match recommendations 
- Pre-match analysis 
- Football banter 
- On This Day 
- Football DNA quiz 
- Advanced analytics 

Build the code so later phases do not require rewriting the initial architecture. 

## 24. Deliverables 

Create: 

1. Complete working source code. 
2. Modular project structure. 
3. Database models and migrations. 
4. Docker Compose configuration. 
5. Environment variable template. 
6. README with Persian setup instructions. 
7. API integration documentation. 
8. Automated tests. 
9. Example demo content. 
10. Local development commands. 
11. Deployment instructions. 
12. A list of external credentials and integrations still required. 

Include instructions for obtaining and configuring the Telegram bot token through BotFather. 

Document the difference between development polling and production webhook deployment. 

## 25. Testing and Acceptance Criteria 

Create automated tests covering at least: 

- First-time user onboarding 
- Profile creation and editing 
- Winger membership selection 
- Supported competition filtering 
- Fixtures and results formatting 
- Favorite team matching 
- Reminder scheduling 
- One-notification default limit 
- Two-notification absolute limit 
- Notification deduplication 
- Daily question validation 
- One answer per user per day 
- Card category navigation 
- Card selection persistence 
- Website URL generation 
- Missing football provider credentials 
- Missing Wingeriha integration 
- External API failures 

The application must remain usable in a local demo mode without real football API credentials. 

Development/demo data must be clearly distinguished from real production data. 

## 26. Instructions for Working in Codex 

First inspect the existing repository and determine whether any code already exists. 

Do not overwrite working project files unnecessarily. 

Then: 

1. Summarize the proposed architecture. 
2. Create a practical implementation plan. 
3. Start implementing Phase 1 immediately. 
4. Create actual source files. 
5. Install or document dependencies. 
6. Run available tests. 
7. Fix discovered errors. 
8. Explain how to launch the bot locally. 
9. Identify remaining credentials or external integrations. 
10. Continue through later phases when feasible. 

Do not stop after merely providing an architecture proposal. 

Do not invent successful test results, existing external APIs, or completed integrations. 

When a requirement depends on unavailable credentials or undocumented website APIs, implement a clean integration interface and a clearly labeled development fallback. 

Ask for clarification only when an essential implementation decision cannot reasonably be made safely. 

**Final goal: A maintainable, deployable, Persian-language football Telegram bot that provides daily value to football fans and creates natural, measurable pathways into the Wingeriha website.**

