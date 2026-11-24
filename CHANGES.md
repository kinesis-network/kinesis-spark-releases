**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/CHANGES.tr.md)

# What's new in Spark

## 0.4.20

Everything since 0.4.18. (0.4.19 was a test build at one cafe and was never published.) Installed PCs update by
themselves; a cafe image gets it at its next image update (steps 3 and 4 of the [guide](README.md)).

### Cafes

- **A lost graphics card is handled, not guessed at.** When the NVIDIA driver on Windows says "GPU is lost"
  (nvidia-smi), or the card is lost on the Linux side, Spark stops offering the PC to Kinesis and restarts its own
  Linux once. On a cafe PC, Windows can also be restarted for it, but only when nobody is at the PC (no customer
  session, Windows locked or nobody signed in, no recent keyboard or mouse), after a 30-second warning that any key
  or mouse movement cancels, and only where Kinesis switches it on; it is off everywhere for now.
  Spark offers the PC again by itself once the card is back.
- **The GPU freeze watch is gone.** It judged freezes from power readings and could call a finished job a freeze. Spark
  now only records what the card reports, so the false "GPU frozen" and "GPU recovered" warnings stop.
- **Original CCBoot and PanCafe Pro.** Supported since 0.4.17, now faster: Spark now notices PanCafe's lock screen as
  Windows shows or hides it, instead of at its next 2-second check.
- **The boot type is read right away.** With the original CCBoot, Spark now reads at once whether a PC started as a
  customer PC or in edit (Super Client) mode. When CCBoot's log says which, customer PCs start working straight
  after boot, without the 2.5-minute wait.
- **No surprise new PCs in your account.** Setting up an image that has never had Spark makes every PC of the cafe a
  new node, so Spark now asks first: **Continue: make every PC a new node**. An image that already has Spark keeps its
  PCs, as before.
- **Fewer warnings.** PanCafe's two optional lines are no longer reported as missing; a PC's status reaches Kinesis even when one field in it is unusual, instead of being refused whole.
- **CafePlus menu path.** The setup screen and guide now point to **Ayarlar** > **Client Ayarları** >
  **Açma Kapama Scripti**.
- **The game pause never applies at a cafe PC** (the cafe software already says when a customer is there).

### Home PCs

- **Dashboard tiles show real figures**: processor, memory and graphics card, each on one line, with the reason
  shown when a figure cannot be read.
- **Checks before the administrator prompt.** Setup checks the PC first (graphics card, processor, memory, free disk space, virtualization) and
  says what Spark sends to Kinesis before you agree. An older processor (no AVX2) gets a note, not a refusal.
- **Windows 10: apps stay off your home network.** Kinesis work on Windows 10 runs only while that guard is
  confirmed in place.
- **Sleep and shutdown.** Spark pauses its work before the PC sleeps or shuts down.
- **Pause while you game (optional, off by default).** Spark can pause while another program uses the graphics card.
- **A required update never pops up over a game.**

### Everyone

- **The app is called Spark everywhere**: Installed apps, shortcuts, the Start menu, the tray (startup entry
  **Spark Notification Area**) and the setup window.
- **Signed code.** The files Spark installs are signed by Kinesis Network Inc., so Windows' Smart App Control lets
  them run. Windows may still say "Windows protected your PC" for a new release: click **More info**, check the
  publisher, then **Run anyway**.
