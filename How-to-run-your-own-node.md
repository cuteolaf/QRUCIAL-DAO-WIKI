# Running your QDAO node (dev release)

## Minimum system requirements for dev release

```OS: Linux
CPU: 64-bit, 2+ cores (eg. from AMD Ryzen 3 and Intel i3)
RAM: 8GB RAM, DDR3-1333
Storage: 64GB+ 
GPU: Not needed.
Environment: Non-root user.
```

## Running test node using docker (limited performance)

You only need docker to be installed. Everything else will be running inside the container.

```
mkdir QDAO && cd QDAO && mkdir scripts
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/Qrucial/QRUCIAL-DAO/milestone1/docker/files/dockerfile
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/Qrucial/QRUCIAL-DAO/milestone1/docker/files/scripts/supervisord.conf -o scripts/supervisord.conf
docker build -t "qdao:dockerfile" . 
```


## Prepare and start the full node

On Debian based systems, eg. Ubuntu, you need to have the following installed:

```
sudo apt update
sudo apt-get install tmux git curl python3 docker-ce
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install keccak256-cli
```

We have prepared "node-setup.sh" to automate building a QDAO node. Right now, this script will deploy a local dev node on the machine you are running it on. Execute the following command to start:

```
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/Qrucial/QRUCIAL-DAO/main/node-setup.sh | bash
```

## Check if the node is running
```
tmux ls && echo "" && ps a|egrep "qdao|lar.py"
```
You should see a similar output:
```
qdao-api: 1 windows (created Wed Aug 31 23:24:47 2022)
qdao-exosysd: 1 windows (created Wed Aug 31 23:24:47 2022)
qdao-node: 1 windows (created Wed Aug 31 23:24:42 2022)

  63874 pts/3    Ssl+   0:52 ./qdao-node/target/debug/qdao-node --dev
  63966 pts/4    Ssl+   0:30 ./exosysd/target/debug/qdao-exosysd
  63969 pts/5    Ss+    0:00 python3 exotools/lar.py

```
You can attach to the tmux session using the following commands:
```
tmux a -t qdao-node
tmux a -t qdao-exosysd
tmux a -t qdao-api
```

## How to stop the node
```
killall qdao-node
killall qdao-exosysd
killall lar.py
```

## Using the nodes, testing and development

You can move on by following the [Development and testing guide](https://github.com/Qrucial/QRUCIAL-DAO/wiki/Development-and-testing-guide)