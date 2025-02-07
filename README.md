# Secrets Vault

Ce chart présente l'utilisation du kind VaultStaticSecret afin de retrouver un secret sur [vault](https://www.vaultproject.io/) via [VaultSecretOperator](https://developer.hashicorp.com/vault/tutorials/kubernetes/vault-secrets-operator)

## Création d'un secret

### Via la WebUI

### Via la CLI

## Récupération d'un secret

Pour chaque projet créé dans la console, des objets de type `VaultConnection` et `VaultAuth` sont automatiquement créés afin de pouvoir authentifié le projet auprès du vault.

Pour récupérer un secret, créer le manifest suivant:
- Organisation: orgprch
- Nom du projet: projetdemo

```yaml
apiVersion: secrets.hashicorp.com/v1beta1
kind: VaultStaticSecret
metadata:
  name: db-secrets
spec:
  vaultAuthRef: vault-auth # Nom du VaultAuth, toujours vault-auth dans notre cas
  mount: orgprch-projetdemo # Nom du kv dans vault (<organisation>-<nom du projet>)
  path: db
  type: kv-v1
  refreshAfter: {{ .Values.vaultRefreshAfter }}
  destination:
    name: db-secrets
    create: true
```