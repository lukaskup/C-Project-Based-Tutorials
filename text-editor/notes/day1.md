# C Learning Notes - First Hour

## The Basics

**Function prototypes** - Use `int main(void)` not `int main()`. Empty parentheses means "any arguments" in old C style, `void` explicitly means "no arguments".

**Return codes** - `return 0` means success, non-zero means error. Unix convention.

## File Descriptors

A file descriptor is just an integer the kernel gives you to represent an open file/stream/connection.

Default ones always open:

- `0` (STDIN_FILENO) - stdin
- `1` - stdout
- `2` - stderr

## Pointers Basics

- `&c` - "address of c" - gives you where the variable lives in memory
- `*ptr` - "dereference" - follows an address and gets the value there

They're opposites.

## read() Function

```c
read(STDIN_FILENO, &c, 1)
```

- First arg: file descriptor (where to read from)
- Second arg: address of buffer (where to put the data)
- Third arg: how many bytes to read

Returns `ssize_t`:

- Number of bytes read on success
- `0` on EOF
- `-1` on error

## Terminal Control (termios)

**Naming:** `tc` = Terminal Control (tcgetattr, tcsetattr, etc.)

**TCSAFLUSH** - when applying terminal changes:

- Wait for pending output to be written
- Discard any unread input
- Then apply changes

Gives you a clean slate when switching modes.

## Terminal Flags

```c
raw.c_lflag &= ~(ECHO | ICANON | ISIG);
```

- `ECHO` - show typed characters
- `ICANON` - canonical mode (line-by-line input with backspace, etc.)
- `ISIG` - process signals (Ctrl+C = SIGINT, Ctrl+Z = SIGTSTP)

The `&= ~()` pattern turns these flags OFF.

## Process States

**Terminated** - dead, gone, memory freed, finished forever.

**Suspended** - paused, frozen, still in memory, can be resumed with `fg` or `bg`.

## Misc

- `iscntrl(c)` - checks if character is a control character
- `atexit(function)` - registers a function to run when program exits
- `ssize_t` - signed size type, allows `-1` for errors (unlike `size_t` which is unsigned)

---

_Next session: continue with the kilo text editor tutorial_
