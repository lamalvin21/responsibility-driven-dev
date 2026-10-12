# responsibility-driven-dev

A minimal C++20 command-line project built with CMake.

## Build and run

```sh
cmake -S . -B build
cmake --build build
./build/responsibility-driven-dev
```

## Run tests

GoogleTest must be installed and discoverable by CMake.

```sh
ctest --test-dir build --output-on-failure
```

In VS Code, run **CMake: Build** or **Run: responsibility-driven-dev** from the
Tasks menu. The run task configures and builds the project before launching it.
Run **CTest: Run Tests** to build the project and execute its unit tests.