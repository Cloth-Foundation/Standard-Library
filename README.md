# Cloth Standard Library

The standard library is a Cloth project. All library source files live under
`cloth/`, with ordinary subfolders for each area of the library.

```text
build.toml
module.toml
cloth/
    Library.co
    collections/
```

For example, a future `List` implementation belongs in
`cloth/collections/List.co`. No collection types are implemented in this scaffold.

The module's source root is the repository root (`StandardLibrary = "."`), so
that future file will be imported as `using cloth.collections.List : List`.
The module identity is configuration metadata and is not an import prefix.
Ordinary subfolders do not need their own `module.toml` files. Importable
declarations must be `pub`.

## Build the scaffold

With Shuttle on your PATH, run from this repository:

```text
shuttle build --emit object
```

When checked out as the compiler's `Standard-Library/` submodule, run from the
compiler repository root:

```powershell
.\gradlew.bat :Shuttle:run --args="build --project Standard-Library --emit object"
```

Shuttle currently requires `project.entryPoint` even for object builds. The
configured `StandardLibrary.cloth.Library.main` selects `cloth/Library.co`;
`--emit object` does not require a `main` declaration. The root file is initially
empty apart from comments. Add imports there as library files are implemented
to include them in standalone validation: only reachable sources are compiled.
The output is `build/Cloth-Standard-Library.o`.

## Use library sources

Consumers add this repository root to their existing project's `[modules]`
table, using a path relative to their own `build.toml`:

```toml
[modules]
StandardLibrary = "../Standard-Library"
```

Keep the module identity `StandardLibrary` to match this repository's
`module.toml`. Sources then select public declarations through `cloth.*` paths.
The current toolchain compiles reachable library sources together with the
application; the object build does not provide a separately linked library or
package download support.
