# Building wolfssh on Windows

wolfssh does not have a top-level CMake. Windows builds use the Visual Studio solution in `ide/winvs/`.

## Prerequisites

Build and install wolfSSL for Windows first. wolfSSL provides a Visual Studio solution and CMake support — see the wolfSSL documentation for Windows build instructions. wolfssh requires wolfSSL built with `WOLFSSH_SFTP` or equivalent SSH support defines enabled.

## Visual Studio via ide/winvs/

Open the solution file:

```
ide/winvs/wolfssh.sln
```

The solution includes projects for:

| Project | Description |
|---------|-------------|
| `wolfssh` | Core SSH library |
| `echoserver` | Echo server example |
| `client` | SSH client example |
| `wolfsshd` | SSH server application |
| `wolfsftp-client` | SFTP client example |
| `api-test` | API test suite |
| `unit-test` | Unit tests |
| `testsuite` | Integration test suite |

Build configurations available: Debug, Release, DLL Debug, DLL Release.

### wolfSSL path

The solution references wolfSSL headers and libraries. Set the wolfSSL include and library paths in the project properties to match your wolfSSL installation, or set the `WOLFSSL_ROOT` environment variable before opening the solution.

## Preprocessor defines

Features are controlled via preprocessor defines in the `.vcxproj` files. Key defines:

| Define | Purpose |
|--------|---------|
| `WOLFSSH_SFTP` | Enable SFTP subsystem |
| `WOLFSSH_SCP` | Enable SCP support |
| `WOLFSSL_USER_SETTINGS` | Use a `user_settings.h` for wolfSSL config |

Edit the project properties or add defines to `ide/winvs/user_settings.h` if present.

## Running tests

Build and run `api-test` and `unit-test` from the Visual Studio solution. The `testsuite` project runs integration tests.
