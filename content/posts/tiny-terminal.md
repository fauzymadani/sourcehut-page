+++
date = '2026-02-10T10:02:21+07:00'
draft = true
title = 'Tiny Terminal'
+++

# tiny-terminal

A minimal terminal emulator for resource-constrained systems.

tiny-terminal is designed for old hardware where modern terminal emulators consume excessive memory. It uses X11 directly with no framework dependencies, targeting sub-50MB memory usage during operation.

This is a learning project. Expect bugs and missing features.

## Design

tiny-terminal implements only essential terminal functionality:

- PTY (pseudo-terminal) interface for shell communication
- X11 window with basic input handling
- Direct keyboard-to-PTY mapping
- Minimal ANSI escape sequence support

No GPU acceleration. No tabs. No configuration UI. Just a window that runs your shell.

The entire codebase is written in C with explicit focus on memory efficiency over features.

## Current Status

**Working:**
- PTY setup and shell spawning
- X11 window creation and event handling
- Keyboard input (printable characters, special keys, control sequences)
- Arrow keys and function key escape sequences

**Not Yet Implemented:**
- Output rendering (text display)
- ANSI color support
- Scrollback buffer
- Window resize handling
- Configuration file

## Building

Requirements:
- C99-compatible compiler
- X11 development libraries (`libX11`)
- POSIX system (Linux, *BSD)
```
make
```

To run:
```
./tiny-terminal
```

Note: Currently the window displays blank white because output rendering is not implemented. Input works but you won't see what you're typing.

## Architecture

The codebase is split into modules:

- `pty.c` - PTY allocation and shell process management
- `term.c` - X11 window and event loop
- `main.c` - Initialization and cleanup

Each module is designed to be independently testable and has minimal cross-dependencies.

## Memory Target

Goal: <50MB resident memory under normal shell usage.

Current measurement methodology:
```
ps aux | grep tiny-terminal
```

Binary size is kept minimal by avoiding external libraries where possible. The current stripped binary is approximately 26KB.

## Platform Support

Primary target: Linux with X11.

The code uses POSIX APIs and should be portable to *BSD systems with minimal changes. Wayland support is not planned.

## Contributing

This is primarily a personal learning project, but bug reports and patches are welcome.

The focus is on simplicity and resource efficiency. Feature requests that increase memory usage or add external dependencies will likely be rejected.

## License

See LICENSE file.