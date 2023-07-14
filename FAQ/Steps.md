# PROJECT ROBOT: 

## Here are the current steps I go through to prepare a GHSA SYNC PR:

SYNCIT.SH
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
 * Run "rake"/correct/repeat.

MANUAL
 * Review and correct (Assume part of post-processing).
     1. Check rubygems.org for "gem:" value
     2. Run "mkm" to append template to end of file.
     3. Add "framework: rails" for sub-rails gems.
     4. Google for "cve:" or "ghsa:" values for more info.
     5. Better "url:" choice. (pickurl cmd)
     6. Review "title:" value.
     7. Use "url:" date for "date:" value if missing.
     8. Line wrap "title:" and "description:" fields.
     9. Use "nvd" url for cvss values. 
        * Add "cvss_v2:" if missing.
     10. Review "unaffected_versions:" and "patched_versions"
         values against debug lines. 
     11. Reorder "related:/url:" lines.
     12. Check "related:/url:" for dead links (#674)
  
MANUAL
 * git add, git commit, git push
