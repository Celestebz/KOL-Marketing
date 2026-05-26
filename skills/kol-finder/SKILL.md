---
name: kol-finder
description: "General-purpose KOL/influencer finder for any product category or specific product. Use when the user wants to find, evaluate, shortlist, or prepare outreach for creators/KOLs on platforms such as YouTube, Instagram, TikTok, X/Twitter, LinkedIn, Reddit, blogs, podcasts, or niche communities. The workflow first asks product-specific clarification questions, then defines the target KOL persona, creates a project, collects evidence with OpenCLI/web search, deduplicates, scores, and outputs a candidate list."
---

# KOL Finder - General Product Influencer Research

## Core Principle

This skill works for any product type. Do not assume the right KOL type from the category alone. First understand the exact product, buyer, positioning, platform, market, and campaign goal. Then define the target KOL persona and only then create/search the project.

Use this order:

1. Clarify product and campaign context.
2. Define the target KOL persona.
3. Create or load the project.
4. Build search strategy.
5. Collect candidates with OpenCLI and web search.
6. Validate, deduplicate, score, and output.

## Mandatory Clarification Before Search

If the user only says "find KOLs" or gives a broad category, ask follow-up questions before searching or creating the final candidate list.

Ask only what is missing. Keep it concise. For most products, ask:

- Product: What is the specific product or product type?
- Category: What category/subcategory is it in?
- Target market: Which country/region/language?
- Platform: YouTube, Instagram, TikTok, LinkedIn, X/Twitter, blogs, podcasts, communities, or other?
- Audience: Who is the buyer/user?
- Positioning: Budget, mid-range, premium, professional, luxury, technical, lifestyle, etc.?
- Key selling points: 3-5 product advantages or unique features.
- Competitors: 2-5 comparable brands/products.
- KOL size: minimum followers/subscribers and preferred tier.
- Campaign goal: review, demo, awareness, conversion, UGC, affiliate, launch seeding, expert credibility, or community buzz.

If the user provides a product document, extract product details first, then ask only the gaps.

Useful prompt to the user:

```text
To define the target KOL persona first, I need these details:
1. Product/category:
2. Target market and language:
3. Target user/buyer:
4. Price range/positioning:
5. Main selling points:
6. Competitors:
7. Platforms and follower/subscriber threshold:
8. Campaign goal:
```

## KOL Persona Definition

Before searching, convert product context into a written KOL persona. This is mandatory.

Include:

- Best-fit creator types.
- Secondary creator types.
- Creator types to avoid.
- Platform priority.
- Content formats that fit the product.
- Keywords and competitor terms to search.
- Evidence required before approval.
- Risks and mismatch signals.

Examples by product type:

| Product type | Best-fit KOL types |
|---|---|
| Consumer electronics | Reviewers, comparison channels, setup/tutorial creators, deal/value creators |
| Beauty/skincare | Dermatology/ingredient educators, routine creators, before-after creators, lifestyle influencers |
| SaaS/B2B tools | Workflow educators, founders/operators, LinkedIn experts, YouTube tutorial creators, newsletter writers |
| Fitness products | Coaches, form educators, transformation creators, niche sport creators |
| Food/beverage | Taste-test creators, recipe creators, lifestyle creators, diet-specific communities |
| Musical instruments/effects | Gear reviewers, demo creators, beginner educators, genre-specific players |
| Fashion/accessories | Styling creators, haul/review creators, niche aesthetic creators |
| Pet products | Pet owner creators, trainers, vets, rescue/community accounts |
| Gaming products | Streamers, reviewers, esports educators, setup creators |

## Project Structure

Every KOL project should use this structure:

```text
projects/
+-- [Product_Name]/
    +-- assets/
    |   +-- product_pitch.md
    +-- reference/
    |   +-- kol_persona.md
    |   +-- market_audit_report.md
    |   +-- search_strategy_log.md
    |   +-- opencli_raw/
    +-- results/
        +-- Raw/
        |   +-- kol_candidates_raw.xlsx
        +-- Approved/
            +-- kol_candidates_final.xlsx
```

Create the project after the product/KOL persona is clear enough. If a project already exists, load it instead of recreating it.

Use a filesystem-safe project name:

```text
[Brand_or_Product]_[Market_or_Language]_[Platform]
```

Examples:

```text
GE100_Pro_EN_YouTube_Instagram
AI_Notetaker_US_LinkedIn_YouTube
Skincare_Serum_UK_TikTok_Instagram
```

