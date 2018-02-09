# vdirsyncd

A simple wrapper around vdirsyncer to make for a hopefully secure way of
providing the password to vdirsyncer.

The idea is to encrypt the password to use for connecting to the defined storage
with GPG. Instead of relying on gpg-agent to keep the private key available with
vdirsyncer running in an interval, the required password is read into the shell
environment once. Every time vdirsyncer is started (defined interval) the password
is provided.

## Configuration

Vdirsyncer needs to have a password fetch command defined in the configuration file:

`~/.vdirsyncer/config`

with a value like:

`password.fetch = ["command", "cat", "-" ]`

The password for access to the defined storage should be encrypted using your
gpg key and stored in:

`~/.vdirsyncd.gpg`

You can store it like:

`gpg --encrypt --armor --recipient <email adress> --output vdirsyncd.gpg`

## Usage

vdirsyncd has a couple of options and actions.

`start

Start vdirsyncd. This will check if it is already running. Default it will
run vdirsyncer every 300 seconds.

`stop

Stop vdirsyncd.

`status

Check if vdirsyncd is running. If it is running the return value will be 0. If it
is stopped the return value will be 1.

`-i <interval>

When starting vdirsyncer will be run every 300 seconds. This option will change
the interval to the specified value (in seconds).

`-q

Produce as little output as possible.

`-h

Show the help message.

## Examples

Start vdirsyncd and run vdirsyncer every 3 minutes.

`vdirsyncd -i 180 start`

When logging in on the server `shell` start vdirsyncer and produce as little output
as possible (useful in .bash_profile).

`test "$HOSTNAME" = "shell" && vdirsyncd -q start

