# Peer Review Notes

## Peer Review Summary
Criterion with Most Feedback: Completeness and Clarity received the highest concentration of review comments, primarily concerning diagram component representations, missing persistent storage blocks, and explicit interface connections.
Top Two Issues Raised While Reviewing Others:
Lack of explicit error recovery and fallback transitions in subsystem state diagrams.
Missing risk mitigation protocols for voltage drops across secondary payload power rails during continuous transmission passes.

## Peer Review Action Items
| ID | Rubric Criterion | Issue & Team | Action | Owner | Priority | Due Date |
|:--:|:---|:---|:---|:---|:---:|:---:|
| 1 | Clarity | Missing component coloring legend in subsystem diagrams (Team DigiDarts & StreetSmart) | Add a color-coded legend defining component classifications across all subsystem diagrams | Kristen Griessman | Must-fix | 10/21/26 |
| 2 | Feasibility | Direct connection between Battery and Battery Monitor missing in Power diagram (Team DigiDarts) | Add explicit 1:1 hardware/telemetry connection line between Battery and Battery Monitor | Elmoataz Abdellah | Must-fix | 10/21/26 |
| 3 | Completeness | MRAM non-volatile storage component missing from Data Storage diagram (Team StreetSmart) | Update Payload / Data Storage diagram to include MRAM block and bus interface | Seunghun Lee | Must-fix | 10/21/26 |
| 4 | Risk | Lack of watchdog supervisor coverage for dynamic UART serial interfaces (Team StreetSmart & SkillForge) | Define UART timeout watchdog and recovery handler logic in edge case table | Matthew Goldsberry | Must-fix | 10/28/26 |