**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)

# Earn with your internet cafe's PCs

Kinesis rents out the graphics cards of your cafe PCs to people who need computing power, but only while no customer is using them. You earn for those hours. The moment a customer sits down, it stops and the PC is all theirs. The program that does this on each PC is called **Spark**.

Curious what your PCs could earn? Try the [GPU earnings calculator](https://kinesis.network/grid/join/gpu-calculator).

This guide sets it up for your whole cafe at once. You do it one time.

## Before you start

- **About 30 minutes**, and internet on the PC you work on.
- **Your PCs start from a server** (a "diskless" system such as CCBoot): the PCs have no Windows of their own; they all start one shared copy of Windows, called the **image**, from your server. If your PCs have their own disks, this guide is not for you: just download the installer from step 4 and run it on each PC.
- **Supported cafe software** on your cashier PC: see the [list below](#supported-cafe-software).

## Step by step

1. **Create your Kinesis account.** Go to [portal.kinesis.network/signup](https://portal.kinesis.network/signup) and sign up with the cafe's own email. This website is your Kinesis account: your PCs and earnings show there. In the menu, click **Provide**, read the terms, tick the box and click **Agree & start providing**.
2. **Set up your cafe software.** On the cashier PC, add two lines to your cafe software so it tells Spark when a customer starts and leaves. Follow the page for your software in the [list below](#supported-cafe-software).
3. **Open the image for editing.** Start one PC in your diskless system's edit mode, with write protection off (CCBoot: start it as **Super Client**; other diskless systems have the same thing under another name). Sign in to Windows. Everything below happens on this PC.
4. **Download and run the installer.** Open the [latest release](https://github.com/kinesis-network/kinesis-spark-releases/releases/latest), download the file `spark-ui_windows_x64_v….exe` and run it. (The same file is in your Kinesis account: **Provide** > **Fleet** > **Add machines** > **Windows / WSL** > **Download Dynamo Spark**.) Leave **Launch Dynamo** ticked at the end.
   You should see: the Spark window.
5. **Choose the cafe setup.** On Spark's first screen, click the small link **Setting up a diskless venue image (CCBoot...)? Click here**. Read the page, click **Continue venue setup** and say yes to the Windows prompt. Then click each button as it appears. If Windows asks to restart, that's fine: Spark comes back where it was.
   You should see: the cafe setup, marked **Install**. (If this image already has Spark, it shows **Update** instead.)
6. **Connect your account.** At **Connect to Kinesis**, click **Connect through the Portal**. Your Kinesis account opens in the browser: sign in and click **Authorize for this image**.
   You should see: **Connected** in Spark. Every PC that starts from this image will appear in this account.
   <details><summary>Can't sign in on this PC?</summary>

   Use a code instead. On any other computer, sign in to your Kinesis account and go to **Provide** > **Fleet** > **Add machines** > **Windows / WSL**. Click the small link **Setting up a diskless venue image (CCBoot and similar)? Get a 1-year venue token**, then **Create venue token**, then the copy button. Get the code to this PC. In Spark, click **Paste a token instead**, paste it and click **Use this token**. The code works for one year.

   Make the code in **your own** account, not the account of someone helping you: every PC joins the account the code came from, and that account gets the earnings. After saving the image, never press **Regenerate** on that page: PCs that have not joined yet could no longer join.
   </details>
7. **Prepare and save.** Go through the last screens. At the end, click **Prepare this PC for saving the image** and answer **Yes**. Then, within 1 hour and without using this PC: shut it down, save the image in your diskless system the way you always do, and turn write protection back on.
8. **Check that it works.** Start one cafe PC as usual. Within a few minutes, it appears in your Kinesis account under **Provide** > **Fleet**. Open a customer session on it from the cashier PC: Spark stops within about 20 seconds. Lock it again: Spark goes back to work within about a minute.

Done. To update later, repeat steps 3 and 4: Spark opens on **Update this venue image** by itself, and every PC keeps its place in your account.

## Supported cafe software

<!-- Maintainers: to support new cafe software, add one row here (and the same row in README.tr.md),
     plus hooks/<software>.md and hooks/<software>.tr.md written like hooks/cafeplus.md.
     Nothing else in this README needs to change. -->

| Cafe software | Setup page |
|---|---|
| AKINSOFT CafePlus | [English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) · [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md) |

Using different cafe software? Email **support@kinesis.network** and we'll add it.

## If something goes wrong

<details><summary>A PC does not show up in your account</summary>

On that PC, open Start, type `cmd`, right-click **Command Prompt** and choose **Run as administrator**. Run these two lines:

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" status
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue doctor
```

Send what they show, and the PC's name, to **support@kinesis.network**.
</details>

> The old "Kinesis Spark diskless venue kit" (a PowerShell script) is retired. Use the installer above.
