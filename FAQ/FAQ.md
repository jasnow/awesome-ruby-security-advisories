# FAQ - Frequently Asked Questions

 0. PR Confidence metric:
    * MUST HAVE commit URL (+3) OR PR URL (+2) OR
      Announcement URL with patches (+2) for main "url:" field,
    * AND nvd or equivalent URL (+1)
    * AND CHECK for rubygems.org URL for "gems" files (+1).

 1. If you have a repo, including one associated with a "gem", and 
    there are not releases (GitHub "tags") after the one mentioned
    in the advisories then the "patched_versions:" field should
    be "> LAST-VERSION-RELEASED".

    * 5/7/2023: Update by Postmodern: "If there is truly no patch
      versions, then we should omit "patched_versions" field."

 2. If you have a repo, including one associated with a "gem", and 
    there are releases (GitHub "tags") after the one mentioned
    in the advisories but the vulnerability was not fixed, then
    the "patched_versions:" field should be "> LAST-VERSION-RELEASED".

 3. Advisory PreReqs

    a. CVE Link, such as cve.org, or cve.mitre.org, or 
       - Example: https://nvd.nist.gov/vuln/detail/CVE-2013-7086

    b. Announcement Link with source code changed and release version
       - Example: https://www.ruby-lang.org/en/news/2023/03/30/redos-in-time-cve-2023-28756

 4. Here's how I prefer to fill out a GHSA advisory (YAML) file.

    1. Go to https://github.com/advisories and enter [advisory ID] into search box.

       - More info at: https://docs.github.com/en/code-security/security-advisories/global-security-advisories/browsing-security-advisories-in-the-github-advisory-database

    2. Review advisory and see if you can improve it by changing or adding information.
       You will see the current data for the advisory along with
       - GHSA ID
       - CVE ID
       - NVD Publish Date
       - GHSA Publish Date
       - GHSA Review Date

       - Very good resource is: https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing/best-practices-for-writing-repository-security-advisories

    3. If you see anything in step 2 to improve, go to  the bottom right
       corner of the advisory and click on the **See something to
       contribute? Suggest improvements for this vulnerability.** link.
       - Title              - 1-line summary
       - Description        - 1 or more Paragraphs of text
       - References         - List of URLs
       - Source Code        - Single URL
       - (1 or more times)
         - Ecosystem          - Menu, pick "RubyGems"
         - Package            - Gem name, such as "bundler"
         - Affected versions  - such as "< 1.2.3"
         - Patched versions   - such as "1.2.3"
       - Severity           - (calculate, such as "Critical 9.8")
         - Also dropdown    - Choices: [Low, Moderate, High, Critical, Use CVSS]
         - Vector string    - CVSS Vector (you can cut/paste from other data source)
       - Common weakness enumerator (CWE) - a number associated awith the CWE
       - Reason for change  - I usually use "Did more reseach. Connect the dots."

    - You also have "Documentation", "Contribution Guidelines",
      "About GitHub Advisory Database", and "Give feedback" on right side.

      - GHSA's "Affected products" is defined by [ecosystem, package name, 
        affected/patched versions, and vulnerable functions for the 
        security vulnerability that the security advisory describes].

 5. Here's how I prefer to fill out a ruby-advisory-db advisory (YAML) file:

    a. "gem:" (Required/String) Use the name of the affected 
       gem at https://rubygems.org/search?query=GEM"

    b. "library:" (Optional/String) Use the name of the 
       ruby library which the affected gem belongs to.

    c. "framework" (Optional/String) Use the name of the
       framework which the affected  gem belongs to.
       - So far, only use case seen if to set this to "rails" for rails gemset.

    d. "platform" (Optional/String) If this vulnerability is platform-
       specific, name of platform this vulnerability affects (e.g. jruby).

    e. "cve:" (Optional/String) Use the CVE (Common Vulnerabilities
       and Exposures ID name from [CVE](https://cve.mitre.org).
       - Format: "YYYY-#######" ("#" is usually 4 or more digits)
       - Example: 2014-4996

    f. "osvdb:" (Optional/Integer) Use the name of the
       OSVDB (Open Sourced Vulnerability Database) Id.
       - More Info at: [OSVDB](https://en.wikipedia.org/wiki/Open_Source_Vulnerability_Database)
       - Format: ###### ("#" is usually 5 or 6 digits)
       - Example: 108728
 
    g. "ghsa" (Optional/String) Use the name of the
       GHSA (GitHub Security Advisory ID which can be found at
       [GHSA](https://help.github.com/en/articles/about-maintainer-security-advisories).
       - Example: 67j6-xv27-w6ww

    h. "url:" - (Required/String) Use the URL to the full advisory at
       - Example: https://nvd.nist.gov/vuln/detail/CVE-2013-7086

    i. "title:" - (Required/String) Use a one-line summary of the
       advisory or individual vulnerability probably from offical sources.

    j. "date:" - (Required; YYYY/MM/DD) Use the public announcement/
       disclosure date of the advisory. Try to use the announcement
       URL since CVE may be blank when announced.
       Fallback is the "nvd_published_at" date at NVD "url:".
       - Example: 2019-07-02

    k. "description:" - (Required/String) One or more paragraphs
       describing the vulnerability, usually from the CVE link
       and/or announcement.
       - GHSA say: "type a description of the security vulnerability
         including its impact, any patches or workarounds available,
         and any references"

    l. "cvss_v2:" - (Optional/Float) Use the CVVS(V2) score for 
       the vulnerability - Format: ##.#
       - More Info at: [CVSSv2](https://www.first.org/cvss/v2/guide)
       - Example: 5.0

    m. "cvss_v3:" - (Optional/Float) Use the CVVS(V3) score for
       the vulnerability - Format: ##.#
       - More Info at: [CVSSv3](https://www.first.org/cvss/user-guide)
       - Example: 7.5

    n. "unaffected_versions" (Optional/Array of Strings): The version
       requirements for unaffected versions of the Ruby library.
       Use the following format:
```
       - ~> #.#.## (zero or more of these)
       - ">= #.#.#" (Last one needs to be ">=")
```
    o. "patched_versions" (Optional/Array of Strings): The version
       requirements for the patched versions of the Ruby library.
       Use the following format:
```
       - ~> #.#.## (zero or more of these)
       - ">= #.#.#" (Last one needs to be ">=")
```
    r. "notes" (Optional/String): Internal notes regarding the
       vulnerability's inclusion in this database.

    q. "related" (Optional/Hash Array String): Sometimes an advisory
       references many urls and other identifiers. Supported keys:
       "cve:", "ghsa:", "osvdb:", and "url:".
```
related:
  url:
  - https://github.com/brianmario/yajl-ruby/blob/7168bd79b888900aa94523301126f968a93eb3a6/ext/yajl/yajl_buf.c#L64
```

Sample Template:
```
---
gem: xor engine:
library:
framework:
platform:
cve:
osvdb:
ghsa:
url:
title:
date:
description: |
  TBD

  GHSA's SOURCE CODE LOCATION:
  GHSA's ECOSYSTEM:
  GHSA's PACKAGE NAME:
  GHSA's CWE: (more info at: https://cwe.mitre.org/index.html)
  GHSA's CWE SEVERITY:
cvss_v2:
cvss_v3:
unaffected_versions:
 - 'TBD'
patched_versions:
 - 'TBD'
related:
 cve:
  - TBD
 url:
  - TBD
# Comments start with "#" followed by space.
```

 6. GSD#185: 
    - The pull down for reference type lists the various types e.g. 
      WEB, REPORT, FIX, etc. it would be nice to have tooltips popup
      what each one means. The text from 
      https://ossf.github.io/osv-schema/#references-field would be great:
    - The known reference type values are:
      - ADV#: ADVISORY: A published security advisory for the vulnerability.
      - ARTICLE: An article or blog post describing the vulnerability.
      - ANNOUNCEMENTREPORT: A report, typically on a bug or issue
        tracker, of the vulnerability.
      - COMMIT: FIX: A source code browser link to the fix (e.g., a GitHub 
        commit) Note that the fix type is meant for viewing by people
        using web browsers. Programs interested in analyzing the exact
        commit range would do better to use the GIT-typed affected[].ranges
        entries (described above).
      - SOURCE LOCATION/PACKAGE: A home web page for the package.
      - EVIDENCE: A demonstration of the validity of a vulnerability
        claim, e.g. app.any.run replaying the exploitation of the vulnerability.
      - WEB: A web page of some unspecified kind.
    - From: https://github.com/cloudsecurityalliance/gsd-tools/issues/185