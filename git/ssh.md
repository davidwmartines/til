If you have a password-protected ssh key, and don't want to enter it on every pull/push, this is one option.

example:
```
$ ssh-add -t 24h  ~/.ssh/id_ed25519
```

This adds it temporarily for 24 huors.  -t can be any timformat or just seconds.
