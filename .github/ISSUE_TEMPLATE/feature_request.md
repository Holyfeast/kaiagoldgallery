name: ✨ Feature Request
description: Suggest a new feature
title: "[FEATURE] "
labels: ["enhancement"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        Thanks for suggesting a feature! Please fill out the form below.

  - type: textarea
    id: description
    attributes:
      label: Description
      description: Clear description of the feature
      placeholder: "I want to add..."
    validations:
      required: true

  - type: textarea
    id: problem
    attributes:
      label: Problem It Solves
      description: What problem does this feature solve?
      placeholder: "Currently, users cannot..."
    validations:
      required: true

  - type: textarea
    id: solution
    attributes:
      label: Proposed Solution
      description: How should this feature work?
      placeholder: "The feature should..."

  - type: textarea
    id: alternatives
    attributes:
      label: Alternative Solutions
      description: Any alternative approaches?
      placeholder: "Another way could be..."

  - type: textarea
    id: additional
    attributes:
      label: Additional Context
      description: Mockups, examples, or links?
      placeholder: "Add any other context..."

  - type: checkboxes
    id: checklist
    attributes:
      label: Checklist
      options:
        - label: I've searched existing feature requests
          required: true
