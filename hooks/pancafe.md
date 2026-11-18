**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.tr.md)

# Setting up PanCafe Pro

This is step 2 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md).

**There is nothing to add in PanCafe.** On each PC, Spark sees PanCafe's own lock screen (being confirmed at the first cafes): while it shows, the PC is
free and Spark works; while a customer's session is open, Spark stops; while PanCafe is not running, Spark stays off.

During the setup (step 5 of the guide) Spark shows a **PanCafe check** screen. It lists two lines: they are optional.

<details><summary>Optional: the two lines, if your PanCafe can run a command</summary>

If your PanCafe can run a command when a customer's session opens and when the PC locks, you can add these, so Spark
also hears it directly. Use the first pair if it runs a command line, the second pair if it starts a program.

```
if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
```

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
```

The first line of each pair is for a session opening, the second for the PC locking.
</details>

**Do not add Spark to PanCafe's banned or "programs to terminate" lists**: PanCafe would stop Spark on every PC.

Step 8 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) checks that it
works: open a session from the cashier PC and Spark stops within about 20 seconds; lock it and Spark goes back to work
within about a minute.
