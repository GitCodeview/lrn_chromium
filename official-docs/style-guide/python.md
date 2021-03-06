
# Chromium Python Style Guide

**For other languages, please see the [Chromium style guides](README.md).**

Chromium follows [PEP-8](https://www.python.org/dev/peps/pep-0008/).

It is also encouraged to follow advice from [Google&#39;s Python Style Guide](https://google.github.io/styleguide/pyguide.html), which is a superset of PEP-8.

See also:
- [Chromium OS Python Style Guide](https://sites.google.com/a/chromium.org/dev/chromium-os/python-style-guidelines.
- [Blink Python Style Guide](blink-python.md)

## Contents
- [Chromium Python Style Guide](#chromium-python-style-guide)
  - [Contents](#contents)
  - [Our Previous Python Style](#our-previous-python-style)
  - [Making Style Guide Changes](#making-style-guide-changes)
  - [Tools](#tools)
    - [pylint](#pylint)
    - [YAPF](#yapf)
      - [Bugs](#bugs)
      - [Editor Integration](#editor-integration)
  
## Our Previous Python Style

Chromium used to differ from PEP-8 in the following ways:
- Use two-space indentation instead of four-space indentation.
- Use `CamelCase()` method and function names instead of `unix_hacker_style()` names.
- 80 character line limits rather than 79.
New scripts should not follow these deviations, but they should be followed when making changes to files that follow them.

## Making Style Guide Changes

You can propose changes to this style guide by sending an email to `python@chromium.org`. Ideally, the list will arrive at some consensus and you can request review for a change to this file. If there&#39;s no consensus, [`//styleguide/python/OWNERS`](https://chromium.googlesource.com/chromium/src/+/master/styleguide/python/OWNERS) get to decide.

## Tools

### pylint

[Depot tools](http://commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools.html) contains a local copy of pylint, appropriately configured.
- Directories need to opt into pylint presumbit checks via: `input_api.canned_checks.RunPylint()`.

### YAPF

[YAPF](https://github.com/google/yapf) is the Python formatter used by:

Directories can opt into enforcing auto-formatting by adding a `.style.yapf` file with the following contents:

Entire files can be formatted (rather than just touched lines) via:

YAPF has gotchas. You should review its changes before submitting. Notably:
- It does not re-wrap comments.
- It won&#39;t insert characters in order wrap lines. You might need to add ()s yourself in order to have to wrap long lines for you.
- It formats lists differently depending on whether or not they end with a trailing comma.
#### Bugs
- Are tracked here: [https://github.com/google/yapf/issues](https://github.com/google/yapf/issues).
- For Chromium-specific bugs, please discuss on `python@chromium.org`.
#### Editor Integration

See: [https://github.com/google/yapf/tree/master/plugins](https://github.com/google/yapf/tree/master/plugins)
