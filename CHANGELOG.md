# CHANGELOG

### 2018-04-14:3

- `Alan.sublime-syntax` v0.0.5:
    + Bug Fix: __String__ containing 2 escaped DQ inside (`"""""`) was ending string prematurely
    + [`syntax_test_Strings.alan`][test_Strings] (_**now succeeds**_)
- Now __empty strings__ get additional `empty` scope:

    ```
    string.quoted.double.empty.alan
    ```

### 2018-04-14:2

- Added `CHANGELOG.md`
- Added [`TODO.md`](./TODO.md)
- Added [`/tests/`][tests] folder for automated testing syntax scopes:
    + [`syntax_test_Strings.alan`][test_Strings] (_**fails!!!**_)


[tests]: ./tests/ "See 'tests' folder"
[test_Strings]: ./tests/syntax_test_Strings.alan "Open file..."

### 2018-04-14:1

- First commit on GitHub
- `Alan.sublime-syntax` v0.0.4