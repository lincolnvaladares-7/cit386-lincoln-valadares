# CIT 386 — Module 4 — Assignment 4.2
## Shared Access Signature: Permissions, Denial, and Expiration

**Student:** Lincoln Guimaraes Valadares  
**Repository path:** `module04/access-token.md`  
**Status:** Documentation prepared; live Azure tests and evidence pending.

> **Credential safety:** Never commit a real SAS `sig` value, a storage account key, or an unredacted SAS URL. Replace the value with `[REDACTED]` in text and screenshots. Do not expose another student's directory.

## 1. Token configuration — record before generation

| Parameter | First token (read-only) | Second token (short expiry) |
|---|---|---|
| Storage account | [ENTER OWN ACCOUNT] | [ENTER OWN ACCOUNT] |
| Container | [ENTER OWN CONTAINER] | [ENTER OWN CONTAINER] |
| Resource/scope | [ENTER OWN BLOB OR DIRECTORY] | [ENTER OWN BLOB OR DIRECTORY] |
| SAS type | [ENTER ACTUAL TYPE] | [ENTER ACTUAL TYPE] |
| Allowed permissions (`sp`) | Read (`r`) only | Read (`r`) only |
| Start time (`st`, UTC) | [ENTER ACTUAL] | [ENTER ACTUAL] |
| Expiry (`se`, UTC) | [ENTER ACTUAL DATE WITHIN TERM] | [ENTER ACTUAL, A FEW MINUTES LATER] |
| Allowed protocol (`spr`) | HTTPS only (`https`) | HTTPS only (`https`) |
| Signed resource (`sr`) | [ENTER ACTUAL] | [ENTER ACTUAL] |
| IP restriction (`sip`) | [ENTER ACTUAL OR NONE] | [ENTER ACTUAL OR NONE] |
| Other parameters | [ENTER ACTUAL] | [ENTER ACTUAL] |

**Important scope note:** A blob-level SAS can restrict access to one blob. A directory-scoped SAS requires an Azure Data Lake Storage Gen2 hierarchical namespace and the appropriate directory-scoped SAS support. Do not claim that a container SAS restricts access to one folder merely because the URL contains a folder name.

**Example of a redacted URL (not a working credential):**  
`https://[account].blob.core.windows.net/[container]/[own-path]/[file]?sp=r&st=[UTC]&se=[UTC]&spr=https&sr=b&sig=[REDACTED]`

## 2. Evidence: permitted read in an unsigned-in browser

**Test:** Open the SAS URL for my own file in a private/incognito window without signing in to Azure.  
**Test date/time (UTC):** [ENTER]  
**HTTP status and visible result:** [ENTER ACTUAL RESULT]  
**Evidence:** [INSERT SCREENSHOT OR SCREENSHOT PATH, SIGNATURE REDACTED]

## 3. Evidence: refused operation

**Test:** Attempt to list the container using only the read-only token (without list permission).  
**Request tested:** [ENTER EXACT OPERATION/REDACTED URL]  
**Test date/time (UTC):** [ENTER]  
**HTTP status:** [ENTER ACTUAL]  
**Exact Azure error code returned:** [COPY EXACT CODE FROM RESPONSE]  
**Evidence:** [INSERT SCREENSHOT OR SCREENSHOT PATH, SIGNATURE REDACTED]

Do not guess the error code. A container-list test may fail for different reasons depending on SAS scope and request construction; record the response exactly.

## 4. Evidence: short-lived token before and after expiration

**Second token start (UTC):** [ENTER]  
**Second token expiry (UTC):** [ENTER]  
**Before expiry — test time, HTTP status, result:** [ENTER ACTUAL]  
**After expiry — test time, HTTP status, result:** [ENTER ACTUAL]  
**Exact Azure error code after expiry:** [COPY EXACT CODE FROM RESPONSE]  
**Evidence before expiry:** [SCREENSHOT PATH, SIGNATURE REDACTED]  
**Evidence after expiry:** [SCREENSHOT PATH, SIGNATURE REDACTED]

## 5. What the token permits

The intended permission is to read the designated content using a valid HTTPS SAS URL during its signed validity period. Whether this worked is recorded in Section 2.

## 6. What the token forbids

The intended token does not grant list, write, delete, or other permissions beyond read. Section 3 must show an actual denied request and the exact returned error code. Its effective resource scope depends on the SAS type and signed resource.

## 7. From where the token can be used

The token requires HTTPS. If no signed IP restriction was configured, the SAS itself does not restrict access to a particular client IP address. Anyone who possesses the complete token may attempt to use it, subject to its permissions, scope, and validity period.

## 8. Between which two moments it works

**First token:** [START UTC] to [EXPIRY UTC].  
**Second token:** [START UTC] to [EXPIRY UTC].  
The second token must be tested both before and after expiry, with actual results in Section 4.

## 9. What would change for a recruiter needing six months?

I would first confirm that a six-month SAS is permitted by the account's security policies and whether a shorter-lived, renewable access method would be safer. If permitted, I would extend the expiry date while keeping HTTPS-only and the narrowest read-only scope, ideally limiting access to the resume file. A longer-lived SAS increases the time during which a leaked URL could be reused without additional authentication, so it increases exposure and makes revocation planning more important.

## 10. Why not share the storage account key?

Giving a recruiter the storage account key could provide much broader control over the account than is necessary to read one resume, including access to other stored content depending on configuration. A narrowly scoped, time-limited SAS is better even for a trusted recipient because it limits what the credential can do and how long it can be used.

## Completion checklist

- [ ] Both real SAS tokens issued against my own content
- [ ] Parameters above replaced with actual values (without signatures)
- [ ] Successful unauthenticated read captured
- [ ] Refused operation captured with exact error code
- [ ] Short-lived token tested before and after expiry with exact error code
- [ ] Every screenshot and URL has the `sig` value redacted
- [ ] File committed at `module04/access-token.md`
