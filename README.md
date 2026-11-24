# Backup testing

Use this repository to test backing up Git history and restoring it into a separate checkout.

## Run a backup and restore test

Run these commands from a local checkout. Choose fresh paths for the bundle and the restored checkout.

```sh
git status --short
git bundle create ../backup-testing.bundle --all
git bundle verify ../backup-testing.bundle
git clone -b main ../backup-testing.bundle ../backup-testing-restored
git rev-parse main
git -C ../backup-testing-restored rev-parse HEAD
```

The last two commands should print the same commit ID. The bundle contains Git history reachable from local refs. Commit any files you want included before creating the bundle.

## Check restored file contents

The [sample file](fixtures/sample.txt) contains synthetic data and uses LF line endings on all platforms. Check its SHA-256 hash from the restored checkout.

On PowerShell, run `Get-FileHash fixtures/sample.txt -Algorithm SHA256`. On Linux, run `sha256sum fixtures/sample.txt`. On macOS, run `shasum -a 256 fixtures/sample.txt`.

Expected SHA-256:

    d51dc5de135adffc3f9bb5a2b412ff97bfc98edf1643c06f20627d447d5988da
