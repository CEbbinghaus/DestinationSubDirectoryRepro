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

## This repository

This reproduction uses a slightly more real-world inspired usecase. In particular collecting a collection of projects under a single output directory.

`Thing.A` / `Thing.B` / `Thing.C` are all "related" projects that should be collected together. While here they are all class libraries in the real world they are more likely executables that we want to ship within our software.

Things is an empty project
