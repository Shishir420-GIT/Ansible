# Ansible Vault Basic Commands

Ansible Vault allows you to encrypt and manage sensitive data within Ansible, such as passwords and secrets, in a secure way. Below are commands to create, modify, view, remove, and rekey an encrypted file using Ansible Vault, with examples of using both a password file and manually entering a password.

1. Create an Encrypted File with Ansible Vault
- Using a Password File
```
ansible-vault create secret.yml --vault-password-file=/path/to/password_file
```
- Manually Entering a Password
```
ansible-vault create secret.yml
```
This command creates a new encrypted file secret.yml. You’ll be prompted to enter the content of the file in a text editor.

2. Edit an Encrypted File with Ansible Vault
- Using a Password File
```
ansible-vault edit secret.yml --vault-password-file=/path/to/password_file
```
- Manually Entering a Password
```
ansible-vault edit secret.yml
```
This command opens secret.yml in your default text editor and allows you to modify its content.

3. View (Decrypt Temporarily) an Encrypted File
- Using a Password File
```
ansible-vault view secret.yml --vault-password-file=/path/to/password_file
```
- Manually Entering a Password
```
ansible-vault view secret.yml
```
This command lets you view the decrypted content of secret.yml without permanently decrypting it.

4. Encrypt an Existing Unencrypted File
If you have an unencrypted file that you want to encrypt:

- Using a Password File
```
ansible-vault encrypt unencrypted_file.yml --vault-password-file=/path/to/password_file
```
- Manually Entering a Password
```
ansible-vault encrypt unencrypted_file.yml
```
This command encrypts unencrypted_file.yml with Ansible Vault.

5. Decrypt an Encrypted File (Remove Encryption)
- Using a Password File
```
ansible-vault decrypt secret.yml --vault-password-file=/path/to/password_file
```
- Manually Entering a Password
```
ansible-vault decrypt secret.yml
```
This command decrypts secret.yml, removing the encryption and making it a plain text file.

6. Rekey (Change Password) for an Encrypted File
- Using a Password File
```
ansible-vault rekey secret.yml --vault-password-file=/path/to/old_password_file --new-vault-password-file=/path/to/new_password_file
```
- Manually Entering the Password
```
ansible-vault rekey secret.yml
```
With this command, you’ll be prompted to enter both the old and new passwords if not using password files. It updates the encryption password for secret.yml to a new password.


## Example: Password File vs. Manual Password Entry
### To use a password file:
1. Create a plain text file containing the password, e.g., ```/path/to/password_file``` with a single line:
```
my_secure_password
```
2. Use the ```--vault-password-file``` option to provide the path to the password file in any of the commands above.

### To use manual password entry:
- Simply omit the ```--vault-password-file``` option from the command, and Ansible will prompt you to enter the password interactively.


By using these commands, you can securely manage encrypted data files in Ansible.