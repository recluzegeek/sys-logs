# sys-logs

Minimal, manual system tracking. No automation beyond package export. Everything here is intentional and human-written.

## structure

- machine → os → environment
- example: `thinkpad/arch/i3`

inside:

* `logs/` → time-based changes
* `cfg-*` → static config notes
* `pkg-*` → package lists

example layout:

```bash
└── thinkpad
    └── arch
        ├── i3
        │   ├── cfg-keybindings.md
        │   └── logs
        │       ├── 2026-04-01-net-nmapplet-service.md
        │       ├── 2026-04-01-sys-qemu-group.md
        │       ├── 2026-04-05-cfg-i3-changes.md
        │       └── log-template.md
        ├── pkg-aur.txt
        └── pkg-explicit.txt
```

## naming convention

- format: YYYY-MM-DD-<prefix>-<slug>.md
- examples:
  - 2026-04-05-sys-docker-group.md
  - 2026-04-05-pkg-paru.md
  - 2026-04-06-net-torsocks.md
  - 2026-04-06-usr-add-audio-group.md

## prefixes

* pkg → packages (install/remove)
* sys → system changes (services, kernel, groups)
* net → networking (dns, proxy, firewall)
* usr → users/groups/permissions
* cfg → config changes (i3, shell, etc)
* fix → bugfix / troubleshooting
* sec → security-related

## slug rules

* lowercase only
* use hyphens
* short and precise
* no filler words

- good:
  - sys-docker-group
  - pkg-paru
- bad:
  - installed-paru-today
  - random-change

## logging style

each file = one change
keep it short:
* what changed
* why
* command(s) used

example:
- what: added user to docker group
- why: run docker without sudo
- command: sudo usermod -aG docker msi

## package tracking

- explicit packages: `pacman -Qqe > pkg-explicit.txt`
- aur packages: `pacman -Qqm > pkg-aur.txt`
- full system (optional): `pacman -Qq > pkg-all.txt`

## pacman hook (auto-update pkg list)

- script: `~/.local/bin/export-pkgs`

```bash
#!/bin/bash
OUT="$HOME/sys-logs/thinkpad/arch/pkg-explicit.txt"
pacman -Qqe | sort > "$OUT"
```

- make executable: `chmod +x ~/.local/bin/export-pkgs`
- hook: `/etc/pacman.d/hooks/export-packages.hook`

[!IMPORTANT]
- change the home location in the hook
```bash
[Trigger]
Operation = Install
Operation = Remove
Type = Package
Target = *

[Action]
Description = Exporting explicit package list...
When = PostTransaction
Exec = /home/msi/.local/bin/export-pkgs
```

## rules
* one change = one file
* don’t mix unrelated changes
* don’t log junk
* prefer many small files over one big log
* configs go in dotfiles repo, not here

## goal

* rebuild system from scratch
* know what changed and why
* stay minimal and readable
