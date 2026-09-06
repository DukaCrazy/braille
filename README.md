
# - pip install braille

## lib
### braillebase 0.2.9
- https://github.com/DukaCrazy/braillebase
### braillebaseenglish 0.2.9
- https://github.com/DukaCrazy/braillebaseenglish
### braillebasejapanese 0.2.9
- https://github.com/DukaCrazy/braillebasejapanese
### braillebasekorean 0.2.9
- https://github.com/DukaCrazy/braillebasekorean
### braillebaseportuguese 0.2.9
- https://github.com/DukaCrazy/braillebaseportuguese
### braillebasearabic 0.2.9
- https://github.com/DukaCrazy/braillebasearabic
### braillebaseviet 0.2.9
- https://github.com/DukaCrazy/braillebaseviet

# Braille Base
- <b>BrailleBase is an algorithm developed in Python with the goal of making Braille accessible to both blind and sighted individuals.

- Its architecture was designed to be intuitive, easy to understand, and simple to manipulate, allowing any developer to explore, transform, and integrate Braille data without complexity.</b>

## 1) Introduction
### BrailleBase is divided into X parts.
### Register Letters and Characters
<b>The first part of BrailleBase is responsible for registering letters, characters, symbols, icons, and other elements.
The registration methods are organized into four sets:</b>

**General** — where all items are registered: letters, numbers, uppercase and lowercase characters, punctuation, and other elements.

**Uppercase** — stores all uppercase items of the registered language.

**CJK** — registers phonetic alphabets such as Pinyin, Katakana, Hangul, and other East Asian writing systems.

**RTL** — stores alphabets that are written and read from right to left.

The Uppercase, CJK, and RTL sets are also added to the General set.
Therefore:

**General = {General[0], Uppercase[1], CJK[2], RTL[3]}**

```python
from braillebase import BrailleBase

class BrailleBaseExemple(BrailleBase):
        def __init__(self):
        super().__init__()
        #General
        self.append_braille_letter("a", ["⠁"]) 
        self.append_braille_letter("b", ["⠃"]) 
        self.append_braille_letter("c", ["⠉"]) 
        #Upper
        self.append_braille_letter("A", ["⠁"],1) 
        self.append_braille_letter("B", ["⠃"],1) 
        self.append_braille_letter("C", ["⠉"],1) 
        #CJK
        self.append_braille_letter("あ", ["⠁"],2)
        self.append_braille_letter("い", ["⠃"],2)
        self.append_braille_letter("う", ["⠉"],2)
        self.append_braille_letter("え", ["⠋"],2) 
        self.append_braille_letter("お", ["⠊"],2)
        #RTL
        self.append_braille_letter("ا", ["⠁"], 3) 
        self.append_braille_letter("ب", ["⠃"], 3) 
        self.append_braille_letter("ت", ["⠞"], 3) 
        self.append_braille_letter("ث", ["⠹"], 3) 
        self.append_braille_letter("ج", ["⠚"], 3)
        #Other A
        self.append_braille_letter("⠼", ["⠼"])
        self.append_braille_letter("1", ["⠁"]) 
        self.append_braille_letter("2", ["⠃"])
        #Other B
        self.append_braille_letter(".", ["⠲"])
        self.append_braille_letter(",", ["⠂"]) 
        self.append_braille_letter(";", ["⠆"])
        #Other C
        self.append_braille_letter("[ch]", ["⠡"])
        self.append_braille_letter("[sh]", ["⠩"])
        self.append_braille_letter("[th]", ["⠹"]) 
        #Other D
        self.append_braille_letter("[OW]", ["⠪"], 1)
        self.append_braille_letter("[AR]", ["⠜"], 1)
        self.append_braille_letter("[ING]", ["⠬"], 1) 
        #Other E
        self.append_braille_letter("$", ["⠈", "⠎"])
        self.append_braille_letter("¢", ["⠈", "⠉"])
        self.append_braille_letter("¥", ["⠈", "⠽"])
        self.append_braille_letter("€", ["⠈", "⠑"])
```

<b>BrailleBase allows you to register or edit braille directly through the instantiated object.
Since characters are stored in internal dictionaries, any new registration using an existing key automatically replaces the previous value.
This makes it possible to add, correct, or update letters, symbols, and tokens at any point during execution, without recreating the class or reinitializing the system.</b>

