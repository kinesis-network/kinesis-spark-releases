**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)

# Earn with your internet cafe's PCs

Kinesis rents out the graphics cards of your cafe PCs to people who need computing power, but only while no customer is using them. You earn for those hours. The moment a customer sits down, it stops and the PC is all theirs. The program that does this on each PC is called **Spark**.

Curious what your PCs could earn? Try the [GPU earnings calculator](https://kinesis.network/grid/join/gpu-calculator).

This guide sets it up for your whole cafe at once. You do it one time.

## Before you start

* Set aside about 30 minutes. Make sure the PC you work on has internet.
* Make sure you can open, edit and save your Windows image and send it to the PCs in your system.
* Make sure your PCs start from a server with one shared Windows image (a diskless system such as CCBoot). If your PCs have their own disks, just run the installer from step 4 on each PC and click **Set up this PC** under **A PC with its own disk**.
* Make sure your cashier PC runs supported cafe software: see the [list below](#supported-cafe-software).
* If your diskless system is not LingWo/NetKafem CCBoot (for example the original CCBoot), make sure the image already carries a working NVIDIA driver: Spark uses the image's driver and never installs one there. A PC whose graphics card that driver does not cover works without its GPU, and Kinesis sees it as `DRV_IMAGE_NO_DRIVER`.

## Step by step

1. **Create your Kinesis account.** Go to [portal.kinesis.network/signup](https://portal.kinesis.network/signup) and sign up with the cafe's own email. This website is your Kinesis account: your PCs and earnings show there. In the menu, click **Provide**, read the terms, tick the box and click **Agree & start providing**.
2. **Set up your cafe software.** Follow the page for your software in the [list below](#supported-cafe-software). With CafePlus you add two lines on the cashier PC, so it tells Spark when a customer starts and leaves. With PanCafe there is nothing to add: Spark sees PanCafe's lock screen on each PC by itself (being confirmed at the first cafes).
3. **Open the image for editing.** Start one PC in your diskless system's edit mode, with write protection off (CCBoot: start it as **Super Client**; other diskless systems have the same thing under another name). Sign in to Windows. Everything below happens on this PC.
4. **Download and run the installer.** Open the [latest release](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest), download the file `spark-ui_windows_x64_v….exe` and run it. (The same file is in your Kinesis account: **Provide** > **Fleet** > **Add machines** > **Windows / WSL** > **Download Dynamo Spark**.) Leave **Launch Dynamo** ticked at the end.
   You should see: the Spark window.
5. **Choose the diskless setup.** Spark's first screen asks which kind of PC this is: click **Set up a diskless PC** under **A diskless PC (CCBoot)**. (With CCBoot, Spark may open this page by itself.) Read the page, click **Continue venue setup** and say yes to the Windows prompt. Then click each button as it appears. If Windows asks to restart, that's fine: Spark comes back where it was.
   You should see: the cafe setup, marked **Install**. (If this image already has Spark, it shows **Update** instead.)
6. **Connect your account.** At **Connect to Kinesis**, click **Connect through the Portal**. Your Kinesis account opens in the browser: sign in and click **Authorize for this image**.
   You should see: **Connected** in Spark. Every PC that starts from this image will appear in this account.
   <details><summary>Can't sign in on this PC?</summary>

   Use a code instead. On any other computer, sign in to your Kinesis account and go to **Provide** > **Fleet** > **Add machines** > **Windows / WSL**. Click the small link **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token**, then **Create venue token**, then the copy button. Get the code to this PC. In Spark, paste it into the **Or paste a token** field under the Portal button, turn on the confirmation switch and click **Continue with this token**. The code works for one year.

   Make the code in **your own** account, not the account of someone helping you: every PC joins the account the code came from, and that account gets the earnings. After saving the image, never press **Regenerate** on that page: PCs that have not joined yet could no longer join.
   </details>
7. **Finish and save.** Go through the last screens. On the last one, click **Finish**. When Spark says **Setup is finished**, save the image in your diskless system the way you always do (CCBoot: save this PC's image as Super Client), and turn write protection back on.
8. **Check that it works.** Start one cafe PC as usual. Within a few minutes, it appears in your Kinesis account under **Provide** > **Fleet**. Open a customer session on it from the cashier PC: Spark stops within about 20 seconds. Lock it again: Spark goes back to work within about a minute.

Done. To update later, repeat steps 3 and 4: Spark opens on **Update this venue image** by itself, and every PC keeps its place in your account.

## Supported cafe software

<!-- Maintainers: to support new cafe software, add one row here (and the same row in README.tr.md),
     plus hooks/<software>.md and hooks/<software>.tr.md written like hooks/cafeplus.md.
     Nothing else in this README needs to change. -->

| Cafe software | Setup page |
|---|---|
| AKINSOFT CafePlus | [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) · [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md) |
| PanCafe Pro | [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.md) · [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.tr.md) |

Using different cafe software? Email **support@kinesis.network** and we'll add it.

## Day to day and image updates

* Game and Windows updates in an edit (Super Client) boot need nothing from Spark: while you edit the image, Spark does not work and does not register a PC.
* After a Spark update or a new NVIDIA driver in the image: in the edit boot, open the Spark window, press **Finish**, then save the image.
* **Never add Spark to your cafe software's banned-program or "programs to terminate" list**: the cafe software would stop Spark on every PC.

## If something goes wrong

<details><summary>A PC does not show up in your account</summary>

On that PC, open Start, type `cmd`, right-click **Command Prompt** and choose **Run as administrator**. Run these two lines:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

Send what they show, and the PC's name, to **support@kinesis.network**.
</details>
