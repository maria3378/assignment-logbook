Penetration Testing Report – Booking System Phase 1
Author: Maria
Date: 20/2/2025
Target Application: Booking System - Phase 1
Testing Environment: Kali Linux, Docker, OWASP ZAP, Burp Suite
Application URL: http://localhost:8000/register

**1. Summary**
This report documents the penetration testing process for the Booking System - Phase 1. However, the application was not accessible due to technical issues. Below are the findings and recommendations.

**2. Testing Setup**

2.1 Tools Used
Kali Linux – Main testing OS
Docker – To run the application
OWASP ZAP & Burp Suite – For vulnerability assessment
2.2 Steps Taken
Cloned the project:
bash
Copy
Edit
git clone https://github.com/vheikkiniemi/animated-waddle.git
cd animated-waddle/Booking\ system/Phase\ 1/Ver1
Tried to start the application:
bash
Copy
Edit
docker-compose up --build -d
Checked running containers:
bash
Copy
Edit
docker ps
Attempted to access: http://localhost:8000/register

3. **Issues Encountered**
   
Issue	Description	Status
Application not accessible    |	http://localhost:8000/register returned "Unable to Connect." |	 Not Resolved
Docker service issues	docker-compose was not recognized as a valid command.         |	  Fixed (Installed Docker Compose)
Port 8000 not listening	No service running on port 8000.	 Not Resolved
Troubleshooting Steps Attempted
Checked container logs:
bash
Copy
Edit
docker-compose logs
Verified open ports:
bash
Copy
Edit
ss -tulnp | grep 8000
Restarted Docker and tried alternative access methods (container IP).
Despite these efforts, the issue remains unresolved.

4. **Expected Security Tests (If Accessible)**
   
Vulnerability	Description	Risk Level	Testing Method
SQL Injection	Bypass login using malicious SQL queries.	High	' OR 1=1 -- in input fields.
Cross-Site Scripting (XSS)	Inject JavaScript to exploit input validation.	Medium	<script>alert('XSS')</script> in form fields.
Broken Authentication	Test weak/default credentials.	High	Try admin:admin, password123.
Data Exposure	Check for plaintext password storage.	High	Inspect responses for sensitive data.

**5. Conclusion**
Due to technical issues, I was unable to conduct full penetration testing on the Booking System. If the system is fixed and accessible, further security testing should be performed.
