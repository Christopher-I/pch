# PCH Shopping UX Strategy

**Project:** PCH Shopping MVP
**Platform:** Shopify (Horizon theme v3.1.0)
**Audience:** 60-80 years old, 220K-250K daily sweepstakes visitors
**Device split:** 67% desktop, 33% tablet (minimal phone)

---

## Scope Boundaries

This document covers two distinct phases with different scopes:

| Phase | Scope | Status |
|-------|-------|--------|
| **Phase 1** | MVP polish - merch only, no sweepstakes | Current work (15-20 hrs) |
| **Phase 2** | Sweepstakes entry integration | Future (post-MVP validation) |

Recommendations are labeled by phase. Do not conflate them.

---

## Audience Profile: What the Data Actually Says

From the client call, PCH's audience is:

| Attribute | Data Point | Source |
|-----------|------------|--------|
| Age | 60-80 years old | Owen, client call |
| Daily traffic | 220,000-250,000 | Owen, client call |
| Device split | 2/3 desktop, 1/3 tablet | Owen, client call |
| Mobile phone | "Pretty much all tablet" for mobile web | Owen, client call |
| Tech literacy | "Savvy navigators... very good at navigating" | Owen, client call |
| Conversion channel | Email-driven | Owen, client call |
| Primary motivation | Sweepstakes entries (not merch itself) | Owen, client call |

**Critical insight from Owen:**
> "These folks, they're very good at navigating. We have various games and products. They're very good at navigating them."

This is NOT a tech-illiterate audience. They are experienced PCH ecosystem users who navigate complex sweepstakes interfaces daily. Design for clarity, not for hand-holding.

---

## Design Principles for This Specific Audience

### 1. Clarity Over Simplicity

This audience navigates PCH's sweepstakes sites daily. They don't need dumbed-down interfaces - they need **clear, predictable ones**.

**Do:**
- Use standard e-commerce patterns (grid layouts, clear CTAs, visible cart)
- Provide immediate feedback for actions
- Make the value proposition explicit

**Don't:**
- Assume they can't handle standard web interfaces
- Oversimplify to the point of removing useful information
- Treat them as technologically incompetent

### 2. Desktop-First, Tablet-Friendly

With 67% desktop and tablet-dominant mobile traffic, optimize for larger screens.

| Screen | Priority | Approach |
|--------|----------|----------|
| Desktop (1200px+) | Primary | Full-featured, 3-4 column grids |
| Tablet (768-1199px) | Secondary | 2-3 column grids, larger touch targets |
| Phone (<768px) | Tertiary | Functional but not optimized |

### 3. Explicit Value Communication

Owen stated the core insight:
> "Our users basically will do anything that says, 'Hey, go here, you win a prize.' They will go there."

**Phase 1:** Merch value must stand on its own (brand affinity, quality)
**Phase 2:** Entry value becomes the primary driver ("Buy this = X entries")

### 4. Trust Through Familiarity

This audience has a 70+ year relationship with the PCH brand. Leverage that trust.

- Use PCH's established visual language (gold, envelope iconography)
- Reference the Prize Patrol, legacy sweepstakes
- Don't try to look like a "modern startup" - look like PCH

---

## Cart UX Decision: Enhanced Full Page (Not Drawer)

### The Recommendation

**Use Option C: Enhanced Full Page Cart** - not a cart drawer.

### Why This Decision

| Factor | Cart Drawer | Enhanced Full Page | Winner |
|--------|-------------|-------------------|--------|
| Familiarity for 60-80 demo | Lower (newer pattern) | Higher (traditional) | Full Page |
| Accessibility | Smaller targets, overlay dismissal issues | Full-size targets, clear navigation | Full Page |
| Implementation in Horizon | Requires custom JS/Liquid | Theme-native with enhancements | Full Page |
| Competitive reference | OVRLND uses drawer | Van Life skips cart entirely | - |
| Owen's explicit request | "Pop out cart" mentioned | Not explicitly rejected | Drawer |

**Resolution:** Owen mentioned "pop out cart" but also emphasized the 60-80 demographic. The audit recommended Enhanced Full Page because:

1. Drawers/overlays can be accidentally dismissed
2. Smaller interaction areas in constrained drawer space
3. Research shows older users prefer explicit, dedicated pages
4. Full page is more accessible (WCAG compliance easier)

**If the client insists on a drawer:** Implement with senior-friendly constraints:
- Minimum 300px width
- Large close button (44x44px minimum)
- No auto-dismiss
- Instant open (no slide animation over 200ms)
- Clear "View Full Cart" escape hatch

