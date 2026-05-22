# Bookme Single-File Selenium Guide

This document explains:
- how to run the script,
- what each test case does,
- what each code section does,
- and how to adjust speed/logs for demo.

File covered in this guide:
- `bookme_single_file_10_tc.py`

## 1. Project Purpose

This project is a **single-file Selenium automation suite** for Bookme.pk (no Page Object Model), designed for final-lab style demonstration.

It runs **10 real user-flow test cases** and prints:
- `[STEP]` for every action,
- `[RESULT]` for captured business data (prices, event name, car detail),
- `[PASS]/[FAIL]` per test case,
- final summary table.

## 2. How To Run

Open PowerShell in:

`C:\Users\DELLL\Desktop\ast lab final\selenium_bookme_clean_project\selenium_bookme_clean_project`

Run:

```powershell
python bookme_single_file_10_tc.py
```

If `python` does not work:

```powershell
py bookme_single_file_10_tc.py
```

## 3. Run Slowly For Presentation

You can slow execution so teacher can see each action:

```powershell
$env:BOOKME_STEP_DELAY_SECONDS='2.0'
python bookme_single_file_10_tc.py
```

Faster run:

```powershell
$env:BOOKME_STEP_DELAY_SECONDS='0.5'
python bookme_single_file_10_tc.py
```

## 4. Test Cases Implemented

## TC-01: Verify homepage loads
- Opens `https://bookme.pk`
- Confirms major travel content is visible
- Prints detected service sample

## TC-02: Verify main services visible
- Confirms Flights, Bus, Hotel, Movies, Events tabs are visible
- Prints verified tabs

## TC-03: Car Rental flow (updated as requested)
- Opens `https://bookme.pk/car-rental-booking-online`
- Enters city `Lahore`
- Selects Lahore from dropdown
- Selects pickup/drop-off dates
- Clicks Search
- Captures first car-related detail text and prints it

## TC-04: Login success check
- Opens login modal
- Uses provided credentials
- Normalizes phone format for Bookme input
- Clicks Sign in
- Verifies successful account state (`My Bookings` / wallet context)
- Prints user/session badge
- Includes retry if first attempt fails

## TC-05: Flight one-way search Lahore -> Karachi
- Opens flights page
- Selects One Way
- Fills Departure = Lahore, Arrival = Karachi
- Selects date
- Clicks Search
- Waits for result list + ticket prices
- Captures and prints flight prices

## TC-06: Events page flow (updated as requested)
- Opens `https://bookme.pk/event-tickets-online`
- Waits for event cards
- Captures first real event name from card text
- Attempts to select it
- Prints event name + events URL

## TC-07: Verify flight ticket prices visible
- Runs flight search flow
- Waits for flight pricing area
- Captures price values and prints them

## TC-08: Bus search Lahore -> Islamabad
- Opens bus page
- Selects route
- Verifies route context
- Prints route URL

## TC-09: Verify bus availability + prices
- Runs bus route flow
- Confirms availability context
- Extracts and prints bus ticket prices when available

## TC-10: Bus seat-selection progression
- Opens first available bus card from results
- Clicks `Go to seat selection`
- Verifies seat-selection step is visible
- Prints seat-selection status

## 5. Console Output Meaning

- `[STEP] ...`  
  Action currently being performed.

- `[RESULT] ...`  
  Captured business detail from page (prices, names, URLs, etc.).

- `[PASS] ...`  
  Test case passed.

- `[FAIL] ...`  
  Test case failed (see `[ERROR]` line).

At end:
- summary table with pass/fail for all 10.

## 6. Code Structure Explanation

The script is organized in plain functions:

## A) Configuration
- `BASE_URL`, login credentials, waits, speed delay.
- `PROFILE_ROOT` keeps isolated browser profiles.

## B) Utility / Logging Functions
- `print_banner()`: pretty section headers.
- `log_step()`: per-step actions.
- `log_result()`: business data output.
- `step_pause()`: configurable delay between actions.

## C) Browser Setup Functions
- `resolve_chromedriver_path()`: finds local chromedriver.
- `start_browser()`: starts Chrome with options.
- `close_browser()`: quits and removes temp profile folder.

## D) Selenium Action Wrappers
- `safe_get()`: safe page open with timeout handling.
- `click()`: robust click with JS fallback.
- `type_text()`: clear and type input.
- `click_first_visible()`: clicks first visible element matching XPath.

## E) Data Extraction Helpers
- `page_text()`, `page_lines()`: fetch page text.
- `extract_visible_prices()`, `extract_prices_from_lines()`: capture PKR values.
- `extract_first_car_detail()`: pulls first car detail text.
- `extract_first_event_name_from_cards()`: robust first event title extraction.

## F) Flow Helpers
- `open_home()`
- `open_login_modal()`
- `search_flight_lahore_to_karachi()`
- `search_bus_lahore_to_islamabad()`

These helpers are reused by multiple test cases.

## G) Test Case Functions
- `tc_01_...` to `tc_10_...`
- Each function:
1. performs one business journey,
2. validates expected behavior,
3. prints captured details,
4. returns a short success message.

## H) Runner
- `run_test_case()`: wraps each TC in try/except, prints PASS/FAIL.
- `main()`: executes all 10 test cases and prints final summary.

## 7. Why Some Chrome Lines Appear In Terminal

You may see lines like:
- `DevTools listening ...`
- `gcm ...`
- `page_load_metrics ...`

These are browser internal logs and usually not test failures.

Always check:
- `[PASS]/[FAIL]` lines
- final summary.

## 8. Common Troubleshooting

## Browser does not open
- Make sure Chrome is installed.
- Ensure Selenium can access `chromedriver`.
- Re-run in normal PowerShell window (not restricted terminal).

## Test is too fast
- Increase delay:
```powershell
$env:BOOKME_STEP_DELAY_SECONDS='2.5'
python bookme_single_file_10_tc.py
```

## Login fails intermittently
- Script already includes one retry.
- Network/session behavior on site can still vary.

## Dynamic site content changed
- Update target XPath in specific test function.
- Keep the same function structure and logs.

## 9. Submission Note

This implementation follows your teacher’s requirement:
- single-file automation,
- no POM abstraction,
- explicit step-by-step Selenium logic,
- visible and explainable business-flow checks.
