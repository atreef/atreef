# AtReef Therapy: Squarespace 7.1 AI Coding Standards

**Version 3.4**  
**AtReef design system:** v8.5  
**Website:** `https://www.atreef.com`  
**Platform:** Squarespace 7.1, Fluid Engine  
**Updated:** September 28, 2026

---

## How to use this document

This document has two layers:

1. **Part 0: Operating Contract.** One page. These rules are always in force and win over anything in the reference layer.
2. **Parts I to XXVI: Reference.** Tokens, components, compiler rules, and checklists. Consult the part that matches the task.

If time or context is limited, read Part 0, the token tables (Part III), and the Known Violations Register (Part XXV) before writing code.

---

# Part 0: Operating Contract

> **Preserve first. Change only what is necessary. Use the existing AtReef and Squarespace systems before creating new local styling or behavior.**

1. **Scope.** Change only what the user asked for. Preserve copy, URLs, assets, classes, IDs, ARIA, behavior, and breakpoints outside that scope.
2. **System first.** Before writing local CSS, check Site Styles, then global AtReef CSS, then an existing component class. Do not create a second design system inside a section.
3. **Full section output.** Return the complete revised section code, ready to paste, unless the user asks for a snippet.
4. **Production only.** No placeholders, TODOs, fake URLs, or conversational comments in code.
5. **Accessibility floor.** WCAG 2.2 AA. Every color pair must appear in the Verified Contrast Pairs table (§15) or be measured before use. Focus must stay visible on every surface.
6. **Readable sizes.** No reading text below 14px. 12px is allowed only for uppercase labels and eyebrows (§22).
7. **Targets.** Interactive controls are 44px tall when they stand alone. Inline links need at least a 24px hit area (§92).
8. **Headings.** The largest text on a page is the H1. Headings never get a narrow `ch` cap unless the design names it. Code Blocks never set `font-family` on any heading; every H1 to H4 uses the Site Styles heading font (§25).
9. **Case.** Sentence case everywhere, including labels. No all-caps labels and no middle-dot strings ("A · B · C") (§27).
10. **Compiler.** In Design > Custom CSS, escape arithmetic, avoid numeric slash syntax, never use `@container`, and use full asset URLs (Part XII).
11. **Regression.** Before returning code, compare against the original and revert any unrequested change.
12. **Owner preference.** The owner wants the whole site to feel smooth, balanced, and full of personality. When asked, rewrite the CSS and sections completely rather than patching, keep every brand decoration (§59b), and fix size and spacing misalignment on sight using the rhythm in §17a.
13. **Known violations.** If the section you are editing appears in the Known Violations Register (Part XXV), fix only the entries that fall inside the requested scope, and report the others in one line after the code.

---

# Part I: Source of Truth and AI Behavior

## 1. Source of truth order

When sources conflict, use this order:

1. The user's current explicit request.
2. The exact current section code supplied in the request.
3. The current AtReef global CSS supplied with the task.
4. Current Squarespace Site Styles and editor settings.
5. This standards document.
6. Older AtReef code or previous versions.

Do not use an older section or an older standard to overwrite a newer implementation.

If a value is already defined in current code, do not guess a replacement from memory.

Exception: a current value that violates Part 0 (for example, a color pair below AA) is not protected by this order. Flag it, and fix it when it falls inside the requested scope.

---

## 2. Preserve before changing

When modifying existing code:

- Change only what the user requested.
- Preserve unrelated layout, spacing, typography, colors, icons, images, URLs, copy, classes, wrappers, accessibility attributes, behavior, transitions, and breakpoints.
- Do not redesign a section unless the user asks for a redesign.
- Do not restructure working HTML only to make it look cleaner.
- Do not rename classes unless necessary.
- Do not remove a class because it appears unused locally. It may be used by global CSS, JavaScript, analytics, or another block.
- Do not replace real URLs or asset paths with placeholders.
- Do not rewrite copy unless copywriting is part of the request.
- Do not change button destinations unless requested.
- Do not remove animation or interaction unless requested or required for accessibility.
- Do not add decorative styling simply because it looks preferable.

When cleaning code, remove only genuine redundancy, invalid syntax, dead declarations confirmed to be unused, or unnecessary overrides.

---

## 3. Squarespace-first decision order

Before adding local CSS, check whether the requirement is already handled by:

1. Squarespace Site Styles.
2. Current global AtReef CSS.
3. CSS inheritance.
4. An existing AtReef component class.
5. A native Squarespace typography class.
6. Existing section-local CSS.
7. New scoped CSS.
8. JavaScript, only if CSS and native behavior cannot reasonably do the job.

Prefer the highest available option in that list.

---

## 4. Full-code rule

When revising a website section, return the **entire revised section code** unless the user explicitly asks for a snippet.

Do not return only a selector, one declaration, or instructions such as "replace this line."

The default result must be ready to paste directly into the Squarespace Code Block.

When the change is to **Design > Custom CSS**, return the entire stylesheet unless the user asks for a patch.

---

## 5. Production code only

Do not return:

- placeholder URLs
- fake image paths
- pseudo-code
- TODO comments
- unfinished examples
- "insert here" markers
- teaching annotations inside production code
- conversational notes inside code

Documentation examples in this standards file may use placeholders. Production code may not.

---

## 6. Code comments

Production code should be organized but minimally commented.

Use short comments, usually one to three words:

```css
/* Header */
/* Grid */
/* Cards */
/* Mobile */
/* Accessibility */
```

Never write comments such as:

```css
/* Per request */
/* Changed this because the user asked */
/* Keeping the old button */
/* New improved version */
```

Do not include reasoning, changelog notes, or conversation history inside code. The single exception is the version marker on the first line of the global stylesheet, for example `/* AtReef v8.2 */`.

---

## 7. Regression rule

Before returning code, verify that anything outside the requested scope is unchanged.

Check:

- structure
- copy
- URLs
- assets
- typography
- spacing
- colors
- buttons
- icons
- ARIA
- responsive behavior
- animation
- JavaScript behavior
- schema
- SEO semantics

If an unrelated change was introduced, revert it.

---

## 8. Reporting after the code

After the code, add at most five short lines:

- what changed
- anything from Part XXV noticed but left alone
- any Site Styles or editor setting the user must change by hand

Do not repeat the code or explain standard practice.

---

# Part II: AtReef Site Baseline

## 9. Platform

The website uses:

- Squarespace 7.1
- Fluid Engine
- Design > Custom CSS for the global AtReef system
- Code Blocks for section-specific HTML, CSS, and JavaScript
- Squarespace Site Styles for native typography and theme behavior

Do not write code as though this were a standalone React, Webflow, WordPress, or static HTML site.

---

## 10. Site layout baseline

| Setting | Standard |
|---|---|
| Site max width | `1220px` |
| Site margin | `4vw` |
| Fluid Engine column gap | `11px` |
| Fluid Engine row gap | `11px` |
| Standard section vertical padding | `clamp(56px,7vw,96px)` |
| Footer section vertical padding | `clamp(48px,5vw,64px)` |
| Standard card gap | `24px` |
| Standard column gap | `clamp(32px,5.25vw,64px)` |
| Default radius | `5px` |
| Scroll offset | `88px` |
| Minimum supported width | `320px` |

Do not create arbitrary section widths that fight the 1220px Squarespace content width.

Do not add a second custom page container unless a design specifically requires one.

---

## 11. Section rhythm

The global CSS applies vertical section padding to Fluid Engine content wrappers:

```css
.page-section.layout-engine-section>.content-wrapper{
  padding-top:var(--ar-section-y)!important;
  padding-bottom:var(--ar-section-y)!important;
}
```

Footer sections use `--ar-section-y-footer`.

One section, `data-section-id="6a9b4790514b3a068eb2b930"`, is intentionally exempted with zero top and bottom padding. If that section is rebuilt or duplicated, the ID changes and the exemption silently stops working. Check it after any edit to that page.

Do not add local section top or bottom padding unless:

- the section intentionally differs from the global rhythm, or
- the user explicitly asks for it.

If a section appears too tall, first inspect Fluid Engine block height and section settings before adding negative margins or compensating CSS.

---

## 12. Section dividers

Global AtReef CSS draws the default section divider:

```css
.page-section{border-bottom:1px solid var(--ar-divider)}
```

Dark sections use `--ar-divider-dark`.

Footer sections remove the divider.

Do not enable a second Squarespace section divider unless the design intentionally needs both.

---

## 13. Content visibility

The global CSS enables `content-visibility:auto` for these homepage sections:

- `#ar-services`
- `#ar-about`
- `#ar-telehealth`
- `#ar-final-cta`
- `#ar-home-faq`

with:

```css
contain-intrinsic-size:auto 700px;
```

Preserve this unless there is a demonstrated rendering or accessibility problem.

Do not apply `content-visibility` indiscriminately to every section.

Testing note: full-page screenshots in headless browsers render these sections blank. That is a capture artifact, not a site bug. Scroll each section into view before capturing it.

---

# Part III: Canonical Tokens

## 14. Token rule

Global AtReef tokens are the source of truth for repeated values.

Do not hardcode a value locally when the correct token already exists.

Code Blocks should read global tokens with fallbacks when practical:

```css
color:var(--ar-text,#141414);
gap:var(--ar-gap-cards,24px);
border-radius:var(--ar-r,5px);
```

Do not redefine canonical global tokens inside a section unless the section intentionally creates a local theme.

---

## 15. Color tokens

| Token | Value | Use |
|---|---:|---|
| `--ar-teal` | `#004643` | primary brand teal |
| `--ar-text` | `#141414` | primary text on light surfaces |
| `--ar-body` | `var(--ar-text)` | body text |
| `--ar-muted` | `#53635F` | muted text |
| `--ar-ink` | `var(--ar-text)` | ink alias |
| `--ar-gold` | `#FEDA6A` | primary gold accent, fills, and gold marks on dark surfaces |
| `--ar-gold-hover` | `#F6D366` | gold hover and pressed state |
| `--ar-gold-wash` | `rgba(254,218,106,.22)` | light gold state |
| `--ar-gold-border` | `#E8CB68` | gold hover border |
| `--ar-gold-ink` | `#8A6A00` | gold meaning on light surfaces (stars, small gold marks) |
| `--ar-paper` | `#FDFAF7` | paper surface |
| `--ar-cream` | `#F5F0EA` | cream surface |
| `--ar-gold-tint` | `#FFF9EA` | pale gold surface |
| `--ar-white` | `#FFFFFF` | white surface |
| `--ar-border` | `#D6DFDA` | decorative neutral border (cards, dividers) |
| `--ar-field-border` | `#6F857E` | form field and control boundaries |
| `--ar-surface-hover` | `#EEF3F0` | light hover surface |
| `--ar-on-dark` | `#FAFAFA` | primary text on dark surfaces |
| `--ar-on-dark-muted` | `rgba(250,250,250,.74)` | muted dark-surface text |
| `--ar-line` | `rgba(0,70,67,.12)` | light hairline |
| `--ar-line-strong` | `rgba(0,70,67,.22)` | stronger hairline |
| `--ar-line-dark` | `rgba(255,255,255,.14)` | dark-surface hairline |
| `--ar-divider` | `rgba(0,70,67,.08)` | section divider |
| `--ar-divider-dark` | `rgba(255,255,255,.08)` | dark section divider |
| `--ar-focus` | `#004643` | focus outline on light surfaces |
| `--ar-focus-dark` | `#FEDA6A` | focus outline on dark surfaces |

