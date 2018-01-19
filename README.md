# Determinator tests

⚠️ This repository is still being built, the full suite of tests do not exist in here yet ⚠️

This repo contains example inputs and outputs for the Florence/Determinator suite of tools for feature flags and A/B tests.

The `examples.json` file holds all of the examples which need to be executed. Its structure describes:

1. the feature file which should be loaded (referencing files within this repo)
2. the parameters which should be passed into the determinator function being tested
3. the expected results

## An example

This example shows a single test case:

```json
[
  {
    "section": "A description of this section of tests",
    "examples": [
      {
        "why": "A full-sentence explanation of why these arguments result in the specified response.",
        "feature": "path/to/a/feature/definition.json",
        "id": "the id parameter should be set to this value",
        "guid": "the guid parameter should be set to this value",
        "properties": {
          "these": ["are", "the", "properties"],
          "that": ["should", "be", "passed"],
          "into": ["the", "determinator", "function"]
        },
        /* absence of the following key is equivalent to "error": false */
        "error": true,
        /* This key will be absent if "error": true */
        "returns": "the expected result of the determination"
      }
    ]
  }
]
```

## Usage

In your determinator library you can add this repo as a submodule in an appropriate directory, then iterate through the items in the object array in `examples.json` and execute one test for each, potentially printing out the `why` if the test fails.

```bash
# Create a folder called `standard_cases` in the `spec` folder, and ensure it has the contents of this repo in it:
$ git submodule add https://github.com/deliveroo/determinator-standard-tests spec/standard_cases
```

If all of these tests pass then the core determination of the library is compatible with Florence and the other Determinator libraries.

## Updating

It's likely that new test cases will need to be added to this repository as Florence grows. Updating this git submodule will ensure you have the latest version of the tests which should be run.

There is also a `VERSION` file in the root of this repository which contains only a [Semantic Version](https://semver.org) number. As usual:

- a bump in the first number (major release) represents a breaking change — you will need to make some changes to the way your tests are run.
- a bump in the second number (minor release) means that tests have been added or improved, but they're still in the same format. No changes will need to be made to your test code.
- a bump in the third number (patch release) means that some superficial changes have been made, eg. better 'why' explanations, or improvements to the README here.

You may find it useful to hardcode the major version of the tests you have built against into your test suite, so that if it does not match you can fail your suite with a useful error.
