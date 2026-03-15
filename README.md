# glinet-reddit-automod-rules

AutoModerator rules and validation tooling for r/glinet.

## Repository layout

- `automod_scripts/automod-main-rule.yaml`: Primary AutoModerator rule file.
- `automod_scripts/reddit_automod_rules.md`: Local Reddit AutoModerator spec reference.
- `scripts/validate_automod.py`: Validator used locally and in CI.
- `.github/workflows/automod-status-check.yml`: GitHub Actions validation workflow.

## Local validation

Run from repo root:

```bash
python3 scripts/validate_automod.py
```

Explicit file paths:

```bash
python3 scripts/validate_automod.py automod_scripts/automod-main-rule.yaml --spec automod_scripts/reddit_automod_rules.md
```

The validator checks YAML parsing, duplicate keys, rule/action/type constraints, value types, separator usage, and invalid decorative hash separators.

## Rule formatting requirements

- Use one title comment line per rule, for example: `# RULE 1: ...`
- Separate rules with lines containing exactly `---`
- Do not use decorative hash separator lines like `##########` above or below rule titles

## Current rules

- Remove comments from accounts younger than 5 days or with combined karma under 20
- Remind `questions/support` submissions to mark posts as solved
- Remind `news`, `questions/support`, `discussion`, and `question/support- Solved` posts to search first
- Restrict `GL.iNet Announcements` flair to approved accounts
- Leave `GL.iNet Announcements` posts open for normal discussion
- Auto-approve trusted link submissions from `admon.in.ua`, `github.com`, `gl-inet.com`, `gl-inet.net`, `goodcloud.xyz`, `remotetohome.io`, `thewirednomad.com`, `traveryates.com`, `twy4.us`, and `wickedyoda.com` and their subdomains
- Filter non-trusted link submissions to mod queue, notify the author, and send modmail for manual review

## GitHub Actions validation

The `AutoMod Status Check` workflow runs:

- On every pull request update (`opened`, `synchronize`, `reopened`, `ready_for_review`)
- On every push to `main` (including merge commits)
