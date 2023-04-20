# A simple ansible playbook for setting up a new server/VPS/raspberrypi

Feel free to look around. Maybe you'll find something useful :)

## What this playbook does:
1) Configures the system (see the `system_conf` role)
   - adds a new user whose name you can set in `group_vars/all.yml`
   - Gives the user sudo privileges (this assumes that `/etc/sudoers` exists on the target machine)
   - Adds an authorized public SSH key for the new user (path configurable in `group_vars/all.yml`)
   - Makes SSHD listen on a custom port (configurable in  `group_vars/all.yml`)

2) Sets up my personal work environment (see the `personal_setup` role)
   - Installs all my favorite packages  
   - Clones my [dotfiles repo](https://github.com/sz-hankus/dotfiles)

## Usage
```shell
ansible-playbook -i your_hosts_file --ask-pass run.yml 
```
