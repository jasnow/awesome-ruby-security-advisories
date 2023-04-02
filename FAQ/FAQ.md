# FAQ - Frequently Asked Questions

 1. If you have a repo, including one associated with a "gem", and 
    there are not releases (GitHub "tags") after the one mentioned
    in the advisories then the "patched_versions:" field should
    be "> LAST-VERSION-RELEASED".

 2. If you have a repo, including one associated with a "gem", and 
    there are releases (GitHub "tags") after the one mentioned
    in the advisories but the vulnerability was not fixed, then
    the "patched_versions:" field should be "> LAST-VERSION-RELEASED".

 3. Here's how I prefer to fill out a RAD advisory (YAML) file:

    a. "gem:" (Required/String) Use the name of the affected 
       gem at https://rubygems.org/search?query=GEM"

    b. "library:" (Optional/String) Use the name of the 
       ruby library which the affected gem belongs to.

    c. "framework" (Optional/String) Use the name of the
       framework which the affected  gem belongs to.

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
       - Example: 2019-07-02

    k. "description:" - (Required/String) One or more paragraphs
       describing the vulnerability, usually from the CVE link
       and/or announcement.

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
        - ~> #.#.## (zero or more of these)
        - ">= #.#.#" (Last one needs to be ">=")

    o. "patched_versions" (Optional/Array of Strings): The version
       requirements for the patched versions of the Ruby library.
       Use the following format:
       - ~> #.#.## (zero or more of these)
       - ">= #.#.#" (Last one needs to be ">=")

    p. "related" (Optional/Hash Array String): Sometimes an advisory
       references many urls and other identifiers. Supported keys:
       "cve:", "ghsa:", "osvdb:", and "url:".
```
related:
  url:
  - https://github.com/brianmario/yajl-ruby/blob/7168bd79b888900aa94523301126f968a93eb3a6/ext/yajl/yajl_buf.c#L64
```
    q. "notes" (Optional/String): Internal notes regarding the
       vulnerability's inclusion in this database.
