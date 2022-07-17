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

Run the playbook, replace `{desired_password}` with correct value:
```shell
ansible-playbook -i hosts.yml playbook.yml --ask-become-pass --extra-vars "user_password={desired_password}" 
```

Logout and login again.