### Implementation: Enhanced Full Page

| Enhancement | Description | Est. Hours |
|-------------|-------------|------------|
| Toast notification | "Added to cart!" confirmation appears for 3 seconds | 2-3 |
| Cart icon badge | Shows item count, animates on add | 1-2 |
| Continue Shopping CTA | Prominent button on cart page | 0.5 |
| Cart page polish | Larger product images, clearer totals | 1-2 |

**Total:** 4.5-7.5 hours

---

## Phase 1: MVP Polish (Current Scope)

### Priority 1: Cart Feedback (3-4 hours)

**Current problem:** No visual feedback when adding to cart. User clicks "Add to Cart" and nothing happens except a redirect.

**Solution:**
```
1. Add toast notification component
   - Appears top-right on desktop, top-center on mobile
   - Shows product thumbnail + "Added to cart!"
   - Auto-dismisses after 3 seconds
   - Click to go to cart

2. Update header cart icon
   - Add item count badge (gold circle with white number)
   - Animate badge on item add (subtle scale pulse)
```

**Shopify/Horizon implementation:** Requires JavaScript for AJAX add-to-cart and toast. Horizon's default is page redirect. This is the highest-value change.

### Priority 2: Quick-Add on Product Cards (4-5 hours)

**Current problem:** Must click into PDP to add anything to cart. Extra friction for browsing.

**Solution:**
```
Desktop:
- "Add to Cart" button appears on card hover
- If product has variants, clicking opens quick-view modal OR goes to PDP

Tablet/Mobile:
- "Add to Cart" button always visible below price
- Stacks vertically: Image → Title → Price → Button

For products with variants (size/color):
- Option A: Quick-view modal with variant selector
- Option B: Go to PDP (simpler, recommended for Phase 1)
```

**Recommendation:** For Phase 1, use Option B (go to PDP for variants). Quick-view modals add complexity and may confuse this demographic. Revisit for Phase 2.

### Priority 3: CTA Button Styling (1-2 hours)

**Current problem:** Primary CTAs use outline buttons (low contrast, not prominent).

**Current state:**
- Hero CTA: "SHOP ALL COLLECTIONS" - black outline on white
- PDP: "Add to Cart" - black outline button
- Issue: Outline buttons fail WCAG contrast for interactive elements

**Solution:**
```css
/* Primary CTA - filled */
.btn-primary {
  background-color: #E59A38; /* PCH Gold */
  color: #000000;
  border: none;
  font-weight: 600;
  padding: 16px 32px;
  font-size: 18px;
  min-height: 48px; /* Touch target */
}

/* Secondary CTA - outline with higher contrast */
.btn-secondary {
  background-color: transparent;
  color: #000000;
  border: 2px solid #000000;
  font-weight: 600;
  padding: 16px 32px;
}
```

**Apply to:**
- Hero section CTA (primary)
- Add to Cart buttons (primary)
- "Continue Shopping" on cart (secondary)

### Priority 4: Hero Section (2-3 hours)

**Current problems:**
1. Headline is generic: "WELCOME TO PCH Shopping"
2. CTA is weak outline button with no urgency
3. AI-generated lifestyle image (may feel inauthentic)
4. No value proposition or trust signals

**Solution:**

```
Headline options (test):
A: "Official PCH Merchandise"
B: "Gear Up Like the Prize Patrol"
C: "From the Icons Who Brought You the Big Check"

Subheadline:
"Premium apparel and accessories from America's #1 Sweepstakes"

CTA:
"SHOP THE COLLECTION" (filled gold button)

Trust element (below CTA):
"Trusted since 1953 • Secure checkout • Free shipping over $50"
```

**Image recommendation:** Replace AI image with:
- Option A: Prize Patrol van/team (brand recognition)
- Option B: Flat-lay product photography (authenticity)
- Option C: Keep current if budget-constrained (lowest priority issue)

### Priority 5: Trust Elements (2-3 hours)

**Current problems:**
- No trust badges anywhere
- Minimal footer (no FAQ, contact, shipping info)
- No reviews or social proof

**Solution:**

**Footer additions:**
```
Column 1: Shop
- All Products
- Apparel
- Headwear
- Gift Cards (future)

Column 2: Support
- FAQ
- Shipping & Returns
- Size Guide
- Contact Us

Column 3: About PCH
- Our Story (link to pch.com/about)
- Prize Patrol
- Sweepstakes (link to pch.com)

Column 4: Trust
- Secure Checkout badge
- "Trusted since 1953"
- BBB badge (if applicable)

Bottom bar:
- © 2024 Publishers Clearing House
- Terms | Privacy | Accessibility
```