### Convert Text To Braille
<b>BrailleBase is the superclass that centralizes all the logic for processing, organizing, and analyzing Braille databases.
All subclasses inherit this logic and provide different output formats.</b>

#### A)
BrailleBase supports multiple output formats, including:
<b>
- JSON - `output_all_json(txt)`
- CSV - `output_all_csv(txt)`
- XML - `output_all_xml(txt)`
- YAML - `output_all_yaml(txt)`
- Markdown - `output_all_markdown(txt)`
- HTML - `output_all_html(txt)`
- TXT - `output_all_txt(txt)`
</b>

<b>The sequence of data provided in each set is: index, letter, braille, binary, numbering list, unicode, reverse braille, reverse binary, reverse numbering, reverse unicode.</b>

For example, the braille ⠓ produces the following output:

- **Braille:** ⠓
- **Numbering:** 1-2-5.
- **Binary:** 010011
- **Unicode:** U+2813
- **Reverse Braille:** ⠚
- **Reverse Numbering:** 2-4-5
- **Reverse Binary:** 011010
- **Reverse Unicode:** U+281a

#### B)
Additionally, the class provides different types of Braille output:

**I Love Braille!**

`output_braille_txt(txt)`

“Standard Braille — this is the traditional braille used for tactile reading.
Each cell represents the raised dots exactly as they would be perceived by the fingers. `⠠⠊⠀⠠⠇⠕⠧⠑⠀⠠⠃⠗⠁⠊⠇⠇⠑⠖`

`output_braille_txt(txt)`

Reverse Braille — this is the mirrored version of standard braille.
This format corresponds to braille writing, meaning the arrangement of dots as they appear when embossed or punched, before being read by touch. `⠲⠊⠸⠸⠑⠈⠺⠘⠄⠀⠊⠼⠪⠸⠄⠀⠑⠄`

`output_binary_txt(txt)`

Binary corresponding to each Braille symbol: a string containing a number from 0 to 63 in binary, representing each dot position used in that specific braille cell, where 0 means no dot and 1 means a raised dot.

#### C)
At the core of the class is the `confidence_test` method, considered the ‘brain’ of BrailleBase.
This method analyzes the provided sentence, identifies the most appropriate token, and returns a list of braille cells in the correct order, representing the final conversion sequence.

```python
from braillebaseenglish import *

bbe = BrailleBaseEnglish()
# Complete output
print(bbe.output_all_json("insert any text"))
print(bbe.output_all_csv("insert any text"))
print(bbe.output_all_xml("insert any text"))
print(bbe.output_all_yaml("insert any text"))
print(bbe.output_all_markdown("insert any text", "insert any footer"))
print(bbe.output_all_html("insert any text", "insert any footer"))
print(bbe.output_all_txt("insert any text", "insert any footer"))
# Simple output
print(bbe.output_braille_txt("insert any text"))
print(bbe.output_reverse_braille_txt("insert any text"))
print(bbe.output_binary_txt("insert any text"))
# Confidence test
print(bbe.confidence_test("insert any text"))
```

---

-> pip install braillebase 0.2.10

Other
-> pip install braille 
        -> Japanese, Portuguese, English, Arabic, Viet


## 2) Objective and motivation
- The goal is to create a tool capable of translating more complex texts and expressions using simple methods, so that even a beginner in programming can use it and develop their own tools.

- In addition to providing a character‑to‑Braille translation engine, BrailleBase offers classes with a pre‑registered database, allowing the user to simply download it and start using it. This makes it easy to create new translation rules, register new items, and much more.

- Beyond the code itself, BrailleBase will soon allow users to access Braille from other countries simply by calling a method. When sighted people study new languages, the first thing they are introduced to is the alphabet of the target language. With the pre‑registered characters, the user only needs to know which class to call — for example, BrailleBaseEnglish — and insert the character or sentence as the method argument. The Braille output will be generated automatically, along with its metadata if needed.

<b>I Love</b>
⠠⠊⠀⠠⠇⠕⠧⠑
6
2‑4

6
1‑2‑3
1‑3‑5
1‑2‑3‑6
1‑5

