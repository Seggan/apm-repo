# apm-repo
Repository for the APM tool in the Automation Slimefun addon.

## Project structure

Example project structure:
```
hello/
├── 1.1.0/
│   ├── hello.metis
│   ├── libhello.metis
│   └── vinfo.json
├── 1.0.0/
│   ├── hello.metis
│   └── vinfo.json
└── versions.json
```

All projects must be in a folder with the same name as the project. Within that folder, there must be a `versions.json` file 
containing a JSON list of all the available versions of the project. For the example project above, it would look like this:
```json
["1.1.0", "1.0.0"]
```
The higher the version is, the closer it should be to the start of the list.

Each version should be in its corresponding folder. Each folder is required to have a `vinfo.json` file in it. The contents of
that file is a single JSON object. Here is an example for `hello 1.1.0`:
```json
{
  "bin": ["hello.metis"],
  "lib": ["libhello.metis"],
  "dependencies": {
    "sf-dos": "1.2"
  }
}
```
`bin` is a list of files that will be downloaded into the `/bin/` folder and will be available on PATH. `lib` is a list of files 
which the files in `bin` require access to and are downloaded to `/lib/<package>/` (e.x. `/lib/hello/`). `include`, while not 
shown in this example, would be a list of files that get downlaoded into `/include/`, and will be available for `import`.
`dependencies` is an object of pairs of the name of the dependency and a version selector. APM will determine the highest version
that meets the selector. For example, in the example, an `sf-dos` version of `1.2.9` will satisfy the dependency, but a version of
`1.3.4` will not.
