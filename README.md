# HRConvert2 delete leaves the copy the web server is still serving

https://github.com/zelon88/HRConvert2/security/advisories/GHSA-cwc2-f9j8-x8m2

Severity: medium (CVSS 5.3, `CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N`). CWE-459, CWE-200. No CVE. The advisory names no fixed release.

HRConvert2 3.5 and earlier is affected. I reviewed 3.5, commit f27083b. There is no authentication, so anyone who can use the site can hit this.

`deleteFiles()` decides the web-served copy should be removed, then unlinks a different variable that has not been assigned yet. The copy under the web root stays. The application reports the delete as failed, so the user can see that it did not work. This is not a silent success with a leftover. The file stays downloadable until the normal sweep. On the build I tested, that sweep was about an hour. Confidentiality is low because the window is that interval and the failure is visible. I did not find a way to hide the error.

I filed the same bug twice. The duplicate was closed and was not published. This advisory is the one the vendor published. The closed one is not a second issue.

No release after 3.5 is listed as the fix, and I have not retested one. I am not reading a fix into the 3.6.6 hardening note.

The CVE request went to the maintainer on 7 August 2026 with the other HRConvert2 advisories. Closed the same day. No CVE id as of 22 September 2026.

Local instance of 3.5 only.

Reported privately on 31 July 2026. The vendor published the advisory on 3 August 2026.

L0stHeart
