# Remote machine shell

## SSH

Create an ssh tunnel

```bash
# ssh to a specific port that's not 22
ssh -p 56789 root@localhost
```

```bash
ssh root@127.0.0.1 -p 56789 -N -L 5433:database-url:5432
```

### Ignore changing ssh host for 127.0.0.1

`REMOTE HOST IDENTIFICATION HAS CHANGED`

```bash
$cat ~/.ssh/config
Host 127.0.0.1
   StrictHostKeyChecking no
   UserKnownHostsFile=/dev/null
```

## Transfer files with [croc](https://github.com/schollz/croc)

```bash
# Terminal 1
$ croc send test.tif
Code is anita-price-quick
```

```bash
# Terminal 2
crock anita-price-quick
```

## tmux: Close a shell without killing the app that it's running

-   used at IBM when I connected to the Fyre VM
-   an IDE or a long running script

1. `ctrl z` (to send program to background)
2. `disown -a`
