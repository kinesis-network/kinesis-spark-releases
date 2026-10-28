[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/cafeplus.md) | **Türkçe**

# AKINSOFT CafePlus ayarı

Bu, [kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 2. adımıdır. CafePlus'a iki satır eklersiniz; böylece CafePlus, müşteri oturduğunda ve kalktığında Spark'a haber verir. Bilgisayar kiralandığı anda Spark durur.

Bunu **bir kez, kasa bilgisayarında** yaparsınız. CafePlus ayarı kafedeki bütün bilgisayarlara kendisi dağıtır.

1. **Script ayarlarını açın.** Kasa bilgisayarında CafePlus'ta **Client Ayarları** > **Açma Kapama Scripti** bölümüne girin.
   Görmeniz gereken: iki kutu; üstte **Client kullanıma açılırken çalıştırılacak kod satırı**, altta **Client kilitlenirken çalıştırılacak kod satırı**.

2. **Üstteki kutu** (müşteri oturumu başlarken çalışır): bu satırı kopyalayıp olduğu gibi yapıştırın.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue occupied --no-wait --no-window
   ```

3. **Alttaki kutu** (bilgisayar kilitlenince, müşteri kalkınca çalışır): bu satırı kopyalayıp olduğu gibi yapıştırın.

   ```
   if exist "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" "C:\Program Files\Dynamo\Dynamo.Spark.WinService.exe" venue vacant --no-wait --no-window
   ```

4. **Kaydedin.**
   Görmeniz gereken: her kutuda yalnızca kendi satırı var, başka bir şey yok. Satırın hiçbir yerini değiştirmeyin.

5. **Kasa tarafında iş bitti.** Her kafe bilgisayarı yeni satırları bir sonraki açılışında alır. Spark olmayan bilgisayarlar da bu satırları çalıştırır, ama hiçbir şey olmaz.

Spark imajınıza kurulduktan sonra [kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 8. adımında bunun çalıştığını kontrol edersiniz: kasadan bir bilgisayarı kiralayın, Spark yaklaşık 20 saniyede durur; kilitleyin, Spark yaklaşık bir dakikada işe döner.

<details><summary>Bir bilgisayar satırları yeniden başlatmadan hemen alsın mı istiyorsunuz?</summary>

Bu, o bilgisayardaki müşteri oturumunu bitirir; bilgisayar kilit ekranına döner. O bilgisayarın CafePlus penceresinde **Yetkili** sekmesinde **Programdan Çık**'a tıklayın. Sonra CafePlus'ı şuradan yeniden başlatın:

```
C:\Program Files (x86)\AKINSOFT\CafePlusClient12\cplusc.exe
```

Kurulum sırasında (rehberin 5. adımı) Spark'ın **CafePlus kontrolü** ekranı aynı iki satırı **Kopyala** düğmeleriyle gösterir; bunu sizin yerinize yapan bir **CafePlus istemcisini başlat** düğmesi ve bilgisayarı kiralayıp kilitleyen isteğe bağlı bir test de sunar.
</details>
