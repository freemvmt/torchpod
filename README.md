# MLX8 Week 6

Summarising your lovelife into neat little TL;DR's since 2k25.

> by the Perceptron Party


## Script kids

For quick setup of a GPU from [Computa](https://computa.mlx.institute/), we have some handy scripts. To use them to streamline your workflow, do the following:

1. Update your `~/.ssh/config` file with the ip/port of the new server. It should look something like this:

```
Host mlx
	HostName 80.15.7.37
	User root
	Port 43209
	IdentityFile ~/.ssh/id_mlx_computa
```

2. Run `./send.sh` from root. If you named the host something other than `mlx` in the config, or your GitHub private key is called something other than `id_ed25519_gh`, then include these as args:

```sh
./send.sh [host] [private_key]
```

3. SSH into the remote (e.g. by running `ssh mlx` assuming given config)

4. Run `source ssh.sh` on entry to the remote (`ssh.sh` should have been transferred to the home dir of the `root` user). You will be prompted for the password to your GitHub private key. This will clone the repo (into `/workspace/`), cd into it, and further run `source setup.sh` to update packages, sync uv, activate your virtual environment, etc. You can then run `python ...` as required.

NB. If the remote is some cutting edge GPU (e.g. RTX 5090), it will require the nightly version of torch. To let the script handle this, `export BEAST_MODE=1` on the remote, before step 3.
