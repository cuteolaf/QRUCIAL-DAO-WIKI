# Running your QDAO node (dev release)

## Minimum system requirements

```OS: Linux
CPU: 64-bit, 2+ cores (eg. from AMD Ryzen 3 and Intel i3)
RAM: 8GB RAM, DDR3-1333
Storage: 64GB+ 
GPU: Not needed.
Environment: Non-root user.
```


## Prepare and start the node

We have prepared "node-setup.sh" to automate building a QDAO node. Right now, this script will deploy a local dev node on the machine you are running it on. Execute the following command to start:

```wget https://raw.githubusercontent.com/Qrucial/QRUCIAL-DAO/main/node-setup.sh && bash node-setup.sh```

## Check if the node is running
```
tmux -ls
ps a|grep qdao
```
You should see a similar output:
```
qdao-exosysd: 1 windows (created Tue Aug 30 07:35:40 2022)
qdao-node: 1 windows (created Tue Aug 30 07:35:30 2022)

  52023 pts/1    Ssl+   3:55 ./qdao-node/target/debug/qdao-node --dev
  52139 pts/4    Ssl+   2:47 ./exosysd/target/debug/qdao-exosysd
  52702 pts/3    S+     0:00 grep qdao
```
You can attach to the tmux session using the following commands:
```
tmux a -t qdao-node
tmux a -t qdao-node
```

## How to stop the node
```killall qdao-node
killall qdao-exosysd
```

## Using the nodes, testing and development

You can move on by following the [Development and testing guide](https://github.com/Qrucial/QRUCIAL-DAO/wiki/Development-and-testing-guide)