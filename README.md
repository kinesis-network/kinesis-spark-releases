# Kinesis Spark venue kit

Sets up Spark on an internet cafe's Windows image, so every PC that boots the image earns while no customer sits at it.
Run it on the **image PC only**, with the freeze / diskless protection **OFF**.

1. Get a **"1 year (venue image)"** token from the venue's own Portal account (Fleet -> Add machines).
2. In an administrator PowerShell: `mkdir C:\venue-kit; cd C:\venue-kit`, then (the first part turns on TLS 1.2, which Windows PowerShell needs for GitHub)
   `[Net.ServicePointManager]::SecurityProtocol = 'Tls12'; irm https://github.com/kinesis-network/kinesis-spark-releases/releases/latest/download/venue-setup.ps1 -OutFile venue-setup.ps1`
3. Run steps 1 to 9 in order, one at a time: `powershell -ExecutionPolicy Bypass -File .\venue-setup.ps1 -Step 1` (then `-Step 2`, ...). `-Help` lists them.
4. Step 7 prints the two lines for the CafePlus register's client settings (session opens / PC locks).
5. Step 9 prepares the image and deletes the kit. Save the image, then turn the protection back **ON**.

Steps 2 to 5 need the internet (step 4 also fetches Microsoft's .NET and ASP.NET Core runtimes when the PC lacks them). Spark and its engine update themselves; the kit always installs the current Spark.
