# Log-Analyser-V2
This is version 2 of the log analyser.
A Python-based security log analyser that processes login events and generates a simple security report.
The analyser reads a log file, counts successful and failed login attempts, identifies failed logins by IP address and username, and flags IP addresses with multiple failed login attempts as suspicious.

## Features

* Counts successful login attempts
* Counts failed login attempts
* Tracks failed login attempts by IP address
* Tracks failed login attempts by username
* Identifies potentially suspicious IP addresses
* Generates a readable security report in the console
* Processes log entries automatically from a text file

## How It Works

The analyser reads `securitylogins.txt` line by line and checks each entry for either:

* `LOGIN_SUCCESS`
* `LOGIN_FAILED`

Successful login events are added to the successful login count.

For failed login events, the analyser extracts:

* Username
* IP address

These values are then used to keep track of repeated failed login attempts.

An IP address is considered suspicious when it has **3 or more failed login attempts**.

## Example Log Format

The analyser expects log entries containing information similar to:

```text
2026-10-06 14:32:18 LOGIN_FAILED user=admin ip=192.0.2.15
2026-10-06 14:33:01 LOGIN_SUCCESS user=alex ip=192.0.2.20
```

The exact format needs to match the way the Python script extracts the username and IP address.

## Example Output

```text
==============================
       SECURITY LOG REPORT
==============================

Login Summary
------------------------------
Successful logins: 2
Failed logins: 5

Failed Logins by IP
------------------------------
192.0.2.15 : 5

Failed Logins by Username
------------------------------
admin : 3
alex : 2

Suspicious Activity
------------------------------
Suspicious IP: 192.0.2.15 - 5 failed login attempts
```

## Requirements

* Python 3
* A log file named `securitylogins.txt`

No external Python libraries are required.

## Installation

Clone the repository:

```bash
git clone https://github.com/malaikawaqasarshad/log-analyser-V2.git
```

Move into the project directory:

```bash
cd log-analyser
```

Make sure `securitylogins.txt` is in the same directory as the Python script.

## Usage

Run the analyser with:

```bash
python log_analyser.py
```

The program will read the log file and print the security report to the console.

## Project Structure

```text
log-analyser/
│
├── log_analyser.py
├── securitylogins.txt
└── README.md
```

## Suspicious Activity Detection

Version 2 introduces basic suspicious activity detection.

The analyser checks the number of failed login attempts associated with each IP address.

If an IP address has **3 or more failed attempts**, it is reported as suspicious.

For example:

```text
192.0.2.15 : 5
```

will result in:

```text
Suspicious IP: 192.0.2.15 - 5 failed login attempts
```

This is a basic detection rule intended for learning and demonstration purposes. A real security monitoring system would typically use additional factors before determining whether activity is malicious.

## Version 2 Improvements

Compared with a basic log analyser, Version 2 adds more security-focused analysis.

### Version 2 includes:

* Login success tracking
* Login failure tracking
* Failed attempts grouped by IP
* Failed attempts grouped by username
* Basic suspicious IP detection
* Structured security reporting

## Future Improvements

Possible improvements for future versions include:

* Configurable suspicious activity thresholds
* Detection of repeated failed logins within a specific time period
* Detection of multiple usernames being targeted from one IP
* Exporting reports to CSV or JSON
* Date and time analysis
* Improved log parsing
* Command-line arguments for selecting log files
* More detailed security alerts
* Automated report generation

## Disclaimer

This project is intended for learning, development, and security analysis of logs that you are authorised to analyse.

## License

This project is licensed under the MIT License.
