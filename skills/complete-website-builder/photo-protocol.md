# Photo Discovery Protocol (mandatory every build)

This step is non-negotiable. Generic AI sites fail because they reuse the same 7 stock
photos. Every build researches real photos relevant to THIS specific business.

## Photos to find (7 minimum per build)

1. **Hero background** — wide environmental or worker-in-action shot
2. **Hero right panel** — secondary action shot or close-up of the work
3. **Gallery item 1** (large, spans 2 rows) — flagship project or work environment
4. **Gallery item 2** — detail shot, equipment, or finished result
5. **Gallery item 3** — different angle of the work
6. **Gallery item 4** — variety shot (interior, before/after, team)
7. **Why Choose Us** — professional/credibility shot (tools, team, certification, polished workspace)

## Discovery process (run for every build)

For each photo slot, do this:

**1. Build search keywords specific to the business.** Examples:
   - Plumber in Sweden: `plumber working`, `plumbing repair`, `modern bathroom`, `copper pipes`, `professional tool bag`
   - Dental clinic: `modern dental office`, `dentist with patient`, `clean clinic interior`, `dental equipment closeup`
   - Real estate: `luxury home exterior`, `modern interior design`, `realtor handshake`, `aerial neighborhood`
   - Gym: `weight training`, `athlete lifting`, `modern gym equipment`, `fitness transformation`
   - Restaurant: `plated food closeup`, `restaurant interior warm lighting`, `chef plating`, `dining ambiance`

**2. Search Unsplash via WebSearch and WebFetch.**
   - Use WebSearch with queries like: `site:unsplash.com [keyword]` or `unsplash [keyword] photo`
   - Or WebFetch directly on `https://unsplash.com/s/photos/[keyword]` to get the search results page
   - The HTML contains `<img>` tags with `src="https://images.unsplash.com/photo-[ID]..."` URLs. Extract the photo IDs.

**3. Verify every ID before using it.**
   - WebFetch the individual photo page (e.g., `https://unsplash.com/photos/[slug]`) and confirm the canonical `photo-[ID]` appears in the page's `<img>` tag
   - Slugs from URL paths are NOT photo IDs. Only the `photo-XXXXXXXXXXXXXXXXXX` string from `images.unsplash.com/photo-[ID]` is reliable.
   - Never guess. Never invent IDs. Never trust a slug.

**4. Use the verified URL format:**
   ```
   https://images.unsplash.com/photo-[ID]?w=1920&q=85
   ```
   - For `<img>` tags or smaller use cases, drop to `?w=900&q=85`
   - Always include `w=` and `q=` params for performance.

**5. Always add a CSS gradient fallback on the same element** so if the photo 404s the gradient covers it:
   ```css
   background-image: linear-gradient(135deg, [persona dark], [persona accent]),
                     url('https://images.unsplash.com/photo-[ID]?w=1920&q=85');
   ```

## Why this matters

A plumbing site with a generic stock photo of a guy in a suit looks fake. The same
site with a verified Unsplash photo of an actual plumber working on a copper pipe looks
real. The eye notices in milliseconds.

## Last-resort fallback

If WebSearch and WebFetch genuinely fail (rate-limited, no results), fall back to these
verified persona IDs as a SECOND choice (not first). These are known-working but they
are the same photos every other AI site uses, so always prefer fresh research:

- TRADES fallback: `photo-1621905251189-08b45d6a269e` (hero), `photo-1504328345606-18bbc8c9d7d1` (right)
- MEDICAL fallback: `photo-1606811841689-23dfddce3e34` (hero), `photo-1588776814546-1ffbb11a61e8` (right)
- REAL ESTATE fallback: `photo-1600596542815-ffad4c1539a9` (hero), `photo-1568605114967-8130f3a36994` (right)
- GYM fallback: `photo-1534438327276-14e5300c3a48` (hero), `photo-1571019613454-1cb2f99b2d8b` (right)
- RESTAURANT fallback: `photo-1414235077428-338989a2e8c0` (hero), `photo-1517248135467-4c7edcad34c4` (right)
- LAW fallback: `photo-1589829545856-d10d557cf95f` (hero), `photo-1521791055366-0d553872952f` (right)
- DEFAULT fallback: `photo-1497366216548-37526070297c` (hero), `photo-1600880292203-757bb62b4baf` (right)
