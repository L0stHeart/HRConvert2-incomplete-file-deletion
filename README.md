# HRConvert2: delete leaves the web-served copy

https://github.com/zelon88/HRConvert2/security/advisories/GHSA-cwc2-f9j8-x8m2

Affects HRConvert2 3.5 and earlier. The advisory names no fixed release. No CVE assigned.

Medium. CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N (5.3).
CWE-459, CWE-200.

File deletion unlinks a path that has not been assigned yet, and the copy under the web root stays. The application reports the delete as failed, so this is a delete that does not complete, not a success that hides a leftover. The copy remains downloadable until the normal sweep. In the build I tested, that sweep was about an hour.

I filed this twice by mistake. The duplicate was closed and was not published. This advisory is the one the vendor published.

Reported 2026-07-31 through GitHub private vulnerability reporting. The vendor published the advisory on 2026-08-03.

L0stHeart