### - pip install braillebaseenglish

# English
### We believe that the translation generated in this test is 100% correct.
"Library Developed to Handle Simple and Complex Braille 2026"

```python
from braille import *

bb = bbe()
print(bb.output_braille_txt("Library Developed to Handle Simple and Complex Braille 2026"))
```
Output: ⠠⠇⠊⠃⠗⠁⠗⠽⠀⠠⠙⠑⠧⠑⠇⠕⠏⠑⠙⠀⠞⠕⠀⠠⠓⠁⠝⠙⠇⠑⠀⠠⠎⠊⠍⠏⠇⠑⠀⠁⠝⠙⠀⠠⠉⠕⠍⠏⠇⠑⠭⠀⠠⠃⠗⠁⠊⠇⠇⠑⠀⠼⠃⠚⠃⠋

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters

- a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z;

- [ch],[sh],[th],[wh],[ou],[st],[gh],[ed],[er],[ow],[ar],[ing];

- A, B, C, D, E, F, G, H, I, j, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z;

- [CH], [SH], [TH], [WH], [OU], [ST], [GH], [ED], [ER], [OW], [AR], [ING];

- ⠼, 1, 2, 3, 4, 5, 6, 7, 8, 9, 0;

- ., ,, ;, :, !, ?, ';

- ", “, ”, ‘, ’, (, ), /, \ , [, ], ,{ ,} ,< ,> #; 

- +, −, ×, *, ÷, %, =; 

- $, ¢, ¥, €, £, ₣, ₦; 

- →, ↓, ←, ↑, ©, ®, ™, ♀, ♂, §, @, &, [@], [‘], [´], [*], [—], [-];

## Special: Greek
- [Α] ,[Β] ,[Γ] ,[Δ] ,[Ε] ,[Ζ] ,[Η] ,[Θ] ,[Ι] ,[Κ] ,[Λ] ,[Μ] ,[Ν] ,[Ξ] ,[Ο] ,[Π] ,[Ρ] ,[Σ] ,[Τ] ,[Υ] ,[Φ] ,[Χ] ,[Ψ] ,[Ω];
- [α] ,[β] ,[γ] ,[δ] ,[ε] ,[ζ] ,[η] ,[θ] ,[ι] ,[κ] ,[λ] ,[μ] ,[ν] ,[ξ] ,[ο] ,[π] ,[ρ] ,[σ] ,[τ] ,[υ] ,[φ] ,[χ] ,[ψ] ,[ω] ,[ς];



### - pip install braillebasejapanese

# Japanese
### We believe that the translation generated in this test is 100% correct.
"単純な点字と複雑な点字の両方に対応できるライブラリが開発されました 2026年。"

```python
from braille import *

bb = bbj()
print(bb.output_braille_txt("たんじゅんな てんじ と ふくざつな てんじ の りょうほう に たいおう できる らいぶらり が かいはつ されました 2026ねん 。"))
```
Output: ⠕⠴⠘⠹⠴⠅⠀⠟⠴⠐⠳⠀⠞⠀⠭⠩⠐⠱⠝⠅⠀⠟⠴⠐⠳⠀⠎⠀⠈⠚⠉⠮⠉⠀⠇⠀⠕⠃⠊⠉⠀⠐⠟⠣⠙⠀⠑⠃⠐⠭⠑⠓⠀⠐⠡⠀⠡⠃⠥⠝⠀⠱⠛⠵⠳⠕⠀⠼⠃⠚⠃⠋⠏⠴⠀⠲⠀

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters
- あ, い, う, え, お, か, き, く, け, こ, さ, し, す, せ, そ, た, ち, つ, て, と, な, に, ぬ, ね, の, は, ひ, ふ, へ, ほ, ま, み, む, め, も, や, ゆ, よ, ら, り, る, れ, ろ, わ, ゐ, ゑ, を, ん

- が, ぎ, ぐ, げ, ご, ざ, じ, ず, ぜ, ぞ, だ, ぢ, づ, で, ど, ば, び, ぶ, べ, ぼ, ぱ, ぴ, ぷ, ぺ, ぽ

