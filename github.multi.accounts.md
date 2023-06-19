# How to use multiple GitHub accounts from a single machine

## known info

- account name: myaccount
- email: myaccount@163.com
- private key path: ~/.ssh/myaccount_ed25519

## add config file for account `myaccount`

```bash
mkdir -p ~/.gitconfig.dir
cat <<EOF > ~/.gitconfig.dir/.gitconfig.myaccount
[core]
	sshCommand = ssh -i ~/.ssh/myaccount_ed25519 -o IdentitiesOnly=yes
[user]
	name = myaccount
	email = myaccount@163.com
EOF
```

## add `includeIf` to `~/.gitconfig` for `myaccount`

```bash
cat <<EOF >> ~/.gitconfig
[includeIf "gitdir:~/github/myaccount/**"]
	path = ~/.gitconfig.dir/.gitconfig.myaccount
EOF
```

## references

- https://git-scm.com/docs/git-config#_includes