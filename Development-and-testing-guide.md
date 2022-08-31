# Requirements

Please get your system ready using the [Running your QDAO node (dev release)](https://github.com/Qrucial/QRUCIAL-DAO/wiki/How-to-run-your-own-node) guide.


# Testing Tools

Substrate Frontend Template - you can access QDAO node through the template frontend

https://github.com/substrate-developer-hub/substrate-front-end-template

Polkadot JS - Send signed extrinsics, test execution and auditor signup/challenges

https://polkadot.js.org/apps/#/extrinsics

Generating keccak256 hash on linux
```
$ cat exotestflipper.tar|keccak256
```

Convert URL from ASCII to HEX
```
bindechexascii --a2h "https://qrucial.io/"
```
Online tool: https://www.asciitohex.com/
```
# Remove empty spaces in vim or sed
s/ //g
```