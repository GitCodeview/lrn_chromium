# Privacy Budget: Code Locations

Following on from the high level [Privacy
Budget](https://github.com/bslassey/privacy-budget) explainer, the current
implementation focuses on measuring the identifiability of various web exposed
features. Hence the word `Identifiability` occurs often in the code and
documentation.

This document focuses on code layout for Privacy Budget. Concepts and background
for the identifiability study are out of scope.

TODO(asanka): Link to study documents once they are checked in.

## Core Metrics and Aggregation

Locations:

* [`third_party/blink/public/common/privacy_budget`](../third_party/blink/public/common/privacy_budget)
* [`third_party/blink/common/privacy_budget`](../third_party/blink/common/privacy_budget)

Includes:

* Core logic and primitives for constructing identifiability metrics.

  This is what one would use when reporting identifiability study samples.
  Centralized logic makes it easier to construct consistent and stable samples.

* Per-process aggregation of metrics.

  Aggregation minimizes the amount of information being communicated across
  process boundaries.

The code in this directory is shared across `//content`, `//chrome`, and
`//third_party/blink`. Hence its placement in `blink/public/common`.

In addition, this directory also contains logic for per-process aggregation of
metrics so that they can be efficiently communicated across process boundaries.

## Static study settings

Locations:

* [`chrome/common/privacy_budget`](../chrome/common/privacy_budget)

Logic for accessing per-session settings based on externally supplied field
trial configurations. The full set of externally controlled settings are
in
[`privacy_budget_features.h`](../chrome/common/privacy_budget/privacy_budget_features.h).

At a high level, these settings control such things as:

* Whether the study is active.
* Which identifiable surfaces should *not* be sampled.
* Parameters for how surfaces are selected for sampling.

Both the browser and the renderer need to access these settings. The browser
needs them for filtering and reporting. The renderer needs them to avoid
sampling surfaces where sampling itself is harmful for performance or stability
reasons.

## Persistent study state and reporting

Locations:
* [`chrome/browser/privacy_budget`](../chrome/browser/privacy_budget)

Per-client state is primarily used and exposed by `IdentifiabilityStudyState`
([Source](../chrome/browser/privacy_budget/identifiability_study_state.h)).

