# Interim Review

The interim review checks whether each team is on track with their software project:

> Is there a serious walking skeleton (architecture prototype)?

- See [architectural overview section](architectural-overview.md).

> Have the main risks been resolved?

- A minimal version of the RAPTOR algorithm has been implemented and is running.
- The GTFS schedule format is parsed is convertable to the data structure by RAPTOR.
- A REST API for the Public Transit Service is designed in the OpenAPI Specification v3.
- A test project for the JNI integration with calls from Java to C++ is working.
- the library is built in a CI/CD pipeline on windows and linux.

> Are the requirements clear and communicable?

- See [requirements section](requirements.md).

> Are the priorities set correctly?

- The software development process is defined and the time outline of the project is planned. The team members have
  planned their resources, see [schedule section](outline.md).
- Focus is set on the Public Transit Service and its core components (gtfs schedule, RAPTOR algorithm and
  converter).
- A user interface of the service is to be initially realized for demo purposes. If towards the end of the project
  there are more resources left, it will be extended accordingly, see *nice-to-have* requirements.
- The integration with JNI is tested and results are going to be continuously compared with the existing benchmark
  of the Java implementation. To ensure that the additional effort of programming in C++ also provides significant
  benefits in the performance of the algorithm, if the effort does not justify the performance gain, the JNI
  integration will be terminated based on this reasoning.

> Is the approach appropriate?

- We are working in a Scrum-like setup with 4-week sprints between the supervisor meetings, which has proven
  effective.
- The team has a good understanding of the project and the tasks to be done, which are monitored in an agile project
  tracking software (Jira). The structured way of working enables to work independently.
- Weekly meetings are used to synchronize the team and to discuss the progress and problems. We meet in person once
  a month.
- A monthly meeting with the supervisor is used to report the status and challenge the progress of the project.
- A three-day work code sprint is planned (but not yet fixed) in the mountains.

> Is the code readable and following best practices?

- See [code style section](code-style-guide.md).
- We are guided by clean code principles and the code is reviewed by the team members.

> Are there automated tests, tools/infrastructure, and documentation?

- Unit and integration tests are set up.
- CI is realized using GitHub actions.
- Documentation is continuously written in WriteSide and is daily published on GitHub pages.

> Is there a realistic plan for the remainder of the project?

- See Gantt Chart in [outline section](outline.md).

## Feedback

### Reviewer 1

- **Purpose Clarification:** The purpose of the project needs to be better defined.
- **Context Diagram:** A context diagram is missing and is necessary for better understanding.
- **Numbering Issues:** Numbering in the documentation is difficult to follow.
- **Architecture:** While the overview is good, consider applying the C4 model for better structure.
- **Documentation Order:** Improve the sequence of sections in the documentation.
- **API Interface:** Ensure OpenAPI compliance. Review paths to accurately reflect the domain model. The API should be
  designed from the consumer's perspective.
- **JNI Concerns:** Avoid focusing too much on JNI. Consider separating the C++ part into its own microservice.
- **Graph Database:** Look into using Neo4J as a graph database.

### Reviewer 2

- **Patterns and Caches:** Consider using patterns and caches more effectively.
- **Microservices:** Potentially offload computations for the API Gateway to a separate microservice.
- **Data Structures:** Optimize data structures, such as using HashSet instead of checking lists for existing elements.
- **IEnumerable Preference:** Prefer IEnumerable over Iterable and Enumerable.
- **Custom Caches:** Implementing custom caches with thread safety is challenging. Avoid reentrant locks as they are too
  global. Use existing caches like EHCache and annotations like `@Cacheable`.
- **Code Quality:** The code quality is good with appropriate use of patterns.

### Reviewer 3

- **Video Issues:** Ensure the presenter’s face is visible in the video.
- **Testing Requirements:** Invest in more tests, including multiple measurements and integration tests.
- **Java vs. C++ Comparison:** Provide a detailed comparison between Java and C++.
- **Requirement Prioritization:** Use clear prioritization (must-have, should-have, nice-to-have) without including
  priority numbers that might change.
- **Risk-Based Approach:** If not using Scrum, adopt a risk-based approach and provide an analysis.
- **Scrum Implementation:** Open all sprints in Jira, define sprint goals, and document them clearly.
- **Use Case Modeling:** Model use cases comprehensively.

### Reviewer 4

- **Video Length:** The video is too long; adhere to the fixed time schedule for the final presentation.
- **Onion Architecture:** Review and possibly revise the slide on Onion Architecture.
- **Documentation as Cohesive Work:** Ensure the documentation is exported as a single cohesive document.
- **Risk Mitigation Measures:** Define measures to reduce risks.
- **Terminology Clarity:** Improve terminology clarity, for instance, differentiating between "line" and "trip" with
  concrete examples, possibly in German.
- **Code Review:** The code generally looks good, but some methods, like `raptorSpawnFromSourceStop`, are too long and
  need refactoring.

## Consolidated Action Items

- ✔️ Clarify the purpose of the project and add a context diagram.
- ✔️ Improve the numbering and sequence of the documentation.
- ✔️ Apply the C4 model to the architecture section.
- ✔️ Ensure OpenAPI compliance and review paths for domain model accuracy.
- ❌ Consider separating the C++ part into a microservice and look into Neo4J for graph database needs.
- ✔️ Optimize data structures and use cache solutions with proper synchronization mechanisms.
- ✔️ Invest in comprehensive testing, including integration tests, and provide a detailed comparison of Java and C++.
- ✔️ Clearly prioritize requirements and adopt a risk-based approach if not using Scrum. Ensure all sprints and goals
  are documented in Jira.
- ✔️ Review the video presentation regarding length and clarity. Adapt for final presentation.
- ✔️ Export documentation as a cohesive document and improve terminology clarity.
- ✔️ Refactor long methods in the code and define risk mitigation measures.
