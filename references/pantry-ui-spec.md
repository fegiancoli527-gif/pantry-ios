# Pantry — UI Design Specification
### Visual Source of Truth for SwiftUI Implementation

---

## PART 0 — PREFLIGHT: Visual Philosophy, Design System Rationale, and Why This Is Not Generic

---

### 0.1 Visual Philosophy

Pantry is a tool first. It earns trust the way a good kitchen knife earns trust: it does its job, it feels right in the hand, and it doesn't ask for applause. The visual language reflects this. Nothing is decorative unless it is also functional. Nothing is animated unless the animation communicates something.

The aesthetic reference is not "food startup app." It is closer to a well-designed hardcover cookbook — Ottolenghi, Samin Nosrat, Nigel Slater — where warmth and appetite come from restraint, materiality, and editorial confidence. Cream pages, ink-dark type, one color that breathes.

The UI is warm, not cute. Premium, not expensive-looking. Spacious, not empty.

Every decision should pass this test: **would a 35-year-old home cook who shops at a good deli and owns a Dutch oven think this app was designed for them?**

---

### 0.2 Why This Avoids Generic AI-App Aesthetics

Generic AI food apps commit three sins:
1. **The purple-gradient problem**: AI brand colors (violet, indigo, cyan) colonize the palette and signal "tech product" instead of "food."
2. **The dashboard problem**: Stats, streaks, badges, and rings treat cooking as a productivity system rather than a daily pleasure.
3. **The launch-screen problem**: Beautiful hero illustrations and bold mission statements that evaporate the moment you get into the app's actual content.

Pantry avoids all three by making the following deliberate choices:
- **No blue, violet, or gradient primaries.** The accent is a cooked, muted orange — closer to a cast-iron pan than a SaaS logo.
- **No gamification.** No streaks. No XP. No onboarding confetti.
- **Content-led screens.** The app looks good because the food looks good and the type is well-set, not because backgrounds have been given expensive treatment.
- **Serif headings used with restraint.** A display serif for titles only. Not for buttons, tabs, or labels.
- **No skeleton loaders with a branded shimmer.** No fake depth. No blurred frosted card stacks.

---

### 0.3 The Signature Element

The one memorable visual choice: **the ingredient chip cluster** on the Home and Ingredient Review screens — a natural, slightly organic arrangement of warm-toned rounded chips that reads like food labels laid on a kitchen counter, not like a filter tag cloud. This gives the app a tactile, physical quality that is completely absent from the template aesthetic.

---

## PART 1 — DESIGN SYSTEM

---

### 1.1 Color Palette

```
Background       #FAF7F2   Warm cream. The page.
Surface          #FFFFFF   Pure white cards on cream ground.
Surface Alt      #F3EFE8   A slightly deeper cream for secondary cards, dividers.
Text Primary     #1A1410   Near-black with warm undertone. All body and label text.
Text Secondary   #7A6E63   Muted warm gray. Captions, metadata, placeholders.
Text Tertiary    #B0A89E   Lightest readable gray. Disabled, secondary hints.
Accent           #E8622A   Pantry Orange. Primary CTA, active states, highlights.
Accent Light     #FDF0EA   Orange tint at 8%. Used for chip backgrounds, tags.
Accent Dark      #C44F1E   Darker orange. Pressed states.
Success          #4A7C59   Muted olive green. "You have this" ingredient states.
Success Light    #EDF4F0   Green tint. Ingredient chip background for available items.
Separator        #E8E2DA   Warm gray. Rules, card borders, dividers.
Overlay          rgba(26, 20, 16, 0.48)   For image overlays on recipe hero cards.
```

No pure blacks. No cool grays. Every neutral has a warm undertone. The palette should feel like a kitchen in morning light.

---

### 1.2 Typography

**Display / Heading Typeface: New York (SF Serif)**
SF New York is available natively in SwiftUI via `.font(.system(.title, design: .serif))`. Use it for screen titles, recipe names, and the app wordmark. It is elegant without being precious, and it pairs effortlessly with SF Pro.

**Body / UI Typeface: SF Pro (system default)**
Clean, legible, and instantly native-feeling on iPhone. Use SF Pro Text for body copy, labels, and interface elements. No custom body font needed — fighting the system font on iOS creates friction and hurts legibility.

**Type Scale (all values in points, dynamic type supported):**

```
Display          SF New York   34pt   Weight: Semibold   Tracking: -0.5   Screen titles, hero recipe name
Title 1          SF New York   28pt   Weight: Semibold   Tracking: -0.3   Section headers (in-app, top of card)
Title 2          SF Pro        22pt   Weight: Semibold   Tracking: -0.2   Secondary screen titles
Headline         SF Pro        17pt   Weight: Semibold   Tracking: 0      Card titles, prominent labels
Body             SF Pro Text   16pt   Weight: Regular    Tracking: 0      Primary body copy, instructions
Body Small       SF Pro Text   14pt   Weight: Regular    Tracking: 0      Secondary content, descriptions
Label            SF Pro Text   13pt   Weight: Medium     Tracking: 0.1    UI labels, chips, tags
Caption          SF Pro Text   12pt   Weight: Regular    Tracking: 0.2    Metadata, timestamps, footnotes
Micro            SF Pro Text   11pt   Weight: Medium     Tracking: 0.3    Badge text, superscripts
```

