# nightly

Reusable GitHub Action workflow for nightly Flutter desktop builds.

## What it does

- Runs daily at configured UTC time (default 08:00)
- Checks for new commits since last nightly build
- Only builds if there are new commits
- Creates a dated tag (`desktop/nightly-YYYYMMDD`)
- Builds the Flutter macOS app with release configuration
- Creates a signed/unsigned DMG
- Uploads as a prerelease

## Usage

```yaml
name: Nightly Build

on:
  schedule:
    - cron: '0 8 * * *'
  workflow_dispatch:

permissions:
  contents: write

jobs:
  nightly:
    uses: libnudget/nightly/.github/workflows/nightly.yml@main
    with:
      flutter-version: '3.41.6'
      tag-prefix: 'desktop/nightly-'
      app-name: 'browser'
      base-branch: 'main'
    secrets:
      macos-code-sign-identity: ${{ secrets.MACOS_CODE_SIGN_IDENTITY }}
      macos-certificate: ${{ secrets.MACOS_CERTIFICATE }}
      macos-certificate-password: ${{ secrets.MACOS_CERTIFICATE_PASSWORD }}
      macos-keychain-password: ${{ secrets.MACOS_KEYCHAIN_PASSWORD }}
      apple-id: ${{ secrets.APPLE_ID }}
      apple-team-id: ${{ secrets.APPLE_TEAM_ID }}
      apple-app-specific-password: ${{ secrets.APPLE_APP_SPECIFIC_PASSWORD }}
      macos-app-bundle-id: ${{ secrets.MACOS_APP_BUNDLE_ID }}
```

## Inputs

| Name | Type | Default | Notes |
|------|------|---------|--------|
| `flutter-version` | string | `3.41.6` | Flutter SDK version |
| `tag-prefix` | string | `desktop/nightly-` | Nightly tag prefix |
| `app-name` | string | `browser` | App binary name |
| `base-branch` | string | `main` | Base branch to check |

## Secrets

All secrets are optional. Set the ones you need for code signing:

- `macos-code-sign-identity`
- `macos-certificate`
- `macos-certificate-password`
- `macos-keychain-password`
- `apple-id`
- `apple-team-id`
- `apple-app-specific-password`
- `macos-app-bundle-id`

## License

MIT

## About

Reusable GitHub Action workflow for nightly Flutter desktop builds. Tracking: https://github.com/bniladridas/browser/releases