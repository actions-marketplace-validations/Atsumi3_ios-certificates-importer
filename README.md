# iOS Certificates Importer

A GitHub Action to automatically import iOS certificates and provisioning profiles into your CI/CD pipeline. 
This action supports importing P12 certificates and provisioning profiles directly from base64 encoded strings stored in GitHub Secrets.

## Features

- Import P12 certificates from base64 encoded strings
- Import provisioning profiles from base64 encoded strings
- Automatic installation to keychain
- Secure handling of sensitive credentials
- Support for multiple certificate types (Development, Distribution, Ad Hoc)

## Usage

```yaml
jobs:
  build:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Install Certificates
        uses: Atsumi3/ios-certificates-importer@v1
        with:
          p12-base64: ${{ secrets.IOS_P12_BASE64 }}
          p12-password: ${{ secrets.IOS_P12_PASSWORD }}
          provisioning-profile-base64: ${{ secrets.IOS_PROVISIONING_PROFILE_BASE64 }}
```

## Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `p12-base64` | Yes | Base64 encoded P12 certificate string stored in GitHub Secrets |
| `p12-password` | Yes | Password for the P12 certificate stored in GitHub Secrets |
| `provisioning-profile-base64` | Yes | Base64 encoded provisioning profile string stored in GitHub Secrets |


## Preparing Your Certificates

:warning: This key name is sample. You can use your own key name.

1. Export your P12 certificate:
   ```bash
   base64 -i ios_certificates.p12 | pbcopy
   # paste the result to the GitHub Secrets: IOS_P12_BASE64
   # and add the password to the GitHub Secrets: IOS_P12_PASSWORD
   ```

2. Export your provisioning profile:
   ```bash
   base64 -i ios_build_profile.mobileprovision | pbcopy
   # paste the result to the GitHub Secrets: IOS_PROVISIONING_PROFILE_BASE64
   ```

3. Add the base64 encoded strings to your GitHub repository secrets:
   - `IOS_P12_BASE64`: The base64 encoded P12 certificate
   - `IOS_P12_PASSWORD`: The password for the P12 certificate
   - `IOS_PROVISIONING_PROFILE_BASE64`: The base64 encoded provisioning profile

## Security

- All sensitive data should be stored as GitHub Secrets
- The action uses secure methods to handle certificates and profiles
- Keychain access is properly managed and cleaned up after use
- Base64 encoded strings are decoded securely in memory

## Requirements

- macOS runner
- Xcode installed on the runner
- Valid Apple Developer Program account

## License

MIT License

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## Support

If you encounter any issues or have questions, please open an issue in the GitHub repository.
