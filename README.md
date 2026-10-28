**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)

# Dynamo Spark releases

Dynamo Spark lets a Windows PC earn while nobody is using it. This is where its installer is published.

## Install

1. Download the Spark installer from **[the latest release](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest)**: the file `spark-ui_windows_x64_v….exe`.
2. Run it and follow the screens.

## Internet cafe with a diskless image (CCBoot and similar)

Spark is installed **once, into the shared image**; every PC that boots the image then runs it.

### Requirements

- [ ] **A diskless system.** The cafe's PCs boot one shared Windows image from a server (diskless boot software such as **CCBoot**). Anything changed on an ordinary PC is lost at its next restart, so every change is made **once, on the image**, on a PC booted in the boot software's image edit mode (in CCBoot: **Super Client**), with write protection off. Then the image is saved and every PC gets it at its next boot. This page calls that PC the **image PC**.
- [ ] **Internet** on the image PC, the whole time.
- [ ] **A 1-year venue token** from the venue's **own** Portal account (not the account of whoever is helping): every PC that boots the image joins the account the token was made in. The setup can also fetch it for you (**Connect through the Portal**).
- [ ] **Access to the register PC**, for the [CafePlus settings](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md).
- [ ] **Virtualization on** in the BIOS (SVM / VT-x), on every PC.
- [ ] For GPU PCs, **the NVIDIA driver comes from the diskless system**; do not install a driver into the image yourself.

### Setup

1. **Register PC:** set the two CafePlus boxes once: [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md).
2. **Image PC:** boot it in image edit mode (CCBoot: Super Client), protection off, and sign in to Windows.
3. Download and run the Spark installer (above). Leave **Launch Dynamo** on at the end.
4. On Spark's first setup step, click the small link **Setting up a diskless venue image (CCBoot...)? Click here**, read the page, click **Continue venue setup** and approve the one administrator prompt.
5. Follow the wizard. A new image shows **Install**; an image that already has Spark opens on **Update**. A restart, if asked, is safe: the window comes back where it was.
6. **The token**, at **Connect to Kinesis**: click **Connect through the Portal** and sign in with the venue's own account, or click **Paste a token instead**. To get a token in the Portal: **Provide** > **Fleet** > **Add machines** > **Windows / WSL** > the small link **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token** > **Create venue token** > the copy button.
   After imaging, never press **Regenerate** on that page: PCs that have not joined yet could no longer join.
7. **Ready to save:** click **Prepare this PC for saving the image** and answer **Yes**.
8. Within 1 hour, without using the PC for anything else: shut it down, save the image in the boot software (CCBoot: the way you always save it), and turn write protection back on.

To update the image later (new Spark or new token): do steps 2 and 3 again; Spark opens on **Update this venue image** by itself. Every PC keeps its place in the Portal.

### After saving: check one PC

Boot one cafe PC from the saved image. Within a few minutes it shows in the Portal under **Provide** > **Fleet**. Rent it from the register: Spark stops within about 20 seconds; lock it: Spark works again within about a minute.

If it does not show up, open **Command Prompt** as administrator on that PC and run:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

`venue doctor` lists each stage of the PC's boot; the first line that is not fine is where it is stuck. Send both outputs and the PC's name to Kinesis.

## Help

**support@kinesis.network**. Tell us the venue and the PC's name: Kinesis sees the setup in its own logs.

Another cafe software than CafePlus? Contact us first.

> The old "Kinesis Spark diskless venue kit" (the PowerShell line and `venue-setup.ps1`) is retired; its releases are no longer used. Use the installer above.