- きゃ, きゅ, きょ, ぎゃ, ぎゅ, ぎょ, しゃ, しゅ, しょ, じゃ, じゅ, じょ, ちゃ, ちゅ, ちょ, ぢゃ, ぢゅ, ぢょ, にゃ, にゅ, にょ, ひゃ, ひゅ, ひょ, びゃ, びゅ, びょ, ぴゃ, ぴゅ, ぴょ, みゃ, みゅ, みょ, りゃ, りゅ, りょ

- っ, ー

- ア, イ, ウ, エ, オ, カ, キ, ク, ケ, コ, サ, シ, ス, セ, ソ, タ, チ, ツ, テ, ト, ナ, ニ, ヌ, ネ, ノ, ハ, ヒ, フ, ヘ, ホ, マ, ミ, ム, メ, モ, ヤ, ユ, ヨ, ラ, リ, ル, レ, ロ, ワ, ヰ, ヱ, ヲ, ン

- ガ, ギ, グ, ゲ, ゴ, ザ, ジ, ズ, ゼ, ゾ, ダ, ヂ, ヅ, デ, ド, バ, ビ, ブ, ベ, ボ, パ, ピ, プ, ペ, ポ

- キャ, キュ, キョ, ギャ, ギュ, ギョ, シャ, シュ, ショ, ジャ, ジュ, ジョ, チャ, チュ, チョ, ヂャ, ヂュ, ヂョ, ニャ, ニュ, ニョ, ヒャ, ヒュ, ヒョ, ビャ, ビュ, ビョ, ピャ, ピュ, ピョ, ミャ, ミュ, ミョ, リャ, リュ, リョ

- イェ, ウィ, ウェ, ウォ, キェ, クァ, クィ, クェ, クォ, グァ, グィ, グェ, グォ, シェ, ジェ, スィ, ズィ, チェ, ツァ, ツィ, ツェ, ツォ, ティ, ディ, テュ, デュ, トゥ, ドゥ, ニェ, ヒェ, ファ, フィ, フェ, フォ, フュ, フョ, ヴァ, ヴィ, ヴェ, ヴォ, ヴュ, ヴョ, ヴ

- ッ

- 。, 、, ？, ！, ・, ?, !, ―, …, 「, 」, 『, 』, ～, (, ), ((, )), →, ←, ○, △, □, ×, ％, ＆, ＠, ＃, ＊, @, -, ., /, :, _, ~

## Special: Greek Number
- [Α] ,[Β] ,[Γ] ,[Δ] ,[Ε] ,[Ζ] ,[Η] ,[Θ] ,[Ι] ,[Κ] ,[Λ] ,[Μ] ,[Ν] ,[Ξ] ,[Ο] ,[Π] ,[Ρ] ,[Σ] ,[Τ] ,[Υ] ,[Φ] ,[Χ] ,[Ψ] ,[Ω];
- [α] ,[β] ,[γ] ,[δ] ,[ε] ,[ζ] ,[η] ,[θ] ,[ι] ,[κ] ,[λ] ,[μ] ,[ν] ,[ξ] ,[ο] ,[π] ,[ρ] ,[σ] ,[τ] ,[υ] ,[φ] ,[χ] ,[ψ] ,[ω] ,[ς];



### - pip install braillebasekorean

# Korean

```python
from braillebasekorean import BrailleBaseKorean

bbk = BrailleBaseKorean()
print(bbk.output_braille_txt("우리는 한국 점자의 역사에 참여하게 되어 매우 기쁩니다!"))
```
Output: ⠍⠐⠕⠉⠪⠒⠀⠚⠣⠒⠈⠍⠁⠀⠨⠎⠢⠨⠣⠺⠀⠱⠁⠠⠣⠝⠀⠰⠣⠢⠱⠚⠣⠈⠝⠀⠊⠽⠎⠀⠑⠗⠍⠀⠈⠕⠠⠘⠪⠃⠉⠕⠊⠣⠖

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters
78 >>> Jamo
        
        CHOSEONG = (
            "ㄱ","ㄲ","ㄴ","ㄷ","ㄸ","ㄹ","ㅁ","ㅂ","ㅃ","ㅅ",
            "ㅆ","ㅇ","ㅈ","ㅉ","ㅊ","ㅋ","ㅌ","ㅍ","ㅎ"
        )

        JUNGSEONG = (
            "ㅏ","ㅐ","ㅑ","ㅒ","ㅓ","ㅔ","ㅕ","ㅖ","ㅗ","ㅘ",
            "ㅙ","ㅚ","ㅛ","ㅜ","ㅝ","ㅞ","ㅟ","ㅠ","ㅡ","ㅢ","ㅣ"
        )

        JONGSEONG = (
            "", "ㄱ","ㄲ","ㄳ","ㄴ","ㄵ","ㄶ","ㄷ","ㄹ","ㄺ",
            "ㄻ","ㄼ","ㄽ","ㄾ","ㄿ","ㅀ","ㅁ","ㅂ","ㅄ","ㅅ",
            "ㅆ","ㅇ","ㅈ","ㅊ","ㅋ","ㅌ","ㅍ","ㅎ"
        )

