# How to deploy
## Step 1 - Create a new OAuth App for SSO

## Step 2 - Apply ArgoCD Secret

Replace github.clientID: and github.clientSecret: in **argo-sso-secret.yaml** file with new client secret we just created above

Apply it via command below
```
PGP....
sops --decrypt argo-sso-secret.yaml | kubectl apply -f -
```
## Step 3 - Add repository
```
helm repo add argo https://argoproj.github.io/argo-helm
```
## Step 4 - Install chart
```
helm upgrade --install argo-cd argo/argo-cd -n argo -f values-custom.yaml --version 5.49.0 --create-namespace
```
## Step 5 - Apply ArgoCD cred overlay for Github Repo
```
sops --decrypt cred-overlay.yaml | kubectl apply -f -
```

# How to encrypt required kubernetes secrets using SOPS
Assume that we are having a traditional kubernetes file named `secret.yaml` and we want to encrypt that secret using SOPS to push it to Git repo
```
gpg --list-keys
gpg: checking the trustdb
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: depth: 0  valid:   1  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 1u
In the "pub" part of the output, you can get the GPG key fingerprint. Alternatively, you can run gpg --list-secret-keys "${KEY_NAME}" to get it.

Store the key fingerprint for future reference.
sops --encrypt --encrypted-regex '^(data|stringData)$' secret.yaml > secret-encrypted.yaml
```