# PCH Shopping Site Audit & Recommendations

**Prepared for:** Owen, Publishers Clearing House
**Prepared by:** Christopher
**Date:** December 2024

---

## Executive Summary

PCH Shopping is an MVP e-commerce site built on Shopify (Horizon theme v3.1.0) selling branded merchandise. The client is testing e-commerce with their existing audience (60-80 year olds, 220k+ daily visitors) before committing to a full rebuild with sweepstakes integration.

**Key Findings:**
- Site is functional but lacks polish and modern e-commerce UX patterns
- Cart flow needs improvement (currently redirects to separate page)
- No quick-add functionality on product cards
- Missing trust elements and brand story
- Good foundation to build upon

---

## Client Requirements

From Owen (December 2024):

1. Update the Cart checkout to pop out or something else that has a better UX
2. Enable Cart checkout on product image (like vanlife.us)
3. General audit/set of recommendations for a go forward on a full e-commerce/sweepstakes site

---

## Target Audience Profile

| Attribute | Detail |
|-----------|--------|
| Age | 60-80 years old |
| Location | Middle America |
| Daily visitors | 220,000-250,000 (sweepstakes site) |
| Device split | 2/3 desktop, 1/3 tablet (minimal phone) |
| Behavior | Email-driven, convert from promotional emails |
| Tech comfort | Savvy navigators, familiar with PCH ecosystem |

**UX Implications:**
- Prefer explicit, clear navigation over hidden/drawer patterns
- Need larger touch targets and readable text
- Value trust signals and brand familiarity
- May find overlay/drawer UX disorienting

---

## Current Site Analysis

### Theme & Technical Info
- **Platform:** Shopify
- **Theme:** Horizon (v3.1.0)
- **Pages:** Homepage, Product Detail Pages, Standard Shopify Checkout

### Color Scheme
| Color | Usage | Hex (approx) |
|-------|-------|--------------|
| Gold/Orange | Primary - header, footer, CTAs | #E59A38 |
| Black | Text, secondary buttons | #000000 |
| White | Backgrounds | #FFFFFF |

### Typography
- **Headings:** Poppins (clean, modern)
- **Body:** Inter (highly readable)
- **Assessment:** Good choices for older demographic

---

## Homepage Analysis

### Header/Navigation
| Element | Current State | Assessment |
|---------|--------------|------------|
| Announcement bar | "Welcome to the Official Publishers Clearinghouse Shop" | Good - establishes legitimacy |
| Logo | PCH envelope icon (gold/white) | Clean, recognizable |
| Nav items | Home, Apparel, Headwear | Limited - only 2 categories |
| Utility icons | Search, Account, Cart | Standard, good placement |

### Hero Section
| Aspect | Current State | Issues |
|--------|---------------|--------|
| Image | AI-generated lifestyle shot | May feel inauthentic to older demo |
| Headline | "WELCOME TO PCH Shopping" | Generic, no value proposition |
| CTA | "SHOP ALL COLLECTIONS" (outline button) | Low contrast, not prominent |

**Missing from Hero:**
- No mention of sweepstakes, prizes, or legacy
- No trust indicators
- Weak call-to-action

### Product Grid
| Aspect | Current State | Issues |
|--------|---------------|--------|
| Layout | 4-column grid | Clean, good spacing |
| Product cards | Image + Title + Price | Missing quick-add buttons |
| Hover states | None visible | No interaction feedback |
| Badges | None | No "New", "Bestseller", etc. |

### Products (8 visible)
- PCH Classic Snapback – Black & Gold ($38.50)
- PCH Classic Snapback – Lucky Green ($40.00)
- PCH Crewneck Champagne Sweatshirt ($40.00)
- PCH Leather Patch Dad Hat – Red ($22.47)
- PCH Minimalist Cuffed Beanie — Black & Gold ($25.00)
- PCH Prize Patrol Hoodie Red ($60.00)
- PCH Retro Mailbox Trucker Cap ($24.20)
- Prize Patrol Hoodie Blue ($46.53)

