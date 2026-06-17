# Building wolfssh on Linux / macOS

## Prerequisites

wolfssh requires wolfSSL built with SSH support. Build and install wolfSSL first:

```bash
cd wolfssl
./autogen.sh    # requires autoconf, automake, libtool
./configure --enable-ssh
make
sudo make install
```

## Autotools (only supported build system)

There is no top-level CMake for wolfssh. Autotools is the build system on Linux/macOS.

From a git checkout (not a release tarball), generate the configure script first:

```bash
./autogen.sh    # requires autoconf, automake, libtool
```

Then build and test:

```bash
./configure
make
make check      # runs all tests — do this before submitting any PR
sudo make install
```

## Common configure flags

| Flag | Purpose |
|------|---------|
| `--enable-all` | Enable all wolfssh features |
| `--enable-sftp` | SFTP subsystem support |
| `--enable-scp` | SCP (secure copy) support |
| `--enable-shell` | Shell (echoserver) support |
| `--enable-keyboard-interactive` | Keyboard-interactive authentication |
| `--enable-fwd` | TCP/IP port forwarding support |
| `--enable-agent` | ssh-agent support |
| `--enable-debug` | Debug symbols and wolfSSH debug logging |

The full list is in `./configure --help`.

## Running Tests

```bash
make check    # full test suite
```

`make check` runs the unit tests and integration tests under `tests/`. The SFTP and SCP tests require `--enable-sftp` and `--enable-scp` respectively at configure time.

## Typical development build

```bash
./configure --enable-all
make
make check
```
