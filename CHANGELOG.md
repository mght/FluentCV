CHANGELOG
=========

## v1.9.0-beta

*Welcome to the first new version of FluentCV in over a year. The purpose of
this release is to gather feature enhancements and bug fixes collected over the
past 18 months as we reorganize, rebrand, and prepare for the 2.0 release.*

### Added

- Support for **private resume fields**. Mark any non-leaf node in your resume
JSON with the `private` property and it will be omitted from outbound resumes.

    ```json
    "employment": {
      "history": [
        {
          "employer": "Acme Real Estate"
        },
        {
          "employer": "Area 51 Alien Research Laboratory",
          "private": true
        },
        {
          "employer": "H&R Block"
        }
      ]
    }
    ```
- Support for **PDF generation through WeasyPrint** in addition to the
existing support for wkhtmltopdf and PhantomJS.

- Theme authors can now develop and package **custom Handlebars theme helpers**
via the `helpers` key of the `theme.json` file (FRESH themes only) (#158).

- Help system has been updated with a `HELP` command and dedicated help pages
for each command.

- Theme authors can **relocate theme assets** with the `baseFolder` property in
the FRESH `theme.json`.

- FluentCV will now **validate the options file** (if any) loaded with `-o`
or `--options` and warn the user if necessary.

- Ability to **disable Handlebars encoding/escaping** of resume fields with
`--no-escape`.

- Introduced the [fresh-test-themes][ftt] project as a repository for simple,
test-only resume themes in the FRESH format.

### Changed

- Dropped support for Node 4 and 5. FluentCV officially runs on Node 6+.

- The FRESCA project has been renamed to [fresh-resume-schema][fresca]. FRESCA
is still the nickname.

- The FluentCV web page has moved to https://fluentdesk.com/fluentcv.

### Fixed

- Fixed an issue that would cause the `convert` command to detect the inbound
resume type (FRESH or JRS) incorrectly (#162).

- Fixed an issue where generating new JRS resumes would cause a `null` or
`undefined` error (#165).

- Fixed an issue preventing mixed-case themes from being loaded (#172).

- Fixed an issue requiring JSON Resume themes contain `json-resume-theme` in the
theme path (#173).

- Fixed an issue that would cause strange `@@@@` characters to appear in
generated resumes (#207, #168, #198).

- Fixed an issue that would cause resume generation to hang after a JSON Resume
themed resume was generated (#182).

- Fixed an issue that would cause nothing to be generated for Markdown (.md)
formats (#179).

- Fixed an issue that would prevent a JRS resume from being converted to FRESH
via the `convert` command (#180).

- Fixed an issue that would cause broken styling for JSON Resume themes (#155).

### Internal

- Tests: fixed resume duration tests (#181).

- Style: move to

## v1.8.0

### Added

- Updated `Awesome` theme to latest version of [Awesome-CV][acv].

- Introduced new theme helpers: `pad`, `date`.

### Fixed

- Fixed an issue where the `Awesome` theme wouldn't correctly generate LaTeX
outputs (#138).

- Emit a line number for syntax errors around embedded newlines in JSON strings
(#137).

- Fix several PDF / PNG generation errors (#132, others).

- Display a more helpful error message when attempting to generate a PDF or PNG
on a machine where PhantomJS and/or wkhtmltopdf are either not installed or
not path-accessible.

- Fixed an issue that would cause long-running PDF/PNG generation to fail in
certain environments.

- Fixed an issue involving an unhelpful spawn-related exception (#136).

### Internal

- JSHint will no longer gripe at the use of `== null` and `!= null` in
CoffeeScript transpilation.

- Introduced [template-friendly Awesome-CV fork][awefork] to isolate template
expansion logic & provide better durability for FluentCV's `awesome` theme.

- Fixed a couple temporary regressions (#139, #140) on the dev branch.

- Additional tests.

- Minor breaking FluentCV API changes.

## v1.7.4

### Added

- [Build instructions](https://github.com/hacksalot/FluentCV/blob/master/BUILDING.md).

### Changed

- More precise date handling.

### Fixed

- Issue with incomplete PDF generation (#127).

- Issue with building JSON Resume themes (#128).

- Issue with generating `.json` output format by itself (#97).

## v1.7.3

### Fixed

- Issue with generated PDFs being chopped off and displaying a mysterious sequence of numbers of unknown and possibly alien origin (#127).

- Unsightly border on Modern:PDF.

- Modern|Positive:PDF formats now correctly reference their PDF-specific CSS files.

- `Incorrect helper use` warning in Positive:DOC.

## v1.7.2

### Changed

- Interim release supporting FluentCV Desktop.

### Internal

- Moved [HackMyCore](https://github.com/hacksalot/HackMyCore) dependency to
submodule.

## v1.7.1

### Changed

- Caffeinate. CoffeeScript now used throughout
[FluentCV](https://github.com/hacksalot/FluentCV) and
[HackMyCore](https://github.com/hacksalot/HackMyCore); generated JavaScript
lives in `/dist`.

### Fixed

- Issue with generating a single PDF with the `.pdf` extension (#99).

## v1.7.0

### Changed

- [Internal] Relocated HMR processing code to the
[HackMyCore](https://github.com/hacksalot/HackMyCore) project. Shouldn't affect
normal use.

## v1.6.0

### Major Improvements

- Better consistency and coverage for all FRESH resumes and themes ([#45][i45]).

- Initial support for overridable fonts in FRESH themes. Like a particular
theme, but want to change the typography? The specific fonts used by a theme
can now be overridden by the user. (FRESH themes only).

- New resume sections! Support for `projects` and `affiliation` resume sections
for technical and creative projects and memberships / clubs / associations,
respectively ([#92][i92]).

- New command! `PEEK` at any arbitrary field or entry on your `.json` resume.

### Added

- Improved handling of start and end dates on `employment`, `projects`,
`education`, and other sections with start/end dates.

- Support for an `.ignore` property on any FRESH or JSON Resume section or field.
Ignored properties will be treated by FluentCV as if they weren't present.

- Emit extended status and error info with the `--debug` or `-d` switch.

- The `-o` or `--options` switch can now handle either the path to a **JSON
settings file** or **raw JSON/JavaScript**. Since the JSON double quote syntax
is a bit cumbersome from the command line, FluentCV accepts regular
JavaScript object literal syntax:

        fluentcv build resume.json -o "{ theme: 'compact', silent: 'true' }"

- Ability to disable sorting of resume sections (employments, projects, etc.)
with the `--no-sort` option. HMR will respect the order of items as they appear
in your resume `.json` file.

- Improvements to the starter resume emitted by `fluentcv new`.

- Theme Authoring: Annotated the HTML and MS Word (XML) formats of the Modern
theme for FRESH theme authors.

- Theme Authoring: Support for templatized CSS files in FRESH themes. CSS files
are now expanded via Handlebars or Underscore prior to copying to the
destination.

- Added CHANGELOG.md (this file).

### Changed

- Rewrote the FluentCV man/help page.

- Minor incremental updates to the [FRESCA][fresca] schema.

- PDF generation now uses asynchronous `spawn()` which has better compatibility
with old or boutique versions of Node.js.

- Refactored colors in FluentCV output. Errors will now display as red,
warnings as yellow, successful operations as green, and informational messages
as cyan.

- Theme messages and usage tips will no longer display during resume generation
by default. Use the `--tips` option to view them.

- The `--no-tips` option (default: false) has been replaced with the `--tips`
option, also defaulting to false.

- Removed the `hello-world` theme from the [prebuilt themes][themes] that ship
with FluentCV. It can be installed separately from NPM:

  ```bash
  npm install fresh-theme-hello-world
  fluentcv resume.json -t node_modules/fresh-theme-hello-world
  ```

- sd

### Fixed

- PDF generation issues on older versions of Node.

- Stack traces not being emitted correctly.

- Missing `speaking` section will now appear on generated resumes ([#101][i101]).

- Incomplete `education` details will now appear on generated resumes ([#65][i65]).

- Missing employment end date being interpreted as "employment ends today"
([#84][i84]).

- Merging multiple source resumes during `BUILD` sometimes fails.

- Document `--pdf` flag in README ([#111][i111]).

### Internal

- Logging messages have been moved out of core FluentCV code ahead of
localization support.

- All FluentCV console output is described in `msg.yml`.

- Relaxed pure JavaScript requirement. CoffeeScript will now start appearing
in FluentCV and FluentCV sources!

- Additional tests.

## v1.5.2

### Fixed

- Tweak stack trace under `--debug`.

## v1.5.1

### Added

- Preliminary support for `-d` or `--debug` flag. Forces FluentCV to emit a stack trace under error conditions.

## v1.5.0

### Added

- FluentCV now supports **CLI-based generation of PDF formats across multiple engines (Phantom, wkhtmltopdf, etc)**. Instead of talking to these engines over a programmatic API, as in prior versions, FluentCV 1.5+ speaks to them over the same command-line interface (CLI) you'd use if you were using these tools directly.

- FluentCV will now (attempt to) **generate a PDF output for JSON Resume themes** (in addition to HTML).

- Minor README and FAQ additions.

### Changed

- **Cleaner, quicker installs**. Installing FluentCV with `npm install fluentcv -g` will no longer trigger a lengthy, potentially error-prone install for Phantom.js and/or wkhtmltopdf for PDF support. Instead, users can install these engines externally and HMR will use them when present.

- Minor error handling improvements.

### Fixed

- Fixed an error with generating specific formats with the `BUILD` command (#97).

- Fixed numerous latent/undocumented bugs and glitches.

## v1.4.2

### Added

- Introduced [FAQ](https://github.com/hacksalot/FluentCV/blob/master/FAQ.md).
- Additional README notes.

## v1.4.1

### Added

- `fluentcv new` now generates a [valid starter resume with sample data](https://github.com/fluentdesk/fresh-resume-starter).

### Fixed

- Fixed warning message when `fluentcv new` is run without a filename.

## v1.4.0

### Added

- **"Projects" support**: FRESH resumes and themes can now store and display
open source, commercial, private, personal, and creative projects.
- **New command: ANALYZE**. Inspect your resume for gaps, keyword counts, and other metrics. (Experimental.)
- **Side-by-side PDF generation** with Phantom and wkhtmltopdf. Use the `--pdf` or `-p` flag to pick between `phantom` and `wkhtmltopdf` generation.
- **Disable PDF generation** with the `--pdf none` switch.
- **Inherit formats between themes**. Themes can now inherit formats (Word, HTML, .txt, etc.) from other themes. (FRESH themes only.)
- **Rename resume sections** to different languages or wordings.
- **Specify complex options via external file**. Use with the `-o` or `--opts` option.
- **Disable colors** with the `--no-color` flag.
- **Theme messages and usage tips** instructions will now appear in the default FluentCV output for the `build` command. Run `fluentcv build resume.json -t awesome` for an example. Turn off with the `--no-tips` flag.
- **Treat validation errors as warnings** with the `--assert` switch (VALIDATE command only).

### Fixed

- Fixed a minor glitch in the FRESCA schema.
- Fixed encoding issues in the `Highlights` section of certain resumes.
- Fix behavior of `-s` and `--silent` flags.

### Changed

- PDF generation now defaults to Phantom for all platforms, with `wkhtmltopdf`
accessible with `--pdf wkhtmltopdf`.
- Resumes are now validated, by default, prior to generation. This
behavior can be disabled with the `--novalidate` or `--force` switch.
- Syntax errors in source FRESH and JSON Resumes are now captured for all
commands.
- Minor updates to README.
- Most themes now inherit Markdown and Plain Text formats from the **Basis**
theme.

### Internal

- Switched from color to chalk.
- Command invocations now handled through commander.js.
- Improved FRESH theme infrastructure (more partials, more DRY).

## v1.3.1

### Added

- Add additional Travis badges.

### Fixed

- Fix extraneous console log output when generating a FRESH theme to MS Word.
- Fix Travis tests on `dev`.

## v1.3.0

### Added

- **Local generation of JSON Resume themes**. To use a JSON Resume theme, first install it with `npm install jsonresume-theme-[blah]` (most JSON Resume themes are on NPM). Then pass it into FluentCV via the `-t` parameter:

    `fluentcv BUILD resume.json TO out/somefile.all -t node_modules/jsonresume-theme-classy`
- **Better Markdown support.** FluentCV will start flowing basic Markdown styles to JSON Resume (HTML) themes. FRESH's existing Markdown support has also been improved.
- **.PNG output formats** will start appearing in themes that declare an HTML output.
- **Tweak CSS embedding / linking via the --css option** (`<style></style>` vs `<link>`). Only works for HTML (or HTML-driven) formats of FRESH themes. Use `--css=link` to link in CSS assets and `--css=embed` to embed the styles in the HTML document. For example `fluentcv BUILD resume.json TO out/resume.all --css=link`.
- **Improved Handlebars/Underscore helper support** for FRESH themes. Handlebars themes can access helpers via `{{helperName}}`. Underscore themes can access helpers via the `h` object.

### Changed

- **Distinguish between validation errors and syntax errors** when validating a FRESH or JRS resume with `fluentcv validate <blah>`.
- **Emit line and column info** for syntax errors during validation of FRESH and JRS resumes.
- **FRESH themes now embed CSS into HTML formats by default** so that the HTML resume output doesn't have an external CSS file dependency by default. Users can specify normal linked stylesheets by setting `--css=link`.
- **Renamed fluent-themes repo to fresh-themes** in keeping with the other parts of the project.

### Fixed

- Fix various encoding errors in MS Word outputs.
- Fix assorted FRESH-to-JRS and JRS-to-FRESH conversion glitches.
- Fix error when running HMR with no parameters.
- Other minor fixes.

## v1.3.0-beta

- Numerous changes supporting v1.3.0.

## v1.2.2

### Fixed

- Various in-passing fixes.

## v1.2.1

### Fixed

- Fix `require('FRESCA')` error.
- Fix `.history` and `.map` errors on loading incomplete or empty JRS resumes.

### Added

- Better test coverage of incomplete/empty resumes.

## v1.2.0

### Fixed

- Fixed the `new` command: Generate a new FRESH-format resume with `fluentcv new resume.json` or a new JSON Resume with `fluentcv new resume.json -f jrs`.

### Added

- Introduced CLI tests.

## v1.1.0

### Fixed

- MS Word formats: Fixed skill coloring/level bug.

### Changed

- Make the `TO` keyword optional. If no `TO` keyword is specified (for the `build` and `convert` commands), HMR will assume the last file passed in is the desired output file. So these are equivalent:

    ```shell
    fluentcv BUILD resume.json TO out/resume.all
    fluentcv BUILD resume.json out/resume.all
    ```

    `TO` only needs to be included if you have multipled output files:

    ```shell
     fluentcv BUILD resume.json TO out1.doc out2.html out3.tex
    ```

## v1.0.1

### Fixed

- Correctly generate MS Word hyperlinks from Markdown source data.

## v1.0.0

- Initial public 1.0 release.

[i45]: https://github.com/hacksalot/FluentCV/issues/45
[i65]: https://github.com/hacksalot/FluentCV/issues/65
[i84]: https://github.com/hacksalot/FluentCV/issues/84
[i92]: https://github.com/hacksalot/FluentCV/issues/92
[i101]: https://github.com/hacksalot/FluentCV/issues/101
[i111]: https://github.com/hacksalot/FluentCV/issues/111
[fresca]: https://github.com/fresh-standard/fresh-resume-schema
[themes]: https://github.com/fresh-standard/fresh-themes
[awefork]: https://github.com/fluentdesk/Awesome-CV
[acv]: https://github.com/posquit0/Awesome-CV
[ftt]: https://github.com/fresh-standard/fresh-test-themes
