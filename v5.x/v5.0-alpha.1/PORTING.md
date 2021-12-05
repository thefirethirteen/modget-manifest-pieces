# Porting from v4 to v5.0-alpha

_Read through everything before porting a manifest!_

## Directory structure of v5.0-alpha.1

```
manifests/<first letter of the modid>/modid/
├──modid.yaml
├──publisher1/
│   ├── modid.publisher1.yaml
│   ├── 0.x/
│   │   ├── 0.3.x/
│   │   │   ├── 0.3.2.yaml
│   │   │   ├── 0.3.1.yaml
│   │   │   ├── 0.3.0.1.yaml
│   └── └── └── 0.3.0.yaml
├──publisher2/
│   ├── modid.publisher2.yaml
│   ├── 1.x/
│   │   ├── 1.0.x/
│   │   │   ├── 1.0.0.yaml
│   │   │   ├── 1.0.0.1.yaml
│   │   │   └── 1.0.1.yaml
│   │   ├── 1.1.x/
│   │   │   ├── 1.1.0.yaml
│   │   │   ├── 1.1.1.yaml
│   │   │   └── 1.1.2.yaml
│   ├── 2.x/
│   │   ├── 2.0.x/
│   │   │   ├── 2.0.0.yaml 
```
## Steps

1. Find the folder titled after the modid in `manifests/<publisher>/` (e. g. `fabricskyboxes` in `manifests/AmereBagatelle/fabricskyboxes` (Publisher is `AMereBagatelle`))
2. Move the folder titled after the modid to its corresponding `<first letter of the modid>` folder (Create it if it doesn't exist) (e. g. `fabricskyboxes` to `F`)
3. Move the contents of the folder titled after the modid to a new folder inside itself titled after the publisher (e. g. the contents of `fabricskyboxes` into `fabricskyboxes/AMereBagatelle/`)
4. In the folder titled after the modid, make a file `<modid>.yaml` (e. g. in `fabricskyboxes/` make `fabricskyboxes.yaml`)
5. Add this schema to the beginning of the file: `# yaml-language-server: $schema=../../../doc/validation-schemas/4.0/lookup-table.json` and add a newline after
6. ___CUT___ everything relating to your `<modid>` from the lookup table to your `<modid>.yaml` file.
7. Change the packageId(s) under packages to `<modid>.<publisher>` (e. g. `fabricskyboxes.AMereBagatelle`)

Example for 6 & 7:

```yaml
# yaml-language-server: $schema=../../../doc/validation-schemas/4.0/lookup-table.json

- id: fabricskyboxes
  alternativeNames:
    - fabric-skyboxes
  tags:
    - cosmetic
    - utility
    - miscellaneous
    - optifine-alternative
  packages:
    - packageId: fabricskyboxes.AMereBagatelle
      loaders:
        - fabric
```

8. Now, go to the `<modid>/<publisher>` folder.
9. Rename the `main.yaml` file to `<modid>.<publisher>.yaml` (e. g. `fabricskyboxes.AMereBagatelle.yaml`)
10. Check that the versions are in the correct subfolders.

Example for 10:

```
├──publisher2/
│   ├── modid.publisher2.yaml
│   ├── 1.x/                   // level x.x
│   │   ├── 1.0.x/             // level x.x.x
│   │   │   ├── 1.0.0.yaml
│   │   │   ├── 1.0.0.1.yaml   // no more levels after, everything in x.x.x
│   │   │   └── 1.0.1.yaml
```

Basically, you __must__ have two levels, x.x and x.x.x, and then no more levels.

## Steps if the mod is published by multiple people and one of them has been added already

1. SAME
2. SAME
3. Move the contents of the folder titled after the modid to a new folder inside itself titled after the publisher. DO NOT MOVE `<modid>.yaml` or any `<publisher>` folders (e. g. the contents of `fabricskyboxes` into `fabricskyboxes/AMereBagatelle/`, without moving the existing (hypothetical) `fabricskyboxes.yaml` or the existing (hypothetical) `thefirethirteen` folder)
4. IGNORE
5. IGNORE
6. IGNORE
7. IGNORE
8. SAME
9. SAME
10. SAME

To find all the publishers (we have added to the manifests) for a certain mod, just look at `manifests/<modid>/<modid>.yaml` under `packages`.


## That's it! Happy contributing!