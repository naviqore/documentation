# Code Style Guide

## General

- Always use the formatter defined per project before committing.
- Restrict visibility strictly; only allow access from outside the package if absolutely necessary.
- Program to interfaces rather than implementations.
- Follow the SOLID principles to structure the code (classes).
- Adhere to the DRY (Don't Repeat Yourself) principle.
- Avoid magic numbers or literals; use constants instead.
- All code changes must include corresponding unit or integration tests.
- Focus on testing the most relevant and complex features rather than achieving high line coverage.
- Test early and often, writing tests after implementation should be avoided whenever possible.

## Java

- Use the formatter defined for IntelliJ.
- Utilize Maven as the build tool and for dependency management.
- Avoid boilerplate code by using Lombok [9] to generate getters, setters, and constructors.
- Add spaces after class definitions and before return statements if a method has more than three statements. Use spaces
  to clarify blocks that belong together (e.g., before if-control flow statements).
- Group imports into packages after five classes from the same package.
- Follow naming conventions: `camelCase` for methods, `UpperCamelCase` for classes, and `ALL_UPPER_CASE` for static
  constants.
- Do not use `Optional<>` for parameters; it is allowed for return types and internal usage.

### Code Example

```java
public class ExampleService {

    private static final int MAX_ATTEMPTS = 5;
    private final ExampleRepository repository;

    public ExampleService(ExampleRepository repository) {
        this.repository = repository;
    }

    public Optional<Example> findById(String id) {
        return repository.findById(id);
    }
}
```

### Documentation

- Document only non-obvious public members with Javadoc (e.g., do not document getters or setters).
- Ensure non-obvious public members are well documented.
- Avoid comments in code, except when the code or case structure is complex. If commenting, write clear and concise
  comments.

### Testing

- Use JUnit 5 for testing. AssertJ and Mockito are allowed.
- The Surefire plugin runs unit tests (`ExampleTest`), and the Maven Failsafe plugin runs integration
  tests (`ExampleIT`). Follow the naming convention with the postfix `Test` and `IT`.
- Use descriptive names for test cases: `should…`, `shouldNot…`, `shouldThrow...`. The character `_` is allowed in test
  case names to differentiate test cases.
- Use nested test classes to group thematically related cases together.
- If tests are complex in setup, use the test builder pattern and a Jupiter extension to reuse it.

### Test Example

```java
public class ExampleServiceTest {

    @Test
    void shouldReturnExampleWhenIdExists() {
        // Arrange
        ExampleRepository repository = mock(ExampleRepository.class);
        ExampleService service = new ExampleService(repository);
        when(repository.findById("1"))
                .thenReturn(Optional.of(new Example("1")));

        // Act
        Optional<Example> result = service.findById("1");

        // Assert
        assertThat(result).isPresent();
    }
}
```

## C++

- Use GoogleTest as the testing framework.
- Test case names should be descriptive and follow the pattern `TestedFunction_ExpectedBehavior`.
- Group thematically related test cases using test suites.
- Mock dependencies using GoogleMock where applicable.

## Python

Python code written for this module should follow the google python style
guide <http://google.github.io/styleguide/pyguide.html> whenever possible.
All modules and public functions must include a docstring as further described
in <http://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings>

Further:

- Format code with Black and isort.
- Follow PEP8 guidelines.
- Use Poetry as the build tool.
- Follow naming conventions: `snake_case` for methods, `UpperCamelCase` for classes, and `ALL_UPPER_CASE` for constants.

```Python
class ExampleService:


    MAX_ATTEMPTS = 5


def __init__(self, repository):


    self._repository = repository


def find_by_id(self, id: str) -> Optional[Example]:
    return self._repository.find_by_id(id)
```
