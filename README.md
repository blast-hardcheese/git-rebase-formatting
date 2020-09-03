git rebase-formatting
===

A small script to make it easier to reflow the formatting of an entire PR.

Usage:

```bash
user$ git rebase-formatting -c 'sbt-client scalafmt' upstream/master mybranch -- src/
```

This will:
- rebase between the two specified commits
- run `sbt-client scalafmt` on every commit
  - commit the output of scalafmt
  - _revert_ that formatting change, to avoid merge conflicts
- then, once complete, rebase again to:
  - squash each revert commit into the subsequent commit
  - squash each formatting commit into the previous commit

At the end of this process, you'll end up with either the same number of
commits as before, but with each one formatted, or fewer commits than you
started with because the formatting-only changes will have dropped out.
