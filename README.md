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
