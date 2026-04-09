# SUDO

A repository to keep Samba configuration files for reference and version control.

## Contents

- `smb.conf` — Main Samba configuration file template

## Usage

Copy `smb.conf` to `/etc/samba/smb.conf` and adjust the settings to match your environment, then restart Samba:

```bash
sudo systemctl restart smbd nmbd
```

Verify the configuration syntax with:

```bash
testparm
```