**Note:** Price range $22-$60. Inconsistent naming conventions.

### Footer
| Element | Current State | Issues |
|---------|---------------|--------|
| Email signup | "Join our email list" | Basic, functional |
| Social links | YouTube, X only | Limited |
| Legal | Terms and Policies link | Present |

**Missing from Footer:**
- About PCH section
- FAQ/Help links
- Trust badges (BBB, secure checkout)
- Shipping/returns info
- Contact information

---

## Product Detail Page (PDP) Analysis

### Layout
- Two-column: Large image left, product info right
- Image carousel with pagination

### Product Information
| Element | Current State | Assessment |
|---------|---------------|------------|
| Title | Clear, descriptive | Good |
| Price | Prominent | Good |
| Variants | Dropdowns (Size, Color) | Functional but dark styling |
| Quantity | +/- stepper | Good |
| Add to Cart | Black outline button | Could be more prominent |
| Shop Pay | Purple "Buy with Shop" | Good express option |
| Description | Bullet points below fold | Adequate |

### Issues Identified
| Problem | Impact |
|---------|--------|
| No cart feedback | User doesn't know if item was added |
| Redirects to /cart page | Disrupts browsing flow |
| No reviews/ratings | Reduces trust |
| No size guide | Issue for apparel items |
| No inventory indicators | No urgency messaging |

### Cross-Sell Section
- "You may also like" with 4 products
- Same card layout (no quick-add)
- Good recommendation logic

---

## Checkout Analysis

Standard Shopify checkout with:
- Express options: Shop Pay, PayPal, Google Pay, Venmo
- Contact, Delivery, Payment sections
- Order summary sidebar

**Assessment:** Checkout itself is fine. The issue is the flow TO checkout, not the checkout page itself.

---

## Reference Site Analysis

Owen referenced Van Life (vanlife.us) and OVRLND (ovrlnd.com) as inspiration.

### Van Life
| Feature | Implementation |
|---------|----------------|
| Add to Cart | Custom handler with A/B testing |
| Post-add behavior | **Direct redirect to /checkout** |
| Entry system | $1 spent = 1 entry |
| Cart experience | Minimal - skips cart page entirely |

### OVRLND
| Feature | Implementation |
|---------|----------------|
| Add to Cart | Button on product cards |
| Post-add behavior | **Cart drawer/sidebar** |
| Entry system | $1 spent = 10 entries (with 3X promos) |
| Cart experience | Sidebar shows entry count tracking |
| Product cards | Display entry value on each product |

### Key Insight
The two reference sites use **different approaches**:
- Van Life: Direct to checkout (aggressive conversion)
- OVRLND: Cart drawer with entry tracking (browsing-friendly)

---

## Cart UX Recommendation

### The Question: Is a Cart Drawer Better UX?

**For general e-commerce:** Often yes - keeps users browsing.

**For PCH's 60-80 demographic:** Not necessarily.

### Arguments Against Cart Drawer for PCH
- Older users grew up with full-page navigation
- Drawers/overlays can be disorienting or accidentally dismissed
- Smaller text and cramped space in drawers
- Research shows older users prefer explicit, dedicated pages
- Full cart page is more accessible (larger targets, clearer hierarchy)

### Three Options to Consider

| Option | Description | Pros | Cons | Best For |
|--------|-------------|------|------|----------|
| **A: Cart Drawer** | Slide-out sidebar (OVRLND style) | Modern, can show entries, continue shopping easily | May confuse older users, cramped | Younger audiences, multi-item purchases |
| **B: Direct to Checkout** | Skip cart entirely (Van Life style) | Fewest steps, highest conversion | Can't easily add multiple items | Single-item impulse purchases |
| **C: Enhanced Full Page** | Keep current page + add toast notification | Clearest for older demo, most accessible, familiar | Extra click vs drawer | PCH's 60-80 audience |

### My Recommendation: Option C (Enhanced Full Page)

For PCH's specific audience, I recommend:

