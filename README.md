# Hospital-Patient-Management-System---Java-Backend
A Java-based hospital management system that uses a min-heap for patient prioritization and a circular queue for appointment scheduling. It features a menu-driven interface for managing patients, treatments, and appointments, simulating efficient real-world hospital workflows.


## PREREQUISITES

- Java Development Kit (JDK) 17 or higher installed
- A terminal / command prompt open in the folder containing all .java files
- All source files present:
  AppState.java
  CircularQueue.java
  InputHelper.java
  MedQueue.java
  MinHeap.java
  Patient.java
  UI.java

TIP: For best results, use a terminal that supports ANSI colours
(macOS Terminal, Linux bash, Windows Terminal, or Git Bash).
The classic Windows cmd.exe may not render colours correctly.

---

## STEP 1 - COMPILE

Run this single command to compile all source files at once:

      javac *.java

If you are using the VS Code project layout (src/ folder), run:

      javac -d bin src/*.java

No errors should appear. If you see errors, confirm your JDK version:

      java -version

---

## STEP 2 - RUN

Start the program:

      java MedQueue

(If you compiled into bin/ with the VS Code layout, run:)

      java -cp bin MedQueue

The system will load with 5 demo patients and 3 pre-scheduled
appointments already in place.

## NAVIGATING THE MENUS

All menus work the same way: - Type the NUMBER shown in [ ] brackets and press Enter. - Enter 0 to go BACK to the previous menu. - Enter q from any screen to jump straight back to the MAIN MENU.

---

## MAIN MENU (numbers 0-5)

[1] Admit Patient
[2] Priority Queue
[3] Appointments
[4] Activity Log
[5] Admin Panel
[0] Exit (then choose [1] to restart or [0] to fully quit)


## MENU [1] - ADMIT PATIENT


[1] Register New Patient

---

Walks you through 8 steps. At each step, type the value and press Enter.
Press Enter with no input to skip optional fields.

    Step 1 - Full Name       : type the patient's full name (required)
    Step 2 - Age             : type a number 0-130, or press Enter to skip
    Step 3 - Gender          : type 1 Male / 2 Female / 3 Non-binary /
                               4 Other / 0 Prefer not to say
    Step 4 - Phone           : digits with spaces/hyphens (min 7 digits),
                               or press Enter to skip
    Step 5 - Doctor          : type the number [1]-[5] next to the doctor
    Step 6 - Preferred Time  : 24-hour HH:MM (e.g. 14:30),
                               or press Enter for default 09:00
    Step 7 - Condition       : describe symptoms (required)
    Step 8 - Notes           : allergies, history, etc., or press Enter
    Step 9 - Severity        : type 1 through 5
                                 1 = Critical (life-threatening)
                                 2 = Urgent   (high risk, 15 min)
                                 3 = Moderate (stable, 30 min)
                                 4 = Minor    (non-urgent)
                                 5 = Routine  (scheduled check-up)
    Step 10 - Confirmation   : review the summary, then type y to confirm
                               or n to cancel

NOTE: At any step, enter 0 to go back one step.

[2] Emergency Admission

---

Same flow as above but severity is automatically set to 1 (Critical)
and that step is skipped. The patient jumps to the top of the queue.

[3] View / Search Patient Records

---

Shows all patients ever admitted this session.

    [1]  All Records         : lists every patient and their status
    [2]  Search by Name      : type part of a name to filter results
    [3]  Search by ID        : type an exact patient ID number
    [4]  Filter by Status    : choose  1 waiting / 2 scheduled /
                               3 treated / 4 removed
    [0]  Back


## MENU [2] - PRIORITY QUEUE


Displays all patients currently waiting, ranked by severity (lowest
number = highest priority). Patients with the same severity are
ordered by admission time (earlier = higher priority).

[1] Treat Next (Extract-Min)

---

Automatically treats the HIGHEST-PRIORITY patient (the one at the
top of the heap). No input needed beyond confirming with Enter.

[2] Treat Specific Patient by ID

---

Shows the queue table, then prompts:

      Enter Patient ID to treat:  [type the ID number]

[3] Remove Patient by ID

---

Shows the queue table, then prompts:

      Enter Patient ID to remove:  [type the ID number]

Then confirms: type y to confirm or n to cancel.

[4] Show Raw Heap Array

---

Displays the internal backing array of the binary min-heap.
Index [0] is always the root (highest priority patient).
Press Enter to return.


## MENU [3] - APPOINTMENTS (Circular Queue, max 8 slots)


[1] Book Appointment

---

Shows all patients in the queue, then prompts:

      Enter Patient ID:        [type the ID number]
      Date (YYYY-MM-DD):       [e.g. 2025-07-14]
                               Press Enter for today's date.
      Time (HH:MM):            [e.g. 10:30]
                               Press Enter for the patient's preferred time.

A confirmation screen shows the booking details.
Type y to confirm or n to cancel.

NOTE: The circular buffer holds a maximum of 8 appointments.
If it is full, complete (dequeue) the next appointment first.

[2] View All Appointments

---

Shows all occupied slots in the circular buffer with slot number,
patient name, date, time, and doctor. Press Enter to return.

[3] Complete Next Appointment (Dequeue Head)

---

Removes and completes the OLDEST appointment at the head of the
circular queue. The patient's status is updated to "treated".
Press Enter to confirm.

[4] Search Appointments by Date

---

Prompts:

      Search date (YYYY-MM-DD):  [type the date]
                                  Press Enter for today.

Lists all appointments booked for that date.

[0] Back


## MENU [4] - ACTIVITY LOG


Displays a timestamped list of all system events this session
(admissions, treatments, removals, admin actions, etc.).

Press Enter to return to the main menu.


## MENU [5] - ADMIN PANEL


PIN-PROTECTED. The default PIN is: 1234

You have 3 attempts before being locked out for that session.

Once unlocked:

[1] Add Doctor

---

Prompts:

      Doctor name:  [type the name]

"Dr." is prepended automatically if you leave it out.

[2] Remove Doctor

---

Shows the numbered doctor list, then prompts:

      Select doctor number to remove [1-N]:  [type the number]

Confirms with y / n. At least one doctor must remain at all times.

[3] List All Doctors

---

Prints the current doctor roster. Press Enter to return.

[4] Reset All Session Data

---

Clears ALL patients, appointments, records, and the activity log.
Doctor list is preserved.
Requires TWO y confirmations before executing.

[5] Change Admin PIN

---

Three-step process:

    Step 1 - Enter current PIN     : type the 4-digit current PIN
    Step 2 - Enter new PIN         : type a new 4-digit numeric PIN
    Step 3 - Confirm new PIN       : retype the new PIN to confirm

[9] Lock Admin Session

---

Ends the admin session. The PIN will be required again next time.

[0] Back


## QUICK-REFERENCE: SPECIAL INPUT KEYS


Key Effect

---

0 Go BACK one level (or select "Prefer not to say" for gender)
q Jump immediately to the MAIN MENU from anywhere
Enter Accept default value (where a default is offered)
y Confirm a yes/no prompt
n Cancel a yes/no prompt


## EXAMPLE WALKTHROUGH - Admit and Treat a New Patient


1. From main menu, press 1 then Enter --> Admit Patient
2. Press 1 then Enter --> Register New Patient
3. Enter: Jane Smith --> name
4. Enter: 34 --> age
5. Enter: 2 --> Female
6. Enter: 416-555-0199 --> phone
7. Enter: 1 --> select Doctor #1 (Dr. Patel)
8. Enter: 11:00 --> preferred time
9. Enter: Chest pain --> condition
10. Press Enter --> skip notes
11. Enter: 2 --> Urgent
12. Enter: y --> confirm admission

13. Press 0 then Enter --> back to main menu
14. Press 2 then Enter --> Priority Queue
15. Press 1 then Enter --> Treat Next (Jane will appear at top
    if severity 2 is the highest priority)
