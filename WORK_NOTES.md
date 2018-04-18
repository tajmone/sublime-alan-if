# Alan Syntax Notes

Some working notes on how to scope the Alan syntax elements.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [Syntax Scopes](#syntax-scopes)
    - [Identifiers](#identifiers)
    - [Classes](#classes)
- [Reference Links](#reference-links)

<!-- /MarkdownTOC -->

-----

# Syntax Scopes

## Identifiers

The BNF definion of `Identifier` in "`alan.g`" source (line 15):

```bnf
fragment IDENTIFIER : LETTER ( LETTER | DIGIT | '_' )* ;

```

Also, in "`alan.g`" (line 9)::

```bnf
fragment LETTER : 'A' .. 'Z' | 'a' .. 'z' | '_' | '$' | '\u00e0'..'\u00f6' | '\u00f8'..'\u00fe' ;
```

... where `'\u00e0'..'\u00f6'` stands for:

- `U+00E0` = à
- `U+00E1` = á
- `U+00E2` = â
- `U+00E3` = ã
- `U+00E4` = ä
- `U+00E5` = å
- `U+00E6` = æ
- `U+00E7` = ç
- `U+00E8` = è
- `U+00E9` = é
- `U+00EA` = ê
- `U+00EB` = ë
- `U+00EC` = ì
- `U+00ED` = í
- `U+00EE` = î
- `U+00EF` = ï
- `U+00F0` = ð
- `U+00F1` = ñ
- `U+00F2` = ò
- `U+00F3` = ó
- `U+00F4` = ô
- `U+00F5` = õ
- `U+00F6` = ö

... and `'\u00f8'..'\u00fe'` for:

- `U+00F8` = ø
- `U+00F9` = ù
- `U+00FA` = ú
- `U+00FB` = û
- `U+00FC` = ü
- `U+00FD` = ý
- `U+00FE` = þ

... i.e., Unicode points for character from the [Latin-1 Supplement] ([ISO-8859-1]):

[Latin-1 Supplement]: http://jrgraphix.net/r/Unicode/00A0-00FF
[ISO-8859-1]: https://en.wikipedia.org/wiki/ISO/IEC_8859-1

## Classes

> Fields, properties, members and attributes of a class or other data structure should use:
> 
>     variable.other.member

# Reference Links

- [ST3 Documentation » Scope Naming]
- [ST3 Documentation » Syntax Definitions]


[ST3 Documentation » Scope Naming]: https://www.sublimetext.com/docs/3/scope_naming.html
[ST3 Documentation » Syntax Definitions]: https://www.sublimetext.com/docs/3/syntax.htm