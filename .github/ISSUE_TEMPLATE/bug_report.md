name: 🐛 Bug Report
description: Report a bug to help us improve
title: "[BUG] "
labels: ["bug"]
assignees: []

body:
  - type: markdown
    attributes:
      value: |
        Thanks for reporting a bug! Please fill out the form below to help us understand the issue.

  - type: textarea
    id: description
    attributes:
      label: Description
      description: Clear description of the bug
      placeholder: "What's the problem?"
    validations:
      required: true

  - type: textarea
    id: steps
    attributes:
      label: Steps to Reproduce
      description: How to reproduce the issue?
      placeholder: |
        1. Go to ...
        2. Click on ...
        3. See error
    validations:
      required: true

  - type: textarea
    id: expected
    attributes:
      label: Expected Behavior
      description: What should happen?
      placeholder: "The page should..."

  - type: textarea
    id: actual
    attributes:
      label: Actual Behavior
      description: What actually happens?
      placeholder: "Instead, the page..."

  - type: textarea
    id: environment
    attributes:
      label: Environment
      description: Your environment details
      placeholder: |
        - OS: Windows/macOS/Linux
        - .NET Version: 9.0
        - Node.js Version: 20.x
        - Browser: Chrome/Firefox/Safari
    validations:
      required: true

  - type: textarea
    id: logs
    attributes:
      label: Logs/Screenshots
      description: Any error logs or screenshots
      placeholder: "Paste error logs or attach screenshots"

  - type: checkboxes
    id: checklist
    attributes:
      label: Checklist
      options:
        - label: I've searched existing issues
          required: true
        - label: I've included error logs
