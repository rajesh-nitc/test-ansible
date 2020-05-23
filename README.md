## deploy

### prerequisite

```
pip3 install ansible requests google-auth ansible-lint
```
create instances on gcp and attach a label env=dev
### validate templates
```
ansible-lint -v playbook.yml
```
### get dynamic inventory from cloud
```
ansible-inventory -i data.gcp.yml --output dynamic-ini --list
```
### build inventory file for dev at runtime
```
echo "[dev]" > dev/ini
cat dynamic-ini | jq -r '.gcp_env_dev.hosts[]' >> dev/ini
```
### run playbook
```
ansible-playbook -i dev/ini playbook.yml
```
