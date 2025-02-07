## Minimal DestinationSubDirectory repro

When using the `DestinationSubDirectory` I expected it to work recursively. This means that if you had **Project A** included under `A/` and **Project B** referencing A being included under `B/` I would expect the output of **Project C** (referencing B) to have the following directory structure:
```
C/bin 
- C.dll
- B/
-- B.dll
-- A/
--- A.dll
```

The actual result:
```
C/bin
- C.dll
- A.dll
- B/
-- B.dll
```
