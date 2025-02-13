---
layout: auto-doc
title: step ssh renew
menu:
  docs:
    parent: step ssh
---

## Name
**step ssh renew** -- renew a SSH certificate using the SSH CA

## Usage

```raw
step ssh renew <ssh-cert> <ssh-key> [--out=<file>]
[--issuer=<name>] [--password-file=<file>] [--force] [--offline]
[--ca-config=<file>] [--ca-url=<uri>] [--root=<file>]
[--context=<name>]
```

## Description

**step ssh renew** command renews an SSH Host Cerfificate
using [step certificates](https://github.com/smallstep/certificates).
It writes the new certificate to disk - either overwriting `ssh-cert` or
using a new file when the **--out**=`file` flag is used. This command cannot
be used to renew SSH User Certificates.

## Positional arguments

`ssh-cert`
The ssh certificate to renew.

`ssh-key`
The ssh certificate private key.

## Options


**--out**=`file`, **--output-file**=`file`
The new certificate `file`. Defaults to overwriting the `ssh-cert` positional argument

**--provisioner**=`name`, **--issuer**=`name`
The provisioner `name` to use.

**--provisioner-password-file**=`file`
The path to the `file` containing the password to decrypt the one-time token
      generating key.

**--sshpop-cert**=`chain`
Certificate (`chain`) in PEM format to store in the 'sshpop' header of a JWT.

**--sshpop-key**=`file`
Private key `file`, used to sign a JWT, corresponding to the certificate that will
be stored in the 'sshpop' header.

**-f**, **--force**
Force the overwrite of files without asking.

**--offline**
Creates a certificate without contacting the certificate authority. Offline mode
uses the configuration, certificates, and keys created with **step ca init**,
but can accept a different configuration file using **--ca-config** flag.

**--ca-config**=`file`
The certificate authority configuration `file`. Defaults to
$(step path)/config/ca.json

**--ca-url**=`URI`
`URI` of the targeted Step Certificate Authority.

**--root**=`file`
The path to the PEM `file` used as the root certificate authority.

**--context**=`name`
The context `name` to apply for the given command.

## Examples

Renew an ssh certificate overwriting the previous one:
```shell
$ step ssh renew -f id_ecdsa-cert.pub id_ecdsa
```

Renew an ssh certificate with a custom out file:
```shell
$ step ssh renew -out new-id_ecdsa-cer.pub id_ecdsa-cert.pub id_ecdsa
```