### Verified contrast pairs

Measured with the WCAG 2.x formula. Text needs 4.5:1 (3:1 at 24px, or 18.66px bold). Control boundaries, focus rings, and meaningful icons need 3:1.

| Foreground | Background | Ratio | Allowed for |
|---|---|---:|---|
| `--ar-text` | page `#FAFAFA` | 17.7 | all text |
| `--ar-text` | `--ar-gold` | 13.6 | button labels on gold |
| `--ar-teal` | page, paper, white | 10.3 | text, focus ring, icons |
| `--ar-muted` | page, paper | 6.1 | muted body text |
| `--ar-muted` | `--ar-gold-tint` | 6.0 | muted body text |
| `--ar-muted` | `--ar-cream` | 5.6 | muted body text |
| `--ar-on-dark` | `--ar-teal` | 10.3 | text on dark |
| `--ar-on-dark-muted` | `--ar-teal` | 6.4 | muted text on dark |
| `--ar-gold` | `--ar-teal` | 7.9 | labels, focus ring, stars on dark |
| `--ar-gold-ink` | white | 5.1 | stars, gold marks on light |
| `--ar-gold-ink` | `--ar-cream` | 4.47 | stars and icons only (non-text, 3:1); not for small text |
| `--ar-field-border` | white | 3.9 | field boundaries |

### Pairs that fail and must not carry meaning

| Foreground | Background | Ratio | Rule |
|---|---|---:|---|
| `--ar-gold` | any light surface | 1.2 to 1.4 | never as text, icon, star, or focus ring on light |
| `--ar-border` | white or page | 1.3 to 1.4 | decoration only, never a field boundary |
| `rgba(0,70,67,.45)` | page | 2.4 | retired focus value; do not reintroduce |

### Color rules

- Light-theme primary text is `#141414`.
- Teal is an accent and semantic brand color, not the default paragraph color.
- Do not scatter `#141414` across sections when inheritance or `--ar-text` can handle it.
- Use section themes and global tokens before local background colors.
- Do not change theme colors while solving a layout-only problem.
- Do not add a border to a solid surface unless the component system calls for it.
- Gold on light surfaces is a fill, never a foreground. When gold meaning must appear as a mark on a light surface, use `--ar-gold-ink`.
- Do not introduce a new color outside this palette. The owner-approved brand decorations in §59b (the verified badge, the colored calendar, and the pill icons) are the only exceptions, and they must never be removed or recolored.

---

## 16. Typography tokens

| Token | Current value |
|---|---|
| `--ar-fs-label` | `12px` |
| `--ar-fs-small` | `14px` |
| `--ar-fs-note` | `14px` |
| `--ar-fs-body` | `16px` |
| `--ar-lh-small` | `22px` |
| `--ar-lh-body` | `28px` |
| `--ar-fs-lead` | `clamp(1.125rem,1.068rem + .242vw,1.25rem)` |
| `--ar-fs-h4` | `clamp(1.25rem,1.193rem + .242vw,1.375rem)` |
| `--ar-fs-h3` | `clamp(1.375rem,1.204rem + .727vw,1.75rem)` |
| `--ar-fs-h2` | `clamp(1.75rem,1.409rem + 1.455vw,2.5rem)` |
| `--ar-fs-display` | `clamp(2rem,1.545rem + 1.939vw,3rem)` |
| `--ar-fs-hero` | `clamp(2.25rem,1.568rem + 2.909vw,3.75rem)` |

The arithmetic `clamp()` values are escaped in Custom CSS because of Squarespace's legacy LESS compiler.

Do not retype these formulas inside Code Blocks when the token exists.

---

## 17. Spacing tokens

| Token | Value |
|---|---:|
| `--ar-1` | `4px` |
| `--ar-2` | `8px` |
| `--ar-3` | `12px` |
| `--ar-4` | `16px` |
| `--ar-6` | `24px` |
| `--ar-8` | `32px` |
| `--ar-12` | `48px` |
| `--ar-16` | `64px` |
| `--ar-gap-label` | `12px` |
| `--ar-gap-pill` | `16px` |
| `--ar-gap-heading` | `24px` |
| `--ar-gap-para` | `16px` |
| `--ar-gap-cta` | `32px` |
| `--ar-gap-header` | `48px` |
| `--ar-gap-cards` | `24px` |
| `--ar-gap-cols` | `clamp(32px,5.25vw,64px)` |
| `--ar-card-pad` | `clamp(24px,2.6vw,32px)` |
| `--ar-section-y` | `clamp(56px,7vw,96px)` |
| `--ar-section-y-footer` | `clamp(48px,5vw,64px)` |

### Spacing rhythm (§17a)

One rhythm for every section. Measure it after every change.

| Relationship | Value |
|---|---|
| label to title | 12px (`--ar-gap-label`) |
| pill to title | 16px (`--ar-gap-pill`) |
| icon tile row to title | 16px |
| title to lead or first paragraph | 24px |
| paragraph to paragraph | 16px |
| section header to content | 48px (`ar-head`) |
| card padding | `--ar-card-pad` (32px desktop, 24px mobile, 16px under 380px); never set locally |
| carousel first card | flush with the section heading's left edge; the next card peeks in on the right |

### Spacing rhythm, legacy notes

Default relationships:

- eyebrow to heading: use the label or pill component's own margin
- heading to lead: `24px`
- header block to content: `48px`
- CTA separation: `32px`
- cards: `24px`
- paragraphs in a stack: `16px`

Do not create one-off values such as `27px`, `37px`, or `53px` unless the layout genuinely requires them.

---

## 18. Measure tokens

| Token | Value | Use |
|---|---:|---|
| `--ar-measure` | `64ch` | readable body measure |
| `--ar-measure-tight` | `46ch` | compact body measure in narrow cards |
| `--ar-measure-heading` | `20ch` | intentionally constrained headings |

`--ar-measure-heading` is **not** a default maximum width for every heading.

Do not constrain a heading to `20ch`, `18ch`, or another character measure unless the design intentionally needs wrapping.

In a card wider than about 480px, a `46ch` copy cap leaves dead space on the right. Use `ar-card__copy--wide` (64ch) there.

---

## 19. Shape, depth, and target tokens

| Token | Value |
|---|---|
| `--ar-r` | `5px` |
| `--ar-r-inner` | `2px` |
| `--ar-tile` | `40px` |
| `--ar-tile-sm` | `24px` |
| `--ar-band` | `48px` |
| `--ar-target` | `44px` |
| `--ar-target-min` | `24px` |
| `--ar-shadow` | `0 8px 24px rgba(0,70,67,.05)` |
| `--ar-shadow-hover` | `0 12px 32px rgba(0,70,67,.065)` |
| `--ar-shadow-lift` | `0 16px 32px rgba(0,70,67,.08)` |
| `--ar-ease` | `cubic-bezier(.22,1,.36,1)` |
| `--ar-fast` | `160ms` |
| `--ar-reveal` | `320ms` |

Use the site radius and shadows consistently. Do not introduce large rounded cards, pill-shaped cards, or heavy shadows unless the user explicitly asks for a different visual language.

---

## 20. Wave backgrounds

The global CSS provides:

- `--ar-wave`
- `--ar-wave-cream`
- `--ar-wave-dark`

These are subtle radial gradients used on system cards and dark surfaces.

Do not reproduce the gradient locally. Use the existing card variants.

Use `background-color` and `background-image` separately when preserving a wave. Avoid a `background:` shorthand that accidentally removes the image.

---

# Part IV: Typography and Site Styles

## 21. Native typography first

Use semantic HTML and allow Squarespace Site Styles to control typography when the design does not intentionally depart from native styles.

Use heading levels for document structure and SEO, not merely for visual size.

Do not change a heading level only because another level looks larger or smaller.

---

## 22. Type size floor

| Text | Minimum |
|---|---|
| Body, card copy, answers, testimonials | `16px` |
| Notes, captions, footer links, legal links, cookie text | `14px` |
| Uppercase labels and eyebrows (with tracking) | `12px` |
| Anything else | not allowed below `14px` |

Rules:

- Do not use Squarespace **scaled text** for body copy, links, or legal text. It shrinks text to fit and can drop it below 11px.
- Do not solve a fit problem by reducing font size. Let the text wrap.
- Testimonials are persuasive content. They use body size, never small text.

---

## 23. Paragraph styles

### Paragraph 1

```html
<p class="sqsrte-large">...</p>
```

### Paragraph 2

```html
<p>...</p>
```

### Paragraph 3

```html
<p class="sqsrte-small">...</p>
```

Paragraph 3 must render at 14px or larger. In Site Styles, set Paragraph 3 to at least `0.875rem`. The global CSS guards the footer only.

When using native paragraph styles, avoid local font family, size, weight, line height, and letter spacing unless the design requires a deliberate exception.

---

## 24. Miscellaneous / meta typography

The Miscellaneous font on this site is a script face (`lovely-r6xgg0`). Use it only where a script accent is intended.

If only the font family is needed:

```css
font-family:var(--meta-font-font-family);
```

If the component is intended to follow the complete Miscellaneous control, use the available Squarespace variables:

```css
font-family:var(--meta-font-font-family);
font-size:var(--meta-font-font-size);
font-style:var(--meta-font-font-style);
font-weight:var(--meta-font-font-weight);
line-height:var(--meta-font-line-height);
letter-spacing:var(--meta-font-letter-spacing);
text-transform:var(--meta-font-text-transform);
```

