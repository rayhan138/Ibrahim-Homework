# Requirements Document

## Introduction

This feature adds three new sections of Arabic homework exercises to the existing Arabic learning webpage. The new sections maintain the established neo-brutalist design system and include letter connection exercises and vocabulary translation/sorting activities. These exercises are designed to help students practice Arabic letter combinations and gender-based vocabulary classification.

## Glossary

- **Webpage**: The existing index.html file containing Arabic learning exercises
- **Neo-Brutalist_Design**: A design style characterized by bold borders, shadows, bright colors, and large typography
- **Letter_Connection_Exercise**: An exercise where students connect Arabic letters to form words
- **Reveal_Button**: An interactive details/summary element that shows answers when clicked
- **Vocabulary_Sorting_Exercise**: An exercise where students categorize Arabic words by grammatical gender
- **Section**: A distinct group of exercises with a numbered heading and consistent background color
- **Card**: A bordered container element with shadow effects containing exercise content
- **Responsive_Design**: Layout that adapts to different screen sizes (desktop, tablet, mobile)
- **Arabic_Text_Display**: Right-to-left text rendering with large font size (3.5rem) for Arabic characters

## Requirements

### Requirement 1: Add Connect the Letters Section (Page 1)

**User Story:** As a student, I want to practice connecting Arabic letters in the first set of exercises, so that I can learn how letters combine to form words.

#### Acceptance Criteria

1. THE Webpage SHALL display a new section titled "8️⃣ Connect the Letters (Page 1)" after the existing seven sections
2. THE Section SHALL contain exactly 7 letter connection exercises
3. WHEN an exercise is displayed, THE Webpage SHALL show Arabic letters separated by plus signs (e.g., ك + ق + ك)
4. THE Section SHALL use bg-teal background color for all exercise cards
5. WHEN a student clicks a Reveal_Button, THE Webpage SHALL display the connected Arabic letters as a single word
6. THE Arabic_Text_Display SHALL render all Arabic text at 3.5rem font size with right-to-left direction
7. THE Section SHALL include the following letter combinations: ك+ق+ك, ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت

### Requirement 2: Add English to Arabic Translation Section

**User Story:** As a student, I want to translate English vocabulary words to Arabic and sort them by gender, so that I can practice identifying masculine and feminine nouns.

#### Acceptance Criteria

1. THE Webpage SHALL display a new section titled "9️⃣ Translate: English to Arabic" after the Connect the Letters (Page 1) section
2. THE Section SHALL use bg-yellow background color
3. THE Section SHALL display a word bank containing 8 English vocabulary items: blackboard, table, stapler, book, pen, door, ruler, bag
4. THE Section SHALL provide two sorting columns labeled "👧 Feminine (Ends in ة)" and "👦 Masculine (No ة)"
5. WHEN a student clicks the Reveal_Button, THE Webpage SHALL display the Arabic translations sorted into masculine and feminine columns
6. THE Feminine column SHALL contain: سَبُّورَةٌ (blackboard), طَاوِلَةٌ (table), دَبَّاسَةٌ (stapler), مِسْطَرَةٌ (ruler), حَقِيبَةٌ (bag)
7. THE Masculine column SHALL contain: كِتَابٌ (book), قَلَمٌ (pen), بَابٌ (door)
8. THE Section SHALL use two-column responsive layout that stacks vertically on mobile devices

### Requirement 3: Add Connect the Letters Section (Page 2)

**User Story:** As a student, I want to practice connecting Arabic letters in the second set of exercises, so that I can reinforce my understanding of letter combinations.

#### Acceptance Criteria

1. THE Webpage SHALL display a new section titled "🔟 Connect the Letters (Page 2)" after the English to Arabic Translation section
2. THE Section SHALL contain exactly 7 letter connection exercises
3. WHEN an exercise is displayed, THE Webpage SHALL show Arabic letters separated by plus signs
4. THE Section SHALL use bg-lime background color for all exercise cards
5. WHEN a student clicks a Reveal_Button, THE Webpage SHALL display the connected Arabic letters as a single word
6. THE Arabic_Text_Display SHALL render all Arabic text at 3.5rem font size with right-to-left direction
7. THE Section SHALL include the following letter combinations: ه+ن+ه, ك+ت+ب, ك+ل+ب, ق+ل+ب, ق+ط+ة, ب+ي+ت, ك+ق+ك

### Requirement 4: Maintain Design System Consistency

**User Story:** As a student, I want the new sections to match the existing design, so that I have a consistent learning experience.

#### Acceptance Criteria

1. THE Webpage SHALL apply Neo-Brutalist_Design styling to all new sections
2. THE Card elements SHALL have 4px solid black borders and 8px box shadows
3. THE Reveal_Button elements SHALL use black background with white text and uppercase styling
4. WHEN a Reveal_Button is hovered, THE Webpage SHALL translate the button position and reduce shadow size
5. THE Webpage SHALL use Space Grotesk font for all English text
6. THE Webpage SHALL use Arial font for all Arabic text
7. THE Section headings SHALL use black background with colored shadows matching the section theme

### Requirement 5: Implement Responsive Behavior

**User Story:** As a student using different devices, I want the new sections to display properly on all screen sizes, so that I can learn on any device.

#### Acceptance Criteria

1. WHEN the viewport width is 768px or less, THE Webpage SHALL reduce Arabic text size to 2.8rem
2. WHEN the viewport width is 480px or less, THE Webpage SHALL reduce Arabic text size to 2rem
3. WHEN the viewport width is 480px or less, THE Webpage SHALL stack sorting columns vertically
4. THE Webpage SHALL reduce border widths and shadow sizes proportionally on smaller screens
5. THE Webpage SHALL maintain readability and touch-friendly button sizes on mobile devices
6. THE Responsive_Design SHALL apply existing media query rules to all new sections
