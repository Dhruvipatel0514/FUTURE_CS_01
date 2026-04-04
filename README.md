\# Vulnerability Assessment — demo.testfire.net



\*\*Internship:\*\* Future Interns — Cyber Security Task 1 (2026)

\*\*Assessed by:\*\* Dhruvi Patel



\---



\## What I Did



I performed a passive vulnerability assessment on a demo banking website

to identify common security weaknesses. The goal was to think like a

security consultant — find the risks, understand the impact, and suggest

practical fixes.



No hacking. No exploitation. Read-only analysis only.



\---



\## Targets



| Tool | Website |

|------|---------|

| Nmap | scanme.nmap.org |

| OWASP ZAP | demo.testfire.net |

| Browser DevTools | demo.testfire.net |



\---



\## Tools I Used



\*\*Nmap\*\* — scanned for open ports and checked what services were running

and whether any version information was being exposed.



\*\*OWASP ZAP\*\* — ran a passive scan on the website to detect vulnerabilities

without sending any attacking requests.



\*\*Browser DevTools\*\* — manually checked HTTP response headers, cookie

settings, and the overall security status of the page.



\---



\## What I Found



| Severity | Finding |

|----------|---------|

| 🔴 Critical | Website running on HTTP — no HTTPS at all |

| 🔴 Critical | Session cookie has no Secure flag |

| 🟠 High | Content-Security-Policy header missing |

| 🟠 High | X-Frame-Options header missing |

| 🟠 High | X-Content-Type-Options header missing |

| 🟡 Medium | Server version visible in response headers |

| 🟡 Medium | Session cookie missing SameSite attribute |



\---



\## Quick Summary of Issues



\*\*No HTTPS\*\* is the biggest issue. The entire website runs on HTTP which

means any data sent — including passwords and session tokens — travels

in plain text. Anyone on the same network can read it.



\*\*Missing security headers\*\* means the browser has no instructions on

how to protect the user. No CSP means XSS is possible. No X-Frame-Options

means the site can be embedded in an iframe and used for clickjacking.



\*\*Insecure cookie\*\* — the session cookie JSESSIONID has no Secure flag,

so it can be transmitted over HTTP and stolen easily.



\*\*Server version exposed\*\* — the response header shows

`Apache-Coyote/1.1` which tells attackers exactly what software is

running and what known vulnerabilities to target.



\---



\## DevTools — Headers Found



| Header | Present? |

|--------|----------|

| Content-Security-Policy | ❌ |

| X-Frame-Options | ❌ |

| X-Content-Type-Options | ❌ |

| Strict-Transport-Security | ❌ |

| Referrer-Policy | ❌ |



\## DevTools — Cookie Flags



| Cookie | Secure | HttpOnly | SameSite |

|--------|--------|----------|----------|

| JSESSIONID | ❌ | ✅ | ❌ |



\---



\## How to Fix It



\*\*Immediately:\*\*

\- Move the site to HTTPS and redirect all HTTP traffic

\- Add the Secure flag to session cookies



\*\*Soon:\*\*

\- Add Content-Security-Policy, X-Frame-Options, and

&#x20; X-Content-Type-Options headers to the server config



\*\*Later:\*\*

\- Hide the server version from response headers

\- Add SameSite=Strict to all cookies



\---



\## Evidence



All screenshots are inside the `evidence/` folder.

