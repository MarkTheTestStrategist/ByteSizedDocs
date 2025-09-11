 # Testing Project Instructions

These instructions define how ChatGPT should generate and format test cases for my projects. They ensure consistency, accuracy, and direct usability in Azure Test Plans.

## 🎯 Purpose

Standardise test case output when using ChatGPT.

Keep prompts clean, accurate, and relevant to the system under test.

Provide a style guide for formatting, naming, and structuring tests.

## 📝 Test Format

Use Given / When / Then format only.

Do not include Feature or Background.

Each step must be on its own new line.

Tests must be a single continuous block (no blank lines).

**Example**
```
Title: ➖ [Balance] Cannot be empty or null
Given a request to the CreateOrder endpoint with order_data.balance set to null
When the request is submitted
Then the request is rejected with a validation error for balance
And the card balance is unchanged
And no events are recorded in the system
```

## 🔖 Titles

Every test must have a title.

Title format: Title: [emoji] [Field/Feature] [Description].

Emoji conventions:

➕ = Positive test (valid input, expected success).

➖ = Negative test (invalid input, expected rejection).

➕➖ = Mixed positive and negative scenarios.

Titles should be factual and descriptive (no fluff).

## 🚫 Formatting Rules

Do not use tables.

Use “AND” or “OR” as plain text in steps when needed.

No blank lines between steps or tests.

Keep tests immediately usable (copy-paste ready for Azure Test Plans).

## 📂 Project Organisation

All testing instructions live inside a dedicated ChatGPT Project titled Testing.

This keeps the context “pure” and isolated from non-testing prompts.

## 🤝 Dual Instruction System

Written instructions (this file): the baseline rules for consistency.

Conversational refinements: adjustments made collaboratively with ChatGPT based on project needs (e.g., “always put each GWT step on a new line,” “no inline ANDs”).

This two-layer approach ensures both structure and flexibility:

Written instructions = foundation.

Conversational history = adaptation.

## ✅ Best Practices

Be precise with prompts—describe exact rules, constraints, and expected outputs.

Avoid vague wording that could let ChatGPT make assumptions.

Always review generated tests against specs and system behaviour before use.

Keep prompts and outputs within this Testing project folder for consistency.