## Project Initialization

If project exists, read:

- `projects/[Product]/assets/product_pitch.md`
- `projects/[Product]/reference/kol_persona.md`
- `projects/[Product]/reference/search_strategy_log.md`
- existing XLSXs under `results/Raw/` and `results/Approved/`

If project is new, create folders and files:

- `assets/product_pitch.md`
- `reference/kol_persona.md`
- `reference/market_audit_report.md`
- `reference/search_strategy_log.md`
- `reference/opencli_raw/`
- `results/Raw/`
- `results/Approved/`

Use `templates/product_pitch_template.md`, `templates/kol_persona_template.md`, and `templates/search_strategy_log_template.md` when creating these files.

`product_pitch.md` should include:

- Product name.
- Category/subcategory.
- Target market and language.
- Target user/buyer.
- Positioning and price range if known.
- Key selling points.
- Competitors.
- Campaign goal.
- Platforms and KOL size threshold.

`kol_persona.md` should include:

- Primary KOL persona.
- Secondary KOL persona.
- Exclusion persona.
- Platform strategy.
- Search keywords.
- Approval criteria.

## OpenCLI Usage

If `opencli` is installed, use it before normal web search when a relevant platform command exists.

Check availability:

```powershell
Get-Command opencli -ErrorAction SilentlyContinue
opencli --help
opencli list
```

Common platform checks:

```powershell
opencli youtube --help
opencli instagram --help
opencli tiktok --help
opencli twitter --help
opencli linkedin --help
opencli reddit --help
opencli google --help
```

YouTube examples:

```powershell
opencli youtube search "PRODUCT_OR_COMPETITOR review" --limit 30 --type video --format csv
opencli youtube search "best CATEGORY for TARGET_USER" --limit 30 --type video --format csv
opencli youtube video "VIDEO_URL" --format json
opencli youtube channel "CHANNEL_ID_OR_HANDLE" --format json
opencli youtube comments "VIDEO_URL" --format csv
opencli youtube transcript "VIDEO_URL" --format json
```

Instagram examples:

```powershell
opencli instagram search "CATEGORY keyword" --format csv
opencli instagram profile "USERNAME" --format json
opencli instagram user "USERNAME" --format json
```

General discovery examples:

```powershell
opencli google search "site:youtube.com CATEGORY review influencer" --format csv
opencli reddit search "PRODUCT_OR_CATEGORY recommendations" --format csv
```

Important:

- Treat OpenCLI output as source data, not final truth.
- If OpenCLI fails because login/cookies/browser bridge are missing, fall back to web search and mention the limitation.
- Save raw exports in `reference/opencli_raw/`.
- Do not use follower counts or engagement numbers blindly. Validate recent relevant content.

## Market Audit

Build a compact audit before large-scale search.

Audit:

- Main competitors and adjacent products.
- Where target users discover this category.
- Content formats that usually work in this category.
- Common user pain points and buying objections.
- KOL types competitors already use.
- Product claims that need expert/technical validation.

Use sources appropriate to the category:

- YouTube reviews/comments/transcripts.
- Instagram/TikTok content and comments.
- Reddit/community threads.
- Amazon, Shopify, App Store, G2, Product Hunt, Sephora, Sweetwater, Steam, or other category-specific reviews.
- Blogs, newsletters, podcasts, professional communities.

Save to `reference/market_audit_report.md`.

## Search Strategy

Use a 7-cycle rotation. Log each search in `search_strategy_log.md`.

| Cycle | Strategy | Query pattern |
|---|---|---|
| C1 | Competitor-based | "[competitor] review", "[competitor] alternative", "[competitor] vs [competitor]" |
| C2 | Category-based | "best [category]", "[category] review", "top [category] for [audience]" |
| C3 | Use-case-based | "best [product] for [use case]", "[problem] solution", "[audience] setup" |
| C4 | Feature-based | "[feature] review", "[feature] demo", "[feature] comparison" |
| C5 | Audience/identity-based | "[audience] creator", "[community] recommendations", "[niche] essentials" |
| C6 | Platform-native | hashtags, Shorts/Reels/TikTok searches, LinkedIn/newsletter/podcast searches |
| C7 | Spider-web | similar creators, collaborations, tagged posts, comments, featured channels, follower/following graphs |

Preferred pattern:

```powershell
opencli PLATFORM search "QUERY" --format csv
```

When using YouTube:

