# 🔎 Advanced Web Directory Scanner

An automated Python-based web directory enumeration tool designed to identify accessible directories and resources on an authorized web server using a wordlist.

The scanner sends HTTP requests to potential paths and analyzes the server's responses to identify interesting resources such as login pages, administrative directories, backups, APIs, and other accessible endpoints.

## 🎯 Objective

Web servers may contain directories and files that are not directly linked from the main website.

The objective of this project is to automate the discovery of these resources during **authorized security assessments**.

## 🚀 Features

* 🔎 Automated directory enumeration
* 📄 Wordlist-based scanning
* ⚡ Multithreaded scanning
* 📊 HTTP status-code analysis
* ⏱️ Response-time measurement
* 📦 Response-size detection
* 🔀 Redirect detection
* 🔐 Authentication-required detection
* 📋 Content-Type identification
* 💾 CSV report generation
* 📈 Scan progress tracking
* 🛑 Connection and timeout handling

## 🧠 How It Works

```text
Target Web Server
       ↓
Read Wordlist
       ↓
Generate URLs
       ↓
Send HTTP Requests
       ↓
Analyze HTTP Responses
       ↓
┌──────────┬──────────┬───────────┐
│ Status   │ Response │ Response  │
│ Code     │ Size     │ Time      │
└──────────┴──────────┴───────────┘
       ↓
Classify Results
       ↓
Generate CSV Report
```

## 📊 HTTP Status Codes

The scanner interprets common HTTP responses:

| Status | Meaning                                     |
| ------ | ------------------------------------------- |
| 200    | Resource exists                             |
| 301    | Permanent redirect                          |
| 302    | Temporary redirect                          |
| 401    | Authentication required                     |
| 403    | Resource may exist but access is restricted |
| 404    | Resource not found                          |
| 500    | Server error                                |
| 503    | Service unavailable                         |

## ⚡ Multithreading

The scanner uses Python's `ThreadPoolExecutor` to perform multiple HTTP requests concurrently.

This reduces scanning time compared with sending every request sequentially.

```python
ThreadPoolExecutor(max_workers=10)
```

The number of concurrent workers can be adjusted depending on the authorized testing environment.

## 🛠️ Technologies Used

* Python
* Requests
* Concurrent Futures
* CSV
* URL parsing
* HTTP protocol concepts

## 📂 Project Structure

```text
Advanced-Web-Directory-Scanner/
│
├── scanner.py
├── common.txt
├── scan_results.csv
├── README.md
└── requirements.txt
```

## ▶️ How to Run

### 1. Install dependencies

```bash
pip install requests
```

### 2. Create a wordlist

Example:

```text
admin
login
robots.txt
test
backup
uploads
images
css
js
api
dashboard
config
```

Save it as:

```text
common.txt
```

### 3. Configure the target

Inside the Python program:

```python
TARGET_URL = "http://AUTHORIZED-TARGET"
WORDLIST = "common.txt"
```

### 4. Run the scanner

```bash
python scanner.py
```

## 📋 Example Output

```text
======================================================================
        ADVANCED WEB DIRECTORY SCANNER
======================================================================

Target      : http://authorized-target
Wordlist    : common.txt
Directories : 12
Threads     : 10

[+] Starting scan...

[200] FOUND
http://authorized-target/login

[403] FORBIDDEN
http://authorized-target/admin

[302] REDIRECT
http://authorized-target/dashboard

======================================================================
                    SCAN SUMMARY
======================================================================

Total URLs scanned : 12
Interesting URLs   : 3
Scan time          : 1.25 seconds

[+] Results saved to: scan_results.csv
[+] Scan completed!
```

## 📄 Output Report

The scanner generates:

```text
scan_results.csv
```

The report contains:

```text
URL
Status Code
Result
Response Size
Response Time
Content Type
Redirect Location
```

This allows the scan results to be analyzed later or imported into spreadsheet/data-analysis tools.

## 🔐 Cybersecurity Use Case

Directory enumeration is commonly used during the **reconnaissance and discovery phase** of authorized web security assessments.

It can help security testers identify:

* Administrative interfaces
* Login endpoints
* Backup directories
* Upload locations
* APIs
* Development/test directories
* Potentially exposed resources

Finding a directory does **not automatically mean that it is vulnerable**. Further authorized security testing is required to determine whether a discovered resource presents a security issue.

## ⚠️ Legal & Ethical Disclaimer

This tool is intended **only for authorized security testing, educational labs, and systems you own or have explicit permission to assess**.

Do not scan public websites or systems without authorization.

The developers are not responsible for misuse of this software.

## 👨‍💻 Project

**Advanced Web Directory Scanner – Automated Web Resource Discovery Tool**

Developed as an educational cybersecurity project demonstrating HTTP analysis, directory enumeration, automation, multithreading, and security reporting.