If the user requests one intentional delta, keep only that delta local. Example inside a Code Block:

```css
font-size:calc(var(--meta-font-font-size) + 4px);
```

Do not set `font-family` from Miscellaneous while separately hardcoding every other typography property unless that mixed behavior is intentional.

---

## 25. Brand fonts and heading font rule

Site Styles currently set:

- heading font: `pogonia-q6ye39`
- body font: `Karla`
- Miscellaneous font: `lovely-r6xgg0`

The global CSS defines:

```css
--ar-font:"Karla",Arial,sans-serif;
--ar-font-display:"pogonia-q6ye39",sans-serif;
--ar-font-script:"AR Autumn","Snell Roundhand","Brush Script MT",cursive;
```

`AR Autumn` is loaded through `@font-face` from the existing Squarespace CDN URL.

### Heading font rule

- **Every heading, H1 to H4,** uses the Site Styles heading font. Code Blocks never set `font-family` on a heading, and never set `font-family` on a section root (it cascades into headings).
- **Section titles (H2)** use `ar-title` and take size, weight, line-height, and tracking from Site Styles. Change Heading 2 in Site Styles to resize every section at once.
- **Component titles (H3)** use `ar-card__title`, which sets size only. Family, weight, and tracking come from Site Styles.
- **Body text** inherits the Site Styles paragraph font. Leads use Paragraph 1 (`sqsrte-large`).
- A heading that renders in Karla is a violation of this rule.
- Labels styled as H3 (`<h3 class="ar-label">`) are the one exception: the label class sets the body font on purpose.

### Brand font rules

- Preserve the current font file URL.
- Do not share or expose font files outside the website.
- Do not replace brand fonts with generic substitutes unless requested.
- Do not use the script font for body copy, links, or anything a person must read to act.
- Use display or script typography sparingly and intentionally.

---

## 26. Global text behavior

The global CSS applies:

```css
h1,h2,h3,h4{text-wrap:balance}
p{text-wrap:pretty}
```

Light-theme headings, paragraphs, and list items inside Squarespace content areas are standardized to `--ar-text`.

Do not fight `text-wrap:balance` with arbitrary narrow widths.

---

## 27. Case and capitalization

- Use sentence case for headings, buttons, labels, card titles, and navigation: "Free consultation", not "Free Consultation".
- Proper nouns keep their capitals: "Gottman Method", "Cambridge", "AtReef Therapy".
- Labels are sentence case, 14px, weight 600, marked with the brand diamond (`/s/Diamond-Dot.svg`, 14px, set in `.ar-label::before`). The marker box is 20px tall, equal to the label line-height, so the diamond centers on the first line; never offset it with a margin. Use `ar-label--plain` where an icon tile or pill already marks the line.
- Never type capitals for emphasis ("START HERE").
- Do not join phrases with middle dots. Write them as a phrase: "Online therapy in Massachusetts", "Structured, active, collaborative".

---

## 28. Heading wrapping rules

A repeated AtReef issue has been headings wrapping too early because local code adds narrow values such as:

```css
max-width:18ch;
```

Rules:

- Do not add a heading `max-width` unless the design intentionally needs a constrained measure.
- Do not use `--ar-measure-heading` automatically.
- If a heading should use the available section width, use `width:100%` and `max-width:none` only when a conflicting cap must be neutralized.
- Do not use `white-space:nowrap` as a default desktop rule.
- If a specific heading must remain on one line, use `nowrap` deliberately and restore wrapping before overflow can occur.
- Test long headings at intermediate widths, not only desktop and mobile.

---

## 29. Typography and layout separation

Typography classes and layout classes serve different jobs.

Do not remove a layout class simply because typography is inherited from Squarespace.

Do not hardcode typography into a class whose purpose is only alignment, grid placement, or spacing.

---

# Part V: Layout and Responsive Behavior

## 30. Fluid Engine placement

When building a section:

- Prefer one Code Block that spans the intended content width.
- Do not use extra Fluid Engine rows to create vertical spacing.
- Let global section padding create section rhythm.
- Keep block height tight to its content.
- Do not use absolute positioning to solve a normal layout problem.
- Text blocks must not extend past the content edge. Check the right edge of right-aligned blocks at 1024px and 1440px.

---

## 31. Section scoping

Every custom section should have one unique root ID:

```html
<section id="ar-example" aria-labelledby="ar-example-title">
```

Scope local CSS to that ID:

```css
#ar-example .ar-example__title{...}
```

Avoid broad local selectors such as:

```css
h2{...}
.card{...}
a{...}
```

unless the change is intentionally global and belongs in Custom CSS.

---

## 32. Box sizing

A section may safely normalize box sizing inside its scope:

```css
#ar-example,
#ar-example *,
#ar-example *::before,
#ar-example *::after{
  box-sizing:border-box;
}
```

Do not create a site-wide reset inside a Code Block.

---

## 33. Responsive strategy

Use this order:

1. intrinsic layout
2. flexible grid or flex behavior
3. existing global responsive component behavior
4. container queries inside Code Blocks
5. viewport media queries only when viewport behavior is genuinely required

Do not invent a viewport breakpoint simply because a design has two columns.

The component should respond to the space it actually has whenever possible.

---

## 34. Mobile content order

On narrow screens, the first viewport must show what the page offers and how to act on it.

- In a hero, the order on mobile is: eyebrow, H1, lead, primary CTA, then the image.
- A portrait or decorative image may lead only if it is 280px tall or less on a 390px wide screen.
- Test at 390×844. The primary CTA of the hero should start above 844px with the cookie banner dismissed.

---

## 35. Card-grid standard

The AtReef card-grid system responds to available width rather than a fixed viewport breakpoint.

```css
.ar-card-grid{
  display:grid;
  grid-template-columns:minmax(0,1fr);
  align-items:stretch;
  gap:var(--ar-gap-cards);
  width:100%;
  min-width:0;
}

.ar-card-grid--2{
  grid-template-columns:repeat(auto-fit,minmax(min(100%,420px),1fr));
}

.ar-card-grid--3{
  grid-template-columns:repeat(auto-fit,minmax(min(100%,320px),1fr));
}
```

### Grid rules

- Use `ar-card-grid ar-card-grid--2` for reusable two-card layouts.
- Use `ar-card-grid ar-card-grid--3` for reusable three-card layouts.
- Do not recreate the same grid locally in a section.
- Do not add a section-specific `900px` breakpoint for these grids.
- Use a custom local grid only when the section's information architecture genuinely differs from the global card system.
- Preserve the standard `24px` card gap unless the design explicitly requires a different relationship.

---

## 36. Container queries

Container queries are preferred for section-local layout when a component must respond to its own available width.

```css
#ar-example{
  container:ar-example / inline-size;
}

@container ar-example (max-width:760px){
  #ar-example .ar-example__layout{
    grid-template-columns:1fr;
  }
}
```

Important: container queries belong in Code Block `<style>` tags, not in Design > Custom CSS, because the Squarespace Custom CSS compiler cannot parse `@container`.

---

## 37. Breakpoints currently used globally

The global CSS uses viewport media queries primarily at:

- `380px`
- `640px`
- `768px`

Do not add another global breakpoint unless it solves a site-wide need.

Section-local container breakpoints do not need to match these viewport values.

---

## 38. Minimum widths and overflow

Use `min-width:0` on grid and flex children when text or nested content could otherwise force overflow.

Do not solve overflow by hiding it unless the content is intentionally clipped.

Avoid fixed widths for text cards.

Do not join inline items with `&nbsp;` runs. They cannot wrap and will overflow at narrow widths. Use a list with `gap`.

---

# Part VI: AtReef Button System

## 39. Button architecture

The global button system uses:

- `.ar-btn`
- `.ar-btn--primary`
- `.ar-btn--secondary`
- `.ar-btn--tertiary`
- `.ar-btn--compact`
- `.ar-btn__label`
- `.ar-btn__chip`
- `.ar-btn__icon`
- `.ar-btn__image`

Do not rebuild buttons locally if one of these variants fits the job.

---

## 40. Button tokens

| Token | Value |
|---|---|
| `--arb-h` | `44px` |
| `--arb-r` | `var(--ar-r)` |
| `--arb-px` | `24px` |
| `--arb-py` | `8px` |
| `--arb-gap` | `8px` |
| `--arb-ico` | `20px` |
| `--arb-badge` | `32px` |
| `--arb-fs` | `15px` |
| `--arb-fw` | `500` |

The base button uses `width:fit-content`, inherits font family, and keeps a maximum width of 100%.

Labels stay on one line above 640px and wrap below it.

---

## 41. Primary button

`ar-btn--primary` is the split gold button.

```html
<a class="ar-btn ar-btn--primary" href="...">
  <span class="ar-btn__label">Label</span>
  <span class="ar-btn__chip" aria-hidden="true">
    <span class="ar-btn__icon ar-btn__icon--arrow"></span>
  </span>
</a>
```

Characteristics:

- gold label and chip
- separate 44px chip
- 5px radius
- subtle border and shadow
- slight hover lift
- gold-hover background on press

The chip holds either a monochrome `ar-btn__icon` or an owner-approved colored image (`<img class="ar-btn__image" src="/s/calendar.svg" alt="">`). Consultation CTAs use the colored calendar. Do not use emoji.

Do not combine the split pieces into one generic button without a design request.

---

## 42. Secondary button

`ar-btn--secondary` uses a bordered teal-tinted surface with a separate right chip area.

Use it for strong secondary navigation and especially on dark surfaces with `ar-btn--on-dark` when appropriate.

---

## 43. Tertiary button

`ar-btn--tertiary` is the low-emphasis text link with:

- underlined label
- 32px circular badge
- chevron-style icon
- no outer border or fill

Use it for actions such as "More questions answered" or a low-priority continuation link.

Do not add an extra circle around the whole button.

---

## 44. Compact button

`ar-btn--compact` is a compact gold control with a dark circular icon chip.

It supports block width with `ar-btn--block`.

---

## 45. Icon utilities

Current icon utilities:

- `ar-btn__icon--book`
- `ar-btn__icon--read`
- `ar-btn__icon--arrow`
- `ar-btn__icon--chevron`
- `ar-btn__icon--cal`
- `ar-btn__icon--check`
- `ar-ico-cal`
- `ar-ico-check`
- `ar-ico-chevron`

Do not introduce a new icon system for a single section when an existing utility already matches.

---

## 46. Button width utilities

- `ar-btn--block` makes a button full width.
- `ar-btn--hug` keeps content width.

