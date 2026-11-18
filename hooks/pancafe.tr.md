[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.md) | **Türkçe**

# PanCafe Pro kurulumu

Bu, [kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 2. adımıdır.

**PanCafe'ye eklenecek bir şey yok.** Spark her bilgisayarda PanCafe'nin kendi kilit ekranını görür (ilk kafelerde doğrulanıyor): kilit ekranı
görünürken bilgisayar boştur ve Spark çalışır; müşteri oturumu açıkken Spark durur; PanCafe çalışmıyorken Spark kapalı kalır.

Kurulum sırasında (rehberin 5. adımı) Spark bir **PanCafe kontrolü** ekranı gösterir. Orada iki satır listelenir: isteğe
bağlıdır.

<details><summary>İsteğe bağlı: PanCafe'niz komut çalıştırabiliyorsa iki satır</summary>

PanCafe'niz müşteri oturumu açılınca ve bilgisayar kilitlenince bir komut çalıştırabiliyorsa bunları ekleyebilirsiniz;
Spark bunu doğrudan da duyar. Komut satırı çalıştırıyorsa ilk çifti, program başlatıyorsa ikinci çifti kullanın.

```
if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
```

```
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
"C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
```

Her çiftin ilk satırı oturum açılması, ikincisi bilgisayarın kilitlenmesi içindir.
</details>

**Spark'ı PanCafe'nin yasaklı programlar ya da "sonlandırılacak programlar" listesine eklemeyin**: PanCafe her
bilgisayarda Spark'ı durdurur.

[Kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 8. adımı çalıştığını
kontrol eder: kasadan bir oturum açın, Spark yaklaşık 20 saniyede durur; kilitleyin, Spark yaklaşık bir dakikada işe döner.
