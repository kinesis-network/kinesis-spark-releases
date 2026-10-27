**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)

# Hook setup: AKINSOFT CafePlus

Done once, on the **register (kasa) PC**, not on the image PC. CafePlus sends these settings to every PC in the venue.

1. Open **Genel Client Ayarları** (General Client Settings), tab **Açma Kapatma Scripti** (open / close script).
2. Top box, **Client kullanıma açılırken çalıştırılacak kod satırı** (line run when the client is opened for use, i.e. a customer starts), paste exactly:

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. Bottom box, **Client kilitlenirken çalıştırılacak kod satırı** (line run when the client is locked, i.e. the customer leaves), paste exactly:

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. Save. One line per box, nothing else in it. Keep the path as written: never `%ProgramFiles%` (CafePlus runs a 32-bit `cmd`, where it points to `C:\Program Files (x86)`).

**When it takes effect:** a client PC picks up the boxes only when its CafePlus client starts, so in practice at its next boot.

**PCs without Spark** run the same lines and do nothing: the `if exist` part skips them.

**Check it works** (on a PC with Spark, after a reboot): rent the PC from the register, and Spark stops within about 20 seconds. Lock it, and Spark is working again within about a minute. The kit's step 7 (`-Step 7`) checks this PC's CafePlus script for the line; step 8 (`-Step 8`) shows the rent / lock live.
