# cwa-sync

Syncs the default branches of the cosee cwa (corona-warn-app) forks with the upstream repositories.

Note that the sync will break if there are downstream changes on the default branch, so always
do your work on a separate branch.

## Adding a repo

- Create a deploy key with write access for the repo you want to push to (preferably in ed25519 format)
- Register the public key in the target repo
- Add the key pair as secrets in this repo (encode private key with base64 to preserve line breaks)
- Create a new job in the [workflow config](.github/workflows/sync.yml)
  - Copy-paste an existing job
  - Adjust source and target branch
  - Adjust source and target repo
  - Adjust secret name in `env` section
