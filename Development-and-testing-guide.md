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

## Testing the auditor sign_up/onboarding workflow

A new user can obtain an auditor status by:

1. The user signs up by calling the `sign_up` extrinsic which involves locking a certain amount of tokens. Every user which is not already signed up can do this.
2. The `AuditorData` struct which is assigned to every user holds the auditor's `score`, which is a `Option<u32>` and set to `None` until the auditor is approved.
3. Every user which already has an auditor score which is larger then `MinimalApproverScore`, a configuralbe runtime constant, can approve new members.
4. As soon as an auditor received approvals from three different existing auditors, his or her `score` changes to `Some(InitialAuditorScore)`, where `InitialAuditorScore` is a configurable runtime constant.

At the current point of development, the onboarding/signup workflow of new auditors is primarily tested through extensive unit tests which are defined in: `./qdao-node/audit-pallet/src/tests.rs`. These tests cover all aspects of the described onboarding process and prove that our implemented business logic for the extrinsics behaves as expected.

For on-chain testing after compiling and running qdao-node and communicating with it through Substrate Frontend template, we need to start with an existing pre-defined set of auditors which are already capable of approving new auditors. These initial auditors and their initial scores are now provided through the genesis config of qdao-node. The users `Alice`, `Bob` and `Charlie` and `Dave` are capable of approving the sign-up of new auditors. To test this on chain with the runnning `qdao-node`, we suggest to call the extrinsics through the Substrate Frontend Template:

1. Try to approve `Ferdie` by `approve_auditor` through `Alice`. Call should fail, since `Ferdie` did not sign up.
2. `Ferdie` calls `sign_up` extrinsic. Should work.
3. Try to approve `Ferdie` by `approve_auditor` through `Alice`. Call should be succesful, since `Ferdie` has signed up now. Second call by `Alice` should fail, since every applicant can't receive two approvals by the same user.
4. Approval by `Bob` and `Charlie` should work.
5. Since now `Ferdie` obtained auditor status, further attempts to approve `Ferdie` should fail. Especially `Dave` will not be able to approve `Ferdie`, since `Ferdie` already received three approvals.
