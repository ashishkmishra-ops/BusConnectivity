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


****Code****
#Bus Connectivity Tracker
from datetime import datetime

# --- Configuration ---
# Removed DATA_FILE, json, and os imports as data is now hardcoded.
COLLEGE_LOCATION = "College Gate/Main Stop"
TIME_FORMAT = "%H:%M"

# --- Utility Functions ---

def load_dummy_schedule():
    """Initializes and returns a dummy, in-memory bus schedule."""
    # This simulates data being loaded from a database or file system.
    print("Loading dummy schedule for testing...")
    return {
        "B-01": {"time": "15:00", "location": COLLEGE_LOCATION, "last_updated": "2025-11-19 14:00:00"},
        "B-05": {"time": "17:45", "location": COLLEGE_LOCATION, "last_updated": "2025-11-19 15:30:00"},
        "C-12": {"time": "10:15", "location": COLLEGE_LOCATION, "last_updated": "2025-11-19 09:00:00"},
        "D-44": {"time": "22:30", "location": COLLEGE_LOCATION, "last_updated": "2025-11-19 16:00:00"},
    }

# Removed save_schedule() as data is not persistent

# --- Core Modes ---

def operator_mode(schedule):
    """
    Allows bus operators to update the expected arrival time for a specific bus.
    Note: Updates are only stored in memory for this dummy version.
    """
    print("\n--- OPERATOR UPDATE MODE ---")
    
    # 1. Get bus number
    bus_number = input("Enter Bus Number (e.g., B-04, 101): ").strip().upper()
    if not bus_number:
        print("Bus Number cannot be empty.")
        return

    # 2. Get new estimated time
    while True:
        try:
            new_time_str = input(
                f"Enter NEW Estimated Arrival Time at {COLLEGE_LOCATION} (HH:MM format, e.g., 14:30): "
            ).strip()
            
            # Check for a valid time format
            datetime.strptime(new_time_str, TIME_FORMAT)
            
            # Update the schedule data in memory
            schedule[bus_number] = {
                "time": new_time_str,
                "location": COLLEGE_LOCATION,
                # Record the update time
                "last_updated": datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            }
            
            # No save_schedule() call here, update is in-memory only.
            print(f"\nSUCCESS! Bus {bus_number} updated.")
            print(f"New estimated arrival time: {new_time_str} at {COLLEGE_LOCATION}")
            break
            
        except ValueError:
            print("Invalid time format. Please use HH:MM (24-hour clock) format.")
        except Exception as e:
            print(f"An unexpected error occurred during update: {e}")
            break


def student_mode(schedule):
    """
    Displays the current expected arrival times for all registered buses.
    """
    print("\n--- STUDENT VIEW MODE ---")
    print(f"Current Estimated Bus Arrivals at: {COLLEGE_LOCATION}\n")
    
    if not schedule:
        print("No bus timings are currently available.")
        return

    # Sort the schedule by arrival time for easier reading
    sorted_buses = sorted(
        schedule.items(), 
        key=lambda item: datetime.strptime(item[1]['time'], TIME_FORMAT)
    )

    print("-----------------------------------------------------------------")
    print("| {:<10} | {:<10} | {:<25} |".format("BUS NO.", "EST. TIME", "LAST UPDATED (Local Time)"))
    print("-----------------------------------------------------------------")
    
    for bus_number, data in sorted_buses:
        try:
            # Check if the time is in the future relative to the current time for filtering/highlighting
            # This creates a datetime object for today with the arrival time
            arrival_dt = datetime.strptime(data['time'], TIME_FORMAT).replace(
                year=datetime.now().year, 
                month=datetime.now().month, 
                day=datetime.now().day
            )
            is_upcoming = arrival_dt > datetime.now()
            
            status_indicator = " -> UPCOMING" if is_upcoming else ""

            print("| {:<10} | {:<10} | {:<25} | {}".format(
                bus_number, 
                data['time'], 
                data['last_updated'], 
                status_indicator
            ))
        except Exception as e:
            # In a real app, you might log this error instead of printing
            print(f"| Error processing bus {bus_number}: {e} |")

    print("-----------------------------------------------------------------")
    # Removed reference to the data file
    print(f"\nNote: All times are local time. Data is in-memory for testing.")


# --- Main Application Loop ---

def main():
    """The main function to run the Bus Tracker application."""
    print("=========================================")
    print(" Simple College Bus Tracker Application")
    print(" (IN-MEMORY TEST MODE)")
    print("=========================================")
    
    # Load the dummy data set directly
    schedule = load_dummy_schedule()

    while True:
        print("\nSelect Mode:")
        print("1. Operator (Update Bus Arrival Time)")
        print("2. Student (View Latest Schedule)")
        print("3. Exit")
        
        choice = input("Enter your choice (1/2/3): ").strip()

        if choice == '1':
            operator_mode(schedule)
        elif choice == '2':
            student_mode(schedule)
        elif choice == '3':
            print("\nExiting application. Goodbye!")
            # Note: Any changes made in Operator mode are lost here.
            break
        else:
            print("Invalid choice. Please enter 1, 2, or 3.")

if __name__ == "__main__":
    main()

