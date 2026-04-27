# TheGamingRoom
# CS 230 – Operating Platforms Portfolio Artifact

## Software Design Document: Draw It or Lose It

---

## About the Client and Their Requirements

The Gaming Room is a game development company that currently offers their game *Draw It or Lose It* as an Android-only mobile application. They came to me wanting to expand the game into a web-based platform accessible across multiple operating systems, including Windows, macOS, Linux, and mobile devices. The game needed to support multiple teams playing simultaneously, with each team holding multiple players. Additional requirements included enforcing unique names for all games and teams, and ensuring that only one instance of the game could exist in memory at any given time.

---

## What I Did Particularly Well

I felt strongest in the Recommendations section of the design document. Rather than giving generic suggestions, I grounded each recommendation directly in the client's requirements and backed them up with specific technical reasoning, such as comparing the $1,069 licensing cost of Windows Server against the zero-cost Linux alternative, or explaining exactly why PostgreSQL's transactional guarantees made it a better fit than MySQL for handling concurrent player writes. I also did well at connecting the design patterns used in the code (singleton and iterator) back to specific architectural decisions, like explaining how the singleton pattern in GameService directly supports memory efficiency and how it simplifies race condition prevention in a distributed environment.

---

## How the Design Document Helped During Development

Working through the design document before touching any code forced me to think carefully about the structure of the application before getting lost in implementation details. Building out the domain model, for instance, made it clear that Game, Team, and Player all needed a shared base class (Entity) to avoid duplicating id and name logic across three separate classes. Without that planning step, I might have written redundant code and only realized the problem later when it became harder to fix. The evaluation section was similarly useful, comparing platforms side by side revealed constraints I might not have considered otherwise, like the fact that macOS server tools were largely discontinued in 2022, which ruled it out as a realistic hosting option before I wasted time exploring it.

---

## What I Would Revise

If I could go back and improve one part of the document, I would expand the System Architecture View section. In its current state, it contains a placeholder note acknowledging that architecture content belongs there but does not include any actual diagrams or written description of the physical tiers. I would replace that placeholder with a proper layered architecture diagram showing the browser client, the Tomcat/JVM application server, and the PostgreSQL database server as distinct tiers communicating over the network. Adding that visual would make the document more complete and give a developer or stakeholder a clearer picture of how the components relate before reading through the more detailed sections.

---

## Interpreting and Implementing User Needs

I interpreted the client's needs by breaking down their high-level goals into concrete technical requirements. When The Gaming Room said they wanted the game to run "across multiple operating systems," I translated that into specific requirements: a server-side language and framework that was platform-independent (Java on Tomcat), a client-side delivery method that required no installation (responsive web application in the browser), and a hosting platform that supported all major cloud providers (Linux). When they said they needed unique game and team names, I mapped that to both a code-level solution (the iterator pattern checking existing lists before insertion) and a database-level solution (unique constraints in PostgreSQL). Considering user needs is critical in software design because requirements that seem simple on the surface often have hidden technical implications. Designing for the user first prevents you from building something technically impressive that still fails to solve the actual problem.

---

## My Approach to Software Design

My overall approach was to move from requirements to constraints to architecture before writing any code. I started by clearly stating what the application needed to do, then identified the constraints those requirements created (platform independence, single instance enforcement, unique naming, network communication, and security), and only then made architectural decisions about which patterns, platforms, and technologies to use. For future projects, I would continue using this requirements-first approach. I would also rely more heavily on UML class diagrams early in the process, building the domain model before writing the corresponding classes made it much easier to see relationships between objects and catch design issues before they became bugs. Additionally, I would carry the habit of evaluating multiple platform options against a consistent set of criteria (cost, compatibility, scalability, tooling) rather than defaulting to a familiar choice without analysis.
