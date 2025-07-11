# Create Pull Request Workflow

全て日本語で生成すること
Create a pull request with a descriptive title and detailed description following team conventions. Use Japanese language for title and description.

## Pull Request Creation Process

### 1. Analyze Current Changes

- Get current branch: `git branch --show-current`
- Analyze changes against main:
  - `git log --oneline main..HEAD`
  - `git diff main..HEAD --stat`
  - `git diff main..HEAD --name-only`

### 2. Create Title

- Summarize changes in a concise title
- Focus on the essence of what was accomplished
- Keep it descriptive but brief for team readability

### 3. Generate Detailed Description

Follow this structure:

```markdown
## Overview
[Brief overview of what was changed and why]
[Add `fixes #<ISSUE_NUMBER>` or `refs #<ISSUE_NUMBER>` depending on completion status]

## Key Changes
### [Category 1]
- [Specific change 1]
- [Specific change 2]

### [Category 2]
- [Specific change 3]

## Impact
- [Components or files affected]

## Verification
- [Items to check]
```

### 4. Create PR Using Temporary File Approach

**Important**: Use proper file-based approach to avoid command issues:

1. Create temporary file `/tmp/pr_description.md` with the formatted description
2. Push branch: `git push -u origin HEAD`
3. Create PR: `gh pr create --title "<Title>" --body-file /tmp/pr_description.md`
4. Clean up: `rm /tmp/pr_description.md`

### Best Practices

- **Use temporary files** for multi-line content
- **Avoid `\n` in shell commands** - they become literal strings
- **Use `--body-file`** instead of inline body text
- **Clean up temporary files** after use

### Error Recovery

If PR description shows literal `\n`:

```bash
gh pr edit <PR_NUMBER> --body-file /tmp/corrected_description.md
```

### Quality Checklist

- [ ] Title summarizes changes clearly
- [ ] Description follows template structure
- [ ] Issue references included (fixes/refs #number)
- [ ] Impact areas documented
- [ ] Verification steps listed
- [ ] Temporary files cleaned up

Return the PR URL when complete for user reference.