**Rules:**
- Never use New York for buttons, labels, tabs, or form fields.
- Never set body text smaller than 14pt.
- Line height: 1.4× for body, 1.2× for display/title.

---

### 1.3 Spacing System

Base unit: **4pt**. All spacing is a multiple of 4.

```
XS     4pt    Inline gaps, tight element spacing (icon + label gap)
S      8pt    Chip internal padding (vertical), small card gaps
M      12pt   Chip internal padding (horizontal), row spacing
L      16pt   Standard horizontal screen margin, card padding (vertical)
XL     20pt   Card padding (horizontal), between-section gap
2XL    24pt   Large section gap, top of content below nav
3XL    32pt   Between major screen sections
4XL    48pt   Tall spacers, empty state padding
```

**Screen Margins:** 20pt left and right, consistently. Never let content bleed edge-to-edge except for full-bleed hero images.

**Safe Area:** All interactive elements must respect `safeAreaInsets`. Bottom tab bar lifts from the safe area floor.

**Touch Targets:** Minimum 44×44pt for all interactive elements, per Apple HIG.

---

### 1.4 Corner Radius

```
XS     6pt    Small chips, tags, micro-badges
S      10pt   Input fields, small buttons
M      14pt   Recipe cards (small), filter chips
L      18pt   Hero cards, primary buttons, large recipe cards
XL     24pt   Bottom sheets, modal cards
Full   9999pt Pill-shaped elements (some CTAs, search bar)
```

Cards should feel rounded and friendly, not squared-off. The rounded quality is not "cute" — it signals approachability and warmth, which fits the pantry/home-cooking context perfectly.

---

### 1.5 Shadows

Pantry uses shadows **sparingly**. Only cards that float above the background use shadow. Dividers and borders do most of the separation work.

```
Card Shadow        color: #1A1410 at 6% opacity, blur: 12pt, y-offset: 4pt, x-offset: 0
Floating Shadow    color: #1A1410 at 10% opacity, blur: 20pt, y-offset: 8pt, x-offset: 0
Tab Bar Shadow     color: #1A1410 at 8% opacity, blur: 8pt, y-offset: -2pt, x-offset: 0
No elevation:      Surface Alt sections, inline chips, separators
```

---

### 1.6 Icon Style

Use **SF Symbols** exclusively. This keeps the app feeling native and consistent with iOS conventions.

```
Weight:            Regular (for nav and tab icons), Medium (for action buttons)
Scale:             Medium
Active states:     Filled variant at Accent (#E8622A)
Inactive states:   Outline variant at Text Tertiary (#B0A89E)
Never:             Custom icon fonts, Lottie animations for core navigation
```

Occasionally a filled symbol at Accent on a Surface card creates an effective visual anchor (e.g., a fork.knife symbol on the Home screen header). Use this for one or two moments per screen maximum.

---

### 1.7 Button System

