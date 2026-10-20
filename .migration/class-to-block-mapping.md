---
name: class-to-block-mapping
description: Maps source-site CSS classes to Edge Delivery Services blocks during page migration and import. Use whenever an element carries a class listed in the mapping table below, so it is converted to the specified block instead of being analyzed as a new or custom block.
---

# Class-to-Block Mapping

When migrating or importing a page, check every element's `class` attribute against the table below **before** running block detection or creating a new block. If a class matches, use the mapped block. Do not create a new custom block or variant for it.

## Mapping Table

| Source CSS class        | Target block | Notes                                                    |
|-------------------------|--------------|----------------------------------------------------------|
| `shadow-card-ring-xs`   | `hero`       | Treat the matching element as a hero block.              |

## Rules

1. **Match on class token.** An element matches if `shadow-card-ring-xs` appears anywhere in its class list, for example `class="card shadow-card-ring-xs"`. Do not require an exact string match on the whole attribute.
2. **Mapping takes priority.** If the mapping conflicts with automatic block detection, the mapping wins.
3. **Reuse the existing block.** Use the repository's existing `hero` block (`/blocks/hero`). Do not create a variant such as `hero-card` unless the user asks for one.
4. **Preserve content.** Map the element's content into the hero block's expected structure:
   - Image or background media goes in the first row or cell.
   - Heading (`h1`/`h2`), supporting text, and call-to-action links go in the following row or cell.
5. **Drop the source class.** Do not carry `shadow-card-ring-xs` into the migrated output. Any needed styling belongs in the `hero` block's CSS.
6. **Nested matches.** If a matched element contains other matched elements, convert only the outermost one.

## Example

**Source HTML**

```html
<section class="shadow-card-ring-xs">
  <img src="/images/banner.jpg" alt="Spring collection" />
  <h1>Spring Collection</h1>
  <p>Fresh styles for the new season.</p>
  <a href="/shop">Shop now</a>
</section>
```

**Target (Edge Delivery Services block table)**

| Hero                                              |
|---------------------------------------------------|
| ![Spring collection](/images/banner.jpg)          |
| # Spring Collection                               |
|                                                   |
| Fresh styles for the new season.                  |
|                                                   |
| [Shop now](/shop)                                 |

## Adding More Mappings

To map another class, add a row to the Mapping Table:

| Source CSS class | Target block | Notes |
|------------------|--------------|-------|
| `your-class`     | `block-name` | Optional notes |
