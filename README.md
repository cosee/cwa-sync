# cwa-sync

Syncs the default branches of the cosee cwa (corona-warn-app) forks with the upstream repositories.

Note that the sync will break if there are downstream changes on the default branch, so always
do your work on a separate branch.

## Adding a repo

- Create a deploy key with write access for the repo you want to push to (preferably in ed25519 format)
  ```
  ssh-keygen -t ed25519 -N '' -f ./id_ed25519 -C 'upstream_sync'
  ```
- Register the public key in the target repo (Settings -> Deploy keys). Allow write access.
- Add the key pair as secrets in this repo. The private key has to be base64 encoded to preserve line breaks. `pbcopy` copies stuff to the clipboard and might only be available on OSX.
  ```
  # XXX_SSH_KEY
  cat id_ed25519 | base64 | pbcopy
  # XXX_SSH_PUB_KEY
  pbcopy < id_ed25519.pub
  ```
- Create a new job in the [workflow config](.github/workflows/sync.yml)
  - Copy-paste an existing job
  - Adjust source and target branch
  - Adjust source and target repo
  - Adjust secret name in `env` section
- Delete the ssh keypair on your local machine.
  ```
  rm id_ed25519 id_ed25519.pub
  ```