The element name is intentionally included in global CSS selectors such as `a.ar-btn--block` to win against the base anchor specificity.

---

## 47. Button states

Preserve:

- visible keyboard focus
- active scale and pressed background
- disabled state
- busy spinner
- pointer and touch behavior
- hover behavior only on hover-capable devices
- reduced-motion override
- forced-colors support

The pressed background exists because `-webkit-tap-highlight-color:transparent` removes the browser's default touch feedback, and reduced motion removes the scale. Do not remove either without replacing the feedback.

Do not add hover-only information that is required to understand the action.

---

## 48. Button groups and notes

`ar-btn-group`:

- flex
- wraps
- `16px` gap
- becomes a vertical stack below `640px`

`ar-btn-note`:

- maximum `52ch`
- `14px` size
- `22px` line-height
- muted text

Do not use `ar-btn-note` as a substitute for normal body copy.

---

## 49. CTA label standard

One action has one name across the site.

| Context | Label |
|---|---|
| Primary consultation CTA, full width available | "Book a free 30-minute consultation" |
| Primary consultation CTA, tight space (cards, footer, menu) | "Book a free consultation" |
| Service navigation | the service name in sentence case, for example "Couples therapy" |
| Low-priority continuation | a descriptive phrase, for example "More questions answered" |

Rules:

- Do not introduce new verbs ("Schedule", "Start", "Get") for the consultation CTA.
- Do not use Title Case on button labels.
- Link text must describe the destination. Never "Click here" or "Learn more" alone.

The user owns final wording. If they choose a different canonical label, update this table and use it everywhere.

---

# Part VII: Selection and Disclosure Controls

## 50. Control tokens

The control system uses the `--arc-*` namespace.

| Token | Value |
|---|---|
| `--arc-h` | `48px` |
| `--arc-r` | `var(--ar-r)` |
| `--arc-gap` | `8px` |
| `--arc-px` | `12px` |
| `--arc-py` | `8px` |
| `--arc-dot` | `7px` |
| `--arc-fs` | `14px` |
| `--arc-fs-seg` | `14px` |
| `--arc-fw` | `600` |

---

## 51. Pills

Classes:

- `.ar-pills`
- `.ar-pills--3`
- `.ar-pills--2`
- `.ar-pill__input`
- `.ar-pill__option`

Default `.ar-pills` uses four equal columns.

At `640px` and below, pill layouts become two columns.

At `380px` and below, pill layouts become one column.

Do not rewrite these controls as JavaScript tabs unless the interaction requires more than the existing CSS state behavior.

---

## 52. Segmented controls

Classes:

- `.ar-seg`
- `.ar-seg--3`
- `.ar-seg__input`
- `.ar-seg__option`

Checked segments use teal with light text and a gold dot.

At `380px` and below, segmented controls become one column.

---

## 53. Disclosure / FAQ controls

Classes:

- `.ar-disclosure`
- `.ar-disclosure__summary`
- `.ar-disclosure__panel`
- `.ar-disclosure__mark`

Use native `<details>` and `<summary>` whenever the interaction is a disclosure or FAQ.

Current global disclosure typography:

- summary: `16px`, weight `600`, line-height `24px`
- panel: `16px`, line-height `28px`
- mark: `24px`

The plus/minus mark is built with CSS pseudo-elements.

Do not replace native disclosure behavior with JavaScript solely for animation.

---

# Part VIII: Card and Container System

## 54. Container namespace

The container system uses `--ark-*` compatibility aliases that point back to canonical `--ar-*` values.

Preserve the namespace because existing sections depend on it.

Do not duplicate the old standalone container-system stylesheet on top of the current global CSS.

---

## 55. Base card

`.ar-card`:

- flex column
- width 100%
- `min-width:0`
- height 100%
- fluid padding using `--ar-card-pad`
- 5px radius
- paper background
- subtle wave background
- hidden overflow

At `380px` and below, base card padding becomes `16px`.

---

## 56. Card surface modifiers

Available surfaces:

- `ar-card--green`
- `ar-card--green-alt`
- `ar-card--cream`
- `ar-card--paper`
- `ar-card--white`
- `ar-card--translucent`
- `ar-card--wash`

Available behavior/layout modifiers:

- `ar-card--bordered`
- `ar-card--flush`
- `ar-card--pad-lg`
- `ar-card--lift`
- `ar-card--auto`
- `ar-card--flat`
- `ar-card--interactive`

Important:

- base cards are height 100%
- use `ar-card--auto` when the card should size to its content
- `ar-card--white` uses a stronger line and standard shadow
- `ar-card--flat` removes the wave background image
- dark cards (`--green`, `--green-alt`, `--translucent`) automatically switch `ar-card__title` and `ar-card__copy` to light text, and switch focus rings to gold

Do not recreate these properties in section CSS when a modifier already exists.

---

## 57. Card band and body

Classes:

- `ar-card__band`
- `ar-card__band--gold`
- `ar-card__body`

The band has a standard minimum height of `48px`.

Use these for true labeled or staged card structures, not as decorative stripes.

---

## 58. Tiles

Classes:

- `ar-tile`
- `ar-tile--ghost`
- `ar-tile--sm`

Default tile size is `40px`.

Small tile size is `24px`.

Default icon SVG inside a tile is `20px`; small is `14px`.

Use tiles for compact icon emphasis. Do not place every icon inside a tile automatically.

---

## 59. Labels and eyebrows

Classes:

- `ar-label`
- `ar-label--on-dark`
- `ar-label--muted`
- `ar-label--tight`
- `ar-label--pill`
- `ar-label__icon`

Base label:

- `12px`
- weight `700`
- line-height `16px`
- `.08em` tracking
- uppercase
- teal
- `12px` bottom gap

Pill label:

- inline-flex
- `8px` internal icon gap
- `8px 12px` padding
- white 94% surface
- hairline border
- 5px radius
- subtle shadow
- weight `600`
- `16px` bottom gap

At `380px` and below, the pill may wrap.

A pill eyebrow may sit above a plain label when each has its own job: the pill names who (brand), the label names what or where (topic, location). Keep the spacing 16px pill to label, 12px label to heading.

When an icon is decorative:

```html
<img src="/s/icon.svg" alt="" aria-hidden="true">
```

The hero pill uses the owner's `verified.svg` badge. Keep it as supplied.

---

## 59a. Section text

| Class | Use |
|---|---|
| `ar-title` | section H2; color from `--ar-heading`, everything else from Site Styles |
| `ar-title--on-dark` | section H2 on dark sections (`--ar-heading-on-dark`) |
| `ar-lead` | lead paragraph; pair with `sqsrte-large` so Paragraph 1 sets the size |
| `ar-lead--on-dark` | lead on dark sections |
| `ar-copy` | muted body paragraph, 16px / 28px, 64ch |
| `ar-copy--on-dark` | muted body on dark sections |
| `ar-hl--script` | script-font gold highlight for one phrase in a display headline; use with `ar-hl` |

`--ar-heading` defaults to `--ar-text`. Set it to `var(--ar-teal)` in one place to make every light-section title teal.

---

## 59b. Brand decorations

Decorations are part of the brand, not clutter. Never remove, recolor, or swap them during a code task. Keep them consistent instead.

| Decoration | Where | Purpose |
|---|---|---|
| Pill eyebrow with icon (`ar-label ar-label--pill` + `ar-label__icon`) | hero (`/s/verified.svg`), conversation (`/s/landscape.svg`), FAQ (`/s/Streamline-Ultimate.svg`) | opens a major light section and names who or what it is about |
| Colored calendar (`/s/calendar.svg` in `ar-btn__image`) | every consultation CTA chip | signals "book a time" at a glance |
| Script highlight (`ar-hl ar-hl--script`) | hero headline only | one emotional phrase per page |
| Gold band highlight (`ar-hl`) | one phrase in a section title | emphasis, at most once per section |
| Icon tiles (`ar-tile`, `ar-tile--ghost`, `ar-tile--sm`) | card headers and lists | scannable markers |

Consistency rules:

- Pill: 32px tall, 16px icon, 8px icon gap, 5px radius, soft two-layer shadow. Defined once in global CSS; never restyled locally.
- Button images: 20px, centered in the chip, slight scale on hover (off under reduced motion).
- Pills sit only on light surfaces. On dark sections use a plain `ar-label--on-dark`.
- One pill per section at most.

---

## 59c. Two voices (signature motif)

The site's signature is the two-voice panel from the conversation section: the client's words on gold tint, the therapist's response on teal, inside one framed card.

| Class | Use |
|---|---|
| `ar-voices` | the frame: paper, 8px inset, 8px gap, border, soft shadow |
| `ar-voice` | the client voice: gold tint, card padding |
| `ar-voice ar-voice--reply` | the response or outcome: teal, light text |

Used in the conversation examples and the client experiences carousel. Use it where content is genuinely a statement and a response. Do not use it as a generic card.

## 59d. Section head

`ar-head` stacks label, title, and lead with the §17a rhythm and adds 48px before the content. `ar-head--center` centers it. Closing sections (client experiences, final CTA, FAQ) are centered; content sections are left-aligned.

---

## 60. Card typography

`.ar-card__title`:

- maximum `24ch`
- uses `--ar-fs-h4`
- weight `600`
- line-height `1.27`
- slight negative tracking

`ar-card__title--lead` uses `--ar-fs-h3`.

`ar-card__title--wide` removes the `24ch` cap.

`.ar-card__copy`:

- maximum `--ar-measure-tight` / `46ch`
- `16px`
- weight `400`
- line-height `28px`
- pretty wrapping

`ar-card__copy--wide` raises the cap to `--ar-measure` / `64ch`.

`.ar-card__footer` uses automatic top margin with `32px` top padding.

Use these classes rather than locally retyping the same card styles.

---

## 61. Card grids

See Section 35.

A section that uses system cards should generally use the system grid as well.

Do not define a local `.section__grid` with identical behavior unless the section needs a materially different layout.

---

## 62. Ratings

Classes:

- `ar-stars`
- `ar-stars--on-dark`

```html
<span class="ar-stars" role="img" aria-label="Rated 5 out of 5"></span>
```

Rules:

- Stars are five copies of the brand `/s/Star.svg`, drawn by the CSS from one background image. The span stays empty; `role="img"` and the aria-label carry the rating. Default 16px (88px row); `ar-stars--lg` is 20px (112px row). The star has its own fill and outline, so it reads on light and dark surfaces alike; `ar-stars--on-dark` is kept as a harmless alias. Never type star characters or inline star SVGs.
- `aria-label` on a plain `<span>` is ignored by many screen readers. Always add `role="img"`.
- Show the rating source next to the stars in text ("5.0 on Grow Therapy").

