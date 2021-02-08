# Template

This is template project to allow fast and simple C++ project creation.

## Libraries

| Name | License | Version |
|------|---------|---------|
| ... | `MIT` / `GPLv3` | branch: `master` |

All libraries are used as `static library` to maximize optimization and limit problems with deployment and versions.

## Testing

- Set `BUILD_TESTING` CMake variable to `ON` (`-DBUILD_TESTING=ON`).
- Run `ctest` in build directory or use CLion and select `All CTest` as a run target.

Executable of tests have prefix `t_` (test `abc` would be executable `t_abc`).
After creating new test, add it to [`tests/CMakeLists.txt`](tests/CMakeLists.txt) as `add_subdirectory(abc)` (where `abc` is name of your test).