**Primary Button**
- Background: Accent (#E8622A)
- Text: White, SF Pro Semibold 17pt
- Corner radius: 14pt (full-width) or 18pt (content-width)
- Padding: 16pt vertical, 24pt horizontal
- Width: Full-width (screen margin to screen margin) for primary flow actions
- Pressed state: Accent Dark (#C44F1E), scale 0.97
- Disabled state: Text Tertiary (#B0A89E) background, white text at 50%

**Secondary Button**
- Background: Surface Alt (#F3EFE8)
- Text: Text Primary (#1A1410), SF Pro Semibold 16pt
- Border: 1pt Separator (#E8E2DA)
- Corner radius: 14pt
- Pressed state: Separator (#E8E2DA) background
- Use for: "Skip", "Cancel", non-primary path actions

**Text Button / Link**
- No background
- Text: Accent (#E8622A), SF Pro Medium 15pt
- Use for: "See all", "Sign in instead", inline links

**Destructive Button**
- Background: Clear
- Text: #D93025 (standard iOS destructive red), SF Pro Medium 16pt
- Use only in confirmation contexts

**Icon Button**
- 40×40pt hit target, 24×24pt icon
- Background: Surface (#FFFFFF) with Card Shadow, corner radius: Full
- Use for: camera icon on Scan, back navigation supplemental actions

---

### 1.8 Card System

**Hero Card (Full-width)**
- Width: Screen width minus 40pt (20pt margin each side)
- Corner radius: 18pt
- Background: Recipe image with Overlay gradient (bottom 60%)
- Title text: White, Display or Title 1, SF New York
- Metadata: White at 80%, Caption, SF Pro
- Shadow: Card Shadow

**Recipe Card (Half-width grid)**
- Width: (Screen width - 52pt) / 2 = approx 167pt on iPhone 15 Pro
- Corner radius: 14pt
- Image: Top ~56% of card height, corner radius applied to card (clip)
- Title: Headline, Text Primary, 2 lines max
- Metadata row: Caption, Text Secondary
- Background: Surface (#FFFFFF)
- Shadow: Card Shadow

**Ingredient Chip (in cluster)**
- Height: 36pt
- Padding: 8pt vertical, 12pt horizontal
- Corner radius: 10pt
- Background: Available → Success Light (#EDF4F0) / Unavailable → Surface Alt (#F3EFE8)
- Text: Available → Success (#4A7C59) / Unavailable → Text Secondary
- Icon: Leading checkmark.circle.fill (available) or xmark.circle (unavailable), 14pt

**Surface Card (for stats, grocery, profile sections)**
- Background: Surface (#FFFFFF)
- Corner radius: 14pt
- Padding: 16pt all sides
- Border: 1pt Separator (#E8E2DA)
- No shadow (it sits on cream, not floating)

---

## PART 2 — SCREEN-BY-SCREEN DESIGN SPEC

---

### Screen 01 — Welcome Screen

**Purpose:** First impression. Establish the brand, communicate the value prop in one breath, move the user forward immediately.

**Layout (top to bottom):**

1. **Status bar area** — Cream background, dark content.

2. **Logo lockup** — Centered, approx 140pt from top.
   - Wordmark: "Pantry" in SF New York Semibold, 34pt, Text Primary (#1A1410).
   - Submark: A minimal SF Symbol — `cabinet.fill` or `fork.knife` — 28pt, Accent color, sitting above the wordmark with 8pt gap.
   - The logo is not inside a container or card. It sits directly on the cream background.

3. **Hero illustration zone** — A high-quality photograph of a beautifully lit home kitchen counter: rustic bowl of vegetables, olive oil bottle, a linen cloth. The image occupies roughly 42% of screen height, edge-to-edge width, with corner radius 0 (truly full bleed). It begins roughly 180pt from top. No gradient overlay — the image carries its own warmth.

4. **Value headline** — Below the image, 24pt gap.
   - "Cook what you have." — SF New York Semibold, 28pt, Text Primary, centered.
   - Subtext: "Scan your fridge and pantry. Get meals you can actually make tonight." — SF Pro Text Regular, 16pt, Text Secondary, centered, max 2 lines, 20pt side margins.

5. **Primary CTA** — "Get started" — Primary Button, full-width, 20pt side margins, 32pt below subtext.

6. **Sign-in link** — "Already have an account? Sign in" — Text Button, centered, 16pt below CTA. "Sign in" in Accent color, rest in Text Secondary.

7. **Legal footnote** — "By continuing, you agree to our Terms and Privacy Policy." — Caption, Text Tertiary, centered, 16pt above safe area bottom.

**Tone:** Confident, uncluttered. A first page of a good cookbook. No animation except a subtle fade-in on load (0.3s ease-out).

**Interaction:** CTA navigates to Onboarding flow. Sign-in navigates to auth screen.

---

### Screen 02 — Goals Onboarding

**Purpose:** Understand why the user is here. Personalizes recipe results downstream.

**Layout (top to bottom):**

1. **Progress indicator** — Top, centered, 60pt from status bar. Five small pill-shaped segments, 32pt wide × 4pt tall, 6pt gap. First segment in Accent, remainder in Separator. Not labeled.

2. **Back button** — Leading chevron, 20pt from left, vertically centered with progress indicator.

3. **Heading block** — 32pt below progress bar.
   - "What are you trying to do?" — SF New York Semibold, 28pt, Text Primary.
   - "We'll focus recipes on what matters to you." — Body Small, Text Secondary, 8pt below heading.

4. **Option cards** — 24pt below heading. Each option is a Surface Card (full-width minus margins) with 12pt gap between cards.
   - Card anatomy: 60pt height. Leading icon (SF Symbol, 22pt, Accent) with 16pt left padding. Text: Headline label + Caption sub-label. Trailing radio circle (selected: Accent filled circle, unselected: Separator outlined circle). Corner radius 14pt.
   - Options:
     1. `leaf` icon — **Use what I have** / "Make the most of my fridge and pantry"
     2. `cart` icon — **Save money on groceries** / "Reduce food waste and spend less"
     3. `figure.run` icon — **Eat healthier** / "Focus on balanced, nutritious meals"
     4. `clock` icon — **Cook faster** / "Quick meals with less prep"
     5. `sparkles` icon — **Try new things** / "Expand my cooking and discover recipes"

5. **CTA** — "Next" — Primary Button, fixed at bottom, 32pt above safe area. Disabled until selection made.

**Interaction:** Single-select. Tapping a card immediately fills the radio. Card gets a 1pt Accent border when selected. Subtle spring scale animation on select (0.96 → 1.0).

---

### Screen 03 — Diet Onboarding

**Purpose:** Dietary filtering. Sets persistent recipe filters.

**Layout:**
1. Progress indicator — Step 2 of 5 filled.
2. Heading: "Any dietary needs?" / "We'll filter recipes to match." — same block style.
3. **Multi-select chip grid** — 24pt below heading. Chips arranged in a left-aligned, line-wrapping flow. Each chip: 36pt height, 14pt corner radius, 12pt H padding, 8pt gap. Content-width.
   - Unselected: Surface Alt background, Text Secondary label.
   - Selected: Accent Light background, Accent text, leading checkmark.circle.fill icon.
   - Options: None · Vegetarian · Vegan · Gluten-free · Dairy-free · Nut-free · Halal · Kosher · Low-carb · Keto · Paleo
4. "None of these apply" — Text Button, centered, 16pt below chips.
5. CTA — "Next" — enabled from the start (dietary needs are optional).

---

### Screen 04 — Cooking Confidence Onboarding

**Purpose:** Calibrates recipe complexity recommendations.

**Layout:**
1. Progress indicator — Step 3.
2. Heading: "How confident are you in the kitchen?" / "We'll suggest recipes that match your skill."
3. **Segmented vertical option stack** — Three tall option cards, each 80pt, full-width minus margins, 8pt gap.
   - Option A: `person` icon — **Beginner** / "I can follow a basic recipe"
   - Option B: `frying.pan` icon — **Comfortable** / "I cook regularly and improvise sometimes"
   - Option C: `flame` icon — **Experienced** / "I'm confident and enjoy complex cooking"
   - Each uses the same card treatment as Goals onboarding (radio indicator).
4. CTA — "Next" — Primary Button.

---

### Screen 05 — Household Size Onboarding

**Purpose:** Sets default serving size for recipes.

**Layout:**
1. Progress indicator — Step 4.
2. Heading: "Who are you cooking for?" / "We'll size up portions to match."
3. **Large number stepper** — Centered in screen, 48pt below heading.
   - Minus button (circle, 48×48pt) — Number display (SF New York Semibold, 52pt, Text Primary) — Plus button.
   - Range: 1–8. Below 1: minus disabled. Above 8: "8+ people" text appears below.
   - Sub-label: "1 person" / "2 people" / "3 people" etc., in Body, Text Secondary.
4. **Context chips** — Below stepper, 24pt gap. Small informational chips in row: "Just me" (auto-select 1), "Couple" (auto-select 2), "Family" (auto-select 4). These are secondary shortcuts, not primary UI.
5. CTA — "Next" — Primary Button.

**Interaction:** Stepper increments with spring haptic. Number updates with a tiny crossfade (0.15s).

---

### Screen 06 — Avoid / Dislikes Onboarding

**Purpose:** Exclude ingredients the user dislikes or can't use. Last onboarding step.

**Layout:**
1. Progress indicator — Step 5 (all filled).
2. Heading: "Anything you'd rather avoid?" / "Not dietary restrictions — just personal dislikes."
3. **Search field** — Surface card, pill-shape, 20pt margins. Placeholder: "e.g. blue cheese, anchovies..." `magnifyingglass` leading icon. As user types, inline suggestions appear below in a card drop-down (max 5 results, Surface background, 14pt corner radius, shadow).
4. **Selected avoidances chip cluster** — Below search field, left-aligned wrapping flow. Each chip: Surface Alt background + leading `xmark.circle.fill` in Text Secondary. Tap xmark to remove.
5. **Common suggestions** — "Common picks:" label in Label style, Text Secondary. Below it, a wrapping row of suggestion chips (tap to add): Cilantro · Blue cheese · Mushrooms · Olives · Liver · Fish sauce.
6. CTA — "Finish setup" — Primary Button. This replaces all prior "Next" buttons with a slightly warmer copy.

---

### Screen 07 — Create Account / Sign In

**Purpose:** Gate the app behind account creation. Appears after onboarding.

**Layout:**
1. Back button — top leading.
2. Heading — 60pt from top: "Create your account" (or "Welcome back" for sign-in). SF New York Semibold 28pt.
3. Sub: "Save your pantry and recipes across devices." — Body Small, Text Secondary.
4. **Form fields** — 32pt below heading. Each field: 56pt height, full-width minus margins, Surface background, 1pt Separator border, corner radius 12pt, 16pt left padding.
   - Email address (keyboard type: email)
   - Password (secure entry, trailing `eye` toggle button)
   - Confirm password (create only)
5. **CTA** — "Create account" / "Sign in" — Primary Button, 24pt below last field.
6. **Divider** — "or" in Text Tertiary, horizontal lines to each side.
7. **Apple Sign In** — SF Pro Semibold 16pt, white text, black background (#000000), leading apple logo. Full-width, 56pt height, corner radius 14pt. This must be offered on iOS per App Store guidelines.
8. **Toggle** — "Already have an account? Sign in" / "Don't have one? Create account" — Text Button, centered.

**Error states:** Field border turns to #D93025 (1.5pt), inline error message appears in Caption red below the field. Shake animation on submit failure.

---

### Screen 08 — Home Feed

**Purpose:** The daily surface. Surfaces what to cook today based on what the user has. Most-used screen in the app.

**Layout:**

1. **Navigation bar** — Inline style (not large title). "Good morning" or "Good evening" in Caption, Text Tertiary. "Pantry" in SF New York Semibold 20pt, Text Primary. Trailing: profile avatar (32×32pt, circular, Surface with border) and notification bell (SF Symbol, Text Secondary).

2. **Pantry status bar** — Directly below nav, 20pt margins, Surface card, 14pt corner radius, 12pt padding all sides.
   - Leading: `cabinet.fill` SF Symbol, 18pt, Accent.
   - Text: "47 ingredients in your pantry" in Headline weight. Caption below: "Last scanned 2 days ago."
   - Trailing: "Scan now" — a small secondary button-style chip (Accent Light background, Accent text, 10pt corner radius, Label size).
   - This bar is the persistent heartbeat of the app. It grounds the user in their pantry state.

3. **Hero recipe section** — "Make tonight" heading. Title 1, SF New York, 20pt margins. 8pt below, a horizontal scroll rail containing 2–3 Hero Cards (full-width × 220pt height, image + dark overlay + title + "Ready in 25 min" metadata chip). Cards have 20pt left margin on first, 12pt gap between, 20pt padding after last.
   - Populated: Recipe images with warm overhead-shot photography aesthetic. Recipe name in white Display text. Chip: white background at 20% opacity, Micro text "25 min · 4 ingredients you have."
   - Empty state: A single dashed-border card (Separator color) with centered `fork.knife` SF Symbol (Accent), "Scan your pantry to see tonight's ideas." Body Small, Text Secondary.

4. **"You can make these" section** — 32pt below hero rail. Heading: "You can make these" in Title 2. Trailing: "See all" Text Button.
   - A 2-column grid of Recipe Cards. Show 4 cards (2 rows).
   - Each Recipe Card: image top, title middle, metadata row bottom (time + match percentage chip: "7/8 ingredients").
   - The match chip uses Accent Light background, Accent text: "7 of 8 ingredients."

5. **"Almost there" section** — "One or two away" heading. Horizontal scroll row of Recipe Cards, slightly smaller (same card, horizontal scroll). These are recipes where user is 1–2 ingredients short. Cards show a small "Need: butter, cream" line in Caption, Success Light chip with the missing count.

6. **"By cuisine" section** — Filter chip horizontal scroll. Surface Alt chips: Italian · Mexican · Asian · Mediterranean · American. Tapping filters the grid below (which animates with a crossfade).

**Interaction:** Pull to refresh. On pull, a subtle `arrow.clockwise` indicator appears at top, cream background, Accent. The hero cards support horizontal swipe. The grid supports infinite scroll (pagination at 12 cards per load). Tapping any card → Recipe Detail (with shared element transition: card expands to full screen).

**Empty state (new user, no pantry):** Full-screen centered state. `cabinet` SF Symbol, 48pt, Accent. "Your pantry is empty." Title 2, SF New York. "Scan your kitchen to get started." Body, Text Secondary. "Scan now" Primary Button below.

---

### Screen 09 — Scan Screen

**Purpose:** Core interaction. The camera-based pantry scanning experience.

**This is a full-screen camera experience. All chrome is minimal and dark.**

**Layout:**

1. **Camera viewfinder** — Full screen. Live camera preview.

2. **Top overlay bar** — 20pt from status bar. Semi-transparent dark pill (black at 60%, blur backdrop), centered. Content: `xmark` leading (dismiss), "Scan your pantry" in Headline white centered, `questionmark.circle` trailing.

3. **Scan frame guide** — A rounded-rect outline (Separator white at 40%), 300×300pt, centered in viewfinder. Inside: animated corner brackets that pulse once on load (scale 1.0 → 1.04 → 1.0, 0.6s ease). Below frame: "Point at any food, ingredient, or label" in Caption white, centered.

4. **Capture button** — Bottom center, 56pt above safe area. A 72×72pt circle. Outer ring: white at 30%, 3pt stroke. Inner: Accent-filled circle, 56pt diameter. Tap: triggers capture + haptic impact (medium weight). No shutter sound by default — follows iOS mute switch.

5. **Photo library button** — Leading to capture button, 48×48pt. `photo.on.rectangle` SF Symbol, white. Accesses camera roll for pantry photos already taken.

6. **Manual add button** — Trailing to capture button. `plus.circle` SF Symbol, white, 48×48pt. Tapping slides up a small bottom sheet to type an ingredient name manually.

7. **Running ingredient tray** — A horizontal strip at the bottom, above capture button. Shows ingredient chips that have been scanned in this session. Chips: white background, Text Primary label. Scrollable horizontally if more than fits. When no items: hidden.

**Interaction:** Each captured photo is analyzed (ML or API call). A brief overlay shows a pulsing Accent-colored border on recognized items in the frame. Each recognized item gets added to the running tray with a slide-in animation from the right. Multiple photos can be taken in sequence. CTA at bottom right (if items are in tray): "Review (12)" — Primary Button, compact, that navigates to Ingredient Review.

**Error state (camera permission denied):** Full-screen replacement. `camera.slash` SF Symbol, Accent. "Camera access needed." Body. "Allow camera access in Settings." Text Button with `arrow.up.right.square` icon.

---

### Screen 10 — Ingredient Review Screen

**Purpose:** Review and edit what was detected before confirming the pantry update.

**Layout:**

1. **Navigation bar** — "Review ingredients" in Title 2. Trailing: "Done" Text Button in Accent (or disabled until user confirms).

2. **Summary line** — Below nav, 20pt margins. "Found 14 ingredients from 3 photos." — Body, Text Secondary.

3. **Confirmed section** — Surface card, full-width minus margins, 14pt corner radius, 16pt padding.
   - Section header inside card: "Added to pantry" in Label, Text Secondary + `checkmark.circle.fill` icon in Success color. Count badge in Success Light.
   - Below: wrapping chip cluster of identified ingredients. Chips: Success Light background, Success text, `checkmark` leading icon, 10pt corner radius.
   - Each chip is tappable. Tap → chip shifts to "Uncertain" section (with a gentle slide animation).

4. **Uncertain / Review section** — Same card treatment. "Not sure about these" header, Text Secondary, `questionmark.circle` icon.
   - Chips: Surface Alt background, Text Secondary, `questionmark` leading icon.
   - Tap chip → presents inline popover or sheet: "Keep this ingredient?" with Keep / Remove options.
   
5. **Add manually** — At bottom of chips, a `plus` chip: Accent Light background, Accent text, `plus` icon, "Add ingredient." Tapping → inline text field appears at end of cluster.

6. **Pantry snapshot** — Below both sections, 32pt gap. Surface Alt background, full-width, 14pt corner radius. "Your pantry will have:" in Label, Text Secondary. Below: count breakdown — "47 existing + 12 new = 59 total." Headline weight for 59.

7. **CTA** — "Update my pantry" — Primary Button, fixed bottom. 20pt margins, above safe area.

**Interaction:** Confirming navigates back to Home with a toast notification sliding in from top: "Pantry updated. 12 ingredients added." Accent background, white text, 14pt corner radius.

---

### Screen 11 — Recipe Results Screen

**Purpose:** Full list of recipe matches. Accessed from "See all" on Home, or after pantry update.

**Layout:**

1. **Navigation bar** — "Recipes" title. Trailing: sort icon (`arrow.up.arrow.down`).

2. **Match filter row** — Horizontal scroll chip row, 20pt top margin. Pills: "All" · "Full match" · "1 away" · "2 away" · "30 min or less" · "Vegetarian." Each chip: 14pt corner radius, Label text. Active chip: Accent background, white text. Inactive: Surface Alt, Text Secondary.

3. **Results count** — "83 recipes" in Caption, Text Tertiary, 20pt left margin, 8pt below filter row.

4. **Recipe grid** — 2-column grid, 20pt side margins, 12pt gap. Recipe Cards with match chip on each.

5. **Sort sheet (on sort icon tap)** — Modal bottom sheet. Options: Best match · Fastest · Fewest missing ingredients · Recently added to Pantry.

**Empty state:** If no full matches: large centered block. `fork.knife.circle` SF Symbol, Accent, 48pt. "No exact matches yet." Title 2, SF New York. "Try the 'Almost there' recipes — you're only missing 1–2 ingredients." Body, Text Secondary. "Shop for missing items" — Secondary Button below. "Adjust filters" — Text Button.

---

### Screen 12 — Recipe Detail Screen

**Purpose:** The full recipe experience. Must be satisfying as a standalone cooking screen.

**Layout:**

1. **Hero image** — Full-bleed, edge-to-edge, 280pt tall. Back button floats in top-left (Icon Button, white). Save button floats in top-right (`bookmark` SF Symbol, Icon Button, white → filled on save).

2. **Content card** — Slides up over the image, 24pt corner radius top corners. Background: Background (#FAF7F2). This creates the "recipe card emerging from food photo" metaphor — the content lifts cleanly off the image.

3. **Recipe header (inside content card):**
   - Recipe name: Display, SF New York Semibold, Text Primary. Max 2 lines.
   - Cuisine tag: Caption chip, Surface Alt, Text Secondary, 6pt corner radius.
   - Match status: "You have all 8 ingredients" in a Success-colored row (icon + text).
   - Or: "You have 6 of 8 · Need: butter, cream" — Accent row.

4. **Stats row** — 4 stat cells in a horizontal row. Each: centered icon (SF Symbol, 18pt, Text Secondary) + value (Headline) + label (Caption, Text Tertiary).
   - Prep time / Cook time / Servings / Difficulty

5. **Ingredient list** — Section header: "Ingredients" in Title 2. Below: list rows.
   - Each row: Leading `checkmark.circle.fill` (Success if user has it) or `circle` (empty, if not in pantry). Ingredient name. Quantity/unit on trailing side in Caption, Text Secondary.
   - "In your pantry" items get Success Light row tint.
   - "Missing" items get a shopping bag icon on trailing side: tappable to add to Grocery list. Tap: icon fills in Accent, brief haptic.

6. **Instructions** — Section header: "Instructions" in Title 2. Below: numbered steps. Each step: step number in a 28×28pt Accent Light circle (Accent text, SF Pro Semibold), step text in Body, Text Primary. 16pt gap between steps.

7. **Tips section (optional)** — Faint Surface Alt card: "Chef's note" or "Make it yours" with 1–2 tips.

8. **Similar recipes** — "You might also like" horizontal scroll of Recipe Cards.

9. **Bottom CTA bar** — Fixed. Surface background. "Start cooking" Primary Button, full-width minus margins. Tapping activates a step-by-step cooking mode (future scope, but button exists).

**Scroll behavior:** Hero image parallaxes at 50% rate as user scrolls. Content card follows normally.

---

### Screen 13 — Saved Screen

**Purpose:** Bookmarked recipes. Personal recipe library.

**Layout:**

1. **Large title** — "Saved" — SF New York Semibold 34pt, 20pt side margin. Below: "32 recipes" in Caption, Text Tertiary.

2. **Collection filter row** — Horizontal scroll chips: "All" · "Favorites" · "Tried it" · "Want to try." Accent-style active chip.

3. **Sort / filter bar** — Trailing sort icon. Inline: small "Filter" chip (icon + text) that opens a filter sheet.

4. **Recipe grid** — Same 2-column Recipe Card grid as Results. Cards show a saved indicator (filled `bookmark` chip in top-right corner of card image in Accent).

**Empty state:**
- `bookmark.slash` SF Symbol, Accent, 40pt.
- "Nothing saved yet." Title 2, SF New York.
- "Tap the bookmark on any recipe to save it here." Body, Text Secondary.
- "Browse recipes" — Primary Button.

**Populated, "Tried it" filter:** Cards gain a `checkmark.seal.fill` badge in Success color on the card corner.

---

### Screen 14 — Grocery Screen

**Purpose:** Shopping list of missing ingredients needed for saved/planned recipes.

**Layout:**

1. **Large title** — "Grocery" — SF New York Semibold 34pt.

2. **Store banner** — If user has connected a store: Surface card showing store logo + "Delivery available." Otherwise hidden.

3. **Recipe source chips** — "From which recipes?" — Horizontal scroll chips showing saved recipes that contributed items. Each chip: tiny recipe image thumbnail (18×18pt, circular) + recipe name, 14pt corner radius. Tapping highlights that recipe's items in the list.

4. **Grocery list** — Grouped by category (Produce · Dairy · Meat · Pantry staples · Other). Section headers: Label, Text Secondary, with Separator below.
   - Each row: 52pt height. Leading unchecked/checked circle (44×44pt hit target). Item name in Headline (unchecked) or Body with strikethrough + Text Tertiary (checked). Quantity in Caption trailing.
   - Checked items move to the bottom of their section with a brief animation, faded to Text Tertiary.

5. **Floating "Add item" button** — Bottom right, 80×44pt (text label "Add item" + `plus` icon). Accent background, white text, corner radius 22pt. Full pill. Opens a text field bottom sheet.

6. **Share button** — Top trailing. Exports list via iOS share sheet.

**Empty state:**
- `cart.badge.plus` SF Symbol, Accent.
- "Your grocery list is empty." Title 2, SF New York.
- "Missing an ingredient for a recipe? Tap the cart icon and it'll appear here." Body, Text Secondary.

---

### Screen 15 — Profile Screen

**Purpose:** Account, preferences, and pantry management. Low-traffic but important.

**Layout:**

1. **Profile header** — Full-width, 20pt margins. Circular avatar, 72pt diameter. Name in Title 2. Sub: email address in Caption, Text Secondary. Trailing: "Edit" Text Button.

2. **Pantry section** — Surface card.
   - Title: "Your pantry" in Headline.
   - Stats row: 3 stat chips side by side — "59 ingredients" · "14 proteins" · "Updated 2 days ago."
   - "Manage pantry" → chevron row that opens a full pantry inventory list.

3. **Preferences section** — Surface card, 24pt below.
   - Rows with chevron trailing: "Dietary preferences" · "Cuisine preferences" · "Cooking skill" · "Household size."
   - Each row: 52pt height, SF Symbol leading icon (Accent), label in Body.

4. **Notifications row** — Toggle row: "Meal suggestions" toggle.

5. **Account section** — Surface card.
   - "Change email" · "Change password" · "Connected accounts."

6. **Danger zone** — Text-only section at bottom. "Sign out" in Text Secondary. "Delete account" in destructive red (#D93025). 48pt spacing before these.

---

## PART 3 — REUSABLE COMPONENT INVENTORY

---

### Primary Button
Full-width unless specified. Accent fill, white SF Pro Semibold 17pt text. 16pt vertical, 24pt horizontal padding. 14pt corner radius. Pressed: scale 0.97 + Accent Dark fill. Disabled: Surface Alt fill + Text Tertiary text.

### Secondary Button
Full-width or content-width. Surface Alt fill, Text Primary SF Pro Semibold 16pt text. 1pt Separator border. 14pt corner radius. Pressed: Separator fill.

### Tab Bar
5 items: Home (`house.fill`) · Scan (`camera.fill`) · Saved (`bookmark.fill`) · Grocery (`cart.fill`) · Profile (`person.fill`). Height: 83pt (including safe area). Background: Surface white, top 1pt Separator border + Tab Bar Shadow. Active icon: Accent, filled symbol. Inactive: Text Tertiary, outline symbol. Label: Caption text, matches icon color. Scan tab (center): slightly elevated — Icon Button treatment with Accent background, white icon, 28×28pt icon in a 52×52pt Accent circle. Slight shadow. This makes Scan feel like the primary action.

### Hero Card
Full-width minus 40pt margins. 220pt height. Image with Overlay (bottom 60% dark gradient). Title in white Display SF New York Semibold at bottom-left with 16pt padding. Metadata chip at bottom-left below title: white 20% background, Micro text. Corner radius 18pt. Card Shadow.

### Section Header
Two elements on one row: left-aligned Title 2 (SF New York Semibold, Text Primary), right-aligned "See all" Text Button (Accent). 20pt left margin, 20pt right margin. 8pt below leading to first content item.

### Filter Chips
36pt height. 14pt corner radius. 12pt horizontal padding. 8pt gap. Active: Accent fill, white Label text. Inactive: Surface Alt fill, Text Secondary Label text. Spring animation on toggle (scale 0.95 → 1.0).

### Recipe Card (small grid card)
Width: (screenWidth - 52) / 2. Corner radius 14pt. Surface fill. Card Shadow. Top: 56% height image (clipped to card corners). Middle: Recipe name in Headline, Text Primary, 2 lines max, 12pt horizontal padding. Bottom: metadata row — clock icon + time + match chip. 12pt horizontal padding, 12pt bottom padding.

### Ingredient Chip
36pt height. 12pt horizontal + 8pt vertical padding. 10pt corner radius. Available: Success Light fill, Success text, `checkmark` leading icon. Unavailable/neutral: Surface Alt fill, Text Secondary text. Missing: Accent Light fill, Accent text, `cart` leading icon.

### Stat Card
Surface fill, 1pt Separator border, 14pt corner radius. 16pt padding. Icon top (SF Symbol, 22pt, Accent). Value center (Title 2, Text Primary). Label bottom (Caption, Text Secondary). Min-width 80pt, max 4 per row.

### Empty State Block
Full-screen centered vertical stack: SF Symbol at 48pt in Accent (48pt) → 16pt gap → Title 2 SF New York → 8pt gap → Body Text Secondary (2 lines max) → 24pt gap → Primary Button (full width minus 40pt margins). Background: Background (#FAF7F2).

### Profile Header
72×72pt circular avatar with 2pt Separator border. Name in Title 2, Text Primary, 12pt below. Email in Caption, Text Tertiary, 4pt below. Horizontally centered in its section.

---

## PART 4 — ART DIRECTION SUMMARY FOR CLAUDE CODE

---

**For engineering handoff. Read this before writing any SwiftUI.**

Pantry is a premium consumer food app that feels like a well-made cookbook, not a startup product. Everything in the UI should feel calm, warm, and intentional. Here is what that means in practice:

**Color:** The background is always `#FAF7F2` (warm cream), not white and not gray. Cards are `#FFFFFF` white against this cream background, which creates soft contrast without clinical coldness. The only accent color is `#E8622A` (a warm, cooked orange). It appears on primary buttons, active tab icons, active chips, and selected states. It does not appear as gradients. It does not appear as backgrounds on large surfaces.

**Type:** Headings (screen titles, recipe names) use SF New York (system serif, accessed via `Font.system(.title, design: .serif)`). Everything else — buttons, labels, body, captions — uses SF Pro (default system font). Never use New York for buttons or UI chrome.

**Motion:** Keep animation subtle. Use spring animations for selection states (chips, radio buttons, toggles). Use ease-out for screen transitions. Use crossfade (0.2s) for filter/sort changes. No bouncing hero animations, no particle effects, no lottie decorations.

**Spacing:** Screen horizontal margin is always 20pt. Never go tighter. Cards have 16pt internal padding. Items within cards have 12pt gap. Between major sections: 32pt. Touch targets: minimum 44×44pt, always.

**Shadows:** Only use shadows on cards that visibly float above the background. Most content blocks use a 1pt `#E8E2DA` border instead of a shadow. Shadows are `rgba(26,20,16,0.06)`, soft blur (12pt), small y-offset (4pt).

**Corner radius:** Primary buttons and large cards use 14–18pt. Small chips use 10pt. Input fields use 12pt. Pill shapes (search bar, floating action button) use 9999pt (full pill). Never use 8pt or below for anything the user touches.

**Photography:** Recipes use overhead warm-light food photography. No stock-photo-blue lighting. No gradient filters over photos. Overlay on hero cards is `rgba(26,20,16,0.48)` gradient at bottom 60%.

**Tab bar:** Scan is the hero tab. Give it an Accent-colored center button (like Camera apps or Instagram). All other tabs use standard icon/label treatment.

**Language:** UI copy is direct and practical. "Cook what you have." Not "Unlock your kitchen's potential." "Scan your pantry" not "Discover ingredients." "You have 6 of 8 ingredients" not "You're 75% ready!" No exclamation marks in UI states. No AI buzzwords anywhere in visible copy.

**What this is NOT:** Not a wellness app. Not an AI assistant with a chat interface. Not a productivity tracker. Not a grocery store delivery app. It is a recipe-matching utility that is beautiful to use and disappears when you start cooking.
