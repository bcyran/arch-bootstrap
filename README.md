> [!WARNING]
> This repo is archived because I moved my setup to NixOS and Home Manager. See my [nix-config](https://github.com/bcyran/nix-config) ✨.

# Personal Arch Linux bootstrapping

## archinstall
Once booted into `archiso`, run:
```shell
archinstall --config https://raw.githubusercontent.com/bcyran/arch-bootstrap/main/archinstall/user_configuration.json
```

You only need to set the disk layout and root password, ignore other options.
Once satisfied, confirm the installation.
After the process finishes, reboot into the fresh install and login as root.

## Ansible
Clone the repo into `/tmp`:
```shell
git clone https://github.com/bcyran/arch-bootstrap.git /tmp/arch-bootstrap
```

Enter `ansible` directory:
```shell
cd /tmp/arch-bootstrap/ansible
```

Install required collections:
```shell
ansible-galaxy collection install -r requirements.yml
```

Adjust `hosts.yml` contents:
```yml
---
all:
  hosts:
    home:
      ansible_host: localhost
```
Replace `home` with `work` or `vm` as needed.

Run the playbook:
```shell
ansible-playbook -i hosts.yml playbook.yml --ask-become-pass --skip-tags {xorg,wayland}
```
You probably want to install only one of the `xorg` or `wayland` configs and skip the other.

If it's the first time the playbook is ran on the given machine, and user account didn't exist before, you will be asked to provide the desired password.

After the playbook is finished, logout and login again - ready graphical environment should be started.
