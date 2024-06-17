# Connecting to a Linux Proxmox Host Using VSCode with SSH Keys

This guide provides step-by-step instructions to connect to a Linux Proxmox host using VSCode's Remote-SSH extension with SSH keys for authentication.

## Prerequisites

- A Linux Proxmox host with SSH access.
- Visual Studio Code (VSCode) installed on your local machine.
- Remote-SSH extension installed in VSCode.

## Step 1: Generate SSH Keys on Your Local Machine

1. Open a terminal on your local machine.
2. Generate a new SSH key pair by running the following command:

    ```sh
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

    Follow the prompts to save the key (default path is `~/.ssh/id_rsa`) and optionally set a passphrase.

## Step 2: Add Your Public Key to the Remote Host

1. Copy your public key to the remote host using:

    ```sh
    ssh-copy-id your_username@192.168.178.31
    ```

    If `ssh-copy-id` is not available, manually copy the public key:

    ```sh
    cat ~/.ssh/id_rsa.pub
    ```

    Then, paste the key into the `~/.ssh/authorized_keys` file on the remote host.

## Step 3: Install the Remote-SSH Extension in VSCode

1. Open VSCode.
2. Go to the Extensions view by clicking on the Extensions icon in the Activity Bar on the side of the window.
3. Search for `Remote - SSH` and install the extension from Microsoft.

## Step 4: Configure the Remote-SSH Connection in VSCode

1. Open the Command Palette (`F1` or `Ctrl+Shift+P`).
2. Type `Remote-SSH: Open Configuration File...` and select the SSH configuration file (typically `~/.ssh/config`).
3. Add the following configuration for your remote host:

    ```sh
    Host proxmox
        HostName 192.168.178.31
        User your_username
        IdentityFile ~/.ssh/id_rsa
    ```

## Step 5: Connect to Proxmox via VSCode

1. Open the Command Palette (`F1` or `Ctrl+Shift+P`).
2. Type `Remote-SSH: Connect to Host...`.
3. Select `proxmox` from the list of configured hosts.

You should now be connected to your Proxmox host via VSCode and able to work remotely.

## Summary of Commands

1. **Generate SSH Keys:**

    ```sh
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```

2. **Add Public Key to Remote Host:**

    ```sh
    ssh-copy-id your_username@192.168.178.31
    ```

3. **VSCode SSH Configuration:**

    ```sh
    Host proxmox
        HostName 192.168.178.31
        User your_username
        IdentityFile ~/.ssh/id_rsa
    ```

By following these steps, you can securely connect to your Linux Proxmox host using VSCode with SSH keys.