---

## 63. Dark local surfaces

When a local component has a dark background and does not use a system dark card, add `ar-surface-dark` to its root:

```html
<article class="ar-services__card ar-services__card--green ar-surface-dark">
```

This switches focus rings inside it to gold. The global two-color focus ring keeps focus visible even when this class is missing, but the class gives the intended brand treatment.

---

# Part IX: Heading and Utility Classes

## 64. Highlight

`.ar-hl` creates the gold band highlight behind part of a heading.

Use it for an intentionally emphasized phrase, not every heading.

Do not replace it with `<mark>` unless the semantics actually mean highlighted or relevant content.

---

## 65. Forced line break

`.ar-line` becomes block at `768px` and wider.

Use it only when an intentional desktop line break is part of the design.

Do not use it to repair a heading that is wrapping because of an unnecessary max-width.

---

## 66. Scroll controls

Classes:

- `ar-scroll-nav`
- `ar-scroll-btn`

The scroll button is:

- `44px` square
- paper background
- teal icon
- standard border
- 5px radius
- keyboard focus visible

Use these for previous/next controls in horizontal content. Every scroll button needs an `aria-label` ("Previous step", "Next step").

---

## 67. Measure utilities

- `ar-measure`: `64ch`
- `ar-measure--tight`: `46ch`
- `ar-sr`: visually hidden screen-reader text

Use `ar-sr` for accessible labels that should not be visually displayed.

---

# Part X: Site-wide Squarespace Overrides

## 68. Platform cleanup

The global CSS hides Squarespace block-status and removed-script UI artifacts:

```css
.sqs-block .sqs-blockStatus,
.sqs-block .removed-script{display:none!important}
```

Do not remove these without checking the editor and live site.

---

## 69. Smooth scrolling

Smooth scrolling is enabled only when reduced motion is not requested:

```css
@media (prefers-reduced-motion:no-preference){
  html{scroll-behavior:smooth}
}
```

All IDs use `scroll-margin-top:88px`.

Preserve this behavior when adding anchor targets.

---

## 70. Squarespace site animations

Site Styles > Animations applies a fade or slide to every block, currently about `0.8s` with a stagger. That is slower than the AtReef `--ar-reveal` token (`320ms`) and hides content until JavaScript runs.

Rules:

- Keep Site Styles > Animations set to **None**, or to the shortest fade available.
- The global CSS forces `.preFade`, `.preSlide`, `.preScale`, `.preClip`, and `.preFlex` to their final visible state under `prefers-reduced-motion:reduce`. Preserve that guard.
- Do not add a second entrance animation inside a Code Block.

---

## 71. Forms

Form fields and textareas use:

- white background
- `1px` `--ar-field-border`
- `5px` radius
- `44px` minimum height
- `12px 16px` padding
- teal border plus the global focus ring on focus

Every field needs a visible label. Placeholder text is not a label.

Do not style individual forms differently unless the form has a deliberate special design.

---

## 72. Blog

The global blog system includes:

- gold `.blog-more-link`
- ink text
- 5px radius
- 44px minimum height
- 24px horizontal padding
- hover color on hover-capable devices, pressed color on touch
- 5px radius on supported blog image wrappers

Do not locally rebuild the read-more button on individual posts.

---

## 73. Mobile menu

Current global mobile menu behavior:

- CTA width `86vw`
- CTA max width `420px`
- nav item font size `18px`
- nav item weight `700`
- each nav link `44px` tall (`13px` vertical padding), `50px` pitch

Do not reintroduce negative margins on `.header-menu-nav-item`. They shrink tap targets to about 18px.

Do not change mobile navigation while solving a page-section problem.

---

## 74. Navigation dropdown

The desktop folder dropdown uses:

- 5px padding
- subtle border
- 5px radius
- restrained shadow
- `8px 12px` item padding
- hover gold wash with `--ar-gold-border`
- teal focus outline

Preserve the current interaction and focus behavior.

---

## 75. Newsletter

At `640px` and below, newsletter form controls are forced to full width.

Do not override this locally without testing mobile form usability.

---

## 76. Footer

The global CSS:

- removes text-decoration and background-image from footer anchors
- underlines footer text links on hover and keyboard focus
- sets Paragraph 3 in footer text blocks to `14px` / `22px`
- gives footer text links and all `tel:` links `5px` vertical padding for a larger hit area

Footer content rules:

- Footer column headings follow the heading hierarchy. Use a visually hidden H2 ("Site footer" with `ar-sr`) above the column H3s, or use `<p class="ar-label">` for the column titles.
- Crisis numbers are always `tel:` links: `<a href="tel:988">988</a>`, `<a href="tel:911">911</a>`.
- Legal links are a list, not a line of text joined with `&nbsp;`:

```html
<ul class="ar-footer__legal" aria-label="Legal">
  <li><a href="/privacy-policy">Privacy</a></li>
  <li><a href="/terms-and-conditions">Terms</a></li>
  <li><a href="/disclaimer">Disclaimer</a></li>
  <li><a href="/no-surprises-act">Good Faith Estimate</a></li>
</ul>
```

- Never put prose inside `<pre>` or `<code>`. Screen readers may announce it as code.

Do not add a site-wide link underline rule that unintentionally changes the footer.

---

## 77. Cookie banner

The global CSS sets cookie banner text to `14px` / `22px` and banner buttons to `14px`, `44px` tall, with `.02em` tracking.

Keep Site Styles primary and secondary button letter-spacing equal. The banner uses both, and unequal tracking makes the two buttons look unrelated.

---

## 78. Native Squarespace buttons

Native list and carousel buttons are globally normalized for full-width left-aligned content.

The global CSS also forces `.sqs-block-button-container--center` and `--right` to left alignment. A centered button set in the editor will render left-aligned. That is intentional; do not report it as a bug, and do not fight it with local CSS.

Do not assume every visible button uses the custom `ar-btn` system.

Before editing a button, identify whether it is:

- native Squarespace
- `ar-btn`
- a third-party embed control

---

## 79. Lists and quotes

List cards use:

- teal translucent border
- 5px radius
- 32px padding

Quote blocks use:

- pale gold background
- 24px padding
- 16px teal left border
- dark text

Quote sources are uppercase, 12px, tracked, and right aligned.

Preserve these global styles unless the user asks for a redesign.

---

# Part XI: CSS Architecture

## 80. Global vs local CSS

Put a rule in **Design > Custom CSS** when it is:

- a site-wide token
- a reusable AtReef component
- a global Squarespace override
- a site-wide accessibility rule
- a shared utility

Put a rule in a **Code Block `<style>`** when it is:

- unique to one section
- section layout
- section-specific typography exception
- section-specific responsive behavior
- a container query

Do not move unique section layout into global CSS only to reduce the size of a Code Block.

Do not duplicate a global component inside section CSS.

---

## 81. Specificity

Prefer predictable, scoped selectors.

Good:

```css
#ar-example .ar-example__title{...}
```

Avoid unnecessary specificity such as:

```css
body main .page-section #ar-example div.wrapper h2.ar-example__title{...}
```

Use `!important` only when overriding Squarespace inline styles or high-specificity platform rules that cannot be cleanly overridden otherwise.

Do not use `!important` between AtReef's own component rules.

---

## 82. Reset specificity

A local reset can accidentally override component classes because an ID selector is strong.

Avoid broad rules such as:

```css
#ar-example p{margin:0}
```

when the section contains global components that depend on paragraph margins.

If necessary, exclude system classes with `:where()` to keep specificity controlled:

```css
#ar-example :is(h2,p):not(:where(.ar-label)){
  margin:0;
}
```

---

## 83. Do not duplicate system values

Do not locally redefine:

- palette
- radius
- standard shadows
- standard card padding
- button height
- standard icon sizes
- standard disclosure typography
- label typography
- card-grid behavior
- heading font family

unless the section intentionally departs from the system.

---

## 84. Safe cleanup

Safe cleanup includes:

- removing exact duplicate declarations
- consolidating duplicate selectors
- fixing malformed CSS
- removing unused code only when confirmed unused
- replacing a local duplicate with an existing system class
- simplifying unnecessary wrappers when the change is explicitly a cleanup and semantics remain intact

Do not perform a design-system migration as a side effect of a small requested change.

---

## 85. Global selectors that touch links

A global rule that targets `a` inside a container will also hit `a.ar-btn`. Always exclude buttons:

```css
footer .sqs-html-content a:not(.ar-btn){...}
```

---

# Part XII: Squarespace Custom CSS Compiler

## 86. Compiler model

Squarespace Design > Custom CSS is processed by a legacy LESS compiler.

Code Block `<style>` tags are normal browser CSS and do not pass through that compiler.

This distinction is critical.

To test locally, LESS `1.4.2` reproduces Squarespace's output for this stylesheet, including the escaped `clamp()` values, `min()` inside `minmax()`, `mask` shorthand with `center/contain`, and data URI icons. Newer LESS (1.7 and later) rejects `min()` and is not a valid stand-in.

---

## 87. Verified compiler rules

| Construct in Design > Custom CSS | Result | Rule |
|---|---|---|
| `calc(50% - var(--x))` | unsafe / fatal | escape it |
| `~'calc(50% - var(--x))'` | passes through | use this form |
| fluid `clamp()` with arithmetic such as `1rem + 1vw` | unsafe | escape it |
| `clamp(56px,7vw,96px)` without arithmetic | safe | allowed |
| `min()` / `max()` without arithmetic | safe | allowed |
| `grid-column:1/-1` | miscompiled | do not use |
| `grid-area:9/6/9/15` | miscompiled | do not use |
| `aspect-ratio:16/9` | treated as math | do not use unescaped |
| font shorthand with line-height slash | safe special case | allowed |
| `mask:... center/contain` | safe | allowed |
| `@container` | parse failure | Code Blocks only |
| `:is()`, `:has()`, `:where()`, `:not()` | safe | allowed |
| `@supports`, `@media`, `@keyframes` | safe | allowed |
| encoded SVG data URI | safe | allowed |

---

## 88. Arithmetic rule

In Custom CSS, escape expressions that trigger LESS arithmetic.

```css
--ar-fs-h2:~'clamp(1.75rem,1.409rem + 1.455vw,2.5rem)';
```

Do not escape simple CSS functions merely because they contain different units if there is no arithmetic operation.

