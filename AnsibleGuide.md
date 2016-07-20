# ping hosts

```
ansible -i devops/hosts all -m ping --private-key ~/workspace/octo/web.pem -u ubuntu
54.169.213.173 | success >> {
    "changed": false,
    "ping": "pong"
```

# disable host check

```
touch ~/.ansible.cfg
```

Now edit the `~/.ansible.cfg` to contain the following

```
[defaults]
host_key_checking = False
```

# Install the `rvm_io.rvm1-ruby` role

refer [https://github.com/rvm/rvm1-ansible](https://github.com/rvm/rvm1-ansible)

# Server Setup

```
ansible-playbook -i devops/hosts devops/server_setup.yaml --private-key ~/workspace/octo/web.pem -u ubuntu
```

# Troubleshooting

## unable to install `rvm_io.rvm1-ruby`

```
sudo pip install --upgrade pip
sudo pip install --upgrade setuptools --user python
```
