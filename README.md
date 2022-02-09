## Overview

This is a modification of the [Stockfish](https://stockfishchess.org) engine designed to generate a `dylib` (dynamic library) file.  The generated library provides an interface to interact with the engine.

## Files

This distribution consists of the following files:

  * [Readme.md](https://github.com/daniilbaranov/Stockfish11ToDylibConverter/blob/main/README.md), the file you are currently reading.

  * [License.txt](https://github.com/daniilbaranov/Stockfish11ToDylibConverter/blob/main/License.txt), a text file containing the GNU General Public License version 3.
  * [src](https://github.com/daniilbaranov/Stockfish11ToDylibConverter/tree/main/src), a subdirectory containing the full modified source code, including a Makefile
    that can be used to compile Stockfish `dylib` on macOS.
    
## Interface

The source engine is modified so that query responses are stored in a special vector `searchMsg`. The generated library provides the following set of functions for communicating with the engine:

* `void stockfish_initialize()` - initializes the engine
* `void stockfish_cmd(const char *cmd)` - sends command `cmd` to engine
* `const char* getSearchMessage()` - returns the first message from the beginning of the `searchMsg` and removes it from the vector
* `void clearAllMessages()` - deletes all messages from `searchMsg`

## Supported Architectures and Platforms for dylib (how to compile)
To compile `dylib` use `make build`. This command has 2 important parameters: `PLATFORM` and `ARCH`. Possible combinations of these parameters:
* `ARCH`=apple-silicon `PLATFORM`=ios - compiles `dylib` for iPhones and iPads with arm64 architecture
* `ARCH`=apple-silicon `PLATFORM`=simulator - compiles `dylib` for iPhones' and iPads' simulators running on Mac with arm64 architecture (M1)
* `ARCH`=x86_64 `PLATFORM`=simulator - compiles `dylib` for iPhones' and iPads' simulators running on Mac with x86-64 architecture (Intel)
* `ARCH`=apple-silicon `PLATFORM`=catalyst - compiles `dylib` for Mac Catalyst apps with arm64 architecture (M1)
* `ARCH`=x86_64 `PLATFORM`=catalyst - compiles `dylib` for iPhones and iPads with x86-64 architecture (Intel)