---

## 89. Numeric slash rule

Do not use numeric slash syntax in Design > Custom CSS for:

- grid line shorthand
- grid area shorthand
- aspect ratio

Use explicit longhands, an escaped value where appropriate, or keep the rule inside a Code Block.

---

## 90. Asset URL rule

In **Design > Custom CSS**, use a full AtReef URL for uploaded assets:

```css
url("https://www.atreef.com/s/file.svg")
```

A root-relative `/s/file.svg` can resolve against the Squarespace static CSS origin and fail.

Inside a **Code Block**, root-relative website paths such as `/s/file.svg` are acceptable. When reliability matters, a full `https://www.atreef.com/s/...` URL is also acceptable.

---

## 91. Token collision rule

Do not create a new global token with the same name as a section-local token.

Historical/local blocks may use names such as:

- `--ar-green`
- `--ar-white`
- `--ar-light`
- `--ar-dark`
- `--ar-yellow`
- `--ar-radius`
- `--ar-sp-*`
- `--sp-*`

Prefer canonical global `--ar-*` names already defined in the current system.

---

# Part XIII: Accessibility

## 92. Accessibility floor

Target WCAG 2.2 AA behavior.

Do not remove working accessibility features to achieve a visual effect.

### Targets

| Control | Minimum |
|---|---|
| Buttons, standalone links, form fields, menu items | `44px` tall |
| Inline text links, footer links, legal links, icon links | `24px` hit area (WCAG 2.5.8) |
| Segmented controls and pills | `48px` |

Inline padding on an `<a>` enlarges the hit area without changing layout. Use it to reach 24px.

Do not shrink button or control hit areas just to make a layout visually tighter.

---

## 93. Focus visibility

The global focus system is a two-color ring:

- `2px` solid `--ar-focus` (teal) outline, `2px` offset
- `2px` `--ar-paper` halo drawn by `box-shadow` inside the offset

The teal ring is visible on light surfaces. The paper halo is visible on dark surfaces. Together they satisfy 3:1 on every AtReef surface.

On known dark surfaces (`.dark`, `.dark-bold`, `.black`, `.ar-surface-dark`, dark system cards, card bands), the outline switches to `--ar-focus-dark` (gold).

Rules:

- Do not suppress `outline` without providing an equal or better visible focus state.
- Do not set a translucent focus color. Focus rings need 3:1 against the surface.
- A component that sets its own `box-shadow` on focus replaces the halo. Include the halo in that shadow.

---

## 94. Decorative media

For decorative images and icons:

```html
<img src="..." alt="" aria-hidden="true">
```

Do not write keyword-heavy alt text for decorative assets.

Meaningful images need concise, accurate alt text that explains the content or function. The therapist portrait is meaningful: "Dr. Ehsan Adib Shabahang".

---

## 95. Reduced motion

Preserve `prefers-reduced-motion:reduce` handling.

Do not introduce essential information that is available only through animation.

Auto-moving content (marquees, carousels) must have a pause control and must stop under reduced motion.

Use motion sparingly and intentionally.

---

## 96. Forced colors

The global system includes `forced-colors:active` fallbacks for buttons, controls, cards, ratings, and scroll controls.

When creating a new custom interactive component, add a forced-colors fallback when the custom visuals would otherwise disappear.

---

## 97. Accessible names and ARIA

- `aria-labelledby` must point at the element that is the section's actual heading.
- `aria-label` works on interactive elements, landmarks, and elements with a role. On a plain `<span>` or `<div>`, add a role or use visually hidden text.
- `role="listitem"` requires a parent with `role="list"`. Prefer real `<ul>` and `<li>`.

---

# Part XIV: HTML and Semantics

## 98. Semantic HTML

Prefer meaningful elements when they match the content:

- `<section>`
- `<header>` when appropriate
- `<nav>`
- `<h1>` through `<h4>`
- `<p>`
- `<a>`
- `<button>`
- `<details>`
- `<summary>`
- `<ul>` / `<ol>`

Do not replace a working structure with semantic elements solely for theoretical purity if doing so creates risk.

---

## 99. Anchors vs buttons

Use `<a>` for navigation to another URL.

Use `<button>` for an action on the current page.

Do not convert one to the other for visual reasons.

---

## 100. Heading hierarchy

Use one logical page hierarchy: one H1, then H2 sections, then H3 subsections.

- The visually largest headline on the page is the H1. Do not style the H1 as a small eyebrow while the display headline is a `<p>`.
- If the SEO phrase ("Couples therapy in Cambridge, Massachusetts") and the display headline differ, put both in the H1 and style the parts:

```html
<h1 id="ar-couples-title">
  <span class="ar-label">Couples therapy in Cambridge, Massachusetts</span>
  <span class="ar-display">Change the pattern and find your way back.</span>
</h1>
```

- Do not choose H3 because it visually resembles the desired size.
- If a group heading is semantically a subsection under an H2, an H3 is appropriate even if its typography is controlled by Miscellaneous Site Styles.

Styling and semantics are separate decisions.

---

## 101. IDs and ARIA linkage

When a section has a visible heading, prefer:

```html
<section id="ar-example" aria-labelledby="ar-example-title">
  <h2 id="ar-example-title">...</h2>
</section>
```

IDs must be unique on the page.

---

# Part XV: SEO and LLM-Friendly Structure

## 102. Semantic SEO

Preserve:

- meaningful headings
- descriptive link text
- internal page URLs
- visible crawlable text
- semantic sections
- valid structured data when present

Do not create headings solely for keywords.

---

## 103. FAQ structure

For FAQs, prefer native HTML:

```html
<details class="ar-disclosure">
  <summary class="ar-disclosure__summary">Question</summary>
  <div class="ar-disclosure__panel">
    <p>Answer.</p>
  </div>
</details>
```

Keep question and answer text in the HTML. Do not load core FAQ answers only through JavaScript.

Do not add FAQ schema merely because a FAQ section exists. Structured data must be valid, current, and appropriate for the search platform's current support.

---

## 104. Answer construction

When writing or revising FAQ content for search and AI retrieval:

- answer the question directly in the first sentence
- keep important facts explicit
- use the practice name where attribution matters
- state location or modality when relevant
- avoid keyword repetition that makes the answer unnatural
- use internal links only when they help the reader continue
- do not make unsupported clinical or outcome claims

Coding tasks should not rewrite existing FAQ copy unless copy optimization is requested.

---

## 105. Entity consistency

When content mentions the practice, provider, location, services, fees, or credentials, preserve the site's canonical wording and current facts.

Do not invent alternate business names, addresses, credentials, prices, or service availability.

---

## 106. Structured data

Do not duplicate JSON-LD already present in Squarespace or another code block. The homepage currently carries four JSON-LD blocks; check them before adding another.

When schema is requested:

- validate the schema type
- use real visible information
- keep URLs canonical
- avoid unsupported review markup
- do not hide schema-only marketing claims from users

---

# Part XVI: Clinical Content Compliance

## 107. Testimonials and outcome claims

AtReef is a licensed mental health practice. Marketing content is subject to professional ethics codes and state licensing rules, not only to design standards.

When code touches testimonials, reviews, ratings, or outcome language:

- Do not add, invent, edit, or paraphrase a testimonial. Use only text the user supplies.
- Do not add review schema for testimonials.
- Do not write outcome guarantees or implied results ("unrecognizable", "saved our marriage", "guaranteed").
- Before publishing a testimonial section, remind the user in one line to confirm consent and that no testimonial was solicited from a current client (ACA Code of Ethics C.3.b) and that it meets current Massachusetts licensing board rules.
- Third-party ratings must name their source and must match what that source currently shows.

This part flags issues for the user. It does not decide them. The user owns clinical and legal judgment.

---

## 108. Crisis information

The crisis notice ("In an emergency, do not use this site.") and the 988 and 911 links appear on every page. Do not remove, shorten, restyle to low contrast, or hide them behind interaction.

---

# Part XVII: JavaScript and Interaction

## 109. JavaScript threshold

Do not add JavaScript when CSS or native HTML can solve the requirement.

Prefer CSS/native HTML for:

- hover states
- disclosure behavior
- responsive layout
- simple show/hide states
- styling transitions

Use JavaScript for behavior that genuinely requires state, measurement, scrolling logic, or dynamic interaction.

---

## 110. Existing scripts

If a section already contains working JavaScript:

- preserve event behavior unless the request changes it
- do not change class names or IDs the script depends on
- do not add duplicate listeners
- do not initialize the same component twice
- guard selectors before using them
- avoid global variables when local scope works

---

## 111. Motion

The AtReef visual system favors restrained motion.

Existing global transitions are typically around `160ms` with subtle movement. Reveals use `320ms` at most.

Do not add widespread entrance animations, parallax, bouncing, or large scaling as a default modernization technique.

---

# Part XVIII: Assets and URLs

## 112. Preserve assets

Do not change:

- image sources
- SVG paths
- file URLs
- internal page links
- external links
- booking destinations
- anchors

unless the task requests it or the current value is demonstrably broken.

---

## 113. Uploaded SVGs

In Code Blocks, decorative uploaded SVGs commonly use:

```html
<img src="/s/file.svg" alt="" aria-hidden="true">
```

If the icon fails to load, confirm the path and use the full AtReef URL rather than inventing a new asset.

Icons follow the palette. Do not use multicolor icons or emoji where the system uses monochrome icons.

---

## 114. No placeholders

Never replace a known AtReef URL with:

- `example.com`
- `YOUR_URL`
- `#`
- `javascript:void(0)`
- fake asset names

unless `#` is intentionally part of a real in-page interaction and semantically appropriate.

---

# Part XIX: Building New Sections

## 115. New-section workflow

1. Identify the section's single job.
2. Determine its semantic heading level.
3. Check whether Squarespace Site Styles already handle typography.
4. Check global AtReef components before creating new ones.
5. Use one unique `#ar-*` root.
6. Use system tokens with fallbacks.
7. Use intrinsic layout first.
8. Use container queries only if needed.
9. Add JavaScript only if needed.
10. Test at 320, 390, 820, 1024, and 1440px.
11. Check keyboard focus on every interactive element, reduced motion, and the type size floor.
12. Return complete production code.

---

## 116. New-section template

