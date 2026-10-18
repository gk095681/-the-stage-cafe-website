THE STAGE CAFÉ & CAKE BAR — CASH-ON-DELIVERY ORDERING STARTER

WHAT THIS PROJECT DOES
- Customer menu, search and category filters
- Cart and checkout form
- Delivery OR pickup selection
- Cash on Delivery / pay at pickup only
- Submits orders to a Supabase Edge Function
- Server checks menu item IDs and calculates prices from the database
- Saves order + line items and returns an order number
- Orders can be reviewed in Supabase Dashboard > Table Editor

IMPORTANT BEFORE REAL LAUNCH
- Menu has 149 separate entries transcribed from the supplied menu photos. Similar-price options are separate items.
- The printed menu notes a 10% service charge; checkout and backend add 10%. Delivery fee is currently Rs. 0 because the restaurant has not supplied a delivery fee. Confirm before launch.
- This starter does not yet send WhatsApp/email alerts. Staff can see orders in Supabase Table Editor.
- Reservation form is still demo-only.
- Add rate limiting / CAPTCHA and configure CORS to your real website domain before public launch.
- Never expose the Supabase service_role key in the browser or commit it to GitHub.
- The website is not a complete production system until you test and deploy the backend securely.

STEP 1 — CREATE SUPABASE PROJECT
1. Open https://supabase.com/ and create/sign in to your account.
2. Create a new project and save the database password safely.
3. In Project Settings > API (or Connect), copy the Project URL and anon/publishable key.

STEP 2 — CREATE DATABASE TABLES
1. In Supabase, open SQL Editor > New query.
2. Open supabase/migrations/001_ordering_schema.sql from this project.
3. Copy all its SQL into the SQL Editor and run it.
4. In Table Editor, confirm menu_items, orders and order_items exist.
5. Check menu_items prices and change example prices to the real approved menu prices.

STEP 3 — CONFIGURE THE WEBSITE
1. Open config.js.
2. Replace https://YOUR-PROJECT-REF.supabase.co with your Project URL.
3. Replace YOUR_SUPABASE_ANON_OR_PUBLISHABLE_KEY with the anon/publishable key.
4. Do not use the service_role key in config.js.

STEP 4 — DEPLOY THE EDGE FUNCTION
Recommended easiest route: use Supabase CLI.
1. Install Node.js LTS from https://nodejs.org/
2. Install Supabase CLI following https://supabase.com/docs/guides/cli
3. Open a terminal in this project folder.
4. Run: supabase login
5. Run: supabase link --project-ref YOUR_PROJECT_REF
6. Deploy: supabase functions deploy create-order
The function uses Supabase's server-side SUPABASE_URL and SUPABASE_SERVICE_ROLE_KEY environment values. Do not copy the service role key into any frontend file. If your project environment does not automatically provide them, set them as function secrets using the official Supabase secrets guide.

STEP 5 — RUN LOCALLY
- In VS Code install the Live Server extension.
- Right-click index.html > Open with Live Server.
- Internet is needed for online photos, fonts and Supabase.
- If opening the file directly, the browser may block requests; use Live Server instead.

STEP 6 — TEST
- Add an item to cart, open cart and submit a test order with delivery address.
- Confirm a new row appears in Supabase Table Editor > orders and its items appear in order_items.
- Test pickup and confirm delivery_address is empty.
- Try invalid/empty details and verify the order is rejected.
- Test on phone size and desktop.
- Do not announce the site as live until order storage and staff workflow are tested.

ORDER REVIEW
Supabase Dashboard > Table Editor > orders: sort by created_at descending.
Open the matching order id in order_items to see purchased dishes.
Never expose customer order records publicly. Keep RLS enabled.

FILES
index.html, style.css, script.js, config.js, assets/restaurant-logo.jpg
supabase/migrations/001_ordering_schema.sql
supabase/functions/create-order/index.ts

MENU PHOTO NOTES
- Menu items and prices were transcribed from the three submitted photos; please verify uncertain/blurred entries before public launch.
- The menu photos are menu cards, not individual dish photos. Current card photos are illustrative category photos from Unsplash, reused by category. Replace with real dish photos when available.
- "Sausages Grilled/Devilled (06 Nos)" and variants such as rice/noodles, flavours and sauces have separate entries so customers can choose them independently.