11172 >>> Hangul

```python
from braillebasekorean import BrailleBaseKorean

bbk = BrailleBaseKorean()
print(bbk.confidence_test("우리는 한국 점자의 역사에 참여하게 되어 매우 기쁩니다!"))
```

Output: {0: ['우', ['⠍']], 1: ['리', ['⠐', '⠕']], 2: ['는', ['⠉', '⠪', '⠒']], 3: [' ', ['⠀']], 4: ['한', ['⠚', '⠣', '⠒']], 5: ['국', ['⠈', '⠍', '⠁']], 6: [' ', ['⠀']], 7: ['점', ['⠨', '⠎', '⠢']], 8: ['자', ['⠨', '⠣']], 9: ['의', ['⠺']], 10: [' ', ['⠀']], 11: ['역', ['⠱', '⠁']], 12: ['사', ['⠠', '⠣']], 13: ['에', ['⠝']], 14: [' ', ['⠀']], 15: ['참', ['⠰', '⠣', '⠢']], 16: ['여', ['⠱']], 17: ['하', ['⠚', '⠣']], 18: ['게', ['⠈', '⠝']], 19: [' ', ['⠀']], 20: ['되', ['⠊', '⠽']], 21: ['어', ['⠎']], 22: [' ', ['⠀']], 23: ['매', ['⠑', '⠗']], 24: ['우', ['⠍']], 25: [' ', ['⠀']], 26: ['기', ['⠈', '⠕']], 27: ['쁩', ['⠠', '⠘', '⠪', '⠃']], 28: ['니', ['⠉', '⠕']], 29: ['다', ['⠊', '⠣']], 30: ['!', ['⠖']]}


### The developed algorithm demonstrates accuracy for its intended purpose. If necessary, we may require the assistance of a specialist to review and validate the underlying Jamo mapping table.



### - pip install braillebaseportuguese

# Portuguese
### We believe that the translation generated in this test is 100% correct.
"Biblioteca Desenvolvida para Lidar com Braille Simples e Complexo 2026"

```python
from braille import *

bb = bbp()
print(bb.output_braille_txt("Biblioteca Desenvolvida para Lidar com Braille Simples e Complexo 2026"))
```
Output: ⠨⠃⠊⠃⠇⠊⠕⠞⠑⠉⠁⠀⠨⠙⠑⠎⠑⠝⠧⠕⠇⠧⠊⠙⠁⠀⠏⠁⠗⠁⠀⠨⠇⠊⠙⠁⠗⠀⠉⠕⠍⠀⠨⠃⠗⠁⠊⠇⠇⠑⠀⠨⠎⠊⠍⠏⠇⠑⠎⠀⠑⠀⠨⠉⠕⠍⠏⠇⠑⠭⠕⠀⠼⠃⠚⠃⠋

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters

- a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z;
- á, ã, â, à, é, ê, í, ì, ó, ô, õ, ú, ù, ü, ç, ñ;

- A, B, C, D, E, F, G, H, I, j, K, L, M, N, O, P, Q, R, S, T, U, V, W, X, Y, Z;
- Á, Ã, Â, À, É, Ê, Í, Ì, Ó, Ô, Õ, Ú, Ù, Ü, Ç, Ñ;

- ., ,, ;, :, ?, !, (, ), [, ], “, ”, «, »;

