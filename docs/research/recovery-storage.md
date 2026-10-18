# Recovery storage research

Checked: 2026-10-17. Status: the engineer accepted 1Password and OneDrive on 2026-10-18; the recovery test remains outstanding. The comparisons below retain the original research context. Research only: no personal accounts, keys or cloud resources were accessed.

## Proposed small-lab arrangement

Keep a generated, high-entropy OpenTofu encryption passphrase in a dedicated 1Password Password item (or Secure Note with a password field). Keep the working state locally outside a sync folder, and copy completed encrypted state files to OneDrive under distinct UTC timestamped names. iCloud Drive is an acceptable alternative if already preferred. These are independent copies of the working file, **not immutable or independently administered backups**: deletion and account compromise can still affect the whole cloud folder. This is an architectural recommendation, not a vendor guarantee.

1Password supports Password and Secure Note items, custom fields, and password generation. A dedicated password field makes the secret easier to identify and later retrieve. Optional CLI `op read` can retrieve a field by secret reference; it prints the secret to stdout unless an output file is selected, so future automation must avoid logs and shell tracing. CLI integration is unnecessary for milestone 1. [Item categories](https://support.1password.com/item-categories/), [custom fields](https://support.1password.com/custom-fields/), [generator](https://support.1password.com/generate-website-password/), [CLI read](https://www.1password.dev/cli/reference/commands/read).

## OneDrive versus iCloud Drive

| Concern | OneDrive Personal | iCloud Drive |
| --- | --- | --- |
| Recovery history | Microsoft's generic OneDrive article covers all file types and currently states 30-day history; its Office article says personal accounts can retrieve the last 25 versions. These statements differ: do not assume a uniform last-25 guarantee for encrypted state. Verify the account's behavior and retain dated copies. | The reviewed Apple docs establish deleted-file recovery; do not assume arbitrary historical versions of encrypted state are retained. |
| Deleted files | Personal-account recovery window is 30 days; permanently deleted recycle-bin items cannot be restored. | Deleted files are recoverable for 30 days unless permanently removed earlier. |
| Upload completion | Paused, pending or error status means a local copy is not proof of completed upload. | Finder's “Waiting to Upload” explicitly means the file is not yet stored in iCloud. |

Sources: [Generic OneDrive version history](https://support.microsoft.com/en-us/onedrive/restore-a-previous-version-of-a-file-stored-in-onedrive), [Office version history](https://support.microsoft.com/en-us/office/collab-files/view-previous-versions-of-office-files), [OneDrive deleted-file recovery](https://support.microsoft.com/en-us/onedrive/restore-your-onedrive-files), [OneDrive sync indicators](https://support.microsoft.com/en-us/onedrive/what-do-the-onedrive-icons-mean), [Apple deletion/recovery](https://support.apple.com/en-ca/guide/icloud/mm3b7fcd0c10/icloud), [iCloud file status](https://support.apple.com/en-in/guide/mac-help/mchlc994344b/27/mac/27).

Recommendation: prefer dated copies over repeatedly overwriting one cloud file, retain several completed states, and verify each new backup through the service's web interface and a downloaded-copy recovery exercise. Sync alone is not the recovery procedure. iCloud deletions propagate across devices; OneDrive also has finite recovery windows. Neither service provides an immutable archive through ordinary sync. [Apple sync deletion behavior](https://support.apple.com/en-gb/108922), [Microsoft recovery limits](https://support.microsoft.com/en-us/onedrive/restore-your-onedrive-files).

## Recovery limitations and acceptance evidence

OpenTofu encrypts state and saved plans at rest, configured separately. Encryption cannot recover a lost key or damaged state, prevent replay of older state, or hide secrets from the operator running OpenTofu. Preserve keys required by retained backups after rotation; encryption inputs must be available before state is read. [OpenTofu encryption](https://opentofu.org/docs/language/state/encryption/).

The proposed recovery exercise should retrieve the key from 1Password and download/decrypt a dated backup into a separate working directory. Access to both accounts, MFA/recovery material, network connectivity and sufficient cloud storage are dependencies. Keep the 1Password Emergency Kit accessible independently of the failed laptop; its documentation explains the sign-in information it contains and recommends safe storage. [Emergency Kit](https://support.1password.com/emergency-kit/).

Successfully decrypting an old backup proves readability, not that it matches live resources. Before applying or destroying anything after restoration, reconcile resource identities and changes since the backup and inspect a fresh plan; state records infrastructure bindings and older data can be stale. This is a recovery recommendation based on OpenTofu's state model and replay limitation. [State purpose](https://opentofu.org/docs/language/state/purpose/), [encryption limitations](https://opentofu.org/docs/language/state/encryption/).

## GitHub Actions cost fact

Standard GitHub-hosted runners are free for public repositories. **Larger runners are charged even for public repositories**; artifact/cache storage have separate allowances and billing rules. Therefore public-repository CI can use standard runners without a runner-minute budget, but “all Actions usage is free” would be inaccurate. [GitHub Actions billing](https://docs.github.com/en/billing/concepts/product-billing/github-actions).
