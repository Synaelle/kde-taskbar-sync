# kde-taskbar-sync

Keeps the pinned apps of every KDE Plasma 6 taskbar the same, on all panels and monitors. Pin, unpin or reorder on one taskbar and the others follow.

Needs Plasma 6, Python 3 and systemd.

## Install

Clone your main panel once per monitor (right-click the panel, Show Panel Configuration, Clone Panel), then run

```bash
git clone https://github.com/Synaelle/kde-taskbar-sync
cd kde-taskbar-sync
install -Dm755 plasma-pin-sync ~/.local/bin/plasma-pin-sync
install -Dm644 plasma-pin-sync.service ~/.config/systemd/user/plasma-pin-sync.service
systemctl --user daemon-reload
systemctl --user enable --now plasma-pin-sync.service
```

To update, `git pull` and run the two `install` lines again, then `systemctl --user restart plasma-pin-sync.service`.

## Uninstall

```bash
systemctl --user disable --now plasma-pin-sync.service
rm ~/.local/bin/plasma-pin-sync ~/.config/systemd/user/plasma-pin-sync.service
```

## Limits

Only pinned apps are synced, so other panel changes still need a new clone. At login the primary screen's taskbar wins, and an empty taskbar is never copied over the others. A reorder can make the other taskbars flicker once. Logs are in `journalctl --user -u plasma-pin-sync`.
