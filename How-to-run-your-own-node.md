# Running your QDAO node (currently we have development releases)

## Minimum system requirements

```
OS: Linux
CPU: 64-bit, 2+ cores (eg. from AMD Ryzen 3 and Intel i3)
RAM: 8GB RAM, DDR3-1333
Storage: 64GB+ 
GPU: Not needed.
Environment: Non-root user.```

## Prepare and start the node

We have prepared "node-setup.sh" to automate building a QDAO node. Right now, this script will deploy a local dev node on the machine you are running it on. Execute the following command to start:

```wget https://raw.githubusercontent.com/Qrucial/QRUCIAL-DAO/main/node-setup.sh && bash node-setup.sh```

## Check if the node is running
```
tmux -ls
ps aux|grep qdao
```

## How to stop the node
```killall qdao-node
killall qdao-exosysd```