# Interim Review

The interim review checks whether each team is on track with their software project:

- Is there a serious walking skeleton (architecture prototype)?
    - See architectural overview. [Architectural-Overview](Architectural-Overview.md)

- Have the main risks been resolved?
    - A minimal version of the Raptor algorithm has been implemented and is running.
    - The GTFS schedule format is parsed is convertable to the data structure by raptor.
    - A REST API for the Public Transit Service is designed in the OpenAPI Specification v3.
    - A test project for the JNI integration with calls from Java to C++ is working.
        - the library is built in a CI/CD pipeline on windows and linux.

- Are the requirements clear and communicable?
    - See [requirements section](requirements.md)

- Are the priorities set correctly?
    - The software development process is defined and the time outline of the project is planned. The team members have
      planned their resources, see [schedule section](Schedule.md)
    - Focus is set on the Public Transit Service and its core components (gtfs schedule, raptor algorithm and
      converter).
    - A user interface of the service is to be initially realized for demo purposes. If towards the end of the project
      there are
      more resources left, it will be extended accordingly, see *nice-to-have* requirements.
    - The integration with JNI is tested and results are going to be continuously compared with the existing benchmark
      of the Java implementation. To ensure that the additional effort of programming in C++ also provides significant
      benefits in the performance of the algorithm, if the effort does not justify the performance gain, the JNI
      integration will be terminated based on this reasoning.

- Is the approach appropriate?
    - We are working in a Scrum-like setup with 4-week sprints between the supervisor meetings, which has proven
      effective.
    - The team has a good understanding of the project and the tasks to be done, which are monitored in an agile project
      tracking software (Jira). The structured way of working enables to work independently.
    - Weekly meetings are used to synchronize the team and to discuss the progress and problems. We meet in person once
      a month.
    - A monthly meeting with the supervisor is used to report the status and challenge the progress of the project.
    - A three-day work code sprint is planned (but not yet fixed) in the mountains.

- Is the code readable and following best practices?
    - See [Code style section](requirements.md)
    - we are guided by clean code principles and the code is reviewed by the team members.

- Are there automated tests, tools/infrastructure, and documentation?
    - Unit and integration tests are set up.
    - CI is realized using GitHub actions.
    - Documentation is continuously written in WriteSide and is daily published on GitHub pages.

- Is there a realistic plan for the remainder of the project?
    - See Gantt Chart in [Overview](overview.md).
