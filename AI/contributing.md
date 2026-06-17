# Contributing to wolfssh

## Contributor Agreement

External contributors must sign a contributor agreement before pull requests can be merged. When you open your first PR, a wolfSSL team member will ask you to email support@wolfssl.com referencing the PR. The agreement is tracked via wolfSSL's Zendesk ticketing system. Once signed, your PR will be approved for CI testing.

## Fork Workflow

Do not push branches to this repository. Fork to your personal GitHub account and open pull requests from your fork.

## Source Code Rules

CI enforces all of these on every PR. Violations block merge.

### Formatting

- **No trailing whitespace.** Files must end with a newline.
- **No hard tabs** in C, header, or YAML files. Makefiles are exempt.
- **ASCII only.** No non-ASCII bytes in source files. All code, comments, and string literals must be pure ASCII.
- **No CR characters** (`\r`). Use Unix line endings.

### C Style

- **C comments only.** Use `/* */`, not `//`, in all `.c` and `.h` files.
- **No flush-left function calls** (a sign of debug residue).

### Spelling and Linting

- **codespell** runs on all files in the repository (not just changed files). Fix any flagged typos before submitting. The workflow is at `.github/workflows/codespell.yml`.
- **cppcheck** runs static analysis. See `.github/workflows/cppcheck.yml` for the exact invocation.
- **shellcheck** runs on all shell scripts. Fix warnings before submitting.

### AI Attribution

- **No AI attribution in commits.** CI rejects commits containing `Co-authored-by:` or `Signed-off-by:` trailers that reference:
  - `noreply@anthropic.com`
  - `noreply@openai.com`
  - `+Copilot@users.noreply.github.com`
  - Any `[bot]@users.noreply.github.com` address
- Commits authored by bot email addresses are also rejected.
- **Do not add these trailers.** Your PR will fail CI if they are present.

## PR Requirements

Every PR must include:

- **Description** of the scope of the fix or feature
- **Tracking reference** — `Fixes zd#NNNN` for Zendesk tickets (wolfSSL uses Zendesk, not GitHub Issues, for bug tracking)
- **Test description** — how the change was tested

All CI checks must pass before merge.

## Testing Before Submitting

At minimum, run:

```bash
./configure && make check
```

For broader coverage, test with additional feature flags:

```bash
# All features
./configure --enable-all && make check

# SFTP only
./configure --enable-sftp && make check

# SCP only
./configure --enable-scp && make check

# With keyboard-interactive auth
./configure --enable-keyboard-interactive && make check
```

wolfssh must be tested against a wolfSSL build that includes `--enable-ssh`. Ensure wolfSSL is installed before running these commands.

## Security Reports

Do not open GitHub issues for security vulnerabilities. Report them to support@wolfssl.com.
