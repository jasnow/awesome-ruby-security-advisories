# PROJECT ROBOT: 

## Here are the current steps I go through to prepare a GHSA SYNC PR:

MANUAL
 * On GitHub, click on "Sync fork" to get upstream's commits.

## In the ruby-advisory top directory:

MANUAL
 * Create git branch.

GHIT.SH -- #637/RM-DEBUG-LINES/rejected
 * Run "bundle update" to get latest gems.
 * Run sync script (lib/github_advisory_sync.rb) with GitHub API Token mentioned above.

RMBOTH.SH - (#647+#655 moves step 4 into step 3)
 * Remove known duplicate advisories.

RUNALLPP.SH + emacs/manual (does step 5) - #674/relate/url's,#650/style
 * Do post-processing on all modified and brand new advisories so
   they are formatted per ruby-advisory-db style rules and extra
   debugging lines added by sync script are removed.

MANUAL
 * Review and correct (Assume part of post-processing).
   * Run "mkm" to append template to end of file.
   * Check rubygems.org for "gem:" value
   * Add "framework: rails" for sub-railis gems.
   * Google for "cve:" or "ghsa:" values for more info.
   * Better "url:" choice. (pickurl cmd)
   * Review "title:" value.
   * Use "url:" date for "date:" value if missing.
   * Line wrap "title:" and "description:" fields.
   * Use "nvd" url for cvss values. 
   * Add "cvss_v2:" if missing.
   * Review "unaffected_versions:" and "patched_versions"
     values against debug lines. 
   * Reorder "related:/url:" lines.
   * Check "related:/url:" for dead links (#674)
  
MANUAL
 * Run "rake"/correct/repeat.

MANUAL
 * git add, git commit, git push
