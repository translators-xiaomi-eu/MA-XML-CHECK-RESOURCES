# What is this for?

- Languages.xml - contains all information about the languages available in xiaomi.eu multi-language ROMS.<br>

- /MIUIvX/MIUIvX_filter.yaml - contains filtering information, that is used to automatically filter untranslatable strings from repositories .<br>

Files are used by <a href="https://github.com/Redmaner/MA-XML-CHECK" target="_blank">MA-XML-CHECK</a><br>

## Languages.xml
- check: there are four options possible
- --> false = language will not be checked
- --> basic = basic check (syntax errors, doubles, apostrophe)
- --> normal = basic check + untranslateable strings
- --> full = normal check + array items
- name: name of the language
- iso: ISO code of the language
- url: link to the repository on github/bitbucket
- git: ssh to the repository on github/bitbucket
- branch: branch used on github/bitbucket

## filter.yaml

### yaml spec 
Filter files are drafted using the yaml specification. Always check that edits of a filter.yaml are in accordance with the yaml spec. Use a yaml linter for this. See for example https://jsonformatter.org/yaml-validator 

### Directives 
The filter file provides 6 directives that can be used to appy filtering:
1. _arrays_key_rules_: this directive contains filter rules for array names. 
2. _arrays_value_rules_: this directive contains filter rules for array values.
3. _plurals_key_rules_: this directive contains filter rules for plural names.
4. _plurals_value_rules_: this directive contains filter rules for plural values.
5. _strings_key_rules_: this directive conains filter rules for string names.
6. _strings_key_values_: this directive contains filter rules for string values.

### Applications
All directives are split into application names. With the exception off "all" which applies the defined filter to all applications. 

### Filter modes 
The filter supports 3 filter modes:
1. _contains_: the value contains the specified match, anywhere in the value
2. _prefix_: the value starts with the specified match (prefix).
3. _suffix_: the value ends with the specified match (suffix).

### Example 1: filter all applications strings.xml with values starting with @string
```
strings_value_rules:
  all:
  - match: '@string'
    mode: prefix
```

### Example 2: filter all applications arrays.xml with names ending with _values
```
arrays_key_rules:
  all:
  - match: _values
    mode: suffix
```

### Example 3: filter all MiuiCamera.apk strings.xml with names containing _default
```
strings_key_rules:
  MiuiCamera.apk:
  - match: _default
    mode: contains
```
