
# Logbook

| Date       | Used Hours | Subject(s)          | Output            |
|------------|------------|---------------------|-------------------|
| 30.10.2024 | 2          | Kick-off lecture    | Lecture recording |
| 31.10.2024 | 2          | Kick-off lecture    | Lecture recording |
| 01.11.2024 | 3          | Design discussion   | Wireframes draft  |
| 02.11.2024 | 4          | Coding: Login page  | Functional login  |



# Logbook - Booking System Phase 1

## 1. Initial Setup
- Cloned the repository:
  ```bash
  git clone https://github.com/vheikkiniemi/animated-waddle.git
  cd animated-waddle/Booking\ system/Phase\ 1/Ver2


## 2. Built and ran the database:


docker compose -f 'docker-compose.yml' up -d --build 'database'
Built and ran the web interface:


docker compose -f 'docker-compose.yml' up -d --build 'web'





# Logbook – Booking System Project (Phase 2)  

## Date:  16/3/2025
## Author:  maria
## Project: Booking System – Phase 2  
## Version Tested: Ver1  

---

## Part 1 – Step 1: Application Testing  

### Repository Setup & Initial Review  
- Cloned the updated repository  
- Reviewed the application structure, dependencies, and documentation  

### Application Deployment  
- Started the application using Docker  
docker-compose up --build

pgsql
Copy
Edit
or followed alternative setup instructions as per the documentation  

### Functional Testing  
Conducted a preliminary test to assess core functionalities  
- User authentication (login/logout)  
- Role-based access control  
- Form validation and input handling  
- Navigation and responsiveness  
- API endpoints and request handling  

Issues Identified  
- SQL Injection risk in authentication module  
- Weak password policy with no lockout mechanism  

---

## Part 1 – Step 2: Security & Penetration Testing  

### Static Code Analysis (Checkmarx)  
- Ran a security scan using Checkmarx targeting the application’s codebase  
- Identified vulnerabilities such as  
- SQL Injection risks in authentication module  
- Cross-Site Scripting (XSS) vulnerabilities in user input fields  
- Insecure API endpoints exposing sensitive data  
- Saved the results as checkmarx_report.md and uploaded it to GitHub  

### Dynamic Security Testing (OWASP ZAP)  
- Conducted an automated scan using OWASP ZAP to identify real-time vulnerabilities  
- Key findings included  
- Lack of input validation leading to possible XSS attacks  
- Session Management Weaknesses – session tokens not invalidated after logout  
- Server misconfiguration issues exposing stack traces  
- Generated a detailed ZAP security report (zap_report.md) and committed it to GitHub  

GitHub Repository Update  
mkdir "Booking system - Phase 2" mv checkmarx_report.md zap_report.md "Booking system - Phase 2/" git add . git commit -m "Added Checkmarx & ZAP security reports" git push origin main

yaml
Copy
Edit

GitHub Repo Link:  

---

## Part 2 – Step 1: Password Cracking Attempt  

### Extracting Password Hashes  
- Retrieved hashed passwords from the database  
- Determined hash type using hashid  
hashid hashfile.txt

shell
Copy
Edit
- Result: SHA256  

### Cracking Passwords with Hashcat  
Executed a dictionary attack using rockyou.txt  
hashcat -m 1400 -a 0 hashfile.txt rockyou.txt --force

yaml
Copy
Edit
- Attack duration:  

Cracked Passwords  
| Username         | Recovered Password | Time Taken |
|-----------------|-------------------|------------|
| john@doe.com    | secret1234        | 2 min      |
| admin@test.com  | adminpass         | 5 min      |
| user@example.com| password1         | 10 min     |

---

## Part 2 – Step 2: Findings & Logbook Update  

### Summary of Security Risks Identified  
Critical  
- SQL Injection Vulnerability in authentication  
- Weak password storage – Unsalted SHA256 hashes  
- Exposed session tokens (potential session hijacking)  

Moderate  
- XSS vulnerabilities in form inputs  
- Unrestricted API access exposing sensitive data  

Low Risk  
- Security headers missing (e.g., Content-Security-Policy, X-Frame-Options)  

### Suggested Mitigations  
- Implement prepared statements to prevent SQL injection  
- Strengthen password storage with bcrypt or Argon2 instead of SHA256  
- Enforce multi-factor authentication (MFA) for admin users  
- Implement input validation and escaping mechanisms for user inputs  
- Secure session handling by invalidating tokens after logout  

---

## Final Notes & Next Steps  
- All penetration test reports have been uploaded to GitHub  
- Password cracking results have been documented  
- Security risks and recommended improvements have been noted for the next phase  
- Awaiting feedback and further instructions  
