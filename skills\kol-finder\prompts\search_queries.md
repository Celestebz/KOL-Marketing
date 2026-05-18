# Search Query Generator

Use this file to generate platform search queries for any product category after the KOL persona is defined.

## Inputs

Replace bracketed values with project information:

- `[Product]`: product name
- `[Brand]`: brand name
- `[Category]`: product category/subcategory
- `[Competitor]`: competitor brand/product
- `[Audience]`: target buyer/user
- `[Use Case]`: main use case or problem solved
- `[Feature]`: key product feature
- `[Price/Positioning]`: budget, premium, professional, luxury, etc.
- `[Platform]`: YouTube, Instagram, TikTok, LinkedIn, Reddit, podcast, blog, etc.
- `[Market/Language]`: US, UK, English, Spanish, German, etc.

## Cycle C1 - Competitor-Based

```text
"[Competitor] review"
"[Competitor] vs [Product]"
"[Competitor] alternatives"
"best alternatives to [Competitor]"
"[Competitor] comparison"
"[Competitor] worth it"
"[Competitor] problems"
```

## Cycle C2 - Category-Based

```text
"best [Category]"
"best [Category] for [Audience]"
"[Category] review"
"top [Category] [Market/Language]"
"[Category] comparison"
"[Category] buying guide"
"[Category] recommendations"
```

## Cycle C3 - Use-Case-Based

```text
"best [Category] for [Use Case]"
"how to solve [Use Case]"
"[Use Case] setup"
"[Use Case] essentials"
"[Audience] [Use Case] tools"
"[Product] for [Use Case]"
```

## Cycle C4 - Feature-Based

```text
"[Feature] review"
"best [Category] with [Feature]"
"[Feature] demo"
"[Feature] comparison"
"is [Feature] worth it"
"[Feature] tutorial"
```

## Cycle C5 - Positioning/Value-Based

```text
"best [Price/Positioning] [Category]"
"affordable [Category]"
"premium [Category] review"
"best value [Category]"
"[Category] under [price]"
"cheap vs expensive [Category]"
```

## Cycle C6 - Audience/Community-Based

```text
"[Audience] creator [Category]"
"[Audience] recommendations [Category]"
"[Audience] essentials"
"[Community] [Category] review"
"[Audience] product setup"
"[Audience] daily routine [Category]"
```

## Cycle C7 - Spider-Web

Look for:

- Similar creators suggested by the platform.
- Collaborations and tagged creators.
- Commenters who are also creators.
- Creators followed by competitor brands.
- Creators who reviewed competitor products.
- Podcast guests, newsletter authors, community moderators, and forum experts.

## Platform-Specific Modifiers

| Platform | Useful modifiers |
|---|---|
| YouTube | review, demo, comparison, tutorial, unboxing, worth it, best, setup |
| Instagram | reel, creator, UGC, routine, outfit, demo, before after, setup |
| TikTok | TikTok made me buy it, review, first impression, routine, hack, unboxing |
| LinkedIn | founder, operator, consultant, expert, workflow, SaaS, case study |
| Reddit | recommendations, alternatives, worth it, problems, honest review |
| Blogs/newsletters | review, buying guide, roundup, expert picks, comparison |
| Podcasts | interview, creator, expert, founder, category discussion |

## OpenCLI Examples

```powershell
opencli youtube search "[Competitor] review" --limit 30 --type video --format csv
opencli youtube search "best [Category] for [Audience]" --limit 30 --type video --format csv
opencli instagram search "[Category] [Audience]" --format csv
opencli tiktok search "[Category] review" --format csv
opencli reddit search "[Category] recommendations" --format csv
opencli google search "site:youtube.com [Category] review influencer" --format csv
```

## Product-Specific Examples

### Consumer Electronics

```text
"[Competitor] review"
"best [Category] for travel"
"[Feature] comparison"
"budget [Category] worth it"
"[Category] setup tutorial"
```

### Beauty/Skincare

```text
"[Ingredient] review"
"best [Category] for [Skin Type]"
"[Competitor] before after"
"dermatologist reviews [Category]"
"[Category] routine for [Audience]"
```

### SaaS/B2B Tool

```text
"[Competitor] alternative"
"best [Category] for startups"
"[Use Case] workflow"
"[Feature] tutorial"
"[Category] LinkedIn creator"
```

### Music Gear

```text
"[Competitor] review"
"best [Category] for beginners"
"[Feature] demo"
"budget [Category] comparison"
"[Genre] [Category] setup"
```

## After Search

For each candidate found:

1. Open the profile/channel.
2. Check recent relevant content.
3. Verify audience and language fit.
4. Estimate engagement from recent posts/videos.
5. Check if already in blacklist or existing CSVs.
6. Record one relevant content URL for personalization.

