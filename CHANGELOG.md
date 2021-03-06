
## Unreleased

### breaking changes

### enhancements
  - [JS] Allow extending of translation files ([#354](https://github.com/fnando/i18n-js/pull/354))

### bug fixes



## 3.0.0.rc11

### breaking changes

### enhancements

### bug fixes

- [Ruby] Handle fallback locale without any translation properly ([#338](https://github.com/fnando/i18n-js/pull/338))
- [Ruby] Prevent translation entry with null value to override value in fallback locale(s), if enabled ([#334](https://github.com/fnando/i18n-js/pull/334))


## 3.0.0.rc10

### breaking changes

- [Ruby] In `config/i18n-js.yml`, if you are using `%{locale}` in your filename and are referencing specific translations keys, please add `*.` to the beginning of those keys. ([#320](https://github.com/fnando/i18n-js/pull/320))
- [Ruby] The `:except` option to exclude certain phrases now (only) accepts the same patterns the `:only` option accepts

### enhancements

- [Ruby] Make handling of per-locale and not-per-locale exporting to be more consistent ([#320](https://github.com/fnando/i18n-js/pull/320))
- [Ruby] Add option `sort_translation_keys` to sort translation keys alphabetically ([#318](https://github.com/fnando/i18n-js/pull/318))

### bug fixes

- [Ruby] Fix fallback logic to work with not-per-locale files ([#320](https://github.com/fnando/i18n-js/pull/320))


## 3.0.0.rc9

### enhancements

- [JS] Force currency number sign to be at first place using `sign_first` option, default to `true`
- [Ruby] Add option `namespace` & `pretty_print` ([#300](https://github.com/fnando/i18n-js/pull/300))
- [Ruby] Add option `export_i18n_js` ([#301](https://github.com/fnando/i18n-js/pull/301))
- [Ruby] Now the gem also detects pre-release versions of `rails`
- [Ruby] Add `:except` option to exclude certain phrases or groups of phrases from the
  outputted translations ([#312](https://github.com/fnando/i18n-js/pull/312))
- [JS] You can now set `I18n.missingBehavior='guess'` to have the scope string output as text instead of of the
  "[missing `scope`]" message when no translation is available.  
  Combined that with `I18n.missingTranslationPrefix='SOMETHING'` and you can
  still identify those missing strings.
  ([#304](https://github.com/fnando/i18n-js/pull/304))

### bug fixes

- [JS] Fix missing translation message when scope is passed in options
- [Ruby] Fix save cache directory verification when path is a symbolic link ([#329](https://github.com/fnando/i18n-js/pull/329))


## 3.0.0.rc8

### enhancements

- Add support for loading via AMD and CommonJS module loaders ([#266](https://github.com/fnando/i18n-js/pull/266))
- Add `I18n.nullPlaceholder`  
  Defaults to I18n.missingPlaceholder (`[missing {{name}} value]`)  
  Set to `function() {return "";}` to match Ruby `I18n.t("name: %{name}", name: nil)`
- For date formatting, you can now also add placeholders to the date format, see README for detail
- Add fallbacks option to `i18n-js.yml`, defaults to `true`

### bug fixes

- Fix factory initialization so that the Node/CommonJS branch only gets executed if the environment is Node/CommonJS
  (it currently will execute if module is defined in the global scope, which occurs with QUnit, for example)
- Fix pluralization rules selection for negative `count` (e.g. `-1` was lead to use `one` for pluralization) ([#268](https://github.com/fnando/i18n-js/pull/268))
- Remove check for `Rails.configuration.assets.compile` before telling Sprockets the dependency of translations JS file  
  This might be the reason of many "cache not expired" issues  
  Discovered/reported in #277

## 3.0.0.rc7

### enhancements

- The Rails Engine initializer is now named as `i18n-js.register_preprocessor` (https://github.com/fnando/i18n-js/pull/261)
- Rename `I18n::JS.config_file` to `I18n::JS.config_file_path` and make it configurable  
  Expected a `String`, default is still `config/i18n-js.yml`
- When running `rake i18n:js:export`, the `i18n.js` will also be exported to `I18n::JS.export_i18n_js_dir_path` by default
- Add `I18n::JS.export_i18n_js_dir_path`  
  Expected a `String`, default is `public/javascripts`  
  Set to `nil` will disable exporting `i18n.js`

### bug fixes

- Prevent toString() call on `undefined` when there is a missing interpolation value
- Added support for Rails instances without Sprockets object (https://github.com/fnando/i18n-js/pull/241)
- Fix `DEFAULT_OPTIONS` in `i18n.js` which contained an excessive comma
- Fix `nil` values are exported into JS files which causes strange translation error
- Fix pattern to replace all escaped $ in I18n.translate
- Fix JS `I18n.lookup` modifies existing locales accidentally

## 3.0.0.rc6

### enhancements

- You can now assign `I18n.locale` & `I18n.default_locale` before loading `i18n.js` in `application.html.*`
  (merged to `i18n-js-pika` already)
- You can include ERB in `config/i18n-js.yml`(https://github.com/fnando/i18n-js/pull/224)
- Add support for +00:00 style time zone designator (https://github.com/fnando/i18n-js/pull/167)
- Add back rake task for export (`rake i18n:js:export`)
- Not overriding translation when manually run `I18n::JS.export` (https://github.com/fnando/i18n-js/pull/171)
- Move missing placeholder text generation into its own function (for easier debugging) (https://github.com/fnando/i18n-js/pull/169)
- Add support for milliseconds (`lll` in `yyyy-mm-ddThh:mm:ss.lllZ`) (https://github.com/fnando/i18n-js/pull/192)
- Add back i18n-js.yml config file generator : `rails generate i18n:js:config` (https://github.com/fnando/i18n-js/pull/225)

### bug fixes

- `I18n::JS.export` no longer exports locales other than those in `I18n.available_locales`, if `I18n.available_locales` is set
- I18.t supports the base scope through the options argument
- I18.t accepts an array as the scope
- Fix regression: asset not being reloaded in development when translation changed
- Requires `i18n` to be `~> 0.6`, `0.5` does not work at all
- Fix using multi-star scope with top-level translation key (https://github.com/fnando/i18n-js/pull/221)


## Before 3.0.0.rc5

- Things happened.
