# Poor Man's MFA

Poor Man's MFA (pmmfa) is a simple bash script for managing and generating Time-based One-Time Passwords (TOTP) for multi-factor authentication (MFA), leveraging the following system tools:

* GPG: Encrypts/decrypts the file where TOTP secrets are stored.
* oathtool: Generates the TOTP codes

It's designed for those who prefer a minimalist, command-line approach to MFA, without relying on third-party services or applications.


## Features

* **Secure Storage**: Secrets are encrypted using GPG with AES256 cipher algorithm
* **Easy to Use**: Simple commands to add, edit, list, and generate TOTP codes
* **Clipboard Support**: Automatically copies the TOTP code to the clipboard if `xclip` is available
* **Shell Completion**: Supports shell completion for for Bash, Zsh, Fish
* **Interactive Mode**: Allows entering your GPG password once and generating multiple TOTP codes until the script exits


## Prerequisites

Before you begin, ensure you have met the following requirements:

* `gpg` and `oathtool` installed on your system.
* `xclip` for clipboard support (optional).
* `rlwrap` for interactive mode (optional).

You must have a default gpg keypair configured with a password. This is the password you'll use to unlock the encrypted secrets file.


## Installation

1. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/drylikov/poor_mans_mfa.git
   ```
2. Optionally
  * Add the script directory to your `PATH` for easy access.
  * Add one of the completions files for CLI completion of secret names (`pmmfa` must be in your `PATH` for completions to work)


## Usage

To use Poor Man's MFA, you can run the script with various options:

* Generate a TOTP code: `./pmmfa [name]`
* Add a new secret: `./pmmfa -a`
* List all secret names: `./pmmfa -l`
* Edit the secret file: `./pmmfa -e`
* Generate bash completion data: `./pmmfa -g`
* Interactive mode: `./pmmfa -i`
* Help: `./pmmfa -h`

## Configuration

The script uses the following environment variables for configuration:

* `POOR_MANS_MFA_DIR`: Directory to store the secrets file and completion data file. Defaults to `${HOME}/.poor-mans-mfa`.
* `POOR_MANS_MFA_SECRET_FILE`: Name of the secrets file. Defaults to `2fa.gpg`.
* `POOR_MANS_MFA_COMPLETION_DATA_FILE`: Name of the plain text file that stores secret names for shell completion. Defaults to `completion-data`.
* `POOR_MANS_MFA_DISABLE_CLIPBOARD_INTEGRATION`: By default, TOTP codes are copied to the system clipboard if `xclip` is installed. Set this variable to any non-empty value to disable the feature.

## Security Note

The author makes no claim of security expertise and no warranties of the security of this software -- use at your own risk.

### Considerations

While Poor Man's MFA provides a convenient way to manage TOTP secrets, it's important to be aware of the security implications involved in handling sensitive information such as TOTP secrets and GPG passphrases. Please consider the following security aspects before using this tool:

* **Sensitive Data Handling**: The script temporarily stores secrets in plain text during the edit operation. Although measures are taken to remove these temporary files, there's a risk that sensitive data could be exposed if the script terminates unexpectedly or if the system is compromised during this operation.

* **GPG Passphrase Storage**: The GPG passphrase is stored in a global variable within the script during execution. This approach, while necessary for the script's functionality, could potentially expose the passphrase to other processes on the system, especially on multi-user systems or systems where malicious software is running.

* **Encryption and Decryption**: The script relies on GPG for encryption and decryption of secrets. Ensure that your GPG installation is secure, up-to-date, and configured correctly to minimize vulnerabilities.

* **Clipboard Security**: When using the feature to copy TOTP codes to the clipboard, be aware that the clipboard contents might be accessible to other applications or users on the same system.

### Recommendations

* **Use on Trusted Systems Only**: Run this script on systems you trust, which are secure, up-to-date, and free from unauthorized access or malware.

* **Secure Temporary Files**: Consider using encrypted temporary storage or ensuring that temporary files are stored on a secure filesystem to mitigate risks associated with plain text storage of secrets.

## Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.
