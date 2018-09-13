# Ansible playbook to deploy the example Rails app
This playbook installs the necessary requirements to run a Docker container,
configure secrets and launch the app.

## Before playing it
After cloning this repo, you'll need to configure hosts (either in
/etc/ansible/hosts or by using a file that'll be passed as arguments
of the `ansible-playbook` command with `-i`).

Then you'll need to create your own `vault.yml` file in host_vars/<hostname>/
with the values:
```
vault_secret_key_base: <your_secret_key_base>
vault_secret_token: <your_secret_token>
```
Don't forget to encrypt this file with `ansible-vault encrypt` if you want to
keep it in version control.

You can also set where you want the app repo to be cloned to by changing the value
of the `app_dir` variable in `host_vars/<hostname>/vars.yml`.

## Playing the playbook
Then simply run:
```
ansible-playbook site.yml
```

Don't forget `--ask-vault-pass` if you have encrypted `vault.yml`.

## Level 3 - What would I want to check before deploying to prod?
I would probably test the app more thoroughly, let it run for some time and check
the metrics of the server to see if it sustains and if it still would in a prod
envrionment.