**Above-fold trust signals:**
- Add to announcement bar: "Free shipping on orders over $50"
- Add below hero: "Secure checkout • 30-day returns • Trusted since 1953"

---

## Phase 2: Sweepstakes Integration (Future Scope)

**Prerequisite:** Phase 1 MVP validates conversion rates. Do not build this until data supports it.

### Product Card Integration

```
Current card:
[ Product Image        ]
  Product Name
  $40.00

Phase 2 card:
[ Product Image        ]
  Product Name
  $40.00
  🎟️ Includes 40 entries
  [ Add to Cart ]
```

**Entry display rules:**
- Show entry count prominently (not hidden in description)
- Use consistent "X entries" language
- Entry badge should use PCH gold (#E59A38)

### PDP Integration

```
Product Title
$40.00

🎟️ This purchase includes 40 sweepstakes entries
   into the $1,000,000 Giveaway

[ Size selector ] [ Color selector ]
[ Quantity: - 1 + ]

[ ADD TO CART - 40 ENTRIES ]
[ Buy with Shop Pay ]

ℹ️ No purchase necessary. See rules.
```

**Legal requirement (from Owen):**
> "You can't just sell entries into a sweepstake. You have to offer other benefits as part of it."

Every entry display must link to official rules. Use clear disclaimer copy.

### Cart Integration

```
Your Cart (2 items)

┌─────────────────────────────────────┐
│ [img] PCH Snapback         $38.50  │
│       Size: One Size               │
│       🎟️ 38 entries               │
│       Qty: 1    [Remove]           │
├─────────────────────────────────────┤
│ [img] Prize Patrol Hoodie  $60.00  │
│       Size: L / Color: Red         │
│       🎟️ 60 entries               │
│       Qty: 1    [Remove]           │
└─────────────────────────────────────┘

Subtotal:              $98.50
Shipping:              FREE
─────────────────────────────────────
Total:                 $98.50

🎟️ Total entries earned: 98

[ CHECKOUT ]
[ Continue Shopping ]
```

### Membership/Club (Phase 3+)

Per Owen, this is modeled on Van Life's membership:

```
PCH Rewards Club — $9.99/month

✓ 100 bonus entries per week
✓ 10% off all merchandise
✓ Early access to new products
✓ VIP-only sweepstakes

[ JOIN THE CLUB ]

Current members: 12,847
```

**Do not build this in Phase 2.** Requires:
- Subscription billing integration
- Account system with entry balance
- Backend entry tracking
- Legal review of benefit structure

---

## Competitive Analysis: Van Life vs OVRLND

Owen referenced both sites. Here's how they compare and what to learn:

| Feature | Van Life | OVRLND | PCH Recommendation |
|---------|----------|--------|-------------------|
| Cart pattern | Direct to checkout (skip cart) | Cart drawer | Enhanced full page |
| Entry display | $1 = 1 entry | $1 = 10 entries, multipliers | Match OVRLND (higher perceived value) |
| Product cards | No quick-add visible | Quick-add buttons | Add quick-add (Phase 1) |
| Membership | Core product (club model) | Has membership tier | Phase 3+ consideration |
| Trust signals | Minimal | Strong (countdown, social proof) | Follow OVRLND |
| Target demo | Young, eco-conscious | Mixed | Adapt for 60-80 |

**Key insight:** Both sites target younger demographics. Their patterns need adaptation for PCH's older audience:

- Van Life's direct-to-checkout is too aggressive for multi-item browsing
- OVRLND's drawer is modern but may confuse older users
- Both use small text and dense layouts that won't work for 60-80 demo

---

## Accessibility Requirements

Non-negotiable for 60-80 demographic:

| Element | Minimum | Recommended | Current State |
|---------|---------|-------------|---------------|
| Body text | 16px | 18px | Good (Inter) |
| Button text | 16px | 18px | Needs increase |
| Touch targets | 44x44px | 48x48px | Check mobile |
| Color contrast | 4.5:1 (AA) | 7:1 (AAA) | Outline buttons fail |
| Focus states | Visible | High contrast | Verify |
| Link underlines | Present or obvious | Always underlined | Check |

**Specific fixes needed:**
1. Outline buttons fail contrast - switch to filled
2. Verify all form fields have visible labels
3. Add skip-to-content link
4. Test keyboard navigation through checkout

---

## Typography & Spacing

Current fonts are appropriate (Poppins headings, Inter body). Adjustments:

```css
/* Increase base size for older eyes */
body {
  font-size: 18px;
  line-height: 1.6;
}

/* Generous spacing */
.product-card {
  padding: 24px;
  margin-bottom: 24px;
}

/* Button sizing */
.btn {
  padding: 16px 32px;
  font-size: 18px;
  min-height: 48px;
}

/* Form inputs */
input, select {
  font-size: 18px;
  padding: 14px 16px;
  min-height: 48px;
}
```

---

## What NOT to Do

Based on PCH's specific audience and constraints:

| Don't | Why | Instead |
|-------|-----|---------|
| Use hover-only interactions | 33% tablet users can't hover | Always-visible or click-triggered |
| Add slide-out drawer cart | May disorient older users | Enhanced full page with toast feedback |
| Use outline buttons for primary CTAs | Fail contrast, lack prominence | Filled buttons with gold background |
| Hide navigation in hamburger (desktop) | Older users expect visible nav | Horizontal nav, always visible |
| Use vague copy ("Shop the vibe") | This audience wants explicit info | Clear, direct copy ("Shop Apparel") |
| Implement complex animations | Distracting, may cause issues | Subtle transitions (200ms max) |
| Auto-play video | Unexpected behavior, data usage | Click-to-play with clear controls |
| Use infinite scroll | Disorienting, hard to navigate | Pagination with clear page numbers |
| Rely on iconography alone | Meaning may be unclear | Icons + text labels |

---

## Implementation Roadmap

### Phase 1: MVP Polish (15-20 hours)

| Task | Priority | Hours | Dependency |
|------|----------|-------|------------|
| Toast notification for add-to-cart | 1 | 2-3 | None |
| Cart icon badge + animation | 1 | 1-2 | None |
| Quick-add buttons on product cards | 2 | 4-5 | Toast (for feedback) |
| CTA button styling (filled) | 3 | 1-2 | None |
| Hero section improvements | 4 | 2-3 | Button styling |
| Footer trust elements | 5 | 2-3 | None |
| General CSS polish | 6 | 2-3 | All above |

**Parallel work possible:** Tasks with "None" dependency can run simultaneously.

### Phase 2: Sweepstakes (Scope TBD)

Requires:
- Backend integration with PCH drawing engine
- Entry tracking system (Klaviyo or custom)
- Legal review of all entry-related copy
- Account system for entry balance

Do not scope until Phase 1 data validates the MVP.

### Phase 3: Membership Club (Scope TBD)

Requires Phase 2 + subscription infrastructure. Long-term consideration.

---

## Success Metrics

### Phase 1 (MVP Polish)

| Metric | Current Baseline | Target | Measurement |
|--------|------------------|--------|-------------|
| Add-to-cart rate | Unknown | +20% over baseline | Shopify analytics |
| Cart abandonment | Unknown | -15% from baseline | Shopify analytics |
| Checkout completion | Unknown | +10% over baseline | Shopify analytics |
| Session duration | Unknown | Baseline + engagement | GA/Mixpanel |

### Phase 2 (Sweepstakes)

| Metric | Target | Measurement |
|--------|--------|-------------|
| Entry-driven purchases | >50% cite entries as motivation | Post-purchase survey |
| Repeat purchase rate | 2x vs Phase 1 | Shopify analytics |
| Email click-through | +25% for entry-promoted emails | Marigold/Klaviyo |

---

## Technical Constraints: Shopify Horizon Theme

The Horizon theme (v3.1.0) has limitations:

| Feature | Native Support | Custom Work Required |
|---------|----------------|---------------------|
| Toast notifications | No | Yes - JS + Liquid |
| Cart badge count | Partial | Minor JS enhancement |
| Quick-add buttons | No | Yes - Liquid + JS |
| Filled button variant | Yes (theme setting) | CSS override if not |
| Footer customization | Yes | Content only |
| Entry display (Phase 2) | No | Full custom build |

**Recommendation:** Phase 1 is achievable within Horizon. Phase 2 may require a custom theme or headless approach depending on complexity.

---

## Summary

| Principle | Implementation |
|-----------|----------------|
| Desktop-first, tablet-friendly | Optimize for 1200px+, test at 768px |
| Clarity over cleverness | Explicit labels, visible navigation, filled CTAs |
| Enhanced Full Page cart | Toast feedback + badge, not drawer |
| Trust through brand | PCH legacy, security badges, clear policies |
| Phase separation | Don't build sweepstakes until MVP validates |
| Accessibility by default | 18px text, 48px targets, 4.5:1 contrast minimum |

**Next step:** Begin Priority 1 (cart feedback) implementation.
