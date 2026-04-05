# Symbolic & Hard link

### Hard Link

Önemli Bir not symbolic link veya kopyalama yapıldığında kopyalamayı ele alalım önce

copy.txt dosyamız var  elimizde bunu copyaladığımızda kopyası üzerinde bir değişiklik yaparsak bu sadece kopyası üzerinde işlem görecektir veya kaynakta çünkü arada bir linkleme işlemi yoktur.

![image.png](Symbolic%20&%20Hard%20link/image.png)

![image.png](Symbolic%20&%20Hard%20link/image%201.png)

Görsellerde görüldüğü gibi

Bu kopyalama mantığıydı kısayol (symlink) oluşturduğumuzda da değişiklik yapıldığında kaynağa yansıyacaktır ancak symlinklerde kaynak silinirse kaynağı göremediğinden çalışmayacaktı.Yani hardlinkler hem symlink hemde cp gibi kullanılabiliyor.

**Objeler, benzersiz olan numaralara (ID’lere) sahiptirler. Her dosya ve dizin benzersiz ID’lere sahiptir.
Bu yapının adı inode (düğüm)’dur. Dosya ve dizinlerin ID’lerine de inode ID adı verilir.**

Inode ID’ler, ls -li komutuyla görüntülenebilirler. (Dosya sisteminin inode’ları içinse df -i komutu kullanılır.)

![image.png](Symbolic%20&%20Hard%20link/image%202.png)

**Sembolik linkler için inode ID’ler benzersizdir (farklıdır); fakat hard(katı) linkler için benzeşiktir (aynıdır).**

hardlink oluşturalım;

`echo "merhaba dünya" > orijinal.txt` →Dosyamızı oluşturalım

`ln orijinal.txt kopya.txt` →Hardlink oluşturalım.

![image.png](Symbolic%20&%20Hard%20link/image%203.png)

Görüldüğü gibi ID’ler benzeşiktir

ve ister kaynağın ister orjinalin üzerinde değişiklik yapalım ikisinde de işleme alınacaktır.

![image.png](Symbolic%20&%20Hard%20link/image%204.png)

ve Ayrıca yukarıda bahsettiğim gibi orjinal veya kopyalanan kaynak silinirse yinede çalışmaya devam edecektir.

### Symbolic link

Sembolik link’ler bir dosya için sadece kısayol (shortcut) durumu oluşturur ve içeriğe yönlendirme yaparlar.

Hadi gelin nasıl oluşturduğumuza bakalım ve detaylı incelemesini yapalım.

`echo "merhaba symlink" > orijinal.txt`  →Dosyamızı oluşturalım

`ln -s orijinal.txt link.txt`   →symlink  oluşturalım

![image.png](Symbolic%20&%20Hard%20link/image%205.png)

**`l` ile başlıyor → bu symlink**

**`->` → nereyi gösterdiğini söylüyor**

inode kontrolü yapalım.

![image.png](Symbolic%20&%20Hard%20link/image%206.png)

Ayrı bir dosyadır sadece pointer (yol) tutuyor.

Kopya üzerinde değişiklik yapıldığında orijinal dosyayada değişiklik eklenir.

![image.png](Symbolic%20&%20Hard%20link/image%207.png)

(Link üzerinden kaynak dosyaya gidildi aslında.)

**ÖNEMLİ**

KAYNAK SİLİNİRSE OLUŞTURDUĞUMUZ DOSYA ÇALIŞMAYACAKTIR.

![image.png](Symbolic%20&%20Hard%20link/image%208.png)

symlink = **sadece yol tutar KAYNAĞI SİLDİĞİMİZ İÇİN YOLDA ORTADAN UÇAR GİDER VE KOPYA ÇALIŞMAZ.**

**NOTLAR**

hardlinkler dizinler için çalışmaz yani dosyaları linkleyebildiğimiz gibi dizinleri yapamayız.
(çünkü filesystem yapısını bozabilir ve sonsuz döngü (loop) oluşturur.)

Hardlinkler aynı ınode kullandığından  sistem dışına çıkamaz. 

### inode nedir?

İndex node kısaltmasından gelmektedir.Unix benzeri dosyalama sistemlerindeki veri yapısıdır.

Dosya sistemi içindeki tüm bilgilerin deoplandığı yerdir **DOSYA İSMİ** DIŞINDA tüm bilgiler depolanmaktadır.

- sahibi
- Sahibinin ait olduğu grup
- Yaratıldığı tarih
- boyutu
- Link sayısı
- Tipi
- Erişim hakları
- En son erişim tarihi
- En son değişikliklerin yapıldığı tarih
- ve diğer bilgiler

Unix işletim sistemlerinde bilindiği zere her işlem bir dosya olarak kabul edilir bu yüznden her inode 1 dosyayı ifade eder.