# DuckDB Rust extension template
This is an experimental template for Rust based extensions based on the C Extension API of DuckDB.

## Cloning

Clone the repo with submodules

```shell
git clone --recurse-submodules <repo>
```

## Venv

This template assumes you are using a venv called `venv`. If you are using uv, 

```shell
uv venv venv
source venv/bin/activate
```

## Building
Building is simple just ensure Rust is installed, then run
```shell
make debug
```
or
```shell
make release
```

## Testing
This extension uses the DuckDB Python client. This client ships with a test runner.

### Step 1
- creates a local python3 venv
- installs DuckDB into the venv
- installs the test extension dependencies by running `install_test_dependencies.py`
```sh
make install_test_dependencies
```
Alternatively, a specific duckdb version can be chosen
```shell
DUCKDB_TEST_VERSION=v1.0.0 make install_test_dependencies
```

### Step 2
Run the tests!

```shell
make test_debug
```
or 
```shell
make test_release
```

## Debugging

Start duckdb, allowing unsigned extensions

```shell
duckdb -unsigned
```

Load the extension

```shell
load './build/release/extension/rusty_quack/rusty_quack.duckdb_extension';
from rusty_quack('Hello');
```

### Known issues
This is a bit of a footgun, but the extensions produced by this template may (or may not) be broken on windows on python3.11 
with the following error on extension load:
```shell
IO Error: Extension '<name>.duckdb_extension' could not be loaded: The specified module could not be found
```
This was resolved by using python 3.12