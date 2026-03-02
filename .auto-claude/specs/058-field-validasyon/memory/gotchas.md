# Gotchas & Pitfalls

Things to watch out for in this codebase.

## [2026-03-02 11:15]
This spec (058) is PLANNING ONLY — output is exclusively .md files. No code (.py, .js, .json) may be created or modified. No bench/git/pip/npm commands. All 'implement' and 'create' instructions in the task descriptions are planning context only to be documented in markdown.

_Context: 058-field-validasyon spec constraints_

## [2026-03-02 11:58]
set_only_once:1 is NOT USED in any TradeHub app, despite being critical for fields like order.buyer, quotation.seller, listing.seller, buyer_profile.user. This is a security gap where linking fields can be changed after creation.

_Context: subtask-2-1 field authorization scan — discovered missing set_only_once pattern_

## [2026-03-02 11:58]
When writing files in a git worktree session, always use the worktree-relative path, not the main repo absolute path. The working directory is /home/ali/Masaüstü/istoc/Tradehub_V1/.auto-claude/worktrees/tasks/058-field-validasyon, so all .auto-claude/specs/... paths must be relative to this worktree root. Files written to the main repo path (/home/ali/Masaüstü/istoc/Tradehub_V1/.auto-claude/specs/...) will NOT appear in the worktree's git status and must be copied to the worktree path before committing.

_Context: Writing 112.md and subtask-2-1 scan results -- both were initially written to main repo path instead of worktree path, requiring manual copy_
