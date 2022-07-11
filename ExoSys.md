## Runtime ToDo

- rename pallet-dummy -> exosys 
- check **fee** of tool
- request extrinsic should give an id (**NFT**) to the actual tool run
- extrinsic to complete a request (success / failure)
- tool runs must be completed by a **deadline**
	- **commit** H(nonce || validator || result) on chain
	- **reveal** nonce in next block
- **slash** validators who did not commit result by deadline
- auditors can add **findings** later
- other auditors can **challenge** findings
	- at the end of challenge some reputation gets transferred based on **Élő-scoring**
	- a **random selection of 3 auditors** from the committee decides whether a challenge has succeeded
- any auditor in the top 10 percentile gets into **the committee**
