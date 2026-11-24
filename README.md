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
