# Publish AUR package

GitHub Actions to publish AUR package.

## Inputs

### `pkgname`

**Required** AUR package name.

### `pkgbuild`

**Required** Path to PKGBUILD file.

### `commit_username`

**Required** The username to use when creating the new commit.

### `commit_email`

**Required** The email to use when creating the new commit.

### `ssh_private_key`

**Required** Your private key with access to AUR package.

### `commit_message`

**Optional** Commit message to use when creating the new commit.

### `ssh_keyscan_types`

**Optional** Comma-separated list of types to use when adding aur.archlinux.org to known hosts.

## Example usage

```yaml
name: aur-publish

on:
  push:
    tags:
      - '*'

jobs:
  aur-publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Publish AUR package
        uses: KSXGitHub/github-actions-deploy-aur@master
        with:
          pkgname: my-awesome-package
          pkgbuild: ./PKGBUILD
          commit_username: ${{ secrets.AUR_USERNAME }}
          commit_email: ${{ secrets.AUR_EMAIL }}
          ssh_private_key: ${{ secrets.AUR_SSH_PRIVATE_KEY }}
          commit_message: Update AUR package
          ssh_keyscan_types: rsa,dsa,ecdsa,ed25519
```

**Tip:** To create secrets (such as `secrets.AUR_USERNAME`, `secrets.AUR_EMAIL`, and `secrets.AUR_SSH_PRIVATE_KEY` above), go to `$YOUR_GITHUB_REPO_URL/settings/secrets`. [Read this for more information](https://help.github.com/en/actions/configuring-and-managing-workflows/creating-and-storing-encrypted-secrets).
