# tmux

This is an __Ansible role__ for installing and configuring `tmux`. It installs a fancy `.tmux.conf` that greatly increases usability, including the [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm) and [tmux-resurrect](https://github.com/tmux-plugins/tmux-resurrect) so that you don't have to "quit" `tmux` when you power off your machine.

It also ensures that history is shared between `tmux` windows using [this method](http://unix.stackexchange.com/questions/1288/preserve-bash-history-in-multiple-terminal-windows). Finally, it adds some aliases to `.bashrc` to make managing `tmux` easier. 

## Installation

~~~sh
sudo ansible-galaxy install kylebebak.tmux
# to update
sudo ansible-galaxy install kylebebak.tmux --force
~~~

## Variables

~~~yaml
update: false
install: true

tmux_config: true
tmux_upgrade: true
tmux_plugin_manager: true
tmux_plugins:
  - set -g @plugin 'tmux-plugins/tmux-resurrect'

share_history: true
aliases: true
~~~

## Usage
This role can install __tmux version 2.0__, which is necessary if you include the __Tmux Plugin Manager__. This installation is only tested on Ubuntu. Installing v2.0 requires execution as `sudo`, so if you include `tmux_upgrade`, you should invoke `ansible-playbook` with `--ask-sudo-pass`.

Otherwise, playbooks including this role don't have to elevate to `sudo`, because the role only modifies files in the login user's home directory.

~~~yaml
# playbooks/tmux.yml
- hosts: all
  become: yes

  roles:
    - role: kylebebak.tmux
      tags: [tmux]
~~~

~~~sh
ansible-playbook -u {user} -i {inventory} playbooks/tmux.yml
~~~

## License
This code is licensed under the [MIT License](https://opensource.org/licenses/MIT).
