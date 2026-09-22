# HRConvert2: delete leaves the web-served copy

https://github.com/zelon88/HRConvert2/security/advisories/GHSA-cwc2-f9j8-x8m2

HRConvert2 is a self-hosted PHP file conversion and sharing server (zelon88/HRConvert2). I reviewed v3.5, commit `f27083b`. No authentication. I reported this on 2026-07-31. The vendor published the advisory on 2026-08-03.

There is no fixed version on the advisory, and no CVE.

`deleteFiles()` decides whether the web-served copy should be removed, then unlinks a different variable that has not been assigned yet. The copy under the web root stays. The application reports the delete as failed, so a user can see that the operation did not work. This is not a silent success with a leftover. The file remains downloadable until the normal sweep. On the build I tested, that sweep was about an hour.

Anyone who can use the site can hit this. There is no account system. The practical case is a file the user thinks they deleted, still fetchable by URL until the sweep.

I filed the same bug twice. The duplicate advisory was closed and was not published. GHSA-cwc2-f9j8-x8m2 is the one the vendor published. The closed duplicate is not a second issue.

| | |
|---|---|
| Affected | 3.5 and earlier |
| Fixed | Not stated on the advisory |
| Severity | Medium, 5.3 |
| Vector | CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N |
| CWE | CWE-459, CWE-200 |
| Privileges | None |
| CVE | Not assigned |

Confidentiality is Low rather than High because the window is the sweep interval, and the delete is visibly failed. I did not find a way to suppress that error.

No release after 3.5 is listed as the fix, and I have not retested one. I am not inferring a fix from the v3.6.6 hardening note.

CVE request went to the maintainer on 2026-08-07 with the other HRConvert2 advisories. Closed the same day. No CVE id as of 2026-09-22.

Local instance of v3.5 only.

L0stHeart
https://github.com/L0stHeart
