# KuberFreak-Gensyn-Script
ALL SOLUTIONS AT 1 PLACE

# GENSYN GUIDE BY CLONING OFFICIAL REPO (WHY FEAR WHEN KUBER FREAK IS HERE)

This guide walks you through setting up gensyn.

---

## Step 1: Install Dependencies

Update and upgrade your system, then install required packages:

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt install nano curl screen git ufw -y
sudo apt install unzip
```
---

If sudo: command not found:  ❌❌❌
```bash
apt install sudo
```
---

## Step 2: Clone the Repository

```bash
git clone https://github.com/kuberfreak/KuberFreak-Gensyn-Script.git
cd KuberFreak-Gensyn-Script
```

## If above command giving you error file already exits then run below command first then run the Step 2 else don't run below command (ONLY IF YOU GET ERROR) 

❌❌❌
```bash
rm -rf KuberFreak-Gensyn-Script
```
❌❌❌

---

## Step 3: Make Scripts Executable

```bash
chmod +x setup_gensyn.sh
```

---

If you are using vps then (FOR NEW USERS)
## Step 4: Enable Firewall & Open Required Ports

```bash
# Basic SSH Access
sudo ufw allow 22
sudo ufw allow ssh
sudo ufw allow 3000

# Enable Firewall
sudo ufw enable
```
---

## Step 5: Run the GENSYN

```bash
./setup_gensyn.sh
```

```bash
cd
screen -r gensyn
```
---

## Fix RuntimeError: DHTNode bootstrap failed

Full error:
> **RuntimeError: DHTNode bootstrap failed: none of the initial_peers responded to the ping. (set ensure_bootstrap_success=False to ignore)**

1. Open the file `testnet_grpo_runner.py`
``` bash
nano $HOME/rl-swarm/hivemind_exp/runner/grpo_runner.py
```

3. Find the line:
`dht = hivemind.DHT(start=True, **self._dht_kwargs(grpo_args))`

4. Replace it with:
```dht = hivemind.DHT(start=True, ensure_bootstrap_success=False, **self._dht_kwargs(grpo_args))```

5. Save your changes and exit the editor:
Press `Ctrl+X` and press `Y` to exit.

6. Go to your screen
```screen -r swarm```

7. Restart the node
Press `Ctrl + C`.
Run command:
```./run_rl_swarm.sh```

## Fix Hivemind/Daemon Failed to start : increase timing 

```
sed -i -E 's/(startup_timeout: *float *= *)[0-9.]+/\1120/' $(python3 -c "import hivemind.p2p.p2p_daemon as m; print(m.__file__)")
```

### OOM errors on MacBook? (FOR MACBOOK ONLY)

Try this (experimental) fix to increase memory:

```bash
export PYTORCH_MPS_HIGH_WATERMARK_RATIO=0.0 && ./run_rl_swarm.sh
```


### How to upgrade the node as per new changes in the official repository (Do only If your node is already running if you are new or stopped your node it's fine because script already points to the original repository)

Open the rl-swarm directory:

```bash
cd $HOME/rl-swarm
```

Pull the changes from original repository:
```bash
git reset --hard HEAD
git pull
```

**Note:** If the above command response is already up to date then there is no need to go further. If not then follow below.


Open gensyn screen:

```bash
screen -r gensyn
```
Stop the already running node:
Press Ctrl+c

Restart the node:
```bash
./run_rl_swarm.sh
```


**Note:** Press `Ctrl+A` then `D` to detach from the screen session. 

FOR AGAIN RECONNECTING TO THE SCREEN USE 

```bash
screen -r gensyn
```

IF YOU HAVE ANY DOUBT LET ME KNOW ON TWITTER 
https://x.com/kuberfreak

IF FACING ANY ISSUES DM ME WITH NO FEAR...

