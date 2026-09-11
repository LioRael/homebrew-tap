# Lenso Homebrew tap

Install the native Lenso Agent terminal UI, management CLI, and ACP entrypoint:

```sh
brew install LioRael/tap/lenso-agent
lenso-agent auth login
lenso-agent profiles install coding
lenso-agent --profile code
```

Supported: Apple silicon on macOS 15+, and x86-64 Linux with glibc 2.39+
(Ubuntu 24.04+). Release binaries require no Rust toolchain. Homebrew verifies
all three release archive checksums and installs ripgrep for coding workflows.

```sh
brew upgrade lenso-agent
brew uninstall lenso-agent
```

Uninstalling preserves your Agent Home (`~/.lenso/agent`). The browser interface
is available separately through `npx @lenso/agent web` with Node.js 22.12+.

## Update a release

After the Agent GitHub release is published, dispatch **Update Agent** with its
exact version. The workflow generates a branch and pull request and dispatches tests; review both
platform installation checks before merging. It needs only this repository's
GitHub token and does not modify upstream release assets or registry packages.

To prepare an update locally:

```sh
python3 scripts/update-agent.py 0.1.11
brew audit --strict LioRael/tap/lenso-agent
brew install LioRael/tap/lenso-agent
brew test LioRael/tap/lenso-agent
```

The updater reads the release's SHA256SUMS and requires every supported target
and component. Keep the generated Formula and updater in the same commit.
