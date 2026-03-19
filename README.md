# DiponegoroUniversity-Bug

# Security Advisory: Multiple Information Disclosure Vulnerabilities in Undip Subdomains

## Executive Summary
During a routine security research, I discovered several high-impact information disclosure vulnerabilities across multiple subdomains of `undip.ac.id`. These vulnerabilities expose sensitive data including **Personally Identifiable Information (PII)** of students, internal financial records, and project budget details (RAB) to the public without any authentication.

---

## Vulnerability Details

### 1. Sensitive Data Exposure (Student Academic Records)
- **Vulnerability Type:** Information Disclosure / PII Leakage  
- **Target:** `gizi.fk.undip.ac.id` (and related subdomains)  
- **Severity:** **High**  

**Description:**  
Publicly accessible Excel files containing full names and detailed academic grades of students.

**Impact:**  
- Breach of student privacy  
- Risk of identity theft  
- Potential for targeted phishing attacks  

---

### 2. Internal Financial & Budget Disclosure (LPPM & Projects)
- **Vulnerability Type:** Information Disclosure  
- **Target:** `uppm.ft.undip.ac.id`, `tekkom.ft.undip.ac.id`  
- **Severity:** **Medium - High**  

**Description:**  
Exposure of internal grant research budgets, lecturer NIDN, and detailed construction project budgets (RAB).

**Impact:**  
- Leakage of sensitive financial data  
- Exposure of institutional strategies  
- Potential misuse by competitors or malicious actors  

---

### 3. Server Misconfiguration & Potential Backup Leaks
- **Vulnerability Type:** Security Misconfiguration  
- **Target:** Multiple subdomains  

**Description:**  
Discovery of publicly accessible `error_log` files and potential archive files such as `.zip` and `.rar` in open directories.

**Impact:**  
- Exposure of server internal structure  
- Possible leakage of source code or backup data  
- Increased attack surface for further exploitation  

**Tools Used:**  
- `ffuf`  
- Google Dorking  
- `curl`  

---

## Proof of Concept (PoC)

### Directory Fuzzing Results
Using `ffuf` to identify hidden directories:

```bash
ffuf -u https://[subdomain].undip.ac.id/FUZZ -w common.txt -fw 207 -fs 0
