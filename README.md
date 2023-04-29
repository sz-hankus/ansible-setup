# A simple ansible playbook for setting up a new server/VPS/raspberrypi

Feel free to look around. Maybe you'll find something useful :)

## What this playbook does:
1) Configures the system (see the `system_conf` role)
   - adds a new user whose name you can set in `group_vars/all.yml`
   - Gives the user sudo privileges (this assumes that `/etc/sudoers` exists on the target machine)
   - Adds an authorized public SSH key for the new user (path configurable in `group_vars/all.yml`)
   - Makes SSHD listen on a custom port (configurable in  `group_vars/all.yml`)
   - Turns off SSH password authentication and disables root login for security reasons

2) Sets up my personal work environment (see the `personal_setup` role)
   - Installs all my favorite packages  
   - Clones my [dotfiles repo](https://github.com/sz-hankus/dotfiles)

## Usage
1. Store the password for your new user (defined in `group_vars/all/vars.yml`) in\
an ansible vault at `group_vars/all/vault`.
- Open a new ansible vault and encrypt it with some password
```shell
ansible-vault create group_vars/all/vault
```
- Add a variable called `vault_password` and set it to your desired password for the new user
```
vault_password = putyourpasswordhere
```

2. Run the playbook

- If you're using password authentication for the SSH connection and you don't have the password for the existing sudo user stored in a vault:
```shell
ansible-playbook -i your_hosts_file --ask-pass run.yml 
```

- If you do have the existing sudo user password in an `ansible-vault`, add it in the `hosts` file as `ansible_password` and run:
```shell
ansible-playbook -i your_hosts_file run.yml 
```

- If you're using pubkey authentication, specify the path of the key in your `hosts` file and run:
```shell
ansible-playbook -i your_hosts_file run.yml 
```