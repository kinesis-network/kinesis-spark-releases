[English](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/hooks/pancafe.md) | **Türkçe**

# PanCafe Pro kurulumu

Bu, [kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 2. adımıdır.

**PanCafe'ye eklenecek bir şey yok.** Spark her bilgisayarda PanCafe'nin kendi kilit ekranını görür (TayNet'te bir bilgisayardaki denemede her kilitlemede ve her oturum açılışında görüldü, 23 Kasım 2026): kilit ekranı
görünürken bilgisayar boştur ve Spark çalışır; müşteri oturumu açıkken Spark durur; PanCafe çalışmıyorken Spark kapalı kalır.

Kurulum sırasında (rehberin 5. adımı) Spark bir **PanCafe kontrolü** ekranı gösterir. Orada iki satır isteğe bağlı olarak
listelenir: eklemeyin. PanCafe'de oturum açılınca ya da bilgisayar kilitlenince komut çalıştıran bir ayar yok (TayNet'te kontrol
edildi, 23 Kasım 2026); satırları girecek bir yer yoktur ve Spark'ın bunlara ihtiyacı yoktur: kilit ekranına bakar.

Oturum bitince PanCafe müşterinin programlarını kapatır; Spark'ın tepsi uygulaması da bunlardan biri olabilir. Spark onu
yaklaşık 15 saniye içinde kendisi yeniden başlatır; yapılacak bir şey yok.

**Spark'ı PanCafe'nin yasaklı programlar ya da "sonlandırılacak programlar" listesine eklemeyin**: PanCafe her
bilgisayarda Spark'ı durdurur.

[Kurulum rehberinin](https://github.com/kinesis-network/kinesis-spark-releases/blob/main/README.tr.md) 8. adımı çalıştığını
kontrol eder: kasadan bir oturum açın, Spark yaklaşık 20 saniyede durur; kilitleyin, Spark yaklaşık bir dakikada işe döner.
