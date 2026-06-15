
Finished: No
Source: PortSwigger
Status: Learning

#### SOP Same Origin Policy

A mechanism implemented in modern web browsers that stops Websites from reading or writing to each other except if they have identical:

1. Protocol
2. Host
3. Port

## XSS Overview

- Injecting or Having control over another website’s JavaScript that is viewed by another user. Consequently, they bypass the **Same-Origin Policy (SOP)**
- Client-Side vulnerability

#### Types

1. Reflected
2. Stored
3. Mutation - MXSS
4. Document Object Model - Dom-based XSS

#### Places

1. Input (uname, passwd)
2. Parameters
3. Comments
4. Images
5. Redirection
6. Support messages

#### Reasons

1. Lack of input validation and sanitization
2. Lack of output encoding: For the HTML part, it is critical to properly encode characters such as `<`, `>`, `"`, `'`, and `&` into their respective HTML encoding. For JavaScript, special attention should be given to escape `'`, `"`, and `\`. Failing to encode user-supplied data correctly is a leading cause of XSS vulnerabilities.
3. Improper use of security headers: For example, Content Security Policy (CSP) mitigates XSS risks by defining which sources are trusted for executable scripts. A misconfigured CSP, such as overly permissive policies or the improper use of `unsafe-inline` or `unsafe-eval` directives, can make it easier for the attacker to execute their XSS payloads.
4. Framework and language vulnerabilities
5. Third-party libraries

#### Implications

1. Session hijacking
2. Phishing and credential theft
3. Social engineering
4. Content manipulation and defacement
5. Data exfiltration
6. Malware installation

[https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html)