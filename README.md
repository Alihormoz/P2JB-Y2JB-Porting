# p2jb-y2jb

**PlayStation 5 jailbreak (firmware 9.00 – 12.40)** 
a port of Gezine's [p2jb](https://github.com/Gezine/Luac0re) kernel exploit from the luac0re host to [Y2JB](https://github.com/Gezine/Y2JB).

> **Firmware supported:** works on **9.00 – 12.40** but its recommended on version **12.00 – 12.40**.

---

## Requirements

### PS5 setup (Y2JB)

This payload runs **inside** the Y2JB userland framework on the PS5
(the YouTube TV app modded to run arbitrary JavaScript). Before you
can send anything to the console, you must restore Gezine's Y2JB
system backup on the PS5 — see [Gezine/Y2JB](https://github.com/Gezine/Y2JB)
for the backup file and the restore your console. Without Y2JB
restored and the YouTube TV app launched, the PS5 has no listener
for the payload and nothing will happen.

### Hardware

- PlayStation 5 console running firmware **9.00 – 12.40** but its recommended on version **12.00 – 12.40**.
- A PC on the same LAN as the PS5).
  
### Software (on PC)

- The `payload_sender.py` delivery tool from (not recommended for beginners)
  [Gezine/Y2JB](https://github.com/Gezine/Y2JB) (not included here).
- NetCatGUI (most recommended for beginners) or any tool for delivering ELFs to the loader on `:9021`.

### Files needed

- `p2jb.js` — the jailbreak payload (only the file that is in this repo).

---

## How to use

### 1. Send the payload

just send the `payload_sender.py`

```sh
py payload_sender.py <ps5-ip> p2jb.js
```

The payload streams its log back to `payload_sender.py`'s console.

### 2. Wait about 50 minutes

The payload sender will stay silent for the whole leak no per-percentage progress is printed.
Do not interact with the PS5 while it runs.

### 3. Look for completion
after the 50 minutes check the last lines if you saw this in the last two line
```
[p2jb] stage_elfldr: elfldr launched - listening on :9021
[p2jb] === p2jb complete ===
```
it means that the jailbreak is succesfull.
At this point you have an in-memory jailbreak and a generic ELF loader.
Any ELF (for example [Kstuff](https://github.com/EchoStretch/kstuff-lite) by [EchoStretch](https://github.com/EchoStretch)) you send to `:9021` will run on the jailbroken PS5.

### Sending [Kstuff](https://github.com/EchoStretch/kstuff-lite) to `:9021`

to send [Kstuff](https://github.com/EchoStretch/kstuff-lite) to your ps5 you need to send the payload by the `payload_sender.py` in [Gezine/Y2JB](https://github.com/Gezine/Y2JB) project (not included here).

```sh
py payload_sender.py <ps5-ip> kstuff.elf
```

---

## Credits

- **`p2jb` kernel exploit (cr_ref overflow via `kqueueex`)** —
  Gezine / cheburek3000.
  [Luac0re](https://github.com/Gezine/Luac0re).
- **netcontrol kernel exploit (original)** — TheFlow.
  Source of the kqueue leak and UIO/IOV R/W primitives reused here.
- **Y2JB userland framework** — Gezine.
  [Y2JB](https://github.com/Gezine/Y2JB).
- **`kexp` post-jailbreak all-in-one shellcode** — ufm42
  ([kexp](https://github.com/ufm42/kexp)), merged into Y2JB 1.4.
- **`remote_lua_loader` p2jb port** — notmaj0r.
  Used as a secondary reference during the port.
- **lapse (Y2JB)** — referenced for the `gpu.js` debug-menu apply
  flow; not the exploit itself (lapse exploits AIO, not `kqueueex`).
- **Edigax** — help with the multi-core leak implementation, bringing
  the `cr_ref` leak down from ~2 hours to ~48 minutes.
- **Rviju** and **Dr.Yenyen** — help running test builds on real
  hardware during the close-KP investigation.
- **Claude (Anthropic)** — AI assistant used throughout the port.

---

## License

MIT — see [LICENSE](LICENSE).
