# Requirements

Please get your system ready using the [Running your QDAO node (dev release)](https://github.com/Qrucial/QRUCIAL-DAO/wiki/How-to-run-your-own-node) guide.


# Testing Tools

[Substrate Frontend Template - you can access QDAO node through the template frontend](https://github.com/substrate-developer-hub/substrate-front-end-template)

[Polkadot JS](https://polkadot.js.org/apps/#/extrinsics) - Send signed extrinsics, test execution and auditor signup/challenges. List below.

```
        pub fn tool_exec_req
        pub fn tool_exec_cancel_invalid
        pub fn tool_exec_auto_report
        pub fn challenge_report

        pub fn sign_up
        pub fn update_profile
        pub fn cancel_account
        pub fn approve_auditor
        pub fn game_result
```

Generating keccak256 hash on linux for auditor pallet testing
```
$ cat exotestflipper.tar|keccak256
```

Convert URL from ASCII to HEX for auditor pallet testing
```
bindechexascii --a2h "https://qrucial.io/"
```
Online tool: https://www.asciitohex.com/
```
# Remove empty spaces in vim or sed
s/ //g
```