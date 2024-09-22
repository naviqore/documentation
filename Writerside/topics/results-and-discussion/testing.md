# Testing

In general, tests are divided into unit test cases and integration test cases. Unit tests specifically target one unit
of code (typically a class) in isolation, often with mocked dependencies when necessary. Integration tests, on the other
hand, assess multiple components interacting together (e.g., a file reader working with a records parser and test data).
In our case, integration tests may also include running external dependencies, such as in the client, where a service
instance must be started using Docker Compose. We acknowledge that the boundary between integration and system tests can
be blurred, but we have chosen to categorize these as integration tests rather than introducing a third test category.
It is important that unit tests and integration tests can be executed in distinct phases.

We did not prioritize achieving the highest possible line coverage. Instead, we used this metric as a guiding tool
during development. The focus was on testing the most relevant and complex features. During the review process,
reviewers were required to check the code against the [Code Style Guide](code-style-guide.md), which also included
ensuring that new or modified components were properly tested.

## Setup

- **Java, Maven**: We use JUnit 5, the Maven Surefire Plugin for unit tests (executed in the Maven `test` phase, with
  a `<TestName>Test` suffix), and the Maven Failsafe Plugin (executed in the Maven `verify` phase, with a `<TestName>IT`
  suffix) for integration tests. This allows unit and integration tests to be run in separate phases.

- **Python, Poetry**: Pytest is used as the test runner, with Pytest markers to distinguish between unit and integration
  test categories.

- **C++, CMake and vcpkg**: GoogleTest is used for testing (TODO).

## Code Metrics

The following table provides an overview of some key code metrics for the main repositories involved in this thesis. The
lines of code were counted using the command-line tool `cloc` and include both production and test code, excluding
inline comments and documentation (such as Javadoc or docstrings). Test coverage is measured in terms of line coverage.

| Repository Name            | Language | Short Description                                                                   | Commits | Lines of Code (Test) | Test Cases (Integration) | Test Coverage |
|----------------------------|----------|-------------------------------------------------------------------------------------|---------|----------------------|--------------------------|---------------|
| **public-transit-service** | Java     | Public transit schedule and routing service based on GTFS data and RAPTOR algorithm | 751     | 12'116 (5'662)       | 569 (51)                 | 86%           |
| **public-transit-client**  | Python   | Client to access the public transit service API endpoints.                          | 72      | 822 (419)            | 23 (15)                  | 80%           |
| **public-transit-viewer**  | Python   | Viewer to interact with the public transit service.                                 | 125     | 1'007 (21)           | 1 (1)                    | 0%            |
| **raptorxx**               | C++      | C++ Implementation of the RAPTOR algorithm for benchmarking.                        | TODO    | TODO                 | TODO                     | TODO          |

Since the focus of this thesis is on the RAPTOR algorithm, the service received the most testing attention. The viewer,
primarily developed for demonstration purposes, has only one integration test to verify the application can boot, but
lacks unit tests. For a production-ready frontend, additional unit tests would need to be implemented.
