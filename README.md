# BusConnectivity
Simple College Bus Tracker Simulator

**Project Overview**

This is a proof-of-concept, console-based application built in Python designed to address a common transportation challenge for college students in areas predominantly served by private bus operators.

The core goal is to provide a simple, centralized system where bus operators can quickly update their estimated arrival times, allowing students to plan their commute more efficiently, avoid expensive taxi services, and save money.

Note: This current version of the application runs entirely in memory and uses a dummy dataset for testing and demonstration purposes. Any changes made during a session will be lost upon exit.

** Features**

The application operates in two distinct modes:

@ Operator Update Mode:

Allows bus operators to enter a specific Bus Number (e.g., "B-04").

Accepts a new estimated arrival time in HH:MM (24-hour) format.

Automatically records the time of the last update.

Includes basic input validation for time format.

@ Student View Mode:

Displays the full schedule of all registered buses.

The schedule is dynamically sorted by arrival time for easy reading.

Includes a visual indicator (-> UPCOMING) for buses whose arrival time is in the future relative to the current local time.

Shows the exact date and time the schedule was last updated.

** **Technologies & Tools Used** **

Component

Tool / Technology

Purpose

Language

Python 3

Core logic and application structure.

Libraries

datetime

Used for time format validation, sorting, and determining if a bus is "upcoming."

Data Storage

In-Memory Dictionary

Dummy data storage for non-persistent testing (no external files/databases required for this version).



** **Steps to Install & Run the Project** **

Since this is a single, self-contained Python script, setup is minimal.

Prerequisites: Ensure you have Python 3 installed on your system.

You can check your version by running: python --version or python3 --version

Save the File: Save the provided code as a file named bus_tracker_simulator.py.

Run the Application: Open your terminal or command prompt, navigate to the directory where you saved the file, and execute the following command:

python bus_tracker_simulator.py

or

python3 bus_tracker_simulator.py


** Instructions for Testing**

When the application starts, you will see a menu.

Test Scenario 1: Operator Update

@ Select 1 (Operator).

Enter Bus Number: Type a new bus number (e.g., B-99) or an existing one (e.g., B-01).

Enter NEW Estimated Arrival Time: Input a new time, for example, 16:15.

The system will confirm the update and return to the main menu.

Test Scenario 2: Student View

@ Select 2 (Student).

The program will display a formatted table with four columns: BUS NO., EST. TIME, LAST UPDATED (Local Time), and the UPCOMING status.


Verify that:

The schedule is sorted numerically by the EST. TIME.

The update you made in Test Scenario 1 is reflected in the table.

Buses scheduled to arrive later than the current time are marked with -> UPCOMING.

Test Scenario 3: Input Validation

@ Select 1 (Operator).

Enter NEW Estimated Arrival Time: Input an invalid time string, such as 4pm or 1234.

The system should display: Invalid time format. Please use HH:MM (24-hour clock) format. and prompt you again, without crashing.


**Screenshots (Simulated Console Output)
**
Operator Success Screen

'''SUCCESS! Bus B-99 updated.
New estimated arrival time: 16:15 at College Gate/Main Stop'''
<img width="629" height="428" alt="image" src="https://github.com/user-attachments/assets/762b6718-8911-4147-b186-25b3c0da8ba4" />


            print("Invalid choice. Please enter 1, 2, or 3.")

if __name__ == "__main__":
    main()

