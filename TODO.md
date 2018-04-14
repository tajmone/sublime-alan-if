# Sublime-Alan TODOs

Pending tasks and bugs list.


-----

**Table of Contents**

<!-- MarkdownTOC autolink="true" bracket="round" autoanchor="false" lowercase="only_ascii" uri_encoding="true" levels="1,2,3" -->

- [TODOs](#todos)
- [Bugs](#bugs)

<!-- /MarkdownTOC -->

-----

# TODOs

List of planned tasks and features:

- [x] Add [syntax test files][ST3Docs syntax test] to [`/tests/`][tests]:
    + [x] __Strings__:
        * [`syntax_test_Strings.alan`][test_Strings]
    + [ ] __Comments__
    + [ ] __Keywords__

[ST3Docs syntax test]: https://www.sublimetext.com/docs/3/syntax.html#testing

[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."

# Bugs

Known bugs which need fixing:

- [ ] __Strings__: two consecutive escaped DQs in the middle of a string prematurely end the string:

      ```
      "Enclose in double quotes ("""") what you want to say.".
      ```

      ... strings ends at `("""` and `") what` is treated as normal text.

      Currently the test file [`syntax_test_Strings.alan`][test_Strings] fails with:

      ```
      Packages/Alan/tests/syntax_test_strings.alan:32:36: [string.quoted.double.alan] does not match scope [source.alan]
      Packages/Alan/tests/syntax_test_strings.alan:32:37: [string.quoted.double.alan] does not match scope [source.alan]
      Packages/Alan/tests/syntax_test_strings.alan:32:38: [string.quoted.double.alan] does not match scope [source.alan]
      FAILED: 3 of 94 assertions in 1 files failed
      ```