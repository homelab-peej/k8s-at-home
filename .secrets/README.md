# SOPS setup
---

- Install `gpg` from your package manager and download [SOPS](https://github.com/mozilla/sops/releases/tag/v3.7.3) and install it to your PATH
- Clone the repository
- Install the public key by running `gpg --import .sops.pub.asc` with the public key from the cloned repo
- Create your secret using the following template. If you're encoding simple strings, you can use `stringData` and save your file in plaintext before encrypting it. If your secret contains complex or multi-line data, you might need to use `data` instead. In this case, you need to encode your data in base64 before saving and fully encrypting your secret with `sops`.
  - All names and keys must follow RFC 1123
  - Your `data` or `stringData` keys can be any name you want
  - You can have as many or few key/data pairs as you need per secret
  - `.metadata.name` can be any name you want. This is what you will reference in the application manifest to use your encrypted data
  - `.metadata.namespace` should be the namespace your application runs in. You cannot reference objects in other namespaces.
```
apiVersion: v1
stringData:
    password: SECRET_PASSWORD
    username: SECRET_USERNAME
kind: Secret
metadata:
    name: SECRET_NAME
    namespace: NAMESPACE
type: Opaque
```
- Save your secret as a .yaml file. SOPS only targets .yaml filetypes with the included config.
- Encrypt your secret with `sops -e -i <filename>`
- Examine your secret to ensure it encrypted correctly
  - Only the data for each key should be encrypted
  - SOPS will only target `data` and `stringData` fields. The rest of the secret should be untouched
  - There should be a `.sops` config at the end of the file that will allow the Kustomize Controller in Flux to decrypt your secret before giving it to the Kubernetes API to install
- Commit and push your secret with git just like a normal code change.

### Notes: 
- You should not edit any unencrypted field in the secrets file while the data is encrypted or you will get a "MAC mistmatch" error. This value is validated any time the file is processed by `sops`. If you encounter this, you need to pass the `--igmore-mac` flag when decrypting.
- If you did not create the keypair but are given the private key, you can install it by saving it to a file and running `gpg --import <filename>`. This will let you also decrypt your secrets.
- If you have the private gpg key, you can decrypt your secrets with `sops -d -i <filename>` to edit values. Be sure to encrypt them again before committing back to the repository.