```html
<style>
#ar-example{
  container:ar-example / inline-size;
  width:100%;
}

#ar-example,
#ar-example *,
#ar-example *::before,
#ar-example *::after{
  box-sizing:border-box;
}

/* Layout */

#ar-example .ar-example__layout{
  display:grid;
  grid-template-columns:repeat(2,minmax(0,1fr));
  gap:var(--ar-gap-cols,64px);
}

/* Mobile */

@container ar-example (max-width:760px){
  #ar-example .ar-example__layout{
    grid-template-columns:1fr;
    gap:32px;
  }
}
</style>

<section id="ar-example" aria-labelledby="ar-example-title">
  <div class="ar-example__layout">
    <div>
      <p class="ar-label">Eyebrow</p>
      <h2 id="ar-example-title">Heading</h2>
      <p>Body copy.</p>
    </div>

    <div class="ar-card ar-card--cream">
      <h3 class="ar-card__title">Card title</h3>
      <p class="ar-card__copy">Card copy.</p>
    </div>
  </div>
</section>
```

This is a structural template, not a visual requirement. Use the system classes that fit the actual content.

---

## 117. Reusing global card grids

If a section only needs two or three responsive cards, prefer:

```html
<div class="ar-card-grid ar-card-grid--2">
```

or:

```html
<div class="ar-card-grid ar-card-grid--3">
```

Do not add a custom grid unless it adds real section-specific behavior.

---

# Part XX: Fixing Existing Sections

## 118. Troubleshooting table

| Symptom | Likely cause | First fix |
|---|---|---|
| Whole site loses custom styling | Custom CSS compile failure | inspect compiled CSS and recent change |
| One fluid value becomes incorrect | unescaped LESS arithmetic | escape the value in Custom CSS |
| Container query fails globally | `@container` placed in Custom CSS | move it into Code Block CSS |
| Icon missing only from global CSS | root-relative asset URL | use full `https://www.atreef.com/s/...` URL |
| Heading wraps much too early | local `max-width` in `ch` | remove or increase the intentional measure |
| Section title renders in Karla | local `font-family` on the heading | remove it; Site Styles heading font applies |
| Miscellaneous Site Style changes do not affect text | local typography overrides | remove hardcoded properties or bind meta variables |
| Card grid does not respond to available width | local grid or fixed viewport breakpoint | use global intrinsic `ar-card-grid` |
| Card is too tall | base `.ar-card` is `height:100%` | add `ar-card--auto` when intended |
| Wide card has empty right half | `46ch` copy cap | add `ar-card__copy--wide` |
| Global component class seems ineffective | stronger section ID reset | narrow the reset or exclude the system class |
| Background texture disappears | `background:` shorthand overwrote image | separate `background-color` and `background-image` |
| Section has excess vertical space | Fluid Engine rows or section setting | fix editor layout before CSS hacks |
| Internal button styling changes unexpectedly | local selector overrides global component | remove duplicate local button declarations |
| Disclosure loses keyboard behavior | custom JS replaced native `<details>` | restore native disclosure markup |
| Text clips on mobile | fixed width, `&nbsp;` runs, or missing `min-width:0` | make layout flexible and test wrapping |
| Text below 12px | Squarespace scaled text or Paragraph 3 size | turn off scaled text; raise Paragraph 3 in Site Styles |
| Focus ring invisible | translucent focus color or dark local surface | use the global ring; add `ar-surface-dark` |
| Stars look empty or mismatched | text stars or inline SVG | use an empty `ar-stars` span (Star.svg) |

---

## 119. Heading issue workflow

When a heading looks wrong:

1. inspect local `max-width`
2. inspect `white-space`
3. inspect local `font-family`, font-size, and line-height overrides
4. inspect the section's available width
5. inspect global `text-wrap:balance`
6. inspect Site Styles

Do not immediately add a smaller font size.

---

## 120. Site Styles issue workflow

When changing Squarespace Site Styles does not affect an element:

1. inspect the element's local section CSS
2. inspect global AtReef CSS
3. check whether a native element style is being overridden by a component class
4. inspect inherited variables
5. remove only the blocking declarations

Do not solve a Site Styles inheritance problem by adding more hardcoded local values.

---

# Part XXI: Required Site Styles Settings

## 121. Settings the CSS depends on

These are editor settings, not code. The AI cannot change them; it must tell the user when a task depends on them.

| Setting | Required value | Why |
|---|---|---|
| Fonts > Headings | `pogonia-q6ye39` | heading font rule (§25) |
| Fonts > Paragraph | `Karla` | body font |
| Fonts > Paragraph 3 size | `0.875rem` or larger | type size floor (§22) |
| Animations | None, or the shortest fade | motion rule (§70) |
| Buttons > letter-spacing | same value for primary and secondary | cookie banner and native buttons (§77) |
| Text blocks > scaled text | off for body, links, legal | type size floor (§22) |

---

# Part XXII: Deployment and Verification

## 122. Deployment order

When replacing the system:

1. update Design > Custom CSS
2. verify the compiled stylesheet
3. update dependent Code Blocks
4. verify each edited page on desktop and mobile
5. check keyboard interaction
6. check reduced motion
7. check browser console if JavaScript changed
8. verify assets and links

Do not replace every section at once when only one section changed.

---

## 123. Custom CSS verification

After editing Design > Custom CSS:

- confirm the beginning of the compiled stylesheet exists (the version marker comment)
- confirm the final rules exist (`.ar-sr`)
- look for compiler error text
- test at least one shared component from the beginning and end of the stylesheet
- verify mobile media rules
- tab through the homepage and confirm a visible ring on every stop, including inside dark cards

A compiler problem can remove or corrupt large parts of the site even when the editor appears to accept the save.

---

## 124. Code Block verification

After editing a section:

- confirm unique ID
- confirm no unclosed tags
- confirm no duplicate IDs
- confirm assets load
- confirm system classes still work
- confirm mobile layout at 320px and 390px
- confirm no text below the type size floor
- confirm FAQ/disclosure keyboard access when applicable
- confirm no console errors if JavaScript exists

---

## 125. Drift check

Run this before every release and once a month. Search the page source (View Source, or a saved copy) for:

| Pattern | Violation |
|---|---|
| `max-width:\s*1[0-9]ch` on headings | heading cap (§28) |
| `900px` | section viewport breakpoint (§35) |
| `font-family` inside `#ar-* h1`, `#ar-* h2` rules | heading font override (§25) |
| `sqsrte-scaled-text` | scaled text (§22) |
| `&nbsp;&nbsp;` | unwrappable runs (§38) |
| `<pre>` or `<code>` outside technical content | misused code markup (§76) |
| `aria-label` on `<span>` without `role` | ignored accessible name (§97) |

Add every hit to Part XXV until it is fixed.

---

# Part XXIII: Release Map

## 126. Current v8.3 map

| File | Destination |
|---|---|
| `atreef-custom-css.css` (v8.3) | Design > Custom CSS |
| `blocks/01-hero.html` | `#ar-couples-hero` Code Block |
| `blocks/02-conversation.html` | `#ar-conversation` Code Block |
| `blocks/03-services.html` | `#ar-services` Code Block |
| `blocks/04-about.html` | `#ar-about` Code Block |
| `blocks/05-approach.html` | `#ar-approach` Code Block |
| `blocks/06-telehealth.html` | `#ar-telehealth` Code Block |
| `blocks/07-client-proof.html` | `#ar-client-proof` Code Block |
| `blocks/08-final-cta.html` | `#ar-final-cta` Code Block |
| `blocks/09-faq.html` | `#ar-home-faq` Code Block |
| `atreef_block-footer-consult_v8.html` | `#ar-footer-consultation` Footer Code Block (not yet revised) |

Paste the CSS first. The new blocks depend on v8.3 classes and look wrong on v8.2.

---

## 127. v8.2 changes from v8.1

- Focus: solid teal and gold rings, plus a paper halo that keeps focus visible on any surface; focus also covers inputs; dark system cards and `ar-surface-dark` switch to gold
- Nav dropdown focus: teal instead of gold on white
- Forms: `--ar-field-border`, 44px fields, 5px radius
- Mobile menu: 44px links, no negative margins
- Footer: 14px Paragraph 3 links, 24px+ hit areas, hover and focus underline
- `tel:` links: larger hit area site-wide
- Cookie banner: 14px text and buttons, 44px buttons, even tracking
- Reduced motion: Squarespace block animations shown immediately
- Buttons: pressed state for touch, focus radius only on transparent variants, labels wrap below 640px
- `ar-btn-note`: 14px / 22px
- Pills and segments: 14px
- Cards: dark cards set light title and copy automatically; `ar-card__copy--wide`, `ar-card__title--wide`
- New: `ar-stars`, `ar-stars--on-dark`, `--ar-gold-ink`, `--ar-gold-border`, `--ar-field-border`, `--ar-target`, `--ar-target-min`, `--ar-fs-note`, `--ar-lh-small`, `--ar-lh-body`
- Blog read-more: 24px horizontal padding, touch pressed state

## 127a. v8.3 changes from v8.2

- New tokens: `--ar-heading`, `--ar-heading-on-dark`
- New classes: `ar-title`, `ar-title--on-dark`, `ar-lead`, `ar-lead--on-dark`, `ar-copy`, `ar-copy--on-dark`, `ar-hl--script`
- `ar-card__title` no longer sets `font-family`; Site Styles heading font applies
- Light-section text color rule now skips `ar-` components and anything inside dark cards or `ar-surface-dark` (it was forcing ink text onto dark cards)
- All nine homepage blocks rewritten on the shared system (`squarespace/blocks/`); they require v8.3

## 127c. v8.5 changes from v8.4

- Labels: sentence case, 14px, dot marker, `ar-label--plain`; no more all-caps labels
- New `ar-head` section header and `ar-voices` / `ar-voice` / `ar-voice--reply` signature components
- Client experiences rebuilt as two-voice cards; conversation uses the shared components
- Carousels align with their heading; approach carousel script reads `--ar-inset`
- Unified card padding and label-to-title spacing; removed local padding overrides
- Middle-dot eyebrows rewritten as plain phrases

## 127b. v8.4 changes from v8.3

- Restored the owner's brand decorations: hero pill with verified badge, colored calendar in consultation CTAs
- Pill eyebrow refined: 32px height, fixed 16px icon, softer layered shadow
- Button images get a smooth hover scale (disabled under reduced motion)
- New §59b documents every decoration and its purpose

---

# Part XXIV: Class Reference

## 127d. v8.8 changes from v8.7

- Label marker: the 6px round dot is replaced by the brand Diamond-Dot (14px, original colors, full `https://www.atreef.com/s/` URL). It centers on the first line box instead of using a 7px top margin.

