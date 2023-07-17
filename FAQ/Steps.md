# PROJECT SYNCBOT

## As of July 17, 2023, here is the new "fully" automated way to prepare a GHSA SYNC PR:

 * runsyncbot (which calls syncbot.sh and save stdout/stderr is $HOME/o_s)
 * chksyncbotout (to check $HOME/o_s)

## Here are the current semi-automated steps I go through to prepare a GHSA SYNC PR:

### In the ruby-advisory top directory:

SYNCIT.SH
 * Sync GitHub (upstream) and local forks' commits.

AUTOGITB
 * Create git branch.

GHIT.SH -- #637/RM-DEBUG-LINES/rejected
 * Run "bundle update" to get latest gems.
 * Run sync script (lib/github_advisory_sync.rb) with GitHub API Token mentioned above.
   * On July 14, 2023, ghit.sh created 17 files.
     * On July 14, 2023, if you run "rake" at this point, you get 43 failures.

RMBOTH.SH - (#647+#655 moves step 4 into step 3)
 * Remove known duplicate advisories.
   * On July 14, 2023, rmboth.sh removed 11 files, leaving 6 files.

RUNALLPP.SH + emacs/manual (does step 5) - #674/relate/url's,#650/style
 * Do post-processing on all modified and brand new advisories so
   they are formatted per ruby-advisory-db style rules and extra
   debugging lines added by sync script are removed.
   * On July 14, 2023, if you run "rake" at this point, you get 1 failures.
     * Then if you run "rm2.sh" and then "rake", you get 0 failures.

MANUAL/LINT+REPAIR
 * Run "rake"/correct/repeat.

MANUAL/ASSUME ALL OPTIONAL.
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
  
MANUAL + "git add" + "git commit" + GPSO
 * git add, git commit, git push
