---
aliases: ["04 - Cisco IOS CLI"]
tags: ["ccna", "jeremys-it-lab", "fundamentals", "ios", "cli", "device-management"]
day: "04"
order: 4
type: lecture
status: studied
mastery: developing
topic_group: "Fundamentals"
source_video: "https://www.youtube.com/watch?v=IYbtai7Nu2g"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/7"
---

# Day 04 — Cisco IOS CLI

← [[01 - Lessons/03 - TCP-IP and OSI Models|Day 03 — TCP-IP and OSI Models]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/05 - Ethernet LAN Switching Part 1|Day 05 — Ethernet LAN Switching Part 1]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - `>` **User EXEC** → `enable` → `#` **Privileged EXEC** → `configure terminal` → `(config)#`.
> - `?` gets context help; `do` runs EXEC commands from config mode; `no` removes a command.
> - Running config = active now; startup config = used at boot.
> - Save with `copy running-config startup-config` (or `write memory`).
> - Console defaults: **9600, 8 data bits, no parity, 1 stop bit, no flow control**.

## Accessing Cisco IOS

Common console ports discussed in the course:
- USB console
- RJ-45 console

An RJ-45 console connection traditionally uses a **rollover cable**.

### Default console settings

```text
Speed:        9600 bps
Data bits:    8
Parity:       none
Stop bits:    1
Flow control: none
```

## IOS Command Modes

```mermaid
flowchart LR
    U[User EXEC\nRouter>] -- enable --> P[Privileged EXEC\nRouter#]
    P -- configure terminal --> G[Global Config\nRouter(config)#]
    G --> I[Interface Config\nRouter(config-if)#]
    G --> L[Line Config\nRouter(config-line)#]
    G -- end / Ctrl-Z --> P
    I -- exit --> G
```

| Mode | Prompt | Purpose |
|---|---|---|
| User EXEC | `Router>` | Basic monitoring/limited commands |
| Privileged EXEC | `Router#` | Full show/debug/config-file access |
| Global config | `Router(config)#` | Device-wide configuration |
| Interface config | `Router(config-if)#` | Interface-specific configuration |

## Help and Efficient CLI Use

```cisco
?
show ?
show ip ?
```

IOS accepts unique command abbreviations, but shared notes and production documentation should generally use recognizable full commands.

From a configuration submode, prefix a privileged EXEC command with `do`:

```cisco
do show running-config
```

Use `no` to remove/reverse a configured command:

```cisco
no shutdown
no description
no service password-encryption
```

## Device Identity and Privileged Access

```cisco
configure terminal
hostname R1
enable password cisco
enable secret <secret>
```

> [!warning] Course-era password behavior
> `enable password` is plaintext unless obfuscated. `enable secret` is preferred. In the course material, `service password-encryption` uses **Type 7** reversible obfuscation and `enable secret` is demonstrated as **Type 5 (MD5)**. Modern IOS/IOS XE can use newer secret formats.

Turn on password obfuscation for supported plaintext passwords:

```cisco
service password-encryption
```

Removing it does **not** decrypt passwords that are already stored in obfuscated form.

## Running vs Startup Configuration

- **running-config** — active configuration in RAM.
- **startup-config** — saved configuration used during boot.

View them:

```cisco
show running-config
show startup-config
```

Save changes:

```cisco
copy running-config startup-config
```

Also seen in IOS:

```cisco
write
write memory
```

> [!danger] Operational trap
> A configuration can work perfectly and still disappear after a reboot if it was never saved.

## Command Context Matters

When copying commands, always identify the IOS mode:

```text
R1#             privileged EXEC
R1(config)#     global configuration
R1(config-if)#  interface configuration
```

This is why the command index in [[04 - Reference/IOS Command Index|IOS Command Index]] includes a **mode** column.

## Active Recall

> [!question]- Check yourself
> 1. What command moves from user EXEC to privileged EXEC?
> 2. What is the difference between running-config and startup-config?
> 3. What does `do` do?
> 4. What does the `no` form of a command usually do?
> 5. Does disabling `service password-encryption` decrypt existing Type 7 entries?

> [!check]- Answers
> 1. `enable`.
> 2. Running-config is active now; startup-config is the saved boot configuration.
> 3. Runs an EXEC command from configuration mode.
> 4. Removes/reverses that configuration statement.
> 5. No.

## Related Notes

- [[02 - Labs/04.02 - Basic Device Security|Basic Device Security Lab]]
- [[04 - Reference/IOS Command Index|IOS Command Index]]
- [[09 - Switch Interfaces]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=IYbtai7Nu2g)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/7)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
