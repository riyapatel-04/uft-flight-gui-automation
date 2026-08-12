# UFT Test Automation — Flight GUI (OpenText MyFlight Sample App)

**Course:** INFO6255 – Software Quality Control and Management, Northeastern University
**Term:** Summer 2026
**Tool:** OpenText / Micro Focus UFT One (25.2)
**Language:** VBScript

## Overview

This project automates the ticket-booking flow of the **OpenText MyFlight Sample Application** using UFT One. The script logs in, books a flight, and completes an order — repeated **4 times** with 4 different data rows — using a fully **data-driven framework** with **zero hard-coded values**.

## Project Structure

```
UFT Assignment/
├── UFTFinalScript_Group4.txt      # Main VBScript automation script
├── FlightTestData_Group4.xlsx     # DataTable source — all test data, credentials, paths
└── UFT_Screenshots/               # Before/After screenshots for every form, per booking
    ├── Booking1_01_Login_Before.png
    ├── Booking1_02_Login_After.png
    ├── ... (Booking, FlightSelect, Passenger, Confirmation steps)
    └── CP2_Bitmap_Reference.png   # Reference image for the bitmap checkpoint
```

## Framework Highlights

- **Data-Driven Design** — `AppPath`, `ScreenshotFolder`, `Username`/`Password`, `FromCity`/`ToCity`, `FlightDate`, `Class`, `Passengers`, and `PassengerName` are all read from `dtGlobalSheet` via `DataTable(...)`. No values are hard-coded in the script.
- **Object Repository** — Most objects were captured via UFT's record feature. The `flightsDataGrid` (WpfTable) object was **manually added** to the Object Repository using Object Spy, per the assignment requirement.
- **4 Bookings, 4 Logins** — The script logs in and completes a full booking cycle 4 times, once per row in the data sheet.
- **Screenshots** — `Desktop.CaptureBitmap` fires before and after every form is filled (Login, Booking, Flight Selection, Passenger), for every booking.
- **Error Handling** — App-launch failure and post-booking screen checks report a failure and call `ExitTest` rather than silently continuing.
- **Dynamic Data File Lookup** — The script checks for `FlightTestData_FINAL.xlsx`, then `FlightTestData_UPDATED.xlsx`, then `FlightTestData.xlsx` in the UFT test folder, so it isn't tied to one exact filename.

## Checkpoints (4 total — 3 Pass, 1 Fail)

| # | Checkpoint | Type | Booking | Result |
|---|---|---|---|---|
| CP1 | `CP1_Title_Text_PASS` | Text | Booking 1 | Pass |
| CP2 | `CP2_BookingForm_Bitmap_PASS` | Bitmap | Booking 2 | Pass |
| CP3 | `CP3_PassengerName_Text_PASS` | Text | Booking 3 | Pass |
| CP4 | `CP4_TotalPrice_Text_FAIL_ONCE` | Text | Booking 3 | **Intentional Fail** (wrong expected price, runs once only) |

> **Note:** These checkpoints must exist in the UFT Object Repository under these exact names before running the script — they are referenced, not created, by the code.

## How to Run

1. Install **OpenText Functional Testing (UFT One) 25.2** with the **WPF Add-in** enabled.
2. Place `FlightTestData_Group4.xlsx` in the same UFT test folder as the script.
3. Create the 4 checkpoints listed above in the Object Repository (names must match exactly).
4. Open `UFTFinalScript_Group4.txt` in UFT and run.
5. The script launches the MyFlight app, runs all 4 bookings, and opens the screenshots folder automatically at the end.
6. Check the final `Reporter.ReportEvent` summary for the pass/fail status of all 4 checkpoints.

## Assignment Requirements Checklist

- [x] Data-driven framework, no hard-coded values
- [x] Object Repository used, with one object manually added via Object Spy
- [x] 4 checkpoints — 3 Pass, 1 Fail (at least 1 Bitmap + 1 Text), fail occurs once only
- [x] Adequate comments throughout
- [x] Before/after screenshots for every form
- [x] 4 repetitions across 4 data rows, with login each time
- [x] Test report shows pass/fail status for all checkpoints

## Team

Riya Patel · Tanmay Devraj Pillai · Gunashree Rajakumar
