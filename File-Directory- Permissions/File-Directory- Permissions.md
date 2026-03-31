# File & Directory Permissions

Dosya ve Dizinlerin (objelerin) erişim yetkileri ls -l <nesne> komutuyla görüntülenebilir ls komutu bir dizin için olduğu gibi bir dosya içinde içinde kullanılabilir.

Bir objenin tipi, listelemedeki ilk hanede, – veya d karakterleriyle ifade edilir.

- ‘-’ karakteri nesnenin bir dosya; ‘d’ karakteri ise nesnenin bir dizin olduğunu ifade eder.

Bir nesnenin aitliği kulanıcı ve grup olarak iki şekilde ele alınıyor

![image.png](File%20&%20Directory%20Permissions/image.png)

Görselde, listedeki tüm nesnelerin (sırasıyla) root kullanıcısı ve root grubuna ait olduğu görülmektedir

**Önemli not.Yetkiyi dosyaya değilde dizinde uygularsak tüm dosyaları etkiler.**

`CHOWN` komutu ile aitlik değiştirilir

`chown user:group <nesne>` şeklinde kullanımı mevcuttur.

**Aitliklerin tek kullanıcı ve grup için olabileceğini unutmayın.**

**aitlik durumu tek başına erişimi belirleyemez yani root:root olan aitlik dosyasını sistemdeki user okuyabilir asıl önemli olan burada izinler.**

### Yetki ifadeleri ve Haneleri

Yetkilerdeki ifadeler, dosya veya dizinler (nesneler) için tablodaki gibi anlamlandırılır:

| R | Read anlamındadır. Nesnede okuma yetkisi bulunduğunu belirtir. |
| --- | --- |
| W | Write anlamındadır.Nesnede yazma yetkisi bulunduğunu belirtir. |
| X | Execute anlamındadır.Nesnede çalıştırma yetkisi bulunduğu belirtir. |
| - | Nesnede ilgili hane için bir izin olmadığını belirtir (İlk hanedeki tire ile karıştırılmamalı) |

![image.png](File%20&%20Directory%20Permissions/image%201.png)

-Bir nesne için yetki ifadeleri toplam 9 adettirler

-3 bölümden oluşur.

![image.png](File%20&%20Directory%20Permissions/image%202.png)

yukarıda görülen mor alan 1 bölümü ifade eder bundan 3 tane vardır toplamda 9 eder şimdi bunları açıklayalım

1.Bölüm

- Kullanıcının (User) Yetkileri
- R W X
- Read,Write,eXecute (okuma,yazma,çalıştırma)

2.Bölüm

- Grubun (Group’s)Yetkileri.
- R W X
- Read,Write,eXecute

3.Bölüm

- Diğerlerinin (Others) Yetkileri
- R W X
- Read,Write,eXecute
- Other denilince aklıma dünyanın diğer kalanı gelsin :D

### Nesne Erişim Yetkilendirmeleri

Dosya ve dizinlerin (Kısaca nesnelerin) erişim yetkileri chmod komutuyla değiştiriliyor 

-Syntax’ı şu şekildedir.

`CHMOD U/G/O/A +/-/= R/W/X/S/T <NESNE>`  

Yukarıdaki komutu gelin biraz daha açalım.

| KOMUT | PARAMETRE | ARGÜMAN | NESNE |
| --- | --- | --- | --- |
| chmod | U, G, O, A |  +, -, = | **NESNE** |
|  | ekleme ,çıkarma,eşitleme | Read,Write,eXecute |  |

kısacası chmod bize şunu sorar : **NESNEYE,KİM İÇİN,NE YAPACAKSIN?**

-PEKİ yukarıda syntax yazımında s ve t gördük

`s` → **SetUID / SetGID**

- Bir dosya çalıştırıldığında, onu çalıştıran kullanıcının değil, **dosyanın sahibi (owner) veya grubunun yetkisiyle çalışmasını sağlar.**
- **u+s (SetUID)** → dosya, sahibi kimse onun yetkisiyle çalışır
- **g+s (SetGID)** → dosya, grubun yetkisiyle çalışır

Örnek verecek olursak

`chmod u+s dosya`

En klasik örnek;

![image.png](File%20&%20Directory%20Permissions/image%203.png)

-rwsr-xr-x 1 root root …

Buradaki s → passwd programı çalıştığında root yetkisiyle çalıştığı anlamına geliyor.

`t` → **Sticky Bit**

Bir dizinde kullanılır ve şunu sağlar:

- Herkes yazabilir
- Bu izin tek tek dosyaları etkilemez. Ancak dizin düzeyinde dosya silme işlemini kısıtlar. Yalnızca dosyanın sahibi (ve root) o dizin içindeki dosyayı silebilir. Bunun yaygın bir örneği /tmp dizinidir

![image.png](File%20&%20Directory%20Permissions/image%204.png)

Sonundaki t→sticky bit

/tmp herkese açık

ama başkasının dosyasını sen silemezsin şeklinde aklımıza kodlayabiliriz.

### OCTAL MODE

?Nedir; Yetkiler, rakamlarla da sayısal olarak ifade edilebilir buna **Octal-Mode** deriz.

| YETKİ | SAYISAL DEĞER |
| --- | --- |
| R | 4 |
| W | 2 |
| X | 1 |

İlgili bölümün yetki rakamları toplanır.Toplam sayı,ilgili bölümün yetkilerini ifade eder.

| 1.BÖLÜM | 2.BÖLÜM | 3.BÖLÜM |
| --- | --- | --- |
| USER | GRUOUPS | OTHERS |
| R W X | R W X | R W X |
| 4 + 2 + 1 = 7 | 4 + 2 + 1 = 7  | 4 + 2 + 1 = 7 |

Yetkinin bulunmadığı (-) durum, 0 (sıfır) olarak değerlendirilir

| 1.BÖLÜM | 2.BÖLÜM | 3.BÖLÜM |
| --- | --- | --- |
| USER | GRUOUPS | OTHERS |
| R - X | R W - | - W X |
| 4 + 0 + 1 = 5 | 4 + 2 + 0 = 6 | 0+ 2 + 1 = 3 |

Octal-Mode’da görebileceğiniz, kullanabileceğiniz toplam 7 tane olasılık vardır.
Octal-Mode, değişik hallerde en fazla 7 kez kombine olabilir

![image.png](File%20&%20Directory%20Permissions/image%205.png)

Örnekler.

`CHMOD 777 SİMPLE.TXT`  → simple.txt dosyasına herkes için rwx yetkisi vermiş oluruz.

`CHMOD 536 SİMPLE.TXT` → simple.txt dosyasına **user** için r-x; **group** için -wx ve **others** için rw- yetkisi verilmiş olur