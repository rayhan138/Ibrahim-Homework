# Design Document: Arabic Homework Exercises

## Overview

This design extends the existing Arabic learning webpage (index.html) by adding three new exercise sections that maintain the established neo-brutalist design system. The implementation focuses on HTML/CSS additions without requiring JavaScript, leveraging the existing `<details>` and `<summary>` elements for interactive reveal functionality.

The three new sections are:
1. Section 8: Connect the Letters (Page 1) - 7 letter connection exercises with teal background
2. Section 9: English to Arabic Translation - Vocabulary sorting exercise with yellow background
3. Section 10: Connect the Letters (Page 2) - 7 letter connection exercises with lime background

All sections will be appended to the existing HTML structure before the closing `</div>` and `</body>` tags, maintaining consistency with the current design patterns.

## Architecture

### Design System Consistency

The implementation follows the existing neo-brutalist design patterns established in the current webpage:

**Visual Language:**
- Bold 4px solid black borders on all card elements
- 8px box shadows (offset: 8px right, 8px down, 0px blur, black color)
- Flat colors with no gradients (teal: #5EEAD4, yellow: #FDE047, lime: #BEF264)
- Zero border-radius (sharp corners)
- High contrast black text on colored backgrounds

**Typography:**
- English text: Space Grotesk font (already loaded via Google Fonts)
- Arabic text: Arial font with explicit RTL direction
- Arabic font size: 3.5rem (desktop), 2.8rem (tablet ≤768px), 2rem (mobile ≤480px)
- Section headings: 2rem font size, uppercase, black background with colored shadows

**Interactive Elements:**
- `<details>` and `<summary>` elements for reveal functionality
- Summary buttons: black background, white text, uppercase, 6px shadow
- Hover effect: translate(4px, 4px) with reduced 2px shadow
- Active effect: translate(6px, 6px) with 0px shadow

### Component Hierarchy

```
Section Container (h2 heading)
└── Exercise Cards (div.card with color class)
    ├── Question Display (div.question-text with emoji)
    ├── Interactive Reveal (details element)
    │   ├── Reveal Button (summary element)
    │   └── Answer Content (div.arabic-text)
    └── Optional Explanation (div.explanation)
```

For the sorting exercise (Section 9):
```
Section Container (h2 heading)
└── Card Container (div.card.bg-yellow)
    ├── Instructions (p.question-text)
    ├── Word Bank Display (div.word-bank)
    ├── Interactive Reveal (details element)
    │   ├── Reveal Button (summary)
    │   └── Sort Container (div.sort-container)
    │       ├── Feminine Column (div.sort-column)
    │       └── Masculine Column (div.sort-column)
```

## Components and Interfaces

### Section 8: Connect the Letters (Page 1)

**Component Structure:**
- Section heading: `<h2>8️⃣ Connect the Letters (Page 1)</h2>`
- 7 individual card components with class `card bg-teal`
- Each card contains:
  - Question text showing separated letters (e.g., "ك + ق + ك")
  - Details/summary reveal mechanism
  - Arabic text answer showing connected letters

**Letter Combinations:**
1. ك + ق + ك → كقك
2. ه + ن + ه → هنه
3. ك + ت + ب → كتب
4. ك + ل + ب → كلب
5. ق + ل + ب → قلب
6. ق + ط + ة → قطة
7. ب + ي + ت → بيت

**CSS Requirements:**
- New color class: `.card.bg-teal { background-color: #5EEAD4; }`
- Reuses existing `.card`, `.question-text`, `.arabic-text`, `details`, and `summary` styles
- No new CSS needed beyond the color class

### Section 9: English to Arabic Translation

**Component Structure:**
- Section heading: `<h2>9️⃣ Translate: English to Arabic</h2>`
- Single card with class `card bg-yellow` (already exists in stylesheet)
- Word bank displaying 8 English vocabulary items
- Two-column sorting layout within details reveal

**Vocabulary Mapping:**
- Feminine words (ending in ة):
  - blackboard → سَبُّورَةٌ
  - table → طَاوِلَةٌ
  - stapler → دَبَّاسَةٌ
  - ruler → مِسْطَرَةٌ
  - bag → حَقِيبَةٌ

- Masculine words (no ة):
  - book → كِتَابٌ
  - pen → قَلَمٌ
  - door → بَابٌ

**Layout Behavior:**
- Desktop/Tablet: Two columns side-by-side using flexbox
- Mobile (≤480px): Columns stack vertically
- Reuses existing `.sort-container`, `.sort-column`, and `.word-tag` styles

### Section 10: Connect the Letters (Page 2)

**Component Structure:**
- Section heading: `<h2>🔟 Connect the Letters (Page 2)</h2>`
- 7 individual card components with class `card bg-lime`
- Identical structure to Section 8 but with different color

**Letter Combinations:**
1. ه + ن + ه → هنه
2. ك + ت + ب → كتب
3. ك + ل + ب → كلب
4. ق + ل + ب → قلب
5. ق + ط + ة → قطة
6. ب + ي + ت → بيت
7. ك + ق + ك → كقك

**CSS Requirements:**
- New color class: `.card.bg-lime { background-color: #BEF264; }`
- Reuses all other existing styles

### Responsive Design Strategy

The existing media queries will automatically apply to the new sections:

**Tablet (≤768px):**
- Arabic text: 3.5rem → 2.8rem
- Card padding: 25px → 20px
- Box shadows: 8px → 6px
- Border widths remain 4px

**Mobile (≤480px):**
- Arabic text: 2.8rem → 2rem
- Card padding: 20px → 15px
- Box shadows: 6px → 4px
- Border widths: 4px → 3px
- Sort columns: flex → stack (min-width: 100%)

No new media queries are required as the existing rules use class-based selectors that will apply to the new sections.

## Data Models

### Exercise Card Data Structure

While this is a static HTML implementation, the conceptual data model for each exercise type is:

**Letter Connection Exercise:**
```typescript
interface LetterConnectionExercise {
  letters: string[];        // Array of individual Arabic letters
  connectedForm: string;    // The combined word
  displaySeparator: string; // " + " for visual separation
}
```

**Translation Sorting Exercise:**
```typescript
interface VocabularyItem {
  english: string;
  arabic: string;
  gender: 'masculine' | 'feminine';
}

interface SortingExercise {
  wordBank: string[];           // English words to translate
  vocabulary: VocabularyItem[]; // Translation mappings
  feminineWords: VocabularyItem[];
  masculineWords: VocabularyItem[];
}
```

### Color Theme Mapping

```typescript
interface SectionTheme {
  sectionNumber: number;
  backgroundColor: string;  // Tailwind-inspired color
  shadowColor?: string;     // For heading shadows (optional)
}

const newSections: SectionTheme[] = [
  { sectionNumber: 8, backgroundColor: '#5EEAD4' }, // teal-300
  { sectionNumber: 9, backgroundColor: '#FDE047' }, // yellow-300 (existing)
  { sectionNumber: 10, backgroundColor: '#BEF264' } // lime-300
];
```

### HTML Structure Pattern

Each section follows this template pattern:

```html
<!-- Section Heading -->
<h2>[Emoji] [Title]</h2>

<!-- Exercise Card(s) -->
<div class="card bg-[color]">
  <div class="question-text">
    <span class="big-emoji">[Emoji]</span>
    [Question Content]
  </div>
  <details>
    <summary>Reveal Answer</summary>
    <div class="arabic-text">[Arabic Answer]</div>
    <!-- Optional explanation -->
  </details>
</div>
```

This pattern ensures consistency across all sections and leverages the existing CSS cascade.


## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system-essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Property 1: Letter Separator Display Pattern

*For any* letter connection exercise card (in sections 8 or 10), the question text should display Arabic letters separated by the pattern " + " (space, plus sign, space).

**Validates: Requirements 1.3, 3.3**

### Property 2: Section Background Color Consistency

*For any* exercise card within a given section, all cards should have the same background color class (bg-teal for section 8, bg-yellow for section 9, bg-lime for section 10).

**Validates: Requirements 1.4, 2.2, 3.4**

### Property 3: Reveal Button Interaction

*For any* details element containing a reveal button, when opened, the element should display its child content (arabic-text div or sort-container) that was previously hidden.

**Validates: Requirements 1.5, 2.5, 3.5**

### Property 4: Arabic Text Styling Consistency

*For any* element with class "arabic-text", the computed styles should include font-size of 3.5rem (on desktop), direction: rtl, and font-family containing Arial.

**Validates: Requirements 1.6, 3.6**

### Property 5: Neo-Brutalist Card Styling

*For any* element with class "card" in the new sections, the computed styles should include border: 4px solid black and box-shadow: 8px 8px 0px black (on desktop viewport).

**Validates: Requirements 4.1, 4.2**

### Property 6: Reveal Button Styling

*For any* summary element (reveal button), the computed styles should include background-color: black, color: white, and text-transform: uppercase.

**Validates: Requirements 4.3**

### Property 7: Reveal Button Hover Effect

*For any* summary element with :hover pseudo-class, the CSS should include transform: translate(4px, 4px) and box-shadow: 2px 2px 0px (with appropriate color).

**Validates: Requirements 4.4**

### Property 8: English Text Font Family

*For any* text element not within the "arabic-text" class, the computed font-family should include "Space Grotesk".

**Validates: Requirements 4.5**

### Property 9: Arabic Text Font Family

*For any* element with class "arabic-text", the computed font-family should include Arial.

**Validates: Requirements 4.6**

### Property 10: Section Heading Styling

*For any* h2 element in the new sections, the computed styles should include background-color: black, color: white, and a box-shadow with colored offset.

**Validates: Requirements 4.7**

### Property 11: Responsive Arabic Text Scaling

*For any* element with class "arabic-text", when the viewport width is ≤768px, the computed font-size should be 2.8rem, and when viewport width is ≤480px, the computed font-size should be 2rem.

**Validates: Requirements 5.1, 5.2**

### Property 12: Responsive Column Stacking

*For any* sort-column element, when the viewport width is ≤480px, the computed min-width should be 100% to force vertical stacking.

**Validates: Requirements 5.3**

### Property 13: Responsive Border and Shadow Scaling

*For any* card element, when the viewport width is ≤768px, the box-shadow should reduce to 6px 6px 0px black, and when viewport width is ≤480px, the border should reduce to 3px solid black and box-shadow to 4px 4px 0px black.

**Validates: Requirements 5.4**

### Property 14: Media Query Inheritance

*For any* new section element (sections 8, 9, 10), the existing media query rules defined in the stylesheet should apply without requiring new media query definitions.

**Validates: Requirements 5.6**

## Error Handling

### HTML Validation Errors

**Missing Required Elements:**
- If a section heading (h2) is missing, the section structure will be incomplete
- Mitigation: Validate HTML structure includes all three section headings with correct emoji and text
- Testing: Use HTML validator to check for proper heading hierarchy

**Malformed Details/Summary:**
- If details element is not properly closed or summary is outside details, reveal functionality will break
- Mitigation: Ensure each details element has exactly one summary child as the first element
- Testing: Verify details/summary pairing in DOM structure

**Missing CSS Classes:**
- If bg-teal or bg-lime classes are not defined in stylesheet, cards will have default white background
- Mitigation: Add CSS class definitions before adding HTML sections
- Testing: Verify computed background-color values match expected hex codes

### CSS Specificity Conflicts

**Existing Styles Override:**
- If existing CSS rules have higher specificity, new sections may not render correctly
- Mitigation: Use same class naming patterns as existing sections to inherit correct specificity
- Testing: Inspect computed styles in browser DevTools to verify expected values

**Media Query Conflicts:**
- If new sections don't match existing selectors, responsive behavior may fail
- Mitigation: Use identical class names and structure as existing sections
- Testing: Test at all three breakpoints (desktop, 768px, 480px) to verify responsive behavior

### Content Errors

**Incorrect Arabic Text Direction:**
- If RTL direction is not set, Arabic text will render left-to-right
- Mitigation: Ensure all arabic-text divs have direction: rtl in CSS
- Testing: Visual inspection of Arabic text alignment

**Missing or Incorrect Vocabulary:**
- If Arabic translations are incorrect or missing, educational content will be wrong
- Mitigation: Cross-reference all Arabic text with requirements document
- Testing: Manual review of all Arabic content against requirements

**Incorrect Gender Sorting:**
- If words are placed in wrong gender columns, students will learn incorrect grammar rules
- Mitigation: Verify all words ending in ة are in feminine column, others in masculine
- Testing: Check each word's ending character and column placement

### Browser Compatibility

**Details/Summary Support:**
- Older browsers may not support details/summary elements
- Mitigation: This is acceptable as the existing page already uses these elements
- Testing: Test in modern browsers (Chrome, Firefox, Safari, Edge)

**CSS Grid/Flexbox Support:**
- Very old browsers may not support flexbox for sort-container
- Mitigation: Acceptable as existing page already uses flexbox
- Testing: Verify layout in browsers with flexbox support

**Font Loading:**
- If Google Fonts fails to load, Space Grotesk will fall back to sans-serif
- Mitigation: Acceptable fallback behavior, already handled by existing page
- Testing: Test with network throttling to verify fallback fonts

## Testing Strategy

### Dual Testing Approach

This feature requires both unit tests and property-based tests to ensure comprehensive coverage:

**Unit Tests** will verify:
- Specific content examples (exact letter combinations, vocabulary words)
- Specific section structure (7 exercises in sections 8 and 10, correct headings)
- Edge cases (empty details elements, missing classes)
- Integration points (sections appear in correct order after section 7)

**Property-Based Tests** will verify:
- Universal styling rules across all cards (borders, shadows, colors)
- Responsive behavior across viewport ranges (not just specific breakpoints)
- CSS inheritance patterns (all new sections inherit existing media queries)
- Interaction patterns (all reveal buttons behave consistently)

Together, these approaches provide comprehensive coverage: unit tests catch concrete implementation bugs (wrong vocabulary word, missing exercise), while property tests verify general correctness (all cards have proper styling, all responsive rules apply).

### Unit Testing Strategy

**HTML Structure Tests:**
- Verify section 8 heading exists with text "8️⃣ Connect the Letters (Page 1)"
- Verify section 9 heading exists with text "9️⃣ Translate: English to Arabic"
- Verify section 10 heading exists with text "🔟 Connect the Letters (Page 2)"
- Count exactly 7 cards with class "bg-teal" in section 8
- Count exactly 7 cards with class "bg-lime" in section 10
- Verify section 9 contains exactly 1 card with class "bg-yellow"
- Verify all three sections appear after the existing section 7

**Content Validation Tests:**
- Verify section 8 contains all 7 letter combinations: ك+ق+ك, ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت
- Verify section 10 contains all 7 letter combinations: ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت, ك+ق+ك
- Verify word bank contains all 8 English words: blackboard, table, stapler, book, pen, door, ruler, bag
- Verify feminine column contains: سَبُّورَةٌ, طَاوِلَةٌ, دَبَّاسَةٌ, مِسْطَرَةٌ, حَقِيبَةٌ
- Verify masculine column contains: كِتَابٌ, قَلَمٌ, بَابٌ
- Verify column headers are "👧 Feminine (Ends in ة)" and "👦 Masculine (No ة)"

**CSS Class Tests:**
- Verify all section 8 cards have class "card bg-teal"
- Verify section 9 card has class "card bg-yellow"
- Verify all section 10 cards have class "card bg-lime"
- Verify all Arabic answers have class "arabic-text"
- Verify all reveal buttons use summary element

### Property-Based Testing Strategy

**Testing Library:** Use a DOM-based property testing approach with a library like jsdom for Node.js or browser-based testing with a property testing library such as fast-check (JavaScript/TypeScript).

**Test Configuration:**
- Minimum 100 iterations per property test
- Each test tagged with: **Feature: arabic-homework-exercises, Property {number}: {property_text}**

**Property Test 1: Letter Separator Display Pattern**
- Generate: Random selection of letter connection exercise cards from sections 8 and 10
- Test: Each card's question-text contains the pattern " + " between Arabic letters
- Tag: **Feature: arabic-homework-exercises, Property 1: For any letter connection exercise card, the question text should display Arabic letters separated by " + "**

**Property Test 2: Section Background Color Consistency**
- Generate: Random selection of cards within each section
- Test: All cards in section 8 have bg-teal, all in section 9 have bg-yellow, all in section 10 have bg-lime
- Tag: **Feature: arabic-homework-exercises, Property 2: For any exercise card within a given section, all cards should have the same background color class**

**Property Test 3: Reveal Button Interaction**
- Generate: Random selection of details elements across all three sections
- Test: Opening details element reveals previously hidden content (arabic-text or sort-container)
- Tag: **Feature: arabic-homework-exercises, Property 3: For any details element, when opened, should display its child content**

**Property Test 4: Arabic Text Styling Consistency**
- Generate: Random selection of arabic-text elements across all sections
- Test: Computed styles include font-size: 3.5rem, direction: rtl, font-family includes Arial
- Tag: **Feature: arabic-homework-exercises, Property 4: For any arabic-text element, computed styles should include 3.5rem font-size, rtl direction, and Arial font**

**Property Test 5: Neo-Brutalist Card Styling**
- Generate: Random selection of card elements from new sections
- Test: Computed styles include border: 4px solid black, box-shadow: 8px 8px 0px black
- Tag: **Feature: arabic-homework-exercises, Property 5: For any card element, computed styles should include 4px solid black border and 8px box shadow**

**Property Test 6: Reveal Button Styling**
- Generate: Random selection of summary elements across all sections
- Test: Computed styles include background-color: black, color: white, text-transform: uppercase
- Tag: **Feature: arabic-homework-exercises, Property 6: For any summary element, computed styles should include black background, white text, and uppercase transform**

**Property Test 7: Reveal Button Hover Effect**
- Generate: Random selection of summary elements
- Test: CSS :hover pseudo-class includes transform: translate(4px, 4px) and reduced box-shadow
- Tag: **Feature: arabic-homework-exercises, Property 7: For any summary element with hover, CSS should include translate transform and reduced shadow**

**Property Test 8: English Text Font Family**
- Generate: Random selection of text elements not within arabic-text class
- Test: Computed font-family includes "Space Grotesk"
- Tag: **Feature: arabic-homework-exercises, Property 8: For any English text element, computed font-family should include Space Grotesk**

**Property Test 9: Arabic Text Font Family**
- Generate: Random selection of arabic-text elements
- Test: Computed font-family includes Arial
- Tag: **Feature: arabic-homework-exercises, Property 9: For any arabic-text element, computed font-family should include Arial**

**Property Test 10: Section Heading Styling**
- Generate: Random selection of h2 elements from new sections
- Test: Computed styles include background-color: black, color: white, and colored box-shadow
- Tag: **Feature: arabic-homework-exercises, Property 10: For any h2 element in new sections, computed styles should include black background and colored shadow**

**Property Test 11: Responsive Arabic Text Scaling**
- Generate: Random selection of arabic-text elements at different viewport widths (769px, 768px, 481px, 480px)
- Test: Font-size is 3.5rem at >768px, 2.8rem at ≤768px, 2rem at ≤480px
- Tag: **Feature: arabic-homework-exercises, Property 11: For any arabic-text element, font-size should scale responsively at breakpoints**

**Property Test 12: Responsive Column Stacking**
- Generate: Random viewport widths around 480px breakpoint (481px, 480px, 320px)
- Test: sort-column elements have min-width: 100% at ≤480px
- Tag: **Feature: arabic-homework-exercises, Property 12: For any sort-column element, min-width should be 100% at mobile breakpoint**

**Property Test 13: Responsive Border and Shadow Scaling**
- Generate: Random selection of card elements at different viewport widths
- Test: Border and shadow values scale down at 768px and 480px breakpoints
- Tag: **Feature: arabic-homework-exercises, Property 13: For any card element, border and shadow should scale down at responsive breakpoints**

**Property Test 14: Media Query Inheritance**
- Generate: Random selection of elements from new sections at various viewport widths
- Test: Responsive styles apply without new media query definitions (verify existing selectors match)
- Tag: **Feature: arabic-homework-exercises, Property 14: For any new section element, existing media query rules should apply**

### Manual Testing Checklist

**Visual Inspection:**
- [ ] All three sections appear in correct order (8, 9, 10)
- [ ] Section colors match requirements (teal, yellow, lime)
- [ ] Arabic text displays right-to-left
- [ ] All emojis display correctly
- [ ] Borders and shadows have neo-brutalist appearance

**Interaction Testing:**
- [ ] All reveal buttons expand/collapse correctly
- [ ] Hover effects work on all buttons
- [ ] No JavaScript errors in console

**Responsive Testing:**
- [ ] Test at 1024px (desktop): Arabic text 3.5rem, full layout
- [ ] Test at 768px (tablet): Arabic text 2.8rem, reduced shadows
- [ ] Test at 480px (mobile): Arabic text 2rem, stacked columns
- [ ] Test at 320px (small mobile): All content readable and accessible

**Cross-Browser Testing:**
- [ ] Chrome/Edge (Chromium)
- [ ] Firefox
- [ ] Safari (if available)

**Accessibility Testing:**
- [ ] Keyboard navigation works for details/summary elements
- [ ] Text contrast meets WCAG standards (black on colored backgrounds)
- [ ] Touch targets are at least 44x44px on mobile
