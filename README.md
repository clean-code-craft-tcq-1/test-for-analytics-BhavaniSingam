# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Need a Threshold value to calculate
3. Read and Write access to the server (storing pdf file) 
4. For Whom notification should send (details of receiver if it is via email and also needed the medium which it needs to be sent)
5. third party applications need to record trends

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | Not required to check third party applications
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | No            | Not required to check third party applications

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write the number of times of breach to the PDF, when the csv file contains value that breaches either maximum or minimum values.
4. Write "No breaches found" to the PDF when the csv doesnt contain any breaches
5. Write "Session ended" when the session to the server ended abruptly
6. Write "File Not Found" to the PDF when the csv file is not available in the server
7. Check if the notification is sent after every new PDF generation.
8. Write "No increasing trend in values " to the PDF when the csv doesnt contain any trends.
9. Verify if new PDF is stored every week.
10. Check if battery telemetrics is stored in proper format in CSV

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | PDF          | sent/unsent                 | fake notification
Report inaccessible server | Access to server |Access denied              | fake the access to server
Find minimum and maximum   | csv data     |   Values of min&max           | None - it's a pure function
Detect trend               | csv data     | internal data-structure          | None - it's a pure function
Write to PDF               | csv file |      pdf       | Fake the call to offshelf convertor
