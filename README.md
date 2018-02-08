# vdirsyncd

A simple wrapper around vdirsyncer to make for a hopefully secure way of providing the
password to vdirsyncer.

It requires a password fetch command to be defined in the configuration file:

`~/.vdirsyncer/config`

with a value like:

`password.fetch = ["command", "cat", "-" ]`

The password for access to the defined storage should be encrypted using your gpg key and
stored in:

`~/.vdirsyncd.gpg`

You can store it like:

`gpg --encrypt --armor --recipient <email adress> --output vdirsyncd.gpg`

Then start vdirsynd like:

`vdirsyncd start`
