# Nyumba — rental finder MVP

A responsive web app concept for people finding houses, rooms, and hostels around Kenya. Open `index.html` to preview the experience.

## Included in this delivery

- Mobile-first rental discovery page with sample Nairobi-area listings.
- Location text search, home type and rent filters, save controls, listing details, and call/WhatsApp links.
- Signup and login flows for tenants and landlords, plus a local landlord listing form.
- `supabase/schema.sql` with a production-oriented starting data model and row-level access policies. Rent and availability are attached to individual units.

The page is a **front-end preview**, not yet a live marketplace. The example listings and account/listing forms run in the browser and use local storage. Accounts are not securely authenticated, listings are not shared between devices, photos are sample remote images, and the map panel is a visual preview. Do not collect real passwords or publish user-submitted listings with this preview.

## To launch as a real public service

1. Create a Supabase project and apply `supabase/schema.sql` in its SQL editor.
2. Connect the web app to Supabase Auth and replace the preview form handlers with authenticated account, property, unit, photo, and saved-property operations.
3. Set up photo storage and its access policies. Decide whether landlord phone numbers are public on a listing or revealed only after a renter action.
4. Add a real map provider and geocoding for property pins, current location, and distance sorting. Restrict the map API key to the production site.
5. Configure account verification, privacy/terms, listing moderation and reporting, then deploy the static site to a host such as Cloudflare Pages, Netlify, or Vercel.

No paid service credentials are embedded in the app. Once a Supabase project and map provider are selected, the preview can be wired to those services and prepared for deployment.

## Publish this preview with GitHub Pages

This repository includes `.github/workflows/deploy.yml`. To publish the static preview:

1. Create a GitHub repository.
2. Upload the **contents of this `nyumba` folder** to the repository root (so `index.html` is at the root).
3. In the repository, open **Settings → Pages** and set **Source** to **GitHub Actions**.
4. Push or commit to the `main` branch. GitHub Actions will publish the site and show its URL under the Pages settings and workflow run.

GitHub Pages serves static files only. This publishes the preview; it does not turn the local demo forms into real accounts or a shared listings database. See the production launch steps above for that work. GitHub's current setup instructions are in [Deploying your website automatically](https://docs.github.com/en/get-started/start-your-journey/deploying-your-website-automatically).

## Data model note

A property can have many units; each unit has its own type, monthly rent, and `available` / `occupied` status. Tenant search should return published properties with at least one available matching unit. Landlord access is enforced with Supabase row-level security policies in the schema.
