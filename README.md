**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)

# Kinesis Spark diskless venue kit

Installs Spark on an internet cafe's shared Windows image, so every PC that boots the image earns while no customer sits at it.

## Quick install: two things to do

1. On the **register PC**, set the hooks once: [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md).
2. On the **image PC**, in image edit mode: Windows key → type `powershell` → right-click **Windows PowerShell** → **Run as administrator** → **Yes**; paste this line into the blue window that opens, press Enter and follow the screen:

   ```
   powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol='Tls12'; iwr https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -UseBasicParsing -OutFile ([IO.Path]::GetTempPath()+'venue-setup.ps1'); & ([IO.Path]::GetTempPath()+'venue-setup.ps1')"
   ```

That is all. The rest of this page is the same work, step by step.

## Requirements

- [ ] **A diskless system.** The cafe's PCs boot one shared Windows image from a server (diskless boot software such as **CCBoot**; similar: other diskless / image systems and freeze tools). Anything changed on an ordinary PC is lost at its next restart. So every change is made **once, on the image**, in the boot software's image edit mode (in CCBoot this is called **Super Client**); then the image is saved and every PC gets it at its next boot. This guide calls the PC in that mode the **image PC**.
- [ ] **Internet** on the image PC, the whole time.
- [ ] **A token**: a **"1 year (venue image)"** token from the venue's **own** Portal account. Kinesis marks that account as a venue; ask first.
  In the Portal: **Provide** > **Fleet** > **Add machines** > **Home or office** > validity **1 year (venue image)** > the copy button.
  A 24-hour token is for a test only: PCs that first boot the image a day later cannot join. After imaging, never press **Regenerate** on that page.
- [ ] **Access to the register PC** (for the CafePlus settings).
- [ ] **Virtualization on** in the BIOS (SVM / VT-x), on every PC.
- [ ] For GPU PCs, **the NVIDIA driver comes from the diskless system**; do not install a driver into the image yourself.

<!-- TODO(owner): add screenshots when available: images/portal-token.png (the token in the Portal), images/admin-powershell.png (Run as administrator), images/kit-done.png (the DONE screen). -->

## Install (first time)

1. **Set the hooks on the register PC.** Follow the [CafePlus page](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) (two boxes, once).

2. **Boot the image PC in image edit mode** (CCBoot: Super Client) and sign in to Windows.

3. **Open an administrator window.** Press the Windows key, type `powershell`, right-click **Windows PowerShell** > **Run as administrator** (Turkish Windows: **Yönetici olarak çalıştır**), click **Yes** (**Evet**).
   You should see: a blue window whose title starts with **Administrator:** (**Yönetici:**).

4. **Paste the line** (right-click in the window pastes) and press Enter:

   ```
   powershell -NoProfile -ExecutionPolicy Bypass -Command "[Net.ServicePointManager]::SecurityProtocol='Tls12'; iwr https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -UseBasicParsing -OutFile ([IO.Path]::GetTempPath()+'venue-setup.ps1'); & ([IO.Path]::GetTempPath()+'venue-setup.ps1')"
   ```

   You should see: `=== Kinesis Spark diskless venue kit 1.3.0 - INSTALL ===` and below it `Why: venue mode is not on on this PC yet.`

5. **When it asks for the token**, paste the token (or the whole command the Portal copied) and press Enter.
   You should see: `Using token 1b2c3d4e...` The kit then runs by itself; every line starts with `OK`, `CHECK` or `FAIL`.

6. **If it says to restart** (`RESTART NEEDED`): **Start** > **Power** > **Restart** (not Shut down), staying in edit mode. Then repeat steps 3 and 4: the same line continues where it stopped.

7. **The register question** (`When the two boxes are saved on the register PC, press Enter here`): if you did step 1, press Enter.
   If it asks whether to start CafePlus again (`...start it again from here? [y/N]` or `...Start it now? [y/N]`), answer `n`: this PC takes the boxes at its next boot anyway.
   Then `Test a lock and a rent now?` can be answered `n`; the real test is step 10.

8. **Prepare the image.** When the kit says `Type PREPARE and press Enter to prepare the image`, type `PREPARE` and press Enter. This is the step of no return: it seals the image.
   You should see: `OK prepared.`, `OK deleted the kit: ...` and the green `=== DONE. SAVE THE IMAGE now (within 12 hours) ...`

9. **Save the image.** Within 12 hours, without using the PC for anything else, save the image in the boot software (CCBoot: when you disable Super Client, choose to save the changes to the image) and turn the write protection back on.

10. **Check one PC.** Boot one PC from the image. Within a few minutes it shows in the Portal under **Provide** > **Fleet**. Rent it from the register: Spark stops within about 20 seconds; lock it: Spark works again within about a minute.
    To rent it out: **Fleet** > **Set up** > notice **0 h** > **List as spot capacity**.

## Update the image (new Spark, new engine or new token)

Do steps 2 to 4 above: **the same line**. The kit sees that venue mode is on and updates.

- You should see: `=== ... UPDATE the image ===` and `Every PC keeps its node`.
- At the token question, paste a new token to change it, or just press Enter to keep the current one.
- The kit unseals the image, installs a newer Spark if the feed has one, moves the engine to the latest release, checks, and asks for `PREPARE`. Then save the image as in step 9.
- The PCs keep their nodes: no new entries appear in the Portal.

## If something goes wrong

The kit stops at the first problem and says what to fix on its `FAIL` line. Fix it and **paste the same line again**: it skips the finished steps.

| What you see | What to do |
|---|---|
| `This window is not running as administrator` | Close it; open it with **Run as administrator** as in step 3. |
| `CPU virtualization (SVM / VT-x) is OFF in the BIOS` | Turn on SVM (AMD) / Intel VT-x in the BIOS, then paste the line again. |
| `Cannot read the release feed from any source` or `Download failed` | Check this PC's internet (does github.com open in a browser?), then again. |
| `SHA-256 does NOT match the feed` or `Signature NOT accepted` | The download was deleted; try once more. If it repeats, stop and tell Kinesis this PC's name. |
| `RESTART NEEDED` | Start > Power > Restart, staying in edit mode; then the line again. |
| `Changes made before the restart were lost` | The PC was not in edit mode (write protection on). Turn edit mode on, then the line again. |
| `NOT FINISHED: ... is waiting (WAIT lines above)` | Do what each `WAIT` line says (usually a restart), then the line again. |
| `Note: no Spark line in ...script.cmd yet` | Not a stop; check the register's two boxes against the [CafePlus page](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md). The line appears after the PC has booted again and a rent or lock has happened. |
| `Go on without it? (y/N)` | This PC has no NVIDIA driver at all. If the GPU PCs get theirs from the diskless system, type `y`; if unsure, `n` and ask Kinesis. |
| Any other `FAIL` | Do what the line says. To repeat one step, use the `-Step <n>` command the kit prints. |

**When you ask for help**, tell Kinesis this PC's name (and the venue): Kinesis sees the setup in its own logs, which Spark uploads. Until the image is prepared, the kit also keeps a full log of its run on this PC, `C:\kinesis\venue-setup.log`; step 8 deletes it with the kit.

The screen language follows Windows. To continue in another language (the kit copies itself to `C:\kinesis`):

```
powershell -ExecutionPolicy Bypass -File C:\kinesis\venue-setup.ps1 -Lang tr
```

Spark's own check lines (`OK` / `FIXED` / `WARN` / `WAIT` / `FAIL`) are in English.

Another cafe software? Contact Kinesis.
