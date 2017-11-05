[TPM2 PK11](https://github.com/irtimmer/tpm2-pk11) provides a PKCS#11 backend for a TPM 2.0 chip. This can be used to secure your SSH keys.

**Note:** Only the OpenSSH client is supported as of November 2017.

## SSH Usage

Create keys:

```
$ mkdir ~/.tpm2 && cd ~/.tpm2
$ tpm2_createprimary -A e -g 0x000b -G 0x0001 -C po.ctx
$ tpm2_create -c po.ctx -g 0x000b -G 0x0001 -o key.pub -O key.priv
$ tpm2_load -c po.ctx -u key.pub -r key.priv -n key.name -C obj.ctx
$ tpm2_evictcontrol -A o -c obj.ctx -S 0x81010010
$ rm key.name *.ctx

```

Create configuration file and change it for your setup:

```
$ cp config.sample ~/.tpm2/config

```

Extract public key:

```
$ ssh-keygen -D libtpm2-pk11.so

```

Use your TPM key:

```
$ ssh -I libtpm2-pk11.so ssh.example.com

```

Or add the PKCS#11 module to your ssh configuration in `~/.ssh/config`:

```
Host *
    PKCS11Provider libtpm2-pk11.so

```