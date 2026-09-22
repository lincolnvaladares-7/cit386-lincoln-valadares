# Connection Runbook

**Student:** Lincoln Guimaraes Valadares  
**Course:** CIT 386  
**Module:** Module 02  

## Purpose

This runbook explains how to start with a Windows computer and connect to the class Ubuntu server with PuTTY using SSH key authentication. The instructions are written so that a reader who has not completed the setup before can follow them without guessing.

> **Security:** Never put the contents of the private key, public key, or a key fingerprint in this document or in a public GitHub repository. Do not include a screenshot of PuTTYgen while key material is visible.

## 1. What You Need Before You Begin

Install **PuTTY for Windows**. The PuTTY installation includes **PuTTYgen**, which is used to convert the original private key into the format PuTTY uses.

For this connection, have the following information and files ready:

- Server address: `48.211.168.52`
- SSH port: `22`
- SSH username: `azureuser`
- Original private key: `VM01_key (1).pem`
- Converted PuTTY private key: `pp.ppk`
- Saved PuTTY session name: `cit386`

Create a private folder for SSH keys, for example:

`C:\Users\<your-Windows-user-name>\Documents\SSH-Keys\`

The safest arrangement is to keep `VM01_key (1).pem` and `pp.ppk` in that private folder and **outside the Git repository**. The working PuTTY configuration used during testing selected `pp.ppk` from the Windows Desktop, but a dedicated SSH key folder is recommended for long-term storage.

## 2. Convert the Key with PuTTYgen

The original private key is `VM01_key (1).pem`. PuTTY uses a `.ppk` private-key file, so convert the `.pem` file before configuring PuTTY.

1. Open the Windows **Start** menu.
2. Search for **PuTTYgen** and open it.
3. Click **Load**.
4. If `VM01_key (1).pem` is not visible, change the file-type filter so that all files or the appropriate private-key files are displayed.
5. Select `VM01_key (1).pem` and click **Open**.
6. After PuTTYgen imports the key, click **Save private key**.
7. If a passphrase is required by the class or organization, configure it as instructed. Do not publish the passphrase.
8. Save the converted private key as `pp.ppk`.
9. Store `pp.ppk` in the same protected SSH-key folder.

The conversion is therefore:

`VM01_key (1).pem` → **PuTTYgen** → **Save private key** → `pp.ppk`

Do not copy the text displayed inside PuTTYgen into this document.

## 3. Configure PuTTY

### Server Address and Port

1. Open **PuTTY**.
2. Select **Session** in the left pane.
3. In **Host Name (or IP address)**, enter `48.211.168.52`.
4. In **Port**, enter `22`.
5. Under **Connection type**, select **SSH**.

![PuTTY Session configuration](images/putty-session.png)

**Figure 1. PuTTY Session configuration.** The connection is configured for `48.211.168.52` on SSH port `22`.

### Select the Private Key

1. In the left pane, expand **Connection**.
2. Expand **SSH**.
3. Select **Auth** and, on PuTTY versions that show it, **Credentials**.
4. Find **Private key file for authentication**.
5. Click **Browse**.
6. Select `pp.ppk`.
7. Confirm that the path displayed by PuTTY points to the intended `pp.ppk` file.

The tested configuration selected:

`C:\Users\ilia\Desktop\pp.ppk`

![PuTTY private-key configuration](images/putty-private-key.png)

**Figure 2. PuTTY private-key configuration.** PuTTY is configured to authenticate with the converted `pp.ppk` private key.

### Enter the Username

1. In the left pane, select **Connection > Data**.
2. Find **Auto-login username**.
3. Enter `azureuser`.

### Save the Session

1. Return to **Session** in the left pane.
2. In **Saved Sessions**, type `cit386`.
3. Click **Save**.

The next time you need to connect, open PuTTY, click `cit386`, click **Load**, and then click **Open**. This makes the connection a quick two-click process after PuTTY opens.

## 4. Connect and Verify Success

1. Load the saved `cit386` session.
2. Click **Open**.
3. The first time a Windows computer connects to this server, PuTTY may display a host-key/security warning. The warning means that PuTTY has not previously stored the identity of this SSH server.
4. Confirm that the destination is the server you intended to reach. If the instructor provides a fingerprint through a trusted channel, verify it there without copying the fingerprint into this repository.
5. If the server identity is correct, accept the host key so PuTTY can remember the server for later connections.
6. PuTTY will attempt authentication with username `azureuser` and the selected `pp.ppk` private key.

A successful connection opens the Ubuntu terminal and displays a shell prompt. During testing, the prompt was:

`azureuser@VM01:~$`

![Successful SSH connection](images/successful-connection.png)

**Figure 3. Successful SSH connection to VM01.** The `azureuser@VM01:~$` prompt confirms that authentication succeeded and the user reached the remote Ubuntu shell.

## 5. Troubleshooting

The exact wording can vary slightly by PuTTY or server version. If the Activity 2.1 reference table shows different wording for your environment, use that exact wording in the final submitted version.

| Failure message | What it means | First thing to check |
| --- | --- | --- |
| `Network error: Connection refused` | The destination responded, but an SSH connection was not accepted on the requested port. | Verify the server address `48.211.168.52` and make sure the port is `22`. |
| `Network error: Connection timed out` | PuTTY could not establish the network connection before the timeout. | Check the Windows computer's network connection, then verify that the server is reachable. |
| `Network error: No route to host` | The computer cannot find a network path to the destination. | Check the network or required VPN connection and verify the server address. |
| `Server refused our key` | The server rejected the private key presented by PuTTY. | Check that `pp.ppk` is selected under **Connection > SSH > Auth/Credentials** and that the key belongs to the `azureuser` account. |
| `Access denied` | Authentication was rejected. | Verify that the username is exactly `azureuser` and that the correct `pp.ppk` file is selected. |
| `Host does not exist` | The host name entered in PuTTY could not be resolved. | Check the host name for typing errors. When using this runbook, verify that the IP is `48.211.168.52`. |

Never troubleshoot an authentication problem by posting the private key online.

## 6. Key Handling

The **public key** is the part of an SSH key pair that may be placed on the server or provided to the server administrator for authorization.

The **private key** must remain secret. In this setup, both the original `VM01_key (1).pem` and its converted PuTTY version `pp.ppk` contain private-key material. Neither file should be committed to GitHub, pasted into documentation, or included in screenshots showing its contents.

A private key may be transferred to another trusted computer only when the authorized user needs that computer for SSH authentication. It must still be stored securely.

If the private key is exposed, treat it as compromised. Stop using it, notify the instructor or server administrator, have the corresponding public-key authorization revoked, and obtain or generate a replacement key pair according to the class procedure.

## 7. Test the Runbook

Before submission, test the instructions rather than assuming they work.

1. Close PuTTY.
2. Reopen PuTTY.
3. Select the saved `cit386` session and click **Delete**.
4. Start again at Section 1 and follow this document exactly.
5. Recreate the PuTTY configuration without relying on memory.
6. Save the session again as `cit386`.
7. Open the connection.
8. Confirm that the terminal reaches `azureuser@VM01:~$`.
9. Correct any instruction that required information not written in the runbook.
10. Inspect every screenshot and repository file one final time to ensure no private-key contents, public-key contents, or fingerprint have been exposed.

## 8. Repository and Submission

Save this Markdown document at:

`module02/connection-runbook.md`

Save its screenshots in:

`module02/images/`

The repository should therefore contain the runbook and its safe supporting screenshots, but **must not contain `VM01_key (1).pem` or `pp.ppk`**.

Build the document through multiple meaningful Git commits so the history shows the work developing instead of appearing in one final paste. For example:

- Add runbook prerequisites and key-conversion steps.
- Add PuTTY configuration and connection verification.
- Add troubleshooting and key-handling sections.
- Test and revise the final runbook.

After the final version has been committed and pushed, paste the repository URL into the course submission box.