- ⠼, 1, 2, 3, 4, 5, 6, 7, 8, 9, 0;
- +, -, *, ×, /, ÷, =, °, %, √, <, >;
- R$, $, €;

- #, |, @, _, ª, §, ’, &, ^, ~

## Special: Greek Number
- [Α] ,[Β] ,[Γ] ,[Δ] ,[Ε] ,[Ζ] ,[Η] ,[Θ] ,[Ι] ,[Κ] ,[Λ] ,[Μ] ,[Ν] ,[Ξ] ,[Ο] ,[Π] ,[Ρ] ,[Σ] ,[Τ] ,[Υ] ,[Φ] ,[Χ] ,[Ψ] ,[Ω];
- [α] ,[β] ,[γ] ,[δ] ,[ε] ,[ζ] ,[η] ,[θ] ,[ι] ,[κ] ,[λ] ,[μ] ,[ν] ,[ξ] ,[ο] ,[π] ,[ρ] ,[σ] ,[τ] ,[υ] ,[φ] ,[χ] ,[ψ] ,[ω] ,[ς];



# Arabic
### The algorithm behaves normally, as it does in any other language; however, we are not able to verify whether the braille generated for the Arabic library is correct.
"مكتبة برمجية طُوِّرت للتعامل مع نصوص برايل البسيطة والمعقدة 2026"

```python
from braille import *

bb = bba()
print()
print(bb.output_braille_txt("مكتبة برمجية طُوِّرت للتعامل مع نصوص برايل البسيطة والمعقدة 2026"))
```
Output: ⠍⠅⠞⠃⠡⠀⠃⠗⠍⠚⠊⠡⠀⠾⠥⠺⠠⠑⠗⠞⠀⠇⠇⠞⠷⠁⠍⠇⠀⠍⠷⠀⠝⠯⠺⠯⠀⠃⠗⠁⠊⠇⠀⠁⠇⠃⠎⠊⠾⠡⠀⠺⠁⠇⠍⠷⠟⠙⠡⠀⠼⠃⠚⠃⠋

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters

- ا, ب, ت, ث, ج, ح, خ, د, ذ, ر, ز, س, ش, ص, ض, ط, ظ, ع, غ, ف, ق, ك, ل, م, ن, ه, و, ي;

- لا, ى, ة, ء, أ, إ, ؤ, ئ, آ;


-  َ,  ً ,  ِ ,  ٍ ,  ُ ,  ٌ ,  ْ ,  ّ ;

` Fatha = "\u064e"       # َ  , Tanween Al Fath = "\u064b"   # ً  , Kasra = "\u0650"       # ِ  `

` Tanween Al Kasr = "\u064d"   # ٍ  , Dhamma = "\u064f"       # ُ  , Tanween Al Dham = "\u064c"   # ٌ `  

` Sukoun = "\u0652"       # ْ  , Shaddah = "\u0651"      # ّ  `



## Special: Greek
- [Α] ,[Β] ,[Γ] ,[Δ] ,[Ε] ,[Ζ] ,[Η] ,[Θ] ,[Ι] ,[Κ] ,[Λ] ,[Μ] ,[Ν] ,[Ξ] ,[Ο] ,[Π] ,[Ρ] ,[Σ] ,[Τ] ,[Υ] ,[Φ] ,[Χ] ,[Ψ] ,[Ω];
- [α] ,[β] ,[γ] ,[δ] ,[ε] ,[ζ] ,[η] ,[θ] ,[ι] ,[κ] ,[λ] ,[μ] ,[ν] ,[ξ] ,[ο] ,[π] ,[ρ] ,[σ] ,[τ] ,[υ] ,[φ] ,[χ] ,[ψ] ,[ω] ,[ς];


### - pip install braillebaseviet
### We are truly honored to take part in the ongoing story of Vietnamese Braille.

# Viet
"Thư viện được phát triển để xử lý chữ nổi Braille đơn giản và phức tạp năm 2026"

