# Alan Syntax Notes

Some working notes on how to scope the Alan syntax elements.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [Notes on Identifiers](#notes-on-identifiers)
    - [RegEx Aproach](#regex-aproach)
        - [Known Issues](#known-issues)
    - [Alan Sources BNF References](#alan-sources-bnf-references)
- [Syntax Scopes](#syntax-scopes)
    - [Classes](#classes)
        - [Class Attributes](#class-attributes)
        - [Pre-Defined Alan Classes](#pre-defined-alan-classes)
    - [Special Keywords](#special-keywords)
- [Alan Keywords](#alan-keywords)
- [Reference Links](#reference-links)

<!-- /MarkdownTOC -->

-----

# Notes on Identifiers

A valid identifier in Alan has the following pattern:

```bnf
IDENTIFIER : LETTER ( LETTER | DIGIT | '_' )*
```

... where `LETTER` means:

- any char in the Ascii range `a`..`z`
- any char in the Ascii range `A`..`Z`
- any char in the Unicode range `U+00E0`..`U+00F6` (`à`..`ö`)
- any char in the Unicode range `U+00F8`..`U+00FE` (`ø`..`þ`)


The two Unicode ranges represent characters from the [Latin-1 Supplement] ([ISO-8859-1]), which is the default encoding expected by Alan.

Here is the full [ISO-8859-1] subset of valid characters in an identifier:

    0 1 2 3 4 5 6 7 8 9
    A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
    _
    a b c d e f g h i j k l m n o p q r s t u v w x y z
    à á â ã ä å æ ç è é ê ë ì í î ï ð ñ ò ó ô õ ö ø ù ú û ü ý þ

## RegEx Aproach

To simplify, the Unicode range can be described as the set `U+00E0`..`U+00FE` minus `U+00F7` (_obelus_ symbol: `÷`).

The valid letters can be represented via the following RegExs, in order of simplification:

1. `[a-zA-Z\u00e0-\u00f6\u00f8-\u00fe]`
2. `[a-zA-Z\u00e0-u00fe&&[^\u00f7]]]`
3. `[a-zA-Zà-þ&&[^÷]]`

For some reason, RegExs __1__ and __2__ don't work in Sublime Text syntax files, while the third one does.

The full `identifier` pattern is: `(\b['a-zA-Zà-þ&&[^÷]][0-9_'a-zA-Zà-þ&&[^÷]]*\b)`, which in the sytnax source is represent through variables:

```yaml
variables:
  LETTER: 'a-zA-Zà-þ&&[^÷]'
  ID: '(\b[{{LETTER}}][0-9_{{LETTER}}]*\b)'
```

### Known Issues

While the above RegEx does a fairly good job at matching valid identifiers and ignoring malformed ones, the presence of invalid symbols characters (including `÷`) in the middle of a word will cause the syntax parser to split the word — because most symbols satisfy the boundry condition of `\b`. Therefore, an invalid identifer like `abc÷123` will be actually parsed as:

- `abc` — identifier
- `÷` — stray symbol
- `123` — numeric constant

There isn't much I can do about it; besides, we don't expect users to employ symbols in identifiers — if they chose to do so, at their own peril!

## Alan Sources BNF References

The BNF definion of `Identifier` in "`alan.g`" source (line 15):

```bnf
fragment IDENTIFIER : LETTER ( LETTER | DIGIT | '_' )* ;
```

Also, in "`alan.g`" (line 9):

```bnf
fragment LETTER : 'A' .. 'Z' | 'a' .. 'z' | '_' | '$' | '\u00e0'..'\u00f6' | '\u00f8'..'\u00fe' ;
```

> __NOTE__ — The latter BNF definition might lead to assume that `_` and `$` are also valid characters in the LETTER range, but it is not so (these don't reflect the actual validations carried out by the Alan compiler in real use). The `$` symbol is never a valid character in identifiers, and the `_` can't be used as the first character of an identifier.

# Syntax Scopes

A few notes about Alan language syntax elements and their scoping.

## Classes

Class scopes:

- `entity.name.class`
- `entity.name.class.forward-decl`
- `entity.other.inherited-class`

### Class Attributes

> Fields, properties, members and attributes of a class or other data structure should use:
> 
>     variable.other.member


### Pre-Defined Alan Classes

There are eight pre-defined (hard-coded) Alan classes:

- `entity`
    + `thing`
        * `object`
        * `actor` \*
    + `location` \*
    + `literal`
        * `string`
        * `integer`

> __NOTE 1__ — `actor` and `location` are found in the [Alan Keywords] list, but not the other hard-coded classes.

<!-- separator -->

> __NOTE 2__ — `hero` doesn't appear in the [Alan Keywords] list either, although it's a hard-coded instance. 

## Special Keywords

`THIS` should be scoped as `variable.language` (for reserved language variables like `this`, `super`, `self`, etc.)

# Alan Keywords

[Alan Keywords]: #alan-keywords

There are 123 keywords in Alan 3 language, as mentioned in the _Reference Manual_ (Appendix D.2 Keywords).

|              |             |               |              |              |              |
|--------------|-------------|---------------|--------------|--------------|--------------|
| `actor`      | `add`       | `after`       | `an`         | `and`        | `are`        |
| `article`    | `at`        | `attributes`  | `before`     | `between`    | `by`         |
| `can`        | `cancel`    | `character`   | `characters` | `check`      | `container`  |
| `contains`   | `count`     | `current`     | `decrease`   | `definite`   | `depend`     |
| `depending`  | `describe`  | `description` | `directly`   | `do`         | `does`       |
| `each`       | `else`      | `elsif`       | `empty`      | `end`        | `entered`    |
| `event`      | `every`     | `exclude`     | `exit`       | `extract`    | `first`      |
| `for`        | `form`      | `from`        | `has`        | `header`     | `here`       |
| `if`         | `import`    | `in`          | `include`    | `increase`   | `indefinite` |
| `initialize` | `into`      | `is`          | `isa`        | `it`         | `last`       |
| `limits`     | `list`      | `locate`      | `location`   | `look`       | `make`       |
| `max`        | `mentioned` | `message`     | `min`        | `name`       | `near`       |
| `nearby`     | `negative`  | `no`          | `not`        | `of`         | `off`        |
| `on`         | `only`      | `opaque`      | `option`     | `options`    | `or`         |
| `play`       | `prompt`    | `pronoun`     | `quit`       | `random`     | `restart`    |
| `restore`    | `save`      | `say`         | `schedule`   | `score`      | `script`     |
| `set`        | `show`      | `start`       | `step`       | `stop`       | `strip`      |
| `style`      | `sum`       | `synonyms`    | `syntax`     | `system`     | `taking`     |
| `the`        | `then`      | `this`        | `to`         | `transcript` | `until`      |
| `use`        | `verb`      | `visits`      | `wait`       | `when`       | `where`      |
| `with`       | `word`      | `words`       |              |              |              |


# Reference Links

- [ST3 Documentation » Scope Naming]
- [ST3 Documentation » Syntax Definitions]
- [TextMate Manual » Language Grammars]
    + [Scopes Naming Conventions]
- [TextMate Manual » Scope Selectors]
- [Latin-1 Supplement]
- [ISO-8859-1]


[ST3 Documentation » Scope Naming]: https://www.sublimetext.com/docs/3/scope_naming.html
[ST3 Documentation » Syntax Definitions]: https://www.sublimetext.com/docs/3/syntax.htm

[TextMate Manual » Language Grammars]: https://manual.macromates.com/en/language_grammars
[Scopes Naming Conventions]: https://manual.macromates.com/en/language_grammars#naming_conventions
[TextMate Manual » Scope Selectors]: http://manual.macromates.com/en/scope_selectors

[Latin-1 Supplement]: http://jrgraphix.net/r/Unicode/00A0-00FF
[ISO-8859-1]: https://en.wikipedia.org/wiki/ISO/IEC_8859-1
