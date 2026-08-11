
## 2026/08/11 - Version 0.1.5 Summary
- BrailleBase: Adjustments to the token size definition caused a bug that was not detected in the testing environment but was noticed after the version was released. The inconsistency has been fixed.

## 2026/08/02 - Version 0.1.4 Summary
- Addition of the base reverse Braille.
### braillebase Version 0.1.3
### braillebasejapanese Version 0.1.4
### braillebaseportuguese Version 0.1.4
### braillebasearabic Version 0.1.4
### braillebaseenglish Version 0.1.4
### braillebaseviet Version 0.1.4

## 2026/08/02 - Version 0.1.3 Summary
- Addition of the braillebaseviet.

## 2026/07/20 - Version 0.1.2 Summary
- braillebase 0.1.2
- Bug fix for the [translate_text_to_reverse braille()] method.
- Update to the HTML generator method [output_all_html()].

## 2026/07/13 - Version 0.1.1 Summary
- Addition of the base reverse Braille.
- Definition of the base architecture.
### braillebase Version 0.1.1
### braillebasejapanese Version 0.1.1
### braillebaseportuguese Version 0.1.1
### braillebasearabic Version 0.1.1
### braillebaseenglish Version 0.1.1
### brailletable Version 1.0.2

## 2026/06/23 - Version 0.0.3 Summary
### braillebase Version 0.0.15
- Invocation of the special append methods via the simple append method using the third argument.
- Separating the RTL module for languages like Arabic, Hebrew, and Persian.
- Specific rules for uppercase Latin letters.
- Spelling fix in method names: lettr -> letter
### braillebasejapanese Version 0.0.9
### braillebaseportuguese Version 0.0.5
### braillebasearabic Version 0.0.3
### braillebaseenglish Version 0.0.2

## 2026/06/14 - Version 0.0.2 Summary
### braillebase Version 0.0.13 Summary
- Scope Optimization for Latin Characters: Updated internal variables within the methods responsible for parsing and validating Latin alphabet rules.
- Modularization and Isolation of the CJK Block: Segregated the processing pipeline for CJK languages (Chinese, Japanese, and Korean). 
- This behavior was isolated from both the generic rules_02 method and the non-special character flow, ensuring exclusive and specialized handling for this linguistic group.
Code Refactoring and Cleanup: Removed structural redundancies to improve system readability and maintainability.
- Performance Optimization: Updated the methods responsible for managing Braille character lists and their respective dependencies, reducing computational overhead.
### braillebasejapanese Version 0.0.7
- Scope Optimization for Latin Characters: Updated internal variables within the methods responsible for parsing and validating Latin alphabet rules.
- Modularization and Isolation of the CJK Block: Segregated the processing pipeline for CJK languages (Chinese, Japanese, and Korean). 
- This behavior was isolated from both the generic rules_02 method and the non-special character flow, ensuring exclusive and specialized handling for this linguistic group.
Code Refactoring and Cleanup: Removed structural redundancies to improve system readability and maintainability.
- Performance Optimization: Updated the methods responsible for managing Braille character lists and their respective dependencies, reducing computational overhead.
