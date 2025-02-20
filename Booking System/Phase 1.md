Penetration Testing Report - Booking System Phase 1
Author: Maria
Date: 20/2/2025
**Tested System: Booking System - Phase 1**
Target URL: http://localhost:8000/register
Testing Environment: Kali Linux, Docker, OWASP ZAP, Burp Suite

1. **Introduction**
This penetration testing report aims to evaluate the security of the Booking System - Phase 1 by assessing vulnerabilities in its authentication system and overall security posture.

2. **Environment Setup**
2.1 Tools Used
Kali Linux (Penetration testing OS)
Docker (To run the application)
OWASP ZAP & Burp Suite (For security testing)
2.2 Setup Process
Cloned the project repository:
bash
Copy
Edit
git clone https://github.com/vheikkiniemi/animated-waddle.git
cd animated-waddle/Booking\ system/Phase\ 1/Ver1
Attempted to start the application using Docker:
bash
Copy
Edit
docker-compose up --build -d
Checked running containers:
bash
Copy
Edit
docker ps
Attempted to access http://localhost:8000/register in a browser.
3. **Issues Encountered**
Despite setting up the system, the application was not accessible at localhost:8000/register. Below are the errors encountered:

3.1 Connection Error
Browser displayed: "Unable to connect"
Ran docker ps and found that the web container was not running.
Checked logs using:
bash
Copy
Edit
docker-compose logs
Found errors related to database connection failure / missing dependencies.
3.2 Docker Issues
Running docker-compose returned an error:
bash
Copy
Edit
docker-compose: command not found
Solution attempted: Installed Docker Compose with:
bash
Copy
Edit
sudo apt install docker-compose
Retried but still unable to connect.
3.3 Port Issues
Checked if port 8000 was in use:
bash
Copy
Edit
ss -tulnp | grep 8000
No service was running on port 8000.
Tried using container's IP instead of localhost but still not accessible.
4. **Security Testing Plan**
Since I was unable to fully access the system, I outline the expected vulnerabilities and test scenarios that should be performed if the application was running.

4.1 Potential Vulnerabilities in Registration Page
ID	Vulnerability	Description	Risk Level	Testing Method
V1	SQL Injection	Check if malicious SQL queries can bypass authentication.	High	Use ' OR 1=1 -- in input fields.
V2	Cross-Site Scripting (XSS)	Inject <script>alert('XSS')</script> to test if JavaScript runs.	Medium	Input malicious scripts into form fields.
V3	Broken Authentication	Attempt to bypass login with default credentials.	High	Test with admin:admin or other weak passwords.
V4	Sensitive Data Exposure	Check if passwords are stored in plaintext.	High	Inspect responses for exposed credentials.
5. **Recommendations**
Even though the application was inaccessible, here are general recommendations for securing web applications:

Fix Docker Issues: Ensure that all containers start correctly and dependencies are installed.
Secure Authentication: Implement strong password policies and two-factor authentication.
Sanitize User Input: Use parameterized queries to prevent SQL injection.
Enable HTTPS: Encrypt communications using TLS.
Use Security Headers: Implement CSP, X-Frame-Options, and other headers.
6. **Conclusion**
Due to technical issues, I was unable to conduct a full penetration test on the Booking System. However, I identified key areas that should be tested for vulnerabilities. If the system is fixed and accessible, a detailed security assessment should be conducted using OWASP ZAP and Burp Suite.

