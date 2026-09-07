# Phishing & Email Analysis — Background Overview

> Decided to start documenting my journey and showcasing what I am doing. I will be documenting everything going forward from **September 7, 2026**, but the following is a brief overview of what I had already covered before I started keeping detailed records.

## Summary

Before starting formal documentation, I worked through the fundamentals of phishing and email-based threat analysis. This included studying real-world case studies, learning how to authenticate and investigate email headers, analyzing email content and attachments for malicious indicators, and examining URLs for common obfuscation and spoofing techniques. Below is a brief breakdown of the areas covered.

### Phishing Case Studies

Reviewed several well-known real-world phishing and business email compromise (BEC) incidents to understand impact and attack vectors, including the Colonial Pipeline attack, a hedge fund closure caused by a BEC attack, the Ubiquiti cyberheist, and the 2015 Ukraine power grid hack.

### Email Header & Sender Analysis

- Learned how to view an email's raw source and how to preserve original headers by forwarding emails as `.eml` attachments (a normal forward strips key routing headers).
- Practiced inspecting `.eml` files directly via the command line (`cat`, `grep`) as well as through text editors with header-highlighting plugins.
- Studied how to interpret key headers for signs of spoofing or manipulation, including `From`, `Reply-To`, `Return-Path`, `Message-ID`, `To`/`BCC`, and `Received` headers (and how their reverse-chronological order maps the email's routing path).
- Covered non-standard `X-` headers (e.g. `X-Sender-IP`/`X-Originating-IP`) and how they can support IP geolocation, ASN lookups, and reverse DNS.
- Explored GUI-based header analysis tools (Microsoft's MHA / mha.azurewebsites.net, MxToolbox) as faster alternatives to manual parsing.

### Email Authentication (SPF, DKIM, DMARC)

Studied the three core email authentication mechanisms and how they work together:
- **SPF** — validates which mail servers are authorized to send on behalf of a domain, and how policy strength (`-all`, `~all`) affects handling of unauthorized senders.
- **DKIM** — verifies message origin and integrity via cryptographic signing, without judging the domain's or sender's intent.
- **DMARC** — builds on SPF/DKIM with reporting and enforcement policies (`none`, `quarantine`, `reject`) that domain owners can set for messages that fail authentication.

### Email Content Analysis

- Studied MIME structure and how emails combine multiple content types across boundary-separated sections.
- Learned to recognize and decode Base64 and URL-encoded content used to obfuscate malicious payloads or bypass weak filters, using tools such as CyberChef, Burp Suite, or the command line.

### Attachment Analysis

- Learned safe extraction methods for suspicious attachments, ranging from manual "Save As" (higher risk of accidental execution) to tool-based extraction with `emldump.py`, up to the safest method — pointing analysis tools directly at the `.eml` file without extracting the payload at all (e.g. Email-IOC-Extractor).
- Practiced generating and documenting file hashes (MD5, SHA1, SHA256) on both Linux and Windows (PowerShell `Get-FileHash`).
- Learned to use file reputation services (VirusTotal, Cisco Talos Intelligence) to check attachments — prioritizing hash-based lookups over direct uploads to avoid exposing sensitive files.
- Practiced documenting findings and screenshotting each step to build a defensible, repeatable verdict trail.

### URL Structure & Phishing Techniques

- Studied URL anatomy, focusing on the fact that only the second-level domain plus TLD combination is unique and cannot be duplicated — and the importance of verifying that all parts of a domain genuinely belong together (e.g. a convincing subdomain doesn't guarantee a legitimate parent domain).
- Covered common URL-based phishing techniques: link shortening, subdomain spoofing, homograph/homoglyph attacks (visually identical characters from different character sets), and typosquatting.
- Learned to use tools such as dnstwist, unshorten.it, and search-engine autocorrect as quick ways to catch spoofed or misspelled domains.
- Reviewed social engineering red flags commonly found in phishing content (urgency, false authority, scarcity, requests for sensitive information).

### URL & Domain Investigation Tools

Gained familiarity with a range of tools for validating and safely inspecting suspicious URLs and domains without direct exposure, including MxToolbox, DNSChecker, urlscan.io, VirusTotal, URLVoid, url2png, WannaBrowser, PhishTank, URLhaus, Google Safe Browsing Transparency Report, and Joe Sandbox — along with the practice of "defanging" URLs to make them safe to document and share.

## Note

This overview intentionally summarizes rather than fully reconstructs each individual session, since redoing the full detailed write-ups for prior work isn't a practical use of time. Documentation from September 7, 2026 onward will follow the fuller, step-by-step format used going forward.
