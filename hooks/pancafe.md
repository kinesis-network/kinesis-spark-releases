**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.tr.md)

# Setting up PanCafe Pro

This is step 2 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md).

**There is nothing to add in PanCafe.** On each PC, Spark sees PanCafe's own lock screen (seen at every lock and every session open in a test on one TayNet PC, 23 Nov 2026): while it shows, the PC is
free and Spark works; while a customer's session is open, Spark stops; while PanCafe is not running, Spark stays off.

During the setup (step 5 of the guide) Spark shows a **PanCafe check** screen. It lists two lines as optional: leave them out.
PanCafe has no setting that runs a command when a session opens or the PC locks (checked at TayNet, 23 Nov 2026), so
there is nowhere to put them, and Spark does not need them: it goes by the lock screen.

When a session ends, PanCafe closes the customer's programs, and Spark's tray app may be one of them. Spark starts it
again by itself within about 15 seconds; nothing to do.

**Do not add Spark to PanCafe's banned or "programs to terminate" lists**: PanCafe would stop Spark on every PC.

Step 8 of the [setup guide](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.md) checks that it
works: open a session from the cashier PC and Spark stops within about 20 seconds; lock it and Spark goes back to work
within about a minute.