## 127e. v8.9 changes from v8.8

- Ratings: `ar-stars` now repeats the brand Star.svg five times (16px, `ar-stars--lg` 20px). Hero, services and client experiences all use the same class; the inline SVG stars in client experiences are gone.
- Client experiences: on cards under 700px the stars sit under the title instead of beside it.

## 127f. v8.9.1 client experiences, compact

- Values reduced, no new components: quote 16/26 at every width (the 700px 20/32 override is removed), quote mark 36px with an 18px icon, panel gap 12px, reply panel 20px top and bottom, standard 16px stars, decorative circle 140px.
- Section height drops about 100px (desktop 609 to 509, phone 770 to 672). The Fluid Engine Code Block must be shortened in the editor to match.

## 128. Class reference

### Buttons

- `.ar-btn`
- `.ar-btn--primary`
- `.ar-btn--secondary`
- `.ar-btn--tertiary`
- `.ar-btn--compact`
- `.ar-btn--on-dark`
- `.ar-btn--block`
- `.ar-btn--hug`
- `.ar-btn__label`
- `.ar-btn__chip`
- `.ar-btn__icon`
- `.ar-btn__image`
- `.ar-btn__icon--color`
- `.ar-btn__icon--book`
- `.ar-btn__icon--read`
- `.ar-btn__icon--arrow`
- `.ar-btn__icon--chevron`
- `.ar-btn__icon--cal`
- `.ar-btn__icon--check`
- `.ar-ico-cal`
- `.ar-ico-check`
- `.ar-ico-chevron`
- `.ar-btn-group`
- `.ar-btn-note`
- `.ar-btn-note--on-dark`

### Controls

- `.ar-pills`
- `.ar-pills--3`
- `.ar-pills--2`
- `.ar-pill__input`
- `.ar-pill__option`
- `.ar-seg`
- `.ar-seg--3`
- `.ar-seg__input`
- `.ar-seg__option`
- `.ar-disclosure`
- `.ar-disclosure__summary`
- `.ar-disclosure__panel`
- `.ar-disclosure__mark`

### Cards

- `.ar-card`
- `.ar-card--green`
- `.ar-card--green-alt`
- `.ar-card--cream`
- `.ar-card--paper`
- `.ar-card--white`
- `.ar-card--translucent`
- `.ar-card--wash`
- `.ar-card--bordered`
- `.ar-card--flush`
- `.ar-card--pad-lg`
- `.ar-card--lift`
- `.ar-card--auto`
- `.ar-card--flat`
- `.ar-card--interactive`
- `.ar-card__band`
- `.ar-card__band--gold`
- `.ar-card__body`
- `.ar-card__title`
- `.ar-card__title--lead`
- `.ar-card__title--wide`
- `.ar-card__title--on-dark`
- `.ar-card__copy`
- `.ar-card__copy--wide`
- `.ar-card__copy--on-dark`
- `.ar-card__footer`
- `.ar-card-grid`
- `.ar-card-grid--2`
- `.ar-card-grid--3`

### Tiles, labels, and ratings

- `.ar-tile`
- `.ar-tile--ghost`
- `.ar-tile--sm`
- `.ar-label`
- `.ar-label--on-dark`
- `.ar-label--muted`
- `.ar-label--tight`
- `.ar-label--pill`
- `.ar-label__icon`
- `.ar-stars`
- `.ar-stars--on-dark`

### Section text

- `.ar-title`
- `.ar-title--on-dark`
- `.ar-lead`
- `.ar-lead--on-dark`
- `.ar-copy`
- `.ar-copy--on-dark`
- `.ar-hl--script`

### Surfaces and utilities

- `.ar-surface-dark`
- `.ar-hl`
- `.ar-line`
- `.ar-scroll-nav`
- `.ar-scroll-btn`
- `.ar-measure`
- `.ar-measure--tight`
- `.ar-sr`

Do not create near-duplicate classes with different names unless a new component truly requires different behavior.

---

# Part XXV: Known Violations Register

## 129. How to use the register

This register lists live issues found in the homepage audit of September 26, 2026. It is a to-do list, not a style to copy.

- When a task touches a listed section, fix the entries inside the requested scope.
- Report the rest in one line after the code.
- Remove an entry only after the fix is live and verified.

## 130. Register

Status after the v8.3 block release (September 28, 2026). "Fixed in files" means the corrected code is in `squarespace/blocks/` and is live once pasted.

| Section | Issue | Rule | Status |
|---|---|---|---|
| Site Styles | Paragraph 3 size is `0.7` | §22, §121 | open (editor) |
| Site Styles | Animations fade every block over about 0.8s | §70 | open (editor) |
| Site Styles | primary and secondary button letter-spacing differ | §77 | open (editor) |
| `#ar-couples-hero` | H1 was the eyebrow; display headline was a `<p>` | §100 | fixed in files |
| `#ar-couples-hero` | mobile gap under the text after moving the photo below | §34 | open (Fluid Engine, see blocks README) |
| `#ar-couples-hero` | verified badge and colored calendar | §59b | kept by owner decision; refined in v8.4 |
| `#ar-services` | duplicate grid, gold-on-cream stars, "Schedule" CTA, no dark-surface hook | §35, §62, §49, §63 | fixed in files |
| `#ar-about` | narrow title cap; Karla heading override | §28, §25 | fixed in files |
| `#ar-approach` | Karla heading override; hardcoded colors | §25, §15 | fixed in files |
| `#ar-telehealth` | narrow caps; Karla override; wide-card dead space; aria-label differs from visible label | §28, §25, §18, §97 | fixed in files |
| `#ar-client-proof` | 12.5px quotes; Title Case; blocked vertical page swipe; no way for mouse users to reach card three | §22, §27, §92 | fixed in files |
| `#ar-client-proof` | outcome language in testimonials; consent not documented here | §107 | open (user decision) |
| `#ar-final-cta` | narrow title cap; non-standard CTA label | §28, §49 | fixed in files |
| `#ar-final-cta` | links to the booking portal while the hero links to `/consultation` | §49 | open (user decision) |
| `#ar-home-faq` | invalid `calc(--meta-font-font-size)`; script group titles at 14px | §24, §22 | fixed in files |
| Footer | legal row in scaled text with `&nbsp;` runs; "Good Faith Estimat" link split | §22, §38, §76 | open |
| Footer | `<pre><code>` script line; typed "START HERE"; H3s without H2; "Free Consultation" | §76, §27, §49 | open |
| Footer | footer logo mark differs from header logo mark | brand review | open |

---

# Part XXVI: Final Preflight

## 131. Scope

- [ ] Only requested behavior changed.
- [ ] Unrelated content and design remain intact.
- [ ] Existing classes and IDs were preserved unless change was necessary.

## 132. Squarespace

- [ ] The code is appropriate for Squarespace 7.1.
- [ ] Global CSS rules are not duplicated in a Code Block.
- [ ] `@container` is not placed in Design > Custom CSS.
- [ ] Custom CSS arithmetic is escaped when required.
- [ ] Asset URLs use the correct context.
- [ ] Any required Site Styles change is listed for the user.

## 133. Typography

- [ ] Semantic heading levels are correct, and the largest headline is the H1.
- [ ] Section titles use the Site Styles heading font.
- [ ] Native Site Styles are used when appropriate.
- [ ] Miscellaneous typography is not blocked by unnecessary local overrides.
- [ ] Custom brand fonts are preserved.
- [ ] Headings do not have accidental narrow `ch` caps.
- [ ] No text is below the type size floor.
- [ ] Sentence case is used; no typed capitals.

## 134. Layout

- [ ] Layout respects the 1220px site width and 4vw margins.
- [ ] Standard card grids use `ar-card-grid` when appropriate.
- [ ] Responsive behavior depends on available space where practical.
- [ ] No unnecessary new viewport breakpoint was added.
- [ ] Grid and flex children use `min-width:0` when needed.
- [ ] No accidental overflow occurs at 320px or intermediate widths.
- [ ] On mobile, the hero H1 and primary CTA appear before the image.

## 135. Components

- [ ] Existing AtReef buttons are reused.
- [ ] CTA labels follow §49.
- [ ] Existing card variants are reused.
- [ ] Existing labels and pills are reused.
- [ ] Existing disclosure controls are reused.
- [ ] Ratings use `ar-stars`.
- [ ] Dark local surfaces carry `ar-surface-dark`.
- [ ] No near-duplicate component was created unnecessarily.

## 136. Accessibility

- [ ] Every color pair is in §15 or was measured.
- [ ] Focus is visible on every interactive element, on light and dark surfaces.
- [ ] Targets meet §92.
- [ ] Decorative icons are hidden from screen readers.
- [ ] Meaningful images have appropriate alt text.
- [ ] Reduced-motion behavior is preserved.
- [ ] Forced-colors behavior is preserved where relevant.
- [ ] Native controls remain keyboard accessible.
- [ ] `aria-label` is only on elements that support it.

## 137. SEO and content

- [ ] Heading hierarchy remains logical.
- [ ] Important content remains visible in HTML.
- [ ] URLs and link text are preserved unless intentionally changed.
- [ ] Schema is valid and not duplicated if present.
- [ ] No unsupported claims or invented business facts were added.
- [ ] Testimonial and crisis content follow Part XVI.

## 138. Code quality

- [ ] Code is scoped.
- [ ] No placeholder content remains.
- [ ] No conversational comments are inside code.
- [ ] Comments are short and functional.
- [ ] No unnecessary `!important` was added.
- [ ] No redundant local tokens or components were created.
- [ ] No JavaScript was added unless necessary.

## 139. Output

- [ ] Complete revised section is returned unless a snippet was requested.
- [ ] Code is formatted and production-ready.
- [ ] No tutorial text is embedded inside code.
- [ ] The result can be pasted directly into Squarespace.
- [ ] Out-of-scope Part XXV items are reported in one line.

---

# Governing Principle

When uncertain, apply this rule:

> **Use the current AtReef system first. Preserve working code. Let Squarespace Site Styles control what they already control. Add the smallest scoped change needed. Keep the site responsive to the space it actually has. Keep every word readable and every control reachable. Do not create a second design system inside a section.**

---

# Quick AI Prompt

When this file is attached, the user can say:

> **Follow the AtReef Therapy Squarespace 7.1 AI Coding Standards v3.1. Use the current global CSS and Site Styles as the source of truth, make only the requested change, preserve everything else, and return the complete production-ready section code.**

That instruction activates all rules in this document.
