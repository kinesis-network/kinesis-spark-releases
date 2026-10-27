**English** | [Türkçe](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md)

# Kinesis Spark venue kit

Sets up Spark on an internet cafe's Windows image, so every PC that boots the image earns while no customer sits at it.
Run it on the **image PC only**, with the freeze / diskless protection **OFF**.

1. Get a **"1 year (venue image)"** token from the venue's own Portal account (Fleet -> Add machines).
2. In an administrator PowerShell: `mkdir C:\kinesis; cd C:\kinesis`, then (the first part turns on TLS 1.2, which Windows PowerShell needs for GitHub)
   `[Net.ServicePointManager]::SecurityProtocol = 'Tls12'; irm https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -OutFile venue-setup.ps1`
3. Run `powershell -ExecutionPolicy Bypass -File .\venue-setup.ps1`. It asks for the token, then does the whole setup and stops at the first problem, saying what to fix.
4. If it asks for a restart: restart the PC (Start > Power > Restart), then run the same command again. It continues where it stopped.
5. It waits for you three times: set up the hook on the register PC ("Hook setup" below; step 7 links the page and checks this PC), test a rent and a lock, then type the confirmations that prepare the image and delete the kit. Save the image, then turn the protection back **ON**.

To repeat or repair one step: add `-Step <n>`. `-Help` lists the steps. The internet must work throughout; Spark and its engine update themselves.

## Hook setup

The cafe software tells Spark when a customer sits down and when they leave, so Spark stops the moment a PC is rented. Pick your cafe software:

- [AKINSOFT CafePlus](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md)

Another cafe software? Contact Kinesis.
