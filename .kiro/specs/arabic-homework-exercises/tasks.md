# Implementation Plan: Arabic Homework Exercises

## Overview

This implementation adds three new exercise sections to the existing index.html file. The work involves adding HTML markup and minimal CSS for two new background color classes. All sections follow the established neo-brutalist design patterns and reuse existing CSS classes for cards, buttons, and responsive behavior.

## Tasks

- [x] 1. Add CSS for new background colors
  - Add `.bg-teal` class with background-color: #5EEAD4
  - Add `.bg-lime` class with background-color: #BEF264
  - Insert these classes in the stylesheet alongside existing `.bg-yellow` class
  - _Requirements: 1.4, 3.4, 4.1_

- [ ]* 1.1 Write property test for section background color consistency
  - **Property 2: Section Background Color Consistency**
  - **Validates: Requirements 1.4, 2.2, 3.4**

- [x] 2. Add Section 8: Connect the Letters (Page 1)
  - [x] 2.1 Add section heading with emoji "8️⃣ Connect the Letters (Page 1)"
    - Insert after the last existing section (section 7)
    - Use h2 element with existing heading styles
    - _Requirements: 1.1_
  
  - [x] 2.2 Add 7 letter connection exercise cards with bg-teal background
    - Create card structure for each: ك+ق+ك, ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت
    - Each card includes question-text div with separated letters using " + "
    - Each card includes details/summary reveal with connected Arabic letters
    - Use existing card, question-text, arabic-text, details, and summary classes
    - _Requirements: 1.2, 1.3, 1.4, 1.5, 1.6, 1.7_

- [ ]* 2.3 Write property test for letter separator display pattern
  - **Property 1: Letter Separator Display Pattern**
  - **Validates: Requirements 1.3, 3.3**

- [ ]* 2.4 Write property test for Arabic text styling consistency
  - **Property 4: Arabic Text Styling Consistency**
  - **Validates: Requirements 1.6, 3.6**

- [x] 3. Add Section 9: English to Arabic Translation
  - [x] 3.1 Add section heading with emoji "9️⃣ Translate: English to Arabic"
    - Insert after Section 8
    - Use h2 element with existing heading styles
    - _Requirements: 2.1_
  
  - [x] 3.2 Add vocabulary sorting exercise card with bg-yellow background
    - Create single card with instructions and word bank
    - Word bank displays 8 English words: blackboard, table, stapler, book, pen, door, ruler, bag
    - Add details/summary reveal containing sort-container with two columns
    - Feminine column (👧 Feminine (Ends in ة)): سَبُّورَةٌ, طَاوِلَةٌ, دَبَّاسَةٌ, مِسْطَرَةٌ, حَقِيبَةٌ
    - Masculine column (👦 Masculine (No ة)): كِتَابٌ, قَلَمٌ, بَابٌ
    - Use existing sort-container, sort-column, and word-tag classes
    - _Requirements: 2.2, 2.3, 2.4, 2.5, 2.6, 2.7, 2.8_

- [ ]* 3.3 Write property test for reveal button interaction
  - **Property 3: Reveal Button Interaction**
  - **Validates: Requirements 1.5, 2.5, 3.5**

- [x] 4. Add Section 10: Connect the Letters (Page 2)
  - [x] 4.1 Add section heading with emoji "🔟 Connect the Letters (Page 2)"
    - Insert after Section 9
    - Use h2 element with existing heading styles
    - _Requirements: 3.1_
  
  - [x] 4.2 Add 7 letter connection exercise cards with bg-lime background
    - Create card structure for each: ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت, ك+ق+ك
    - Each card includes question-text div with separated letters using " + "
    - Each card includes details/summary reveal with connected Arabic letters
    - Use existing card, question-text, arabic-text, details, and summary classes
    - _Requirements: 3.2, 3.3, 3.4, 3.5, 3.6, 3.7_

- [x] 5. Checkpoint - Verify visual consistency and functionality
  - Open index.html in browser and verify all three sections appear correctly
  - Test reveal buttons in all sections
  - Verify Arabic text displays right-to-left with correct font size
  - Verify section colors match design (teal, yellow, lime)
  - Ensure all tests pass, ask the user if questions arise

- [ ]* 5.1 Write property tests for neo-brutalist styling
  - **Property 5: Neo-Brutalist Card Styling**
  - **Property 6: Reveal Button Styling**
  - **Property 7: Reveal Button Hover Effect**
  - **Validates: Requirements 4.1, 4.2, 4.3, 4.4**

- [ ]* 5.2 Write property tests for font families
  - **Property 8: English Text Font Family**
  - **Property 9: Arabic Text Font Family**
  - **Validates: Requirements 4.5, 4.6**

- [ ]* 5.3 Write property test for section heading styling
  - **Property 10: Section Heading Styling**
  - **Validates: Requirements 4.7**

- [x] 6. Verify responsive behavior
  - [x] 6.1 Test at tablet breakpoint (768px)
    - Verify Arabic text scales to 2.8rem
    - Verify shadows reduce to 6px
    - Verify existing media queries apply to new sections
    - _Requirements: 5.1, 5.4, 5.6_
  
  - [x] 6.2 Test at mobile breakpoint (480px)
    - Verify Arabic text scales to 2rem
    - Verify borders reduce to 3px and shadows to 4px
    - Verify sort columns stack vertically in Section 9
    - Verify touch targets are adequate for mobile
    - _Requirements: 5.2, 5.3, 5.4, 5.5, 5.6_

- [ ]* 6.3 Write property tests for responsive behavior
  - **Property 11: Responsive Arabic Text Scaling**
  - **Property 12: Responsive Column Stacking**
  - **Property 13: Responsive Border and Shadow Scaling**
  - **Property 14: Media Query Inheritance**
  - **Validates: Requirements 5.1, 5.2, 5.3, 5.4, 5.6**

- [x] 7. Final checkpoint - Complete validation
  - Run HTML validator to check for structural errors
  - Test in multiple browsers (Chrome, Firefox, Safari if available)
  - Verify keyboard navigation works for all details/summary elements
  - Verify text contrast meets accessibility standards
  - Ensure all tests pass, ask the user if questions arise

## Notes

- Tasks marked with `*` are optional and can be skipped for faster MVP
- The implementation reuses existing CSS classes extensively, minimizing new code
- Only two new CSS classes need to be added (bg-teal and bg-lime)
- All HTML follows the established pattern from existing sections
- Responsive behavior is automatic through existing media queries
- No JavaScript is required for this feature
