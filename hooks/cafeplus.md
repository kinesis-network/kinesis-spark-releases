**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.tr.md)

# Setting up AKINSOFT CafePlus

This is step 2 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md). You add two lines to CafePlus, so it tells Spark when a customer sits down and when they leave. Spark then stops the moment a PC is rented.

You do this **once, on the cashier (kasa) PC**. CafePlus passes the setting to every PC in the cafe by itself.

1. **Open the script settings.** In CafePlus on the cashier PC, go to **Client Ayarları** > **Açma Kapama Scripti** (the open / close script).
   You should see: two boxes, **Client kullanıma açılırken çalıştırılacak kod satırı** (top) and **Client kilitlenirken çalıştırılacak kod satırı** (bottom).

2. **Top box** (runs when a customer starts): copy this line and paste it in, exactly as it is.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. **Bottom box** (runs when the PC is locked, the customer has left): copy this line and paste it in, exactly as it is.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. **Save.**
   You should see: each box holds just its one line, nothing else. Do not change any part of it.

5. **That's it for the cashier PC.** Each cafe PC picks up the new lines the next time it starts. PCs without Spark run them too and simply do nothing.

Once Spark is in your image, step 8 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) checks that this works: rent a PC from the cashier PC and Spark stops within about 20 seconds; lock it and Spark goes back to work within about a minute.

<details><summary>Want a PC to pick up the lines now, without restarting it?</summary>

This ends the customer session on that PC; it goes back to the lock screen. In that PC's CafePlus window, on the **Yetkili** tab, click **Programdan Çık** (exit program). Then start CafePlus again from:

```
C:\Program Files (x86)\AKINSOFT\CafePlusClient12\cplusc.exe
```

During the setup (step 5 of the guide), Spark has a **CafePlus check** screen that shows these same two lines with **Copy** buttons, a **Start CafePlus client** button that does this for you, and an optional test that rents and locks the PC.
</details>