1. **Keep the dedicated cart page** - familiar, accessible, clear
2. **Add toast notification** - "Added to cart!" appears briefly after click
3. **Update header cart icon** - Show item count badge, animate on add
4. **Add "Continue Shopping" prominence** - Clear button on cart page
5. **Consider testing** - A/B test drawer vs. current if traffic supports it

This approach respects the demographic while improving feedback and flow.

---

## Quick-Add on Product Cards (Requirement #2)

This is a clear win regardless of cart approach.

### Current State
- Must click into product detail page to add to cart
- No quick-add option on homepage or collection pages

### Recommended Implementation
- Add "Add to Cart" button on product card hover (desktop)
- Always-visible "Add to Cart" button (mobile/tablet)
- If variants exist, show variant selector in mini-modal or go to PDP

### Reference: OVRLND Pattern
- "Add to cart" button visible on cards
- Entry count displayed on each product
- Clear, immediate action

---

## Critical Issues Summary

### Priority 1: Cart Flow
- **Issue:** No feedback when adding to cart, page redirect disrupts browsing
- **Solution:** Add toast notification, update cart icon badge
- **Estimated hours:** 3-4

### Priority 2: Quick-Add on Product Cards
- **Issue:** Requires clicking into each product to add to cart
- **Solution:** Add "Add to Cart" button to product cards
- **Estimated hours:** 4-5

### Priority 3: Hero Section
- **Issue:** Weak CTA, no value proposition, AI image concerns
- **Solution:** Stronger button styling, add trust messaging
- **Estimated hours:** 2-3

### Priority 4: Trust Elements
- **Issue:** No trust badges, no brand story, minimal footer
- **Solution:** Add trust badges, shipping info, about section
- **Estimated hours:** 2-3

### Priority 5: CTA Button Styling
- **Issue:** Outline buttons have low contrast/prominence
- **Solution:** Filled buttons for primary actions
- **Estimated hours:** 1-2

---

## Accessibility Considerations (ADA)

Given the 60-80 demographic:

| Area | Current | Recommendation |
|------|---------|----------------|
| Font size | Good | Maintain or increase slightly |
| Color contrast | Mostly good | Fix outline button contrast |
| Touch targets | Adequate | Increase for mobile |
| Form labels | Present | Verify all labeled properly |
| Focus states | Unknown | Verify keyboard navigation |

---

## Phase 2: Sweepstakes Integration Roadmap

When MVP proves successful, integrate sweepstakes:

### Product-Level Integration
- Display entry count on each product card (like OVRLND)
- Show "Buy this = X entries" on PDP
- Entry multiplier promotions (3X entries, etc.)

### Cart-Level Integration
- Running total of entries in cart
- Entry breakdown by product
- Bonus entry thresholds ("Spend $50, get 2X entries")

### Account Integration
- Entry balance dashboard
- Entry history
- Active sweepstakes display

### Technical Requirements
- Integration with PCH drawing engine backend
- Entry tracking via Klaviyo or existing email system
- Legal compliance (entries must include other benefits)

---

## Estimated Scope: Phase 1 MVP Polish

| Task | Priority | Est. Hours |
|------|----------|------------|
| Toast notification for Add to Cart | #1 | 2-3 |
| Cart icon badge update | #1 | 1-2 |
| Quick-add buttons on product cards | #2 | 4-5 |
| CTA button styling improvements | #3 | 1-2 |
| Trust badges in footer | #4 | 1-2 |
| Hero section CTA improvement | #5 | 1-2 |
| General CSS polish | #6 | 2-3 |
| Documentation & recommendations | #7 | 2-3 |
| **Total** | | **15-20 hours** |

---

## Next Steps

1. Review this audit and confirm priorities
2. Grant Shopify collaborator access for implementation
3. Schedule kickoff working session
4. Begin Phase 1 implementation
5. Review and iterate based on feedback
6. Discuss Phase 2 sweepstakes roadmap

---

## Appendix: Reference URLs

- **Current site:** https://www.pchshopping.com/
- **Reference 1:** https://vanlife.us/
- **Reference 2:** https://ovrlnd.com/
- **Main PCH site:** https://pch.com/
