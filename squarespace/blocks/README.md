# AtReef homepage blocks (v8.8)

## Order of work

1. Paste `../atreef-custom-css.css` into **Design > Custom CSS** (replace everything). Save.
2. Paste each file below into its Code Block (replace everything in the block).
3. Fix the hero gap on mobile (steps at the bottom).
4. Check the page on your phone.

| File | Code Block |
|---|---|
| `01-hero.html` | Hero |
| `02-conversation.html` | "A therapist who engages" |
| `03-services.html` | Couples / Individual cards |
| `04-about.html` | Meet Dr. Shabahang |
| `05-approach.html` | Five steps carousel |
| `06-telehealth.html` | Online therapy |
| `07-client-proof.html` | Client experiences |
| `08-final-cta.html` | "If something here felt familiar" |
| `09-faq.html` | Homepage FAQ |

## v8.5 design pass (frontend-design)

- One spacing rhythm: label to title 12px (pill 16px), title to text 24px, header to content 48px, one card padding token.
- Labels are sentence case with the brand diamond marker (v8.8), not all caps. Middle-dot phrases rewritten.
- Both carousels start flush with their heading; the next card peeks in on the right.
- Signature "two voices" panels now shared by the conversation section and client experiences.

## What changed, by section

Applies to every section: no block sets its own fonts anymore. Headings use your Site Styles heading font and sizes. Body text uses your Site Styles paragraph font. Colors and spacing come from the global CSS.

**1. Hero**
- The big headline is now the H1. "Couples therapy in Cambridge, Massachusetts" sits inside it as the small label.
- Kept the "AtReef Therapy, PLLC" pill with the verified badge, now on the refined global pill style.
- Kept the colored calendar icon in the button chip.

**2. Conversation**
- The eyebrow uses the global pill label.
- The title and lead follow Site Styles.
- Colors use tokens.

**3. Services**
- Rebuilt on global cards, grid, tiles, and labels.
- Titles are in sentence case.
- Stars are readable on cream.
- Proof text is 14px.
- The button now says "Book a free consultation", and buttons no longer overflow on tablets.

**4. About**
- Removed the forced Karla font and the 18ch title cap.
- The credentials card is the global dark card.

**5. Approach**
- Removed the forced Karla font and the hardcoded colors.
- Labels and titles use global classes.
- The carousel script is unchanged.

**6. Telehealth**
- Removed the forced Karla font and the 12ch/16ch title caps.
- The wide card no longer leaves an empty right half.
- The button's hidden label now matches its visible text.

**7. Client experiences**
- Quotes are 16px (they were 12.5px).
- Titles are in sentence case.
- Stars are readable.
- On phones, a swipe that starts on a card now scrolls the page.
- Added previous/next buttons so mouse users can reach the third card.

**8. Final CTA**
- Removed the 18ch title cap.
- Standard button label, with the colored calendar in the chip.
- The copy no longer repeats the button.
- The link announces that it opens a new tab.

**9. FAQ**
- Fixed a broken font-size rule.
- The group titles are readable labels instead of 14px script.
- "Frequently asked questions" is in sentence case.

## Hero gap on mobile (editor fix, not code)

The gap comes from Fluid Engine: on mobile the Code Block keeps its tall desktop height, so empty rows sit between the text and the photo.

1. Open the page in **Edit** and switch to the **mobile view** (phone icon).
2. Click the hero Code Block and drag its bottom handle up until it just clears the "Read how the work is done first" link.
3. Drag the photo block up so its top edge touches the Code Block's bottom edge.
4. If a gap remains, remove any empty Fluid Engine row between them (drag the photo up one row at a time).
5. Save, and check on a real phone.

## Decisions left to you

- Every light-section title is now near-black. For teal titles everywhere, change one line in the CSS: `--ar-heading:var(--ar-teal);`
- Heading sizes now follow Site Styles (H2 is 32px on desktop). To enlarge them, raise Heading 2 in Site Styles.
- The final CTA links straight to the booking portal, while the hero links to `/consultation`. Choose one destination for both.
- Testimonials: confirm consent, and that none came from current clients (ACA C.3.b).
