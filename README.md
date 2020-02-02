# dirtycow

## Table of PoCs
**Note**: if you experience crashes or locks take a look at [this](https://github.com/dirtycow/dirtycow.github.io/issues/25#issuecomment-255852675) fix.

| Link | Usage | Description | Family |
|:---:|:---:|:---:|:---:|
| [dirtyc0w.c](https://github.com/dirtycow/dirtycow.github.io/blob/master/dirtyc0w.c) | `./dirtyc0w file content` | Read-only write | /proc/self/mem |
| [cowroot.c](https://gist.github.com/rverton/e9d4ff65d703a9084e85fa9df083c679) | `./cowroot` | SUID-based root | /proc/self/mem |
| [dirtycow-mem.c](https://gist.github.com/scumjr/17d91f20f73157c722ba2aea702985d2) | `./dirtycow-mem` | libc-based root | /proc/self/mem |
| [pokemon.c](https://github.com/dirtycow/dirtycow.github.io/blob/master/pokemon.c) | `./d file content` | Read-only write | PTRACE_POKEDATA |
| [dirtycow.cr](https://github.com/xlucas/dirtycow.cr) | `dirtycow --target --string --offset` | Read-only write | /proc/self/mem |
| [dirtyc0w.c](https://github.com/timwr/CVE-2016-5195) | `./dirtycow file content` | Read-only write (Android) | /proc/self/mem |
| [dirtycow.rb](https://github.com/rapid7/metasploit-framework/pull/7476) | `use exploit/linux/local/dirtycow` and `run` | SUID-based root | /proc/self/mem |
| [0xdeadbeef.c](https://github.com/scumjr/dirtycow-vdso) | `./0xdeadbeef` | vDSO-based root | PTRACE_POKEDATA |
| [naughtyc0w.c](https://gist.github.com/mak/c36136ccdbebf5ecfefd80c0f2ed6747) | `./c0w suid` | SUID-based root | /proc/self/mem |
| [c0w.c](https://gist.github.com/KrE80r/42f8629577db95782d5e4f609f437a54) | `./c0w` | SUID-based root | PTRACE_POKEDATA|
| [dirty_pass[...].c](https://gist.github.com/ngaro/05e084ca638340723b309cd304be77b2) | `./dirty_passwd_adjust_cow` | /etc/passwd based root | /proc/self/mem |
| [mucow.c](https://gist.github.com/chriscz/f1aca56cf15cfb7793db0141c15718cd) | `./mucow destination < payload.exe` | Read-only write (multi page) | PTRACE_POKEDATA |
| [cowpy.c](https://github.com/nowsecure/dirtycow) | `r2pm -i dirtycow` | Read-only write (radare2) | /proc/self/mem |
| [dirtycow.fasm](https://github.com/sivizius/dirtycow.fasm) | `./main` | SUID-based root | /proc/self/mem |
| [dcow.cpp](https://github.com/gbonacini/CVE-2016-5195) | `./dcow` | /etc/passwd based root | /proc/self/mem |
| [dirtyc0w.go](https://github.com/mengzhuo/dirty-cow-golang/blob/master/dirtyc0w.go) | `go run dirtyc0w.go -f=file -c=content` | Read-only write | /proc/self/mem |
| [dirty.c](https://github.com/FireFart/dirtycow/blob/master/dirty.c) | `./dirty` | /etc/passwd based root | PTRACE_POKEDATA |

## List of PoCs
* https://github.com/dirtycow/dirtycow.github.io/blob/master/dirtyc0w.c
  * Allows user to write on files meant to be read only.
* https://gist.github.com/rverton/e9d4ff65d703a9084e85fa9df083c679
  * Gives the user root by overwriting `/usr/bin/passwd` or a suid binary.
* https://gist.github.com/scumjr/17d91f20f73157c722ba2aea702985d2
  * Gives the user root by patching libc's getuid call and invoking `su`.
* https://github.com/dirtycow/dirtycow.github.io/blob/master/pokemon.c
  * Allows user to write on files meant to be read only.
* https://github.com/xlucas/dirtycow.cr
  * Allows a user to write on files meant to be read only.
* https://github.com/timwr/CVE-2016-5195
  * Allows user to write on files meant to be read only (android).
* https://github.com/rapid7/metasploit-framework/pull/7476
  * Metasploit module based on the `cowroot` PoC.
* https://github.com/scumjr/dirtycow-vdso
  * Gives the user root by patching the vDSO escapes containers/SELinux doesn't need suid.
* https://gist.github.com/mak/c36136ccdbebf5ecfefd80c0f2ed6747
  * Gives the user root by injecting shellcode into a SUID file.
* https://gist.github.com/KrE80r/42f8629577db95782d5e4f609f437a54
  * Gives the user root by injecting shellcode into a SUID file using PTRACE_POKEDATA .
* https://gist.github.com/ngaro/05e084ca638340723b309cd304be77b2
  * Gives the user root by replacing /etc/passwd
* https://gist.github.com/chriscz/f1aca56cf15cfb7793db0141c15718cd
  * Allows user to write on files meant to be read only. Supports writing to multiple pages, not just the first
* https://github.com/nowsecure/dirtycow
  * Allows the user to write on files meant to be read only, implemented as a radare2 IO plugin.
* https://github.com/sivizius/dirtycow.fasm
  * Gives the user root by injecting shellcode into a SUID file. implemented for amd64 in flatassembly.
* https://github.com/gbonacini/CVE-2016-5195
  * Gives the user root by replacing /etc/passwd
* https://github.com/mengzhuo/dirty-cow-golang/blob/master/dirtyc0w.go
  * Allows user to write on files meant to be read only. implemented for arm32/x86/amd64 in Golang faster than c implement.
* https://github.com/FireFart/dirtycow/blob/master/dirty.c
  * Generates a new password hash on the fly and modifies /etc/passwd automatically. Just run and pwn.
