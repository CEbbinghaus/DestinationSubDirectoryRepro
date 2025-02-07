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

Things is an empty project that exists purely to pull in A & B & C. As such the desired resulting directory of `Consumer/bin` structure would be:
```
Consumer/bin
└───Debug
    └───net9.0
        │   Consumer.deps.json
        │   Consumer.dll
        │   Consumer.pdb
        │
        └───Things
            │   Things.dll
            │   Things.pdb
            │
            ├───A
            │       Thing.A.dll
            │       Thing.A.pdb
            │
            ├───B
            │       Thing.B.dll
            │       Thing.B.pdb
            │
            └───C
                    Thing.C.dll
                    Thing.C.pdb
```

Unfortunately this is not the case, And instead the directory structure looks as follows:
```
Consumer/bin
└───Debug
    └───net9.0
        │   Consumer.deps.json
        │   Consumer.dll
        │   Consumer.pdb
        │   Thing.A.dll
        │   Thing.A.pdb
        │   Thing.B.dll
        │   Thing.B.pdb
        │   Thing.C.dll
        │   Thing.C.pdb
        │
        └───Things
                Things.dll
                Things.pdb
```
