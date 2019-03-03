# Mac Development Ansible Playbook

Forked from https://github.com/geerlingguy/mac-dev-playbook

## Installation

### TODO: write bootstrap script to install xcode and Ansible, and run ansible-galaxy install on requirements.yml

  1. Ensure Apple's command line tools are installed (`xcode-select --install` to launch the installer).
  2. [Install Ansible](http://docs.ansible.com/intro_installation.html).
  3. Clone this repository to your local drive. Note that for mas to work, this has to be run against localhost, not remotely.
  4. Sign into the Mac App store manually -- this is required for the mas tool to run successfully. See https://github.com/mas-cli/mas/issues/164
  5. Run `$ ansible-galaxy install -r requirements.yml` inside this directory to install required Ansible roles.
  6. Copy `default.config.jeff.yml` to `config.yml`.
  6. Run `ansible-playbook main.yml -i inventory -K --ask-vault-pass` inside this directory.

> Note: If some Homebrew commands fail, you might need to agree to Xcode's license or fix some other Brew issue. Run `brew doctor` to see if this is the case.

## Overriding Defaults
Not everyone's development environment and preferred software configuration is the same.

You can override any of the defaults configured in `default.config.yml` by creating a `config.yml` file and setting the overrides in that file. For example, you can customize the installed packages and apps with something like:

    homebrew_installed_packages:
      - cowsay
      - git
      - go
    
    mas_installed_apps:
      - { id: 443987910, name: "1Password" }
      - { id: 498486288, name: "Quick Resizer" }
      - { id: 557168941, name: "Tweetbot" }
      - { id: 497799835, name: "Xcode" }
    
    composer_packages:
      - name: hirak/prestissimo
      - name: drush/drush
        version: '^8.1'
    
    gem_packages:
      - name: bundler
        state: latest
    
    npm_packages:
      - name: webpack
    
    pip_packages:
      - name: mkdocs

Any variable can be overridden in `config.yml`; see the supporting roles' documentation for a complete list of available variables.

## Testing the Playbook

Many people have asked me if I often wipe my entire workstation and start from scratch just to test changes to the playbook. Nope! Instead, I posted instructions for how I build a [Mac OS X VirtualBox VM](https://github.com/geerlingguy/mac-osx-virtualbox-vm), on which I can continually run and re-run this playbook to test changes and make sure things work correctly.
