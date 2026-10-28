**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)

# Hook setup: AKINSOFT CafePlus

CafePlus tells Spark when a customer sits down and when they leave, so Spark stops the moment a PC is rented. Done **once, on the register (kasa) PC**, not on the image PC; CafePlus sends these settings to every PC in the venue.

1. **Open the script settings.** In CafePlus on the register PC: **Client Ayarları** (client settings) > **Açma Kapama Scripti** (open / close script).
   You should see: two boxes, **Client kullanıma açılırken çalıştırılacak kod satırı** (top) and **Client kilitlenirken çalıştırılacak kod satırı** (bottom).

2. **Top box** (run when a customer starts): paste exactly this one line.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. **Bottom box** (run when the PC is locked, the customer leaves): paste exactly this one line.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. **Save.**
   You should see: each box holds one line and nothing else, with `C:\Program Files\Dynamo` written out (never `%ProgramFiles%`: CafePlus runs a 32-bit `cmd`, where it means `C:\Program Files (x86)`).

5. **Wait for the next boot.** Each PC takes the boxes when its CafePlus client starts, so at its next boot. PCs without Spark run the same lines and do nothing (the `if exist` part skips them).

6. **Check it on one PC with Spark**, after a boot: rent it from the register.
   You should see: Spark stops within about 20 seconds. Lock it: Spark works again within about a minute.

**To make one PC take the boxes now**, without a reboot (this ends its session; it comes back to the lock screen): in that PC's CafePlus window, tab **Yetkili**, click **Programdan Çık** (exit program), then start this again:

```
C:\Program Files (x86)\AKINSOFT\CafePlusClient12\cplusc.exe
```

The next rent or lock then writes the box's line to that PC's `script.cmd`. On the image PC, Spark's venue setup (see the [installer page](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md)) shows the same two lines with **Copy** buttons at its **CafePlus check** step, looks for the line there, and has a **Start CafePlus client** button; its optional lock and rent test checks that Spark follows.
