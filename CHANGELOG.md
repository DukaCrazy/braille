
## 2026/9/6 - Version 0.2.9 Sumary
### braillebase Version 0.2.9
### braillebasejapanese Version 0.2.9
### braillebaseportuguese Version 0.2.9
### braillebasearabic Version 0.2.9
### braillebaseenglish Version 0.2.9
### braillebaseviet Version 0.2.9
### braillebasekorean Version 0.2.9

- Update to the logic that processes uppercase and lowercase characters.

## 2026/8/30 - Version 0.2.7 Sumary
- dependence logic update

## 2026/8/19 - Version 0.2.6 Sumary
### Improvements in Rule Generation
- Updated rule‑generation methods, increasing translation accuracy for characters, symbols, and numbers.
- Refined internal algorithms for detecting and applying special rules, reducing ambiguities and improving consistency across modules.
### Enhancements to Internal Methods
- Improved the behavior of confidence_test, making output analysis more predictable and better aligned with the translation pipeline.
- Optimized tokenize_text, ensuring more stable segmentation and compatibility with new token sets.
### New Rules for Special Symbols
- Added dedicated rules for translating special symbols, enabling braille generation for icons, markers, and graphical elements.
- Expanded mathematical sub‑rules, extending support for new operators, indicators, and numeric structures.

        Old >> def prepare_number_braille(self, text: str) -> str:
        New >> def prepare_number_braille(self, tokens: list[str]) -> list[str]:

        Old >> def prepare_special_braille_rules_uppercase(self, text: str) -> str:
        New >> def prepare_special_braille_rules_uppercase(self, tokens: list[str]) -> list[str]:

        Old >> def prepare_special_braille_rules_CJK(self, text: str) -> str:
        New >> def prepare_special_braille_rules_CJK(self, tokens: list[str]) -> list[str]:

        Old >> def prepare_special_braille_rules_RTL(self, text: str) -> str:
        New >> def prepare_special_braille_rules_RTL(self, tokens: list[str]) -> list[str]:

        New >> def prepare_special_braille_rules_simbol(self, tokens: list[str]) -> list[str]:

## 2026/8/16 - Version 0.2.0 Sumary
### Architecture Updates
- Centralization of common data:  
- All universal symbols — such as numbers, Roman letters, and other elements shared across multiple languages — are now registered directly in the BrailleBase superclass.
- Language‑specific subclasses no longer duplicate these entries and instead inherit the unified core set automatically.
### Updates to multiple‑append methods
`def append_braille_letter_IO(target_data_path: str):`
- Support for external files:  
- The multiple‑append methods have been updated to allow registering new symbols directly from CSV, JSON, or XML files.
- Dynamic table updates:
- The internal database can now be updated by calling native library methods that process these external files, making maintenance simpler and more automated.

        # Braille Base IO
        Reader for JSON, XML, and CSV formats.

        ## Input Examples
        JSON example:
        ```json
        [
            {
                "letter": "a",
                "braille": "⠁,⠁",
                "pattern": 0
            },
            {
                "letter": "b",
                "braille": "⠟,⠟,⠟",
                "pattern": 0
            }
        ]
        ```
        XML example:
        ```xml
        <?xml version="1.0" encoding="utf-8"?>
        <braille_append>
            <item>
                <letter>a</letter>
                <braille>⠁,⠁</braille>
                <pattern>0</pattern>
            </item>

            <item>
                <letter>b</letter>
                <braille>⠟,⠟,⠟</braille>
                <pattern>0</pattern>
            </item>
        </braille_append>
        ```
        CSV example:
        ```csv
        a,"⠁,⠁",0
        b,"⠟,⠟,⠟",0
        ```
        ## Output Example

        [('a', ['⠁', '⠁'], 0), ('b', ['⠟', '⠟', '⠟'], 0)]

## 2026/08/11 - Version 0.1.6 Summary
### braillebase Version 0.1.5
### braillebasejapanese Version 0.1.6
### braillebaseportuguese Version 0.1.6
### braillebasearabic Version 0.1.6
### braillebaseenglish Version 0.1.6
### braillebaseviet Version 0.1.6
### braillebaseoutput Version 0.1.6
### braillebaseio 1.0.2
### brailletable 1.0.2

### Added
- Full implementation of the BrailleBaseOutput module, responsible for generating multiple output formats based on the data processed by braillebase.
### New export methods:
- output_all_json — detailed JSON structure generation.
- output_all_csv — tabular CSV export.
- output_all_xml — formatted and validated XML output.
- output_all_yaml — clean and readable YAML output.
- output_all_markdown — Markdown documentation with organized sections.
- output_all_html — HTML rendering with tables and a standardized layout.
- output_all_txt — plain text output, ideal for logs and quick inspection.
### Improved
- Complete separation of heavy formatting logic, removing duplication and reducing coupling with the main module.
- Standardization of output fields (index, braille, binary, numbering, unicode, reverse).
- Ensured consistency across all formats, including cross‑validation of Unicode and reverse braille cells.
- Enhanced readability of all outputs with consistent indentation and clear data organization.

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

<img src="./logo.png" alt="Logo" width="500" height="493">