```python
from braille import *

bb = bbv()
print(bb.output_braille_txt("Thư viện được phát triển để xử lý chữ nổi Braille đơn giản và phức tạp năm 2026"))
```
Output: ⠠⠞⠓⠳⠀⠧⠊⠣⠝⠀⠮⠳⠪⠉⠀⠏⠓⠁⠞⠀⠞⠗⠊⠣⠝⠀⠮⠣⠀⠭⠳⠀⠇⠽⠀⠉⠓⠳⠀⠝⠹⠊⠀⠠⠃⠗⠁⠊⠇⠇⠑⠀⠮⠪⠝⠀⠛⠊⠁⠝⠀⠧⠁⠀⠏⠓⠳⠉⠀⠞⠁⠏⠀⠝⠜⠍⠀⠼⠃⠚⠃⠋

# Announcement
- This package is part of an ecosystem called Braille Base. This name does not represent a company or business; it is an independent initiative aimed at providing registered braille tables for all of humanity.

- We constantly need help to register, update, and validate braille tables. There is still no official contact channel, but you can find new information on the blog braillebase.blogspot.com or brailletable.blogspot.com.

## Pre-registered Letters and Characters

- a, á, à, ả, ã, ạ
- ă, ắ, ằ, ẳ, ẵ, ặ
- â, ấ, ầ, ẩ, ẫ, ậ
- b
- c
- d
- đ
- e, é, è, ẻ, ẽ, ẹ
- ê, ế, ề, ể, ễ, ệ
- g
- h
- i, í, ì, ỉ, ĩ, ị
- k
- l
- m
- n
- o, ó, ò, ỏ, õ, ọ
- ô, ố, ồ, ổ, ỗ, ộ
- ơ, ớ, ờ, ở, ỡ, ợ
- p
- q
- r
- s
- t
- u, ú, ù, ủ, ũ, ụ
- ư, ứ, ừ, ử, ữ, ự
- v
- x
- y, ý, ỳ, ỷ, ỹ, ỵ

- f, j, w, z

- A, Á, À, Ả, Ã, Ạ
- Ă, Ắ, Ằ, Ẳ, Ẵ, Ặ
- Â, Ấ, Ầ, Ẩ, Ẫ, Ậ
- B
- C
- D
- Đ
- E, É, È, Ẻ, Ẽ, Ẹ
- Ê, Ế, Ề, Ể, Ễ, Ệ
- G
- H
- I, Í, Ì, Ỉ, Ĩ, Ị
- K
- L
- M
- N
- O, Ó, Ò, Ỏ, Õ, Ọ
- Ô, Ố, Ồ, Ổ, Ỗ, Ộ
- Ơ, Ớ, Ờ, Ở, Ỡ, Ợ
- P
- Q
- R
- S
- T
- U, Ú, Ù, Ủ, Ũ, Ụ
- Ư, Ứ, Ừ, Ử, Ữ, Ự
- V
- X
- Y, Ý, Ỳ, Ỷ, Ỹ, Ỵ
- F,J,W,Z

- ⠼, 1, 2, 3, 4, 5, 6, 7, 8, 9, 0;

- ., ,, ;, :, !, ?, ';

- ", “, ”, ‘, ’, (, ), /, \ , [, ], ,{ ,} ,< ,> #; 

- +, −, ×, *, ÷, %, =; 

- $, ¢, ¥, €, £, ₣, ₦; 

- →, ↓, ←, ↑, ©, ®, ™, ♀, ♂, §, @, &, [@], [‘], [´], [*], [—], [-];

## Special: Greek Number
- [Α] ,[Β] ,[Γ] ,[Δ] ,[Ε] ,[Ζ] ,[Η] ,[Θ] ,[Ι] ,[Κ] ,[Λ] ,[Μ] ,[Ν] ,[Ξ] ,[Ο] ,[Π] ,[Ρ] ,[Σ] ,[Τ] ,[Υ] ,[Φ] ,[Χ] ,[Ψ] ,[Ω];
- [α] ,[β] ,[γ] ,[δ] ,[ε] ,[ζ] ,[η] ,[θ] ,[ι] ,[κ] ,[λ] ,[μ] ,[ν] ,[ξ] ,[ο] ,[π] ,[ρ] ,[σ] ,[τ] ,[υ] ,[φ] ,[χ] ,[ψ] ,[ω] ,[ς];


<img src="./logo.png" alt="Logo" width="500" height="493">
