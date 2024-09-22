# Software Development Process

The development process follows an iterative Scrum-like [10] setup with 4-week sprints between supervisor meetings. Task
management and monitoring are facilitated using the agile project tracking software, Jira. This structured way of
working enables team members to work independently.

Key aspects of the process include:

- No daily stand-ups
- Weekly meetings every Friday to synchronize the team, discuss progress, and address any issues
- Sprints lasting one month, aligned with the supervisor sync meetings
- Sprint reviews and demos at the end of each sprint

Weekly meetings help in team synchronization, while the monthly meetings with the supervisor are used to report status,
challenge progress, and define the upcoming sprints. A three-day work code sprint is planned for mid-July, although the
exact dates are yet to be fixed.

## Increments

The project is divided into three phases:

1. **Phase 1: Walking Skeleton (v0.1.0)**
2. **Phase 2: Main Implementation (v1.0.0)**
3. **Phase 3: Feature Freeze for Final Documentation and Presentation**

Each phase builds incrementally towards the project's final goals.

## Estimation Method

Scrum Poker is used for task estimation, categorizing issues into T-Shirt sizes:

- **S** (Small) = 1 hour
- **M** (Medium) = 4 hours
- **L** (Large) = 8 hours
- **XL** (Extra Large) = 2 days

## Testing Method

The testing strategy includes both unit tests and integration tests. Reviewers are responsible for ensuring that tests
are present and that the code coverage, especially for edge cases, is adequate. Automated unit and integration tests are
set up, and continuous integration (CI) is realized using GitHub Actions.

## Best Practices

The fail-fast concept is preferred in development. Given the complexity of the project, failing quickly allows for early
identification and resolution of issues, ensuring a more efficient development process.

Clean code principles are followed, and all code is reviewed by team members. For more details, refer to
the [Code Style Section](code-style-guide.md).

## Documentation

Documentation is continuously written in WriterSide and is published daily on GitHub Pages. The primary language for
source code, documentation, and issues is English.
