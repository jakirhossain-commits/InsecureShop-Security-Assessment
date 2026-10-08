# InsecureShop Security Assessment

> **Advanced Penetration Testing Report**
>
> A comprehensive security vulnerability assessment of the InsecureShop vulnerable Android application.

![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)
![Vulnerabilities Found](https://img.shields.io/badge/Vulnerabilities-21-critical?style=flat)
![Report Type](https://img.shields.io/badge/Type-Penetration%20Test-blue?style=flat)
![Testing Date](https://img.shields.io/badge/Date-October%202026-informational?style=flat)
![Complexity](https://img.shields.io/badge/Complexity-Expert-red?style=flat)

---

## 📋 Executive Summary

This repository contains a **professional penetration testing report** for the **InsecureShop** vulnerable Android e-commerce application. The assessment identified **21 critical security vulnerabilities** across authentication, data storage, API security, and infrastructure components.

### Key Findings
- **Total Vulnerabilities:** 21
- **Critical Severity:** 8
- **High Severity:** 9
- **Medium Severity:** 4
- **Assessment Methodology:** Static + Dynamic + API + Infrastructure Testing
- **Report Format:** Professional with CVSS 3.1 Scoring & Visual Evidence

---

## 🎯 Assessment Overview

### Testing Scope
| Category | Details |
|---|---|
| **Application Name** | InsecureShop (E-commerce Android App) |
| **Package Name** | com.insecureshop |
| **Testing Type** | Black-box Penetration Testing |
| **Methodology** | OWASP Mobile Top 10 + API Testing |
| **Tools Used** | ADB, JADX, Burp Suite, MobSF, Frida |
| **Assessment Period** | October 2026 |
| **Evidence Included** | 4 embedded screenshots with annotations |
| **Tester** | Md. Jakir Hossain (Junior Penetration Tester) |

### Testing Phases
1. ✅ **Environment Setup** - Application installation and configuration
2. ✅ **Static Analysis** - APK decompilation and code review
3. ✅ **Dynamic Analysis** - Runtime testing with visual evidence
4. ✅ **API Security Testing** - Backend endpoint analysis
5. ✅ **Infrastructure Assessment** - Server-side vulnerabilities
6. ✅ **Documentation** - Professional report with PoC and screenshots

---

## 🔴 Vulnerabilities Identified (21 Total)

### CRITICAL SEVERITY (8)

#### 1. Weak Authentication Implementation
**CVSS Score:** 9.8 (Critical) | **CWE:** CWE-287 | **OWASP:** A1 - Broken Authentication

Default credentials and hardcoded authentication tokens enable unauthorized access.

**Evidence:** Screenshots showing login bypass, hardcoded tokens in code  
**Impact:** Complete account takeover, administrative access

---

#### 2. Insecure Data Storage
**CVSS Score:** 9.6 (Critical) | **CWE:** CWE-200 | **OWASP:** A2 - Insecure Data Storage

Sensitive user data (credentials, tokens, PII) stored in plaintext.

**Storage Locations:** SharedPreferences, SQLite (unencrypted), temporary files  
**Impact:** Privacy breach, credential theft, identity fraud

**Vulnerable Data Found:**
- User credentials (username/password)
- API tokens and session cookies
- Credit card information
- Personal identification data
- Payment history

---

#### 3. API Authentication Bypass
**CVSS Score:** 9.7 (Critical) | **CWE:** CWE-640 | **OWASP:** A1 - Broken Authentication

API endpoints lack proper authentication, allowing unauthorized access.

**Evidence:** Burp Suite traffic capture showing requests without authentication  
**Impact:** Unauthorized data access, manipulation of user information

**Vulnerable Endpoints:**

GET /api/users/{id} # No authentication required
POST /api/orders/{order_id} # Authentication bypass possible
GET /api/payments # Exposes all payment data

---

#### 4. SQL Injection in API & Database
**CVSS Score:** 9.9 (Critical) | **CWE:** CWE-89 | **OWASP:** A1 - Injection

Multiple SQL injection points in API endpoints and application code.

**Vulnerable Parameters:** Search fields, user profile lookups, order filtering  
**Impact:** Database compromise, data theft, administrative access

**Proof of Concept:**

GET /api/users/search?name=' OR '1'='1
GET /api/orders?user_id=1' UNION SELECT * FROM users--

---

#### 5. Insecure API Communication
**CVSS Score:** 9.4 (Critical) | **CWE:** CWE-295 | **OWASP:** A6 - Sensitive Data Exposure

APIs transmit sensitive data over unencrypted HTTP or without proper validation.

**Evidence:** Network traffic capture showing plaintext data transmission  
**Impact:** Man-in-the-Middle (MITM) attacks, credential interception

---

#### 6. Hardcoded API Keys & Secrets
**CVSS Score:** 9.2 (Critical) | **CWE:** CWE-798 | **OWASP:** A6 - Sensitive Data Exposure

API keys, encryption keys, and backend secrets hardcoded in the application.

**Evidence:** Decompilation reveals hardcoded credentials  
**Keys Found:**
- AWS S3 access keys
- Database connection strings
- Payment gateway tokens
- Firebase API keys

---

#### 7. Unencrypted Local Storage
**CVSS Score:** 9.1 (Critical) | **CWE:** CWE-256 | **OWASP:** A2 - Insecure Data Storage

Sensitive files stored without encryption in accessible directories.

**Evidence:** Screenshots showing readable files with adb pull  
**Impact:** Complete compromise of stored sensitive data

---

#### 8. Broken Authorization
**CVSS Score:** 8.9 (Critical) | **CWE:** CWE-639 | **OWASP:** A5 - Broken Authorization

Users can access and modify other users' data and administrative functions.

**Evidence:** Authorization bypass allowing user escalation  
**Impact:** Privilege escalation, unauthorized data modification

---

### HIGH SEVERITY (9)

#### 9. Weak Cryptography
**CVSS Score:** 8.2 (High) | **CWE:** CWE-327 | **OWASP:** A5 - Broken Cryptography

Deprecated and weak cryptographic algorithms used for sensitive data.

**Weaknesses:** MD5 hashing, DES encryption, hardcoded keys  
**Impact:** Encrypted data can be decrypted

---

#### 10. Missing Certificate Pinning
**CVSS Score:** 7.8 (High) | **CWE:** CWE-295 | **OWASP:** A6 - Sensitive Data Exposure

No SSL/TLS certificate pinning allows MITM attacks via malicious certificates.

**Evidence:** Burp Suite intercepts HTTPS traffic without errors  
**Impact:** Session hijacking, credential theft

---

#### 11. Insecure WebView Implementation
**CVSS Score:** 8.1 (High) | **CWE:** CWE-79 | **OWASP:** A3 - Sensitive Data Exposure

WebView component vulnerable to XSS and allows JavaScript execution without validation.

**Vulnerabilities:**
- JavaScript enabled without input validation
- File system access enabled
- DOM manipulation possible

---

#### 12. Intent-based Vulnerabilities
**CVSS Score:** 7.5 (High) | **CWE:** CWE-927 | **OWASP:** A1 - Access Control

Exported activities and broadcast receivers without proper protection.

**Impact:** Unauthorized functionality access, data theft

---

#### 13. Sensitive Data in Logs
**CVSS Score:** 7.2 (High) | **CWE:** CWE-532 | **OWASP:** A9 - Using Components with Known Vulnerabilities

Sensitive information (credentials, tokens, PII) logged and accessible via logcat.

**Evidence:** Screenshots showing logcat output with sensitive data  
**Data Exposed:** Passwords, API tokens, user IDs, transaction data

---

#### 14. Insecure Deserialization
**CVSS Score:** 8.0 (High) | **CWE:** CWE-502 | **OWASP:** A8 - Insecure Deserialization

Unsafe deserialization of untrusted data from API responses.

**Impact:** Remote code execution, application crash

---

#### 15. File Permission Issues
**CVSS Score:** 7.3 (High) | **CWE:** CWE-276 | **OWASP:** A2 - Insecure Data Storage

Application data files have improper permissions, accessible to other apps.

**Evidence:** adb shell commands revealing world-readable files  
**Impact:** Unauthorized access to sensitive application data

---

#### 16. Insecure File Upload
**CVSS Score:** 7.6 (High) | **CWE:** CWE-434 | **OWASP:** A4 - Insecure File Upload

File upload functionality lacks validation, allowing malicious file uploads.

**Vulnerabilities:**
- No file type validation
- No size restrictions
- Predictable upload locations
- Executable files allowed

---

#### 17. Missing Input Validation
**CVSS Score:** 7.4 (High) | **CWE:** CWE-20 | **OWASP:** A3 - Injection

User input not properly validated before processing, leading to multiple attack vectors.

**Impact:** Injection attacks, XXE, command injection

---

### MEDIUM SEVERITY (4)

#### 18. Debuggable Application
**CVSS Score:** 6.8 (Medium) | **CWE:** CWE-489 | **OWASP:** A9 - Using Components with Known Vulnerabilities

Application compiled with debugging enabled in production build.

**Evidence:** android:debuggable="true" in AndroidManifest.xml  
**Impact:** Complete application control via ADB

---

#### 19. Hardcoded Configuration Values
**CVSS Score:** 6.5 (Medium) | **CWE:** CWE-798 | **OWASP:** A6 - Sensitive Data Exposure

Server addresses, encryption keys, and configuration hardcoded in the app.

**Impact:** Inability to update configuration without app release

---

#### 20. Insecure HTTP Usage
**CVSS Score:** 6.2 (Medium) | **CWE:** CWE-295 | **OWASP:** A6 - Sensitive Data Exposure

Application uses HTTP for some communications instead of HTTPS.

**Endpoints:** Several API endpoints use unencrypted HTTP  
**Impact:** Data interception, MITM attacks possible

---

#### 21. Missing Security Headers
**CVSS Score:** 6.0 (Medium) | **CWE:** CWE-693 | **OWASP:** A5 - Security Misconfiguration

API responses lack security headers (HSTS, CSP, X-Frame-Options).

**Missing Headers:**
- Strict-Transport-Security
- Content-Security-Policy
- X-Frame-Options
- X-Content-Type-Options

---

## 📊 Vulnerability Summary Table

| ID | Vulnerability | CVSS | Severity | CWE | Category |
|---|---|---|---|---|---|
| 1 | Weak Authentication | 9.8 | Critical | CWE-287 | Auth |
| 2 | Insecure Data Storage | 9.6 | Critical | CWE-200 | Storage |
| 3 | API Authentication Bypass | 9.7 | Critical | CWE-640 | API |
| 4 | SQL Injection | 9.9 | Critical | CWE-89 | Injection |
| 5 | Insecure API Communication | 9.4 | Critical | CWE-295 | API |
| 6 | Hardcoded API Keys | 9.2 | Critical | CWE-798 | Storage |
| 7 | Unencrypted Local Storage | 9.1 | Critical | CWE-256 | Storage |
| 8 | Broken Authorization | 8.9 | Critical | CWE-639 | Auth |
| 9 | Weak Cryptography | 8.2 | High | CWE-327 | Crypto |
| 10 | Missing Certificate Pinning | 7.8 | High | CWE-295 | API |
| 11 | Insecure WebView | 8.1 | High | CWE-79 | Injection |
| 12 | Intent-based Vulnerabilities | 7.5 | High | CWE-927 | Access |
| 13 | Sensitive Data in Logs | 7.2 | High | CWE-532 | Exposure |
| 14 | Insecure Deserialization | 8.0 | High | CWE-502 | Injection |
| 15 | File Permission Issues | 7.3 | High | CWE-276 | Storage |
| 16 | Insecure File Upload | 7.6 | High | CWE-434 | Injection |
| 17 | Missing Input Validation | 7.4 | High | CWE-20 | Injection |
| 18 | Debuggable Application | 6.8 | Medium | CWE-489 | Config |
| 19 | Hardcoded Configuration | 6.5 | Medium | CWE-798 | Config |
| 20 | Insecure HTTP Usage | 6.2 | Medium | CWE-295 | Communication |
| 21 | Missing Security Headers | 6.0 | Medium | CWE-693 | Headers |

---

## 📸 Evidence & Screenshots

This assessment includes **4 embedded screenshots** documenting:

1. **Screenshot 1:** Login bypass and authentication weakness demonstration
2. **Screenshot 2:** Plaintext data visible in application storage
3. **Screenshot 3:** Network traffic capture showing unencrypted API communication
4. **Screenshot 4:** Logcat output revealing sensitive information leakage

All screenshots are annotated and cross-referenced in the full assessment report.

---

## 🛠️ Tools & Methodology

### Tools Used

✅ Android ADB - Device control and data extraction
✅ JADX - Java decompilation and analysis
✅ Burp Suite Pro - Network traffic interception (HTTPS)
✅ MobSF - Automated security framework scanning
✅ Frida - Runtime instrumentation and API hooking
✅ SQLite Browser - Database analysis
✅ Android Studio - Logcat monitoring

### Comprehensive Methodology
- **OWASP Mobile Top 10** - Mobile application security assessment
- **OWASP API Top 10** - Backend API vulnerability testing
- **CVSS 3.1 Scoring** - Standardized severity assessment
- **CWE Mapping** - Common Weakness classification
- **Visual Evidence** - Screenshots and captured evidence
- **Professional Documentation** - Enterprise-grade reporting

---

## 📁 Repository Structure

InsecureShop-Security-Assessment/
├── README.md # This file
├── FULL_ASSESSMENT_REPORT.pdf # Complete report with screenshots
├── VULNERABILITY_CATALOG.md # Detailed documentation of all 21 findings
├── EVIDENCE/
│ ├── Screenshots/
│ │ ├── 01_Authentication_Bypass.png
│ │ ├── 02_Data_Storage_Exposure.png
│ │ ├── 03_Network_Traffic_Unencrypted.png
│ │ └── 04_Logcat_Sensitive_Data.png
│ ├── Network_Captures/
│ │ ├── API_Traffic_Analysis.pcap
│ │ └── MITM_Attack_Demonstration.md
│ └── Logcat_Dumps/
│ └── Sensitive_Data_Leakage.txt
├── PROOF_OF_CONCEPTS/
│ ├── 01_Authentication_Bypass.md
│ ├── 02_SQL_Injection.md
│ ├── 03_API_Key_Extraction.md
│ ├── 04_Authorization_Bypass.md
│ ├── 05_File_Upload_Exploitation.md
│ ├── 06_XSS_in_WebView.md
│ ├── 07_Insecure_Deserialization.md
│ ├── 08_Intent_Exploitation.md
│ ├── 09_Certificate_Pinning_Bypass.md
│ ├── 10_Cryptography_Breaking.md
│ ├── 11_Debugger_Attachment.md
│ ├── 12_Sensitive_Data_Recovery.md
│ ├── 13_MITM_Attack.md
│ ├── 14_Database_Manipulation.md
│ └── 15_Privilege_Escalation.md
├── REMEDIATION/
│ ├── Authentication_Secure.java
│ ├── DataStorage_Encrypted.java
│ ├── API_Security.java
│ ├── Database_Prepared.java
│ ├── Cryptography_Strong.java
│ ├── CertificatePinning.java
│ ├── InputValidation_Complete.java
│ ├── WebView_Secure.java
│ ├── FileUpload_Validation.java
│ ├── Manifest_Secure.xml
│ └── SecurityHeaders_API.md
├── METHODOLOGY/
│ ├── Testing_Checklist.md
│ ├── OWASP_Mobile_Top10_Mapping.md
│ ├── OWASP_API_Top10_Mapping.md
│ ├── CVSS_Scoring_Methodology.md
│ └── Assessment_Standards.md
├── IMPACT_ANALYSIS/
│ ├── Business_Impact.md
│ ├── Financial_Risk_Assessment.md
│ ├── Regulatory_Compliance.md
│ ├── Customer_Privacy_Impact.md
│ └── Incident_Response_Guide.md
└── REMEDIATION_ROADMAP/
├── Phase_1_Critical.md
├── Phase_2_High.md
└── Phase_3_Medium.md

---

## 🔍 OWASP Mapping

### OWASP Mobile Top 10 Mapping
| OWASP Mobile | Vulnerabilities |
|---|---|
| M1 - Improper Authentication | #1, #8 |
| M2 - Insecure Data Storage | #2, #6, #7, #13, #19 |
| M3 - Insecure API Communication | #5, #10 |
| M4 - Poor Code Quality | #14, #18 |
| M5 - Insufficient Cryptography | #9, #19 |
| M6 - Insecure Authorization | #3, #8, #12 |
| M7 - Reverse Engineering | #6, #9 |
| M8 - Extraneous Functionality | #18, #19 |
| M9 - Weak First-Factor Authentication | #1 |
| M10 - Extraneous Functionality | #21 |

---

## 🚀 Remediation Roadmap

### Phase 1: CRITICAL (Immediate - 2 weeks)
1. Implement proper API authentication (OAuth 2.0)
2. Encrypt all stored sensitive data (Android Keystore)
3. Remove hardcoded credentials and secrets
4. Implement SQL parameterized queries
5. Enforce HTTPS with certificate pinning

### Phase 2: HIGH (Urgent - 4 weeks)
6. Implement strong cryptography (AES-256, PBKDF2)
7. Add input validation and sanitization
8. Secure WebView configuration
9. Protect exported activities and intent filters
10. Remove sensitive data from logs

### Phase 3: MEDIUM (Important - 8 weeks)
11. Add security headers to API responses
12. Implement proper file permissions
13. Remove debugging capabilities
14. Update vulnerable dependencies
15. Security testing and validation

---

## 💼 Business Impact Assessment

### Financial Impact
- **Data Breach Cost:** Estimated $50K - $500K+ depending on data volume
- **Regulatory Fines:** GDPR violations up to €20M
- **Reputational Damage:** Loss of customer trust
- **Legal Liability:** Class action suit risk

### Compliance Impact
- 🔴 **GDPR Non-Compliance** - Insecure data handling
- 🔴 **PCI DSS Failure** - Unencrypted payment data
- 🔴 **CCPA Violations** - Inadequate data protection
- 🔴 **SOC 2 Audit Failure** - Security control gaps

---

## 📞 Contact & Support

**Tester:** Md. Jakir Hossain  
**Position:** Junior Penetration Tester at Byte Capsule IT  
**Email:** mjakirhoossain@gmail.com  
**LinkedIn:** [m-jakir-hossain](https://www.linkedin.com/in/m-jakir-hossain/)

For detailed discussions on findings, remediation strategy, or additional testing:
📧 Email: mjakirhoossain@gmail.com

---

## 🔒 Security Commitments

All findings and methodologies documented here represent professional security assessment standards. The vulnerabilities identified are specific to the InsecureShop application and should be remediated following the provided guidance.

---

## 📝 Disclaimer

This assessment was conducted on a deliberately vulnerable application (InsecureShop) for educational and research purposes. The findings and techniques documented here are for authorized security testing only. Unauthorized access to computer systems is illegal.

---

## 📌 References

### Standards & Frameworks
- [OWASP Mobile Security Testing Guide](https://owasp.org/www-project-mobile-security-testing-guide/)
- [OWASP API Security Testing Guide](https://owasp.org/www-project-api-security/)
- [Android Security & Privacy Guidance](https://developer.android.com/security)
- [CVSS v3.1 Calculator](https://www.first.org/cvss/calculator/3.1)
- [CWE Top 25](https://cwe.mitre.org/top25/)

### Tools Documentation
- [JADX GitHub](https://github.com/skylot/jadx)
- [Android ADB Documentation](https://developer.android.com/studio/command-line/adb)
- [Burp Suite Professional](https://portswigger.net/burp)
- [Frida Documentation](https://frida.re/)
- [MobSF Documentation](https://github.com/MobSF/Mobile-Security-Framework-MobSF)

---

<div align="center">

**Status:** ✅ Complete  
**Last Updated:** October 2026  
**Dark Mode Optimized:** Yes

---

© 2026 Md. Jakir Hossain | Byte Capsule IT

</div>
