# Commit Changes with Quality Checks

全て日本語で生成すること
Create a commit using Conventional Commits format, with comprehensive quality validation. Use Japanese language for commit message.

## Commit Process for: $ARGUMENTS

Execute commits with proper quality gates and well-formed descriptions.

### 1. Validate Branch and Environment

- Check current branch: `git branch --show-current`
- **Fail if on main or develop branch** - commits should be on feature branches
- Ensure we're in a clean git state (no merge conflicts, etc.)

### 2. Determine Target Files

Based on the argument provided:

- **`current`**: Analyze files that were recently modified in the current LLM conversation context (files we've been working on)
- **`staged`**: Analyze currently staged changes (`git diff --cached --name-only`)
- **`custom`**: Ask user to specify which files to include, then stage them

### 3. Pre-Commit Quality Checks

Run all quality checks and report any failures:

```bash
# Type checking
pnpm typecheck

# Linting and formatting
pnpm check

# Test suite
pnpm test
```

**Stop process if any check fails** - display error details and ask user to fix before proceeding.

### 4. Analyze Changes for Commit Message

- Review file changes and git diff output
- Identify the type of changes (new features, bug fixes, refactoring, etc.)
- Determine appropriate conventional commit type:
  - `feat:` - new feature
  - `fix:` - bug fix
  - `chore:` - configuration changes or maintenance
  - `refactor:` - refactoring
  - `docs:` - documentation update
  - `test:` - add or update tests
  - `style:` - code style change

### 5. Generate Commit Message

Create commit message following this format:

```
<type>: <description>

<Optional longer description if needed>
```

Examples:

- `feat: add user authentication feature`
- `fix: correct validation error in date input field`
- `refactor: improve database query performance`

Keep the description:

- **Simple and clear** - explain what was changed
- **User-focused** - describe the impact, not technical details
- **Concise** - typically one line, use body only if necessary

### 6. Execute Commit

- Stage files if needed (for `current` or `custom` mode)
- Create commit with generated message
- Display commit hash and summary
- Confirm commit was successful

### 7. Post-Commit Summary

- Show commit details: `git log -1 --oneline`
- Indicate next steps (push to remote, create PR, etc.)
- Remind about running `/project:create-pr` when ready

### Error Handling

- **Quality check failures**: Display specific errors and stop process
- **No changes detected**: Inform user and exit gracefully
- **Git errors**: Show git error messages and suggest solutions

### Quality Checklist

- [ ] Not committing to main branch
- [ ] All quality checks pass (compile, lint, test)
- [ ] Appropriate conventional commit type selected
- [ ] Description is clear and concise
- [ ] Files properly staged and committed
- [ ] Commit hash returned successfully

This ensures every commit meets project quality standards while maintaining clear communication.
