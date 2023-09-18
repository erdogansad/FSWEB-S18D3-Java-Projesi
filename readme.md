# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sizin için hazırladığımız veritabanında aşağıda istediğimiz sonuçları elde etmenize yarayan SQL sorgularını oluşturacaksınız.

## Proje Kurulumu

Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

### Kütüphane Bilgi Sistemi

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındırmaktadır.

#### Tablolar

`ogrenci` tablosu öğrencilerin listesini tutar.
`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar
`kitap` tablosu kütüphanedeki kitapların bilgisini tutar
`yazar` tablosu kitapların yazarları bilgisini tutar
`tur` tablosu kitapların türlerini tutar.

Tablo ilişiklerini görmek için [ktphn.png] dosyasına göz atın.

Yazdığınız sorguları buradan test edebilirsiniz: [https://ergineer.com/assets/materials/fkg36so5-kutuphanebilgisistemi-sql/]

##### Görevler

Aşağıda istenilen sonuçlara ulaşabilmek için gerekli SQL sorgularını yazın.

MIN-MAX, COUNT-AVG-SUM, GROUP BY, JOINS (INNER, OUTER, LEFT, RIGHT
#ilk 3 soruyu join kullanmadan yazın.

    1) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    CEVAP: select ogrenci.ad, ogrenci.soyad, islem.atarih from ogrenci, islem where ogrenci.ogrno = islem.ogrno;

    2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    CEVAP: select kitap.ad, tur.ad from kitap, tur where kitap.turno = tur.turno and tur.ad = 'Fıkra' or tur.ad = 'Hikaye';

    3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

    CEVAP: select ogrenci.ogrno, ogrenci.ad, ogrenci.soyad, kitap.ad from ogrenci, islem, kitap where ogrenci.ogrno = islem.ogrno and islem.kitapno = kitap.kitapno and ogrenci.sinif = '10B' or ogrenci.sinif = '10C';

    #join ile yazın
    4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    CEVAP: select ogrenci.ad, ogrenci.soyad, islem.atarih from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno;

    5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    CEVAP: select kitap.ad, tur.ad from kitap inner join tur on kitap.turno = tur.turno where tur.ad = 'Fıkra' or tur.ad = 'Hikaye';

    6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

    CEVAP: select ogrenci.ogrno, ogrenci.ad, ogrenci.soyad, kitap.ad from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno inner join kitap on islem.kitapno = kitap.kitapno where ogrenci.sinif = '10B' or ogrenci.sinif = '10C' order by ogrenci.ad;

    7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

    CEVAP: select ogrenci.ad, ogrenci.soyad, islem.atarih from ogrenci left join islem on ogrenci.ogrno = islem.ogrno;

    8) Kitap almayan öğrencileri listeleyin.

    CEVAP: select ogrenci.ad, ogrenci.soyad from ogrenci left join islem on ogrenci.ogrno = islem.ogrno where islem.ogrno is null;

    9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    CEVAP: select kitap.kitapno, kitap.ad, count(islem.kitapno) from kitap left join islem on kitap.kitapno = islem.kitapno group by kitap.kitapno order by kitap.kitapno;

    10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

    CEVAP: select kitap.kitapno, kitap.ad, count(islem.kitapno) from kitap left join islem on kitap.kitapno = islem.kitapno group by kitap.kitapno;

    11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

    CEVAP: select ogrenci.ad, ogrenci.soyad, kitap.ad from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno inner join kitap on islem.kitapno = kitap.kitapno;

    12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.

    CEVAP: select ogrenci.ad, ogrenci.soyad, kitap.ad, yazar.adsoyad, tur.ad, islem.atarih from ogrenci left join islem on ogrenci.ogrno = islem.ogrno inner join kitap on islem.kitapno = kitap.kitapno inner join yazar on kitap.yazarno = yazar.yazarno inner join tur on kitap.turno = tur.turno;

    13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

    CEVAP: select ogrenci.ad, ogrenci.soyad, count(islem.kitapno) from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno where ogrenci.sinif = '10A' or ogrenci.sinif = '10B' group by ogrenci.ad, ogrenci.soyad;

    14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    #AVG

    CEVAP: select avg(kitap.sayfa) from kitap;

    15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

    CEVAP: select kitap.ad, kitap.sayfa from kitap where kitap.sayfa > (select avg(kitap.sayfa) from kitap);

    16) Öğrenci tablosundaki öğrenci sayısını gösterin

    CEVAP: select count(ogrno) from ogrenci;

    17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

    CEVAP: select count(ogrno) as toplam_ogrenci from ogrenci;

    18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

    CEVAP: select count(distinct ad) from ogrenci;

    19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    CEVAP: select max(sayfa) from kitap;

    20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    CEVAP: select ad, sayfa from kitap where sayfa = (select max(sayfa) from kitap);

    21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    CEVAP: select min(sayfa) from kitap;

    22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    CEVAP: select ad, sayfa from kitap where sayfa = (select min(sayfa) from kitap);

    23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

    CEVAP: select max(sayfa) from kitap where turno = (select turno from tur where ad = 'Dram');

    24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.

    CEVAP: select sum(sayfa) from kitap where kitapno in (select kitapno from islem where ogrno = 15);

    25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

    CEVAP: select ad, count(ad) from ogrenci group by ad;

    26) Her sınıftaki öğrenci sayısını bulunuz.

    CEVAP: select sinif, count(sinif) from ogrenci group by sinif;

    27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.

    CEVAP: select sinif, cinsiyet, count(cinsiyet) from ogrenci group by sinif, cinsiyet;

    28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

    CEVAP: select ogrenci.ad, ogrenci.soyad, sum(kitap.sayfa) from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno inner join kitap on islem.kitapno = kitap.kitapno group by ogrenci.ad, ogrenci.soyad order by sum(kitap.sayfa) desc;

    29) Her öğrencinin okuduğu kitap sayısını getiriniz.

    CEVAP: select ogrenci.ad, ogrenci.soyad, count(islem.kitapno) from ogrenci inner join islem on ogrenci.ogrno = islem.ogrno group by ogrenci.ad, ogrenci.soyad;
