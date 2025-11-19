**Project Statement: Simple College Bus Tracker
**

**Problem Statement**

Students attending the college, located in a village or remote area, face significant transportation challenges due to limited public connectivity. The primary reliable options are expensive private cabs or scheduled private buses. The unpredictable nature of private bus arrival times forces students to either wait excessively at the college or rely on the high-cost cab service to avoid missed connections. This results in unnecessary financial burden and wasted time.

Scope of the Project

The scope of this initial, lightweight Simple College Bus Tracker project is to provide a low-barrier, instantaneous communication channel between bus operators and the student community.

The system focuses on the final critical step: estimated arrival at the college gate/main stop.

**In Scope:**

Real-time status updates for bus arrival times (manually input by operators).

Two operational modes: Data input (Operator) and Data viewing (Student).

Simple Command-Line Interface (CLI) for ease of use across different systems.

Sorting and filtering of bus data for student convenience.

Python-only implementation for minimal dependencies.

Out of Scope (Future Enhancements):

Automatic GPS tracking.

Web/Mobile application interfaces.

User authentication or security layers.

Persistent data storage (e.g., using a database or a shared file system).

**Target Users**

1. Primary User: College Students

Goal: To accurately determine the next available bus to leave the college premises.

Benefit: Saves money by avoiding expensive cab rides and minimizes unnecessary waiting time.

2. Secondary User: Private Bus Operators

Goal: To easily and quickly update their estimated time of arrival (ETA) at the college stop.

Benefit: Improves service quality and relationship with the student customer base.

**High-Level Features**

Dual Interface: Clear separation between Operator (Input) and Student (Output) functionalities.

Time Estimation Input: Simple input mechanism for operators to provide new arrival times (HH:MM).

Real-Time View: Students can view a dynamically updated list of buses, sorted by their expected arrival time.

Upcoming Status: Visual indicator (-> UPCOMING) to quickly identify buses that have not yet arrived.
