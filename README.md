# Torch on remote 🔥

A base template for a vanilla Pytorch project on Python 3.12, setup with uv, with scripts for racking up remote GPUs, e.g. on [runpod.io](https://www.runpod.io/).


## Script kids

For quick setup of a GPU, we have some handy scripts to streamline your workflow.

Before proceeding, change the `git clone ...` command (and following `cd ...`) in `ssh.sh` to reflect your repo name and location.

Then, when you have a new GPU server spun up and ready to roll, do the following:

1. Update your `~/.ssh/config` file with the ip/port of the new server. It should look something like this:

```
Host pod
	HostName 80.15.7.37
	User root
	Port 43209
	IdentityFile ~/.ssh/id_ed25519_pod
```

2. Run `./send.sh` from root. If you named the host something other than `pod` in the config, or your GitHub private key is called something other than `id_ed25519_gh`, then include these as args:

```sh
./send.sh [host] [private_key]
```

3. SSH into the remote (e.g. by running `ssh pod` assuming given config)

4. Run `source ssh.sh` on entry to the remote (`ssh.sh` should have been transferred to the home dir of the `root` user). You will be prompted for the password to your GitHub private key. This will clone the repo (into `/workspace/`), cd into it, and further run `source setup.sh` to update packages, sync uv, activate your virtual environment, etc. You can then run `python ...` as required.

NB. If the remote is some cutting edge GPU (e.g. RTX 5090), it will require the nightly version of torch. To let the script handle this, `export BEAST_MODE=1` on the remote, before step 3.
