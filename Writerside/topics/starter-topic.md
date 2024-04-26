# Overview

Overview articles give background information and provide context to a particular subject.
Their goal is to explain a concept, not to teach or give instructions.

## What is product/service/concept

Provide some background and context, explain choices and alternatives.

## Glossary

A definition list or a glossary:

First Term
: This is the definition of the first term.

Second Term
: This is the definition of the second term.


## Outline

```mermaid
gantt
    title Naviqore Project Outline
    dateFormat YYYY-MM-DD
    section Setup
        Literature Review: literature, 2024-04-01, 30d
        Kick-Off (on Site): milestone, kickoff, 2024-04-05, 0d
        Project Setup: project, 2024-04-05, 15d
    section v0.1.0
        Analysis: 2024-04-15, 2024-06-13
        Design: 2024-05-01, 2024-06-13
        Supervisor-Sync (Remote): milestone, kickoff, 2024-05-08, 0d
        Implementation: 2024-05-10, 2024-06-13
        Testing: 2024-05-10, 2024-06-13
        Supervisor-Sync (on Site): milestone, kickoff, 2024-05-31, 0d
        Walking Skeleton: milestone, active, walkingSkeleton, 2024-06-13, 0d
    section v1.0.0
        Analysis: 2024-06-13, 2024-08-01
        Design: 2024-06-13, 2024-09-01
        Implementation: 2024-06-13, 2024-09-27
        Testing: 2024-06-13, 2024-09-27
    section Documentation
        Continuous Documentation: 2024-04-15, 2024-09-27
        Thesis: 2024-08-15, 2024-09-27
        Submission: milestone, crit, submission, 2024-09-27, 0d
        Presentation: 2024-09-15, 2024-09-30
        Presentation: milestone, presentation, 2024-09-30, 0d

```

## Semantic Versioning

This project adheres to [Semantic Versioning](https://semver.org/). We use a three-part version numbering system:
MAJOR.MINOR.PATCH. Here is what each part represents:

- **MAJOR version** when we make incompatible API changes,
- **MINOR version** when we add functionality in a backwards compatible manner, and
- **PATCH version** when we make backwards compatible bug fixes.

Each release increases the version number accordingly. For more details on our versioning protocol and for updates,
please visit our release notes.

## Commit Messages
