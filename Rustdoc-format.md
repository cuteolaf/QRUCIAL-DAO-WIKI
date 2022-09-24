## Generate rustdoc for QDAO
Copy relevant the command for generating the documents you are looking for.
```
cd QRUCIAL-DAO/qdao-node && cargo doc                   # Generate docs for the whole project, including dependencies (takes a long time!)
cd QRUCIAL-DAO/qdao-node/exo-pallet && cargo doc        # Generate docs for exo pallet
cd QRUCIAL-DAO/qdao-node/audit-pallet && cargo doc      # Generate docs for audit pallet
...                                                     # ...and so on, just cd to the right folder and you can generate the docs.
```

You can find the results under "_target/docs/_".