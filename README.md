# Password store for <YOUR_PROJECT_NAME>

Uses [gopass](https://github.com/gopasspw/gopass), which must be
[installed
first](https://github.com/gopasspw/gopass/blob/master/docs/setup.md#pre-installation-steps).

`./vpass` is simply an alias to `gopass` that sets the vault directory
to the current path.

## Generating your GPG key

These instructions presume that you are familiar with GPG.
If not, read
[Getting Started with GNU Privacy Guard](https://spin.atomicobject.com/2013/09/25/gpg-gnu-privacy-guard/)
for a general overview, or
[Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
to learn how to create your own keys.
We recommend EDDSA as the key type, but RSA (the default) is fine too.

## Initial vault creation (do this once)

```
./vpass init <your-gpg-id>
```

You can find your GPG id with `gpg --list-keys your@email.com`. The
ID looks something like `79DFFEFC5EC506356B7BCF00E5FEBCA4A034DD65`.


## Add/edit a new password

```
./vpass insert vault/name-of-site
./vpass edit vault/name-of-site
```

Or generate a new password:

```
./vpass generate vault/name-of-site  # generate password for new password entry
./vpass generate -i vault/name-of-site  # re-generate for existing password entry
```

See https://www.passwordstore.org/ for further detail.

## Look up a password

```
./vpass  # list all passwords
./vpass vault/site-name  # show password for site-name
```

## Add a new recipient

1. Find the GPG key ID of the recipient.  This will be a hexadecimal
   string similar to `79DFFEFC5EC506356B7BCF00E5FEBCA4A034DD65`, and
   can be found with:

   ```
   gpg --list-key user@email.com
   ```

2. Add the recipient. The vault will be re-encrypted, including the new recipient:

   ```
   ./vpass recipients add 79DFFEFC5EC506356B7BCF00E5FEBCA4A034DD65
   ```

## List existing recipients

```
./vpass recipients
```

## Removing recipients

Removing a recipient will also re-encrypt the password vault, so
that that persons no longer has access to future version of the vault.
HOWEVER, since they have access to their existing copy, you should
**consider all secrets compromised** and rotate them.


```
./vpass recipients rm 79DFFEFC5EC506356B7BCF00E5FEBCA4A034DD65
```
