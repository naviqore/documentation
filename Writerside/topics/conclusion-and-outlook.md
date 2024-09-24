# Conclusion and Outlook

In conclusion, the project successfully fulfilled all the must-have, most of the should-have, and some of the
nice-to-have requirements, delivering a production-ready transit routing solution.

One of the key strengths of this project was our ability to extend the RAPTOR algorithm to accommodate more complex
real-world requirements, such as calculating connections spanning multiple days, incorporating latest departure routing,
and considering accessibility or bike transportation constraints in connection requests. These aspects were only
identified as requirements during the course of the project. The iterative approach we adopted, along with careful task
management, allowed us to address newly identified requirements while maintaining progress. This demonstrated the
flexibility and adaptability of both the algorithm and the chosen software development process.

The team’s strong motivation and collaborative spirit were essential to our success, creating a productive environment
driven by a compelling and challenging topic. Our extensive use of pull request reviews helped ensure high code quality,
leading to solid design decisions and robust testing practices. In addition to these technical achievements, the final
product is available as open-source under the MIT license, which encourages future contributions and improvements. Each
team member also expanded their expertise in key areas such as data structures, algorithms, language specifics, and
software architecture, making this project a valuable learning experience.

However, there were areas for improvement. One notable challenge was the minimal overlap between the C++ and Java
components, which led to reduced synergy during the development process. Additionally, the lack of optional GTFS
components provided by national transit agencies, such as accessibility or bike information, along with incomplete
transfer data between stops, posed further obstacles. The intense project schedule, with long hours spent coding during
evenings and weekends, also placed considerable strain on the personal lives of the team members, highlighting a
work-life balance issue.

Looking to the future, several areas of potential development could further enhance the product. Introducing fare-based
multi-criteria routing through mcRAPTOR could offer users more tailored, cost-effective options. Incorporating real-time
GTFS updates would make the system more responsive to current conditions, improving its accuracy. Implementing
A*-based routing for footpaths would enhance the precision of walking routes between transit stops. Implementing a
common storage architecture for loaded schedules and router stop times within the public transit service
would enhance horizontal scalability and encapsulate the state within a new, dedicated data layer.

Overall, we believe this project has established a strong foundation for future development. As we conclude our MAS in
Software Engineering at the Eastern Switzerland University of Applied Sciences, we are excited to see how the project
evolves and progresses in the future.
