# SQL-injection-in-Directory-Management-System-v2.0
SQL injection in Directory Management System v2.0


### Title
SQL Injection Leading to Admin Authentication Bypass in Directory Management System v2.0

### Product
Directory Management System

### Vendor
PHPGurukul

### Vendor Homepage
https://phpgurukul.com/directory-management-system-using-php-and-mysql/

### Software Download Link
https://phpgurukul.com/directory-management-system-using-php-and-mysql/

### Affected Version
v2.0

### Affected File
/dms/admin/index.php

### Affected Parameter
adminuser (username field)

### Vulnerability Type
SQL Injection (Authentication Bypass)

### Attack Vector
Remote / Unauthenticated

### Description
A SQL Injection vulnerability exists in the /dms/admin/index.php file of the Directory Management System v2.0.
The application fails to properly sanitize user-supplied input before incorporating it into an SQL query.
The adminuser parameter is directly concatenated into a SQL statement without input validation or prepared statements. This allows an unauthenticated attacker to inject arbitrary SQL logic, resulting in an authentication bypass and unauthorized administrative access.

### Vulnerable Code Snippet
```
$query = mysqli_query($con,
"select ID from tbladmin where UserName='$adminuser' && Password='$password'");
```

### Proof of Concept (PoC)
```
Request Type: POST
Target: /dms/admin/index.php

Injected Payload (Username field):

admin' OR 1='1

Password field: Any value
```
<img width="3264" height="1162" alt="image" src="https://github.com/user-attachments/assets/7cc346a7-0299-4d6c-8512-1e594dd364f3" />
<img width="3264" height="1162" alt="image" src="https://github.com/user-attachments/assets/7cc346a7-0299-4d6c-8512-1e594dd364f3" />



### Result
The injected SQL condition always evaluates to true, allowing an attacker to bypass authentication and gain administrator-level access without valid credentials.

### Impact
Authentication bypass
Unauthorized administrative access
Potential full application compromise
Ability to manipulate or extract sensitive data

### Severity
High

### Root Cause
Improper handling of user input and lack of prepared statements or input sanitization in SQL queries.

### Recommended Fix
Use prepared statements with parameterized SQL queries
Implement strict input validation
Avoid direct concatenation of user input into SQL queries
Disclosure Status
Vendor did not respond or provide a security contact at the time of disclosure.

### Credit
Discovered by:
bhanugoudm041
Contact: https://github.com/bhanugoudm041
