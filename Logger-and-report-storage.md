## What is it?

HTTP API.

## What does it do?

1. The logger gets notified by ExoTool about audit results: success or fail and the details.

2. Stores the results in json format.

3. Sends extrinsics to ExoSys.

4. Provides the reports through HTTP service.

## How does it connect to other parts of the system?

- Input is coming from ExoTool
- Extrinsics are sent to ExoSys
- External users can request reports through the HTTP service.