```powershell
opencli youtube search "QUERY" --limit 30 --type video --format csv
opencli youtube search "QUERY" --limit 20 --type channel --format csv
```

For recency-sensitive categories:

```powershell
opencli youtube search "QUERY" --limit 30 --type video --upload year --sort relevance --format csv
opencli youtube search "QUERY" --limit 30 --type video --upload month --sort date --format csv
```

## Candidate Validation

For each candidate, verify with evidence.

Required checks:

| Criteria | Default threshold | How to verify |
|---|---:|---|
| Size | User-defined, otherwise 10K+ | Platform profile/channel |
| Language/region | User-defined | Recent content and audience signals |
| Niche fit | Product/category relevant | Titles, posts, descriptions, bio |
| Buyer fit | Reaches likely buyers | Content topics and comments |
| Content format | Matches campaign goal | Reviews, demos, tutorials, UGC, expert posts, etc. |
| Recent activity | Usually active in last 60-90 days | Recent uploads/posts |
| Engagement | Healthy for platform and size | Views, comments, likes, saves, shares if available |
| Comparable coverage | Covered similar products/problems | Recent relevant content |
| Contact route | Email, website, agency, DM path | Bio/about page/description |

Evidence should include at least one recent relevant URL. Prefer 2-3 if available.

## Exclusion Logic

Define exclusions based on the product persona, not a fixed category.

Common exclusions:

- Audience mismatch: creator reaches fans, not buyers.
- Positioning mismatch: luxury creator for budget product, or budget creator for premium/luxury product.
- Content mismatch: pure entertainment when the product needs explanation.
- Trust mismatch: too much sponsored content with little genuine evaluation.
- Technical mismatch: creator cannot credibly evaluate a technical product.
- Geography/language mismatch.
- Inactive or weak recent performance.
- On `configs/blacklist.txt`.

## Scoring

Score each candidate from 1 to 5.

5 = Perfect fit:

- Audience matches likely buyers.
- Creator has covered similar products/problems.
- Content format matches campaign goal.
- Recent engagement is healthy.
- Clear contact route.

4 = Strong fit:

- Good fit but missing one non-critical signal.

3 = Possible fit:

- Adjacent audience or useful secondary exposure.

2 = Weak fit:

- Some relevance, but buyer/content/positioning mismatch.

1 = Do not prioritize:

- Poor fit, inactive, wrong market, or high risk.

## Deduplication

Before output, read all existing XLSXs in:

- `projects/[Product]/results/Raw/`
- `projects/[Product]/results/Approved/`

Remove duplicates by:

- Platform profile/channel URL.
- Creator name with fuzzy matching.
- Contact email.
- Cross-platform identity if known.

If one creator appears on multiple platforms, keep one row and list secondary platform URLs in notes unless the user wants one row per platform.

## Output Format

Save to:

```text
projects/[Product]/results/Raw/kol_candidates_[Product]_[Date].xlsx
```

Required columns:

| Column | Description |
|---|---|
| 合作产品 | Product name for collaboration |
| 频道名称 | KOL/channel/profile name |
| 联系人 | Contact person if available |
| YouTube链接 | YouTube channel/profile URL |
| YouTube 粉丝量 | YouTube subscriber count |
| Instagram链接 | Instagram profile URL |
| Instagram 粉丝量 | Instagram follower count |
| Email | Contact email |
| 国家地区 | Country/region/language |
| 推荐理由 | Short evidence-based reason for recommendation |

## Outreach Preparation

For approved KOLs, prepare personalization notes:

- Mention one specific recent relevant piece of content.
- Explain why the product fits their audience.
- Suggest one content concept that matches their style.
- Keep the first message short and low friction.

Use `templates/email_template.md` if available, but adapt the pitch to the product category.

## Error Handling

| Issue | Solution |
|---|---|
| User gives only broad category | Ask clarification before search |
| Product details are in a file | Extract the file first, then ask only missing questions |
| OpenCLI command missing | Use web search and mention OpenCLI was unavailable |
| OpenCLI login/cookie/browser issue | Run `opencli doctor`, then fall back if still blocked |
| Too many irrelevant results | Tighten by audience, use case, competitor, or feature |
| Too few results | Expand platform, adjacent category, competitors, or spider-web cycle |
| Follower count unavailable | Mark unknown and verify manually before approving |
| Duplicate detection unclear | Keep the stronger evidence row and add alternate URLs in notes |
