# NI Standard Error Codes

Every error emitted by the NetDust runtime (`ndr`) includes a code in the format below.

```
0x(Severity)(Category)(4 digit sequence number)
e.g., 0x9SYS0001
```

## Severity

| Code | Name | Meaning |
|---|---|---|
| `0x3` | Warning | Falling back to cache, optional feature failed |
| `0x5` | Error | Format/syntax error, missing config — only the script fails, the runtime stays safe |
| `0x7` | Critical | Network unreachable, required component failed to initialize |
| `0x9` | Fatal | Missing DLL, security violation, data corruption |

## Category

| Code | Name | Scope |
|---|---|---|
| `SYN` | Syntax | `.nd` syntax/parsing errors |
| `RUN` | Runtime | Reference/state errors during execution (room, blueprint, variable) |
| `MOD` | Module | `bring`/module loading |
| `FS` | File System | Script and output file I/O |
| `CLI` | Command Line | `ndr` command-line option errors |
| `SYS` | System | Internal/fatal system errors |
| `PKG` | Package | Package management (paxon, etc. — reserved) |
| `CFG` | Configuration | Config files (`.ndproject`, etc. — reserved) |
| `NET` | Network | Network connectivity (reserved) |
| `WRN` | Warning | Non-fatal diagnostics; the script continues |
| `SEC` | Security | Sandbox, read-only filesystem, and HTTP header policy violations |

---

## SYN — Syntax

| Code | Message |
|---|---|
| `0x5SYN0001` | file must begin with 'code start' |
| `0x5SYN0002` | Unexpected 'end;' outside of a room |
| `0x5SYN0003` | blueprint name is missing |
| `0x5SYN0004` | 'new' requires blueprint name and instance variable |
| `0x5SYN0005` | 'const' variable must be initialized at declaration |
| `0x5SYN0006` | 'try:'/'catch' block malformed (not closed, missing catch, or unexpected header) |
| `0x5SYN0007` | Executable statement is not allowed in global scope |
| `0x5SYN0008` | String literal missing double quotes or undefined identifier |
| `0x5SYN0009` | Invalid range syntax/content |
| `0x5SYN0010` | Block starting at line N is not closed with 'end;'. |
| `0x5SYN0011` | 'break' must end with ';'. / 'continue' must end with ';'. |
| `0x5SYN0012` | 'call' is missing a closing ')'. |
| `0x5SYN0013` | Invalid arithmetic expression (missing ')', unexpected token, unexpected end of expression, expression nested too deeply, ...): '...'. / Incomplete expression, missing operand: '...'. / Room 'X' must be called with 'call': write 'call X(...)'. |
| `0x5SYN0014` | 'const slot' is not supported yet — declare with 'slot' only (without 'const'). |
| `0x5SYN0015` | 'slot a' must be initialized with a bracket literal, e.g. 'slot a = [1, 2, 3];' |

## RUN — Runtime

| Code | Message |
|---|---|
| `0x5RUN0001` | Room not found |
| `0x5RUN0002` | Blueprint instance not found |
| `0x5RUN0003` | Field not found in instance |
| `0x5RUN0004` | Variable not defined |
| `0x5RUN0005` | Cannot reassign const variable |
| `0x5RUN0006` | Unknown command or syntax error |
| `0x5RUN0007` | Blueprint is not defined |
| `0x5RUN0008` | 'main' cannot be called directly |
| `0x7RUN0009` | Entry point 'room main():' is missing |
| `0x5RUN0010` | Maximum call depth (10000) exceeded in room 'X'. Possible infinite recursion. / Maximum nested call depth in expressions (1500) exceeded in room 'X'. Possible infinite recursion. |
| `0x5RUN0011` | Cannot do arithmetic on a non-numeric operand 'c' (value 'abc'): 'c * 2'. / Division by zero: '10 / z'. / Division by zero: '10 % z' (modulo). / Cannot do arithmetic, number out of range 'a': 'a * a'. |
| `0x5RUN0012` | Room 'X' expects N argument(s), but M given. |

## MOD — Module

| Code | Message |
|---|---|
| `0x5MOD0001` | Module is not loaded (missing `bring`) |
| `0x5MOD0002` | Module could not be found |
| `0x7MOD0003` | UI module not available in this build (`NETDUST_ENABLE_UI_MODULE` not defined) |
| `0x5MOD0004` | Library files cannot declare 'main' room |
| `0x5MOD0005` | Library file cannot be found |
| `0x5MOD0006` | No module handles this command |

## FS — File System

| Code | Message |
|---|---|
| `0x5FS0001` | Script file not found |
| `0x5FS0002` | Cannot open file |
| `0x5FS0003` | Cannot write output file |

## CLI — Command Line

| Code | Message |
|---|---|
| `0x5CLI0001` | Unknown option |
| `0x5CLI0002` | Missing argument (`--eval`, `--output`, `--benchmark`) |
| `0x5CLI0003` | Multiple files specified |
| `0x5CLI0004` | No input files |
| `0x5CLI0005` | Invalid integer argument (`--benchmark N`) |
| `0x5CLI0006` | `--init` requires a project name |
| `0x5CLI0007` | `--init` target directory already exists |

## SYS — System

| Code | Message |
|---|---|
| `0x9SYS0001` | Data corruption detected |

## WRN — Warning

Non-fatal. ndr prints these as `warning[code]:` and the script still finishes successfully.

| Code | Message |
|---|---|
| `0x3WRN0001` | cannot convert 'abc' to a number for numeric variable 'n' — defaulting to 0. |
| `0x3WRN0002` | array declared without `var` |
| `0x3WRN0003` | variable 'flag' declared without 'bool' — prefer 'bool flag = true;' |
| `0x3WRN0004` | 'slot[...]' literal is deprecated — write 'slot a = [1, 2, 3];' / 'var a = slot[...]' is deprecated — write 'slot a = [1, 2, 3];' / array 'a' declared with legacy 'slot[...]' literal — prefer 'slot a = [1, 2, 3];' |

## SEC — Security

These always stop the run (including when `runtime.stopOnFirstError` is disabled). The diagnostic label is `security policy violation`.

| Code | Message |
|---|---|
| `0x5SEC0001` | _native.fs_write: refused: write blocked by the read-only filesystem policy / _native.fs_read: refused: path is not inside the sandbox root: '...' / _native.http_set_header: refused: header value has a disallowed control character: '...' / _native.http_set_header: refused: this header is reserved: '...' |

---

Error codes may be added, removed, or changed in future releases.

Last checked against ndr 1.4.8 (Linux).
