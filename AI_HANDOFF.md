# Aura Couture — AI Handoff

**Handoff version:** 2.0  
**Updated:** 2026-11-11  
**Status:** Repository cloned locally; Android project not yet created.

## Continuity rules
1. Read this file, `docs/DECISIONS.md`, `docs/FOUNDATION_SCREEN_SPEC.md`, and `docs/MILESTONE_LOG.md` before making project changes.
2. Do not claim a feature, build, test, or GitHub commit succeeded until its result is verified.
3. Work in small steps. Give the user one PowerShell command at a time and wait for the output.
4. Use complete file contents when asking the user to create or replace source files. Confirm actual paths and package names before writing code.
5. After each verified milestone, update this handoff and the milestone log, then commit the changes.
6. Preserve the approved design direction unless the user explicitly changes it.

## Product
Aura Couture is one role-aware Android app for a fashion boutique:
- Employees manage products, stock, customers, orders, and business insights.
- Customers browse the same catalogue, request orders, view order history, and use AI styling.
- Sneakers are one product category, not a separate business.
- No payment gateway, subscriptions, premium tiers, or monetisation in the initial coursework scope.

## Required coursework alignment
The assignment calls for an Android application using Java, with login, product CRUD, product listing, customer orders/history, database schema, navigation, testing, screenshots, APK, and presentation. It specifies SQLite or Firebase. Supabase is a proposed substitution and must be cleared with the lecturer; do not present it as explicitly approved.

## Approved design direction
- Light background: warm ivory `#F8F6F1`; white surfaces `#FFFFFF`; primary text `#242424`; secondary surface `#E9E5DE`.
- Accents: coral `#FF6B5F`, blue `#4B83F0`, lime `#B9D96D`, amber `#F1B84B`.
- Dark theme: background `#121212`, surface `#202020`, text `#F4F0E9`, coral `#FF8174`, blue `#4B83F0`.
- Editorial serif selectively for headings; clean sans-serif for body.
- Cards 16–22dp radius; primary buttons 52–56dp; 8dp spacing rhythm; page horizontal padding about 20dp; touch targets at least 48dp.
- Premium, modern, vibrant, simple layout; generous spacing, large product imagery, restrained borders/shadows, smooth purposeful transitions.
- Blue replaces lavender.

## First five approved screens
1. Splash/onboarding.
2. Login.
3. Employee dashboard.
4. Product catalogue.
5. AI Scan to Stock.

## AI workflows
**Employee AI Scan to Stock:** capture/select garment image; AI suggests category, type, colour, pattern, material, style, description, and tags; employee reviews/edits; employee manually enters price, cost, sizes, colours, and quantities; then saves.

**Customer AI Scan to Style:** capture/select an outfit or garment; identify clothing, colours, and style; suggest combinations using actual boutique catalogue and available stock; optionally save looks and request products.

**AI business assistant:** insights grounded in authorised business data, such as popular products, low stock, and sales trends.

AI must remain optional. Manual product entry and core catalogue/order workflows must work when AI is unavailable.

## Proposed architecture — not implemented
- Android Studio, Java, XML layouts, Activities and Intents.
- CameraX for camera capture.
- Supabase Auth, PostgreSQL, Storage, and Row Level Security, subject to lecturer approval.
- Use a verified Java-compatible REST client/integration; do not assume an official Java SDK.
- Route AI requests through a protected backend/Edge Function. Never embed service-role keys or AI provider secrets in the APK.
- Validate stock and create orders atomically on the server/database side.
- Store order-item unit-price snapshots to preserve historical prices.
- Employee role assignment must be controlled; clients must not self-assign employee privileges.

## Proposed data model — preliminary
- `profiles`: auth user ID, full name, email, role, created timestamp.
- `categories`: name, description.
- `products`: name, description, category, price, cost price, image, timestamps, creator.
- `product_variants`: product, size, colour, quantity, SKU.
- `customers`: optional linked profile, name, email, phone, timestamp.
- `orders`: customer, employee, status, total, timestamp.
- `order_items`: order, variant, quantity, unit-price snapshot.
- `ai_scans`: user, image, scan type, structured result, timestamp.
- `ai_insights`: insight type, content, timestamp.
This schema is provisional and must be reviewed before SQL implementation.

## Immediate next steps
1. Copy the starter documentation into the cloned repository.
2. Verify the files and Git status.
3. Commit the documentation baseline.
4. Create the Android Java/Views project directly in the repository, using the package name confirmed by the user.
5. Build the untouched Android project before implementing screens.
6. Commit only after each milestone is verified.
