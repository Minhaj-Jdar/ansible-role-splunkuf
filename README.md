ansible-role-splunkuf
=========
Downloads the Splunk Universal Forwarder binary and installs to the target machine (Windows or Linux)

Role Variables
--------------
Defined in `./defaults/main.yml`

* `binary_src_linux`
* `binary_src_windows`
* `binary_tmpdir_linux`
* `binary_tmpdir_windows`
* `binary_filename_linux`
* `binary_filename_windows`
* `splunk_installdir_linux`
* `splunk_installdir_windows`
* `deployment_server`
* `install_cmd_windows`

Task Tags
--------------
Defined in `./tasks/windows.yml` and `./tasks/el.yml`

* `download`
* `install`
* `start`

Usage Examples
--------------
* ansible-playbook tasks/main.yml -vvv -- --tags="download,install,start" --vault-password-file="<path_to_password_file>"

or

* ansible-playbook tasks/main.yml -vvv -- --tags="download,install" --vault-password-file="<path_to_password_file>"

or

* ansible-playbook tasks/main.yml -vvv -- --tags="start" --vault-password-file="<path_to_password_file>"


Role Secrets
--------------
Splunk UF admin credentials are defined in `./tasks/secrets.yml` (for Windows) and `./tasks/user-seed.conf` (for Linux).

Ansible Vault has been used to encrypt these two files with a Vault password. Decryption occurs during the playbook run using the switch `--vault-password-file="<path_to_password_file>"`

Role Development Dependencies
------------
Defined in `./requirements.txt`

* ansible>=2.9.12
* ansible[azure]
* ansible-lint>=4.2.0
* molecule>=3.0.6
* molecule-azure>=0.3
* yamllint>=1.24.2
* pywinrm>=0.4.1
* junit-xml>=1.9
* requests>=2.24.0
* wheel>=0.30.0

Role Development Steps (w/ Molecule/Azure)
----------------
1. Create and access your Ansible control node in Azure (can simply be 1x Ubuntu VM, 1x VNET, 1x SUBNET)
2. `git clone https://github.com/globalbao/ansible-role-splunkuf.git`
3. `cd /ansible-role-splunkuf` 
4. `./run.sh`
5. `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`
6. Update your Azure & Ansible variables in /molecule/scenarioName/files.yml as required
7. `az login`
8. `az subscription set -s SUBSCRIPTIONID`
9. `ansible-lint tasks/main.yml`
10. `molecule list`
11. `molecule create -s scenarioName`
12. `molecule converge -s scenarioName`
13. `molecule verify -s scenarioName`
14. `molecule test -s scenarioName`
