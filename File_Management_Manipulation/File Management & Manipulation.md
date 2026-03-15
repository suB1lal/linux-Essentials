# File Management & Manipulation

Linux sistemlerde **dosya ve dizinleri yönetme, düzenleme, değiştirme ve kontrol etme işlemlerinin tamamını ele alağız bu başlıkta.**

**Navigate**

![image.png](File%20Management%20&%20Manipulation/image.png)

İlk olarak bakacağımız komut **pwd** (print working directory) o an üzerinde çalıştığımız dizini bize gösterir.

`ls`

![image.png](File%20Management%20&%20Manipulation/image%201.png)

Bir sonraki önemli komutumuz **ls** komutu içinde bulunduğumuz dizinde hangi dosyalar klasörler var bize listeler tabikide bununla sınırlı değil

![image.png](File%20Management%20&%20Manipulation/image%202.png)

Ayrıca sadece bulunduğumuz dizindeki dosyalar görmemize yaramaz

`ls -lR`

![image.png](File%20Management%20&%20Manipulation/image%203.png)

bir dizinin içindeki tüm dosya ve klasörleri, alt dizinler dahil olacak şekilde detaylı olarak listelemek için kullanılır.

| `-l` | detaylı (long format) listeleme yapar |
| --- | --- |

| `-R` | tüm alt dizinleri **recursive** olarak gezer |
| --- | --- |

Dosya sahipleri ,gizli dosyalar dahil olmak üzere çok fazla parametresi mevcut olan ve linux sistemlerde sıkça kullanılan çok önemli komutumuzdur.

Tabikide tüm parametrelerini burada göstermeyeceğim detaylı bilgi için 
`ls man` 

Çıktısını incelemekte fayda var.

![image.png](File%20Management%20&%20Manipulation/image%204.png)

**CD (CHANGE DİRECTORY)**

Bir sonraki komutumuz neredeyse her zaman kullandığımız `cd` 

![image.png](File%20Management%20&%20Manipulation/image%205.png)

Adındanda anlaşılacağı üzere dizinler arası gezinmek,bulunduğumuz dizinden başka dizine geçmek için sık sık kullandığımız komuttur.

home dizine gitmek için 

1. cd
2. cd ~

komutlarını yazmak yeterli olacaktır.

![image.png](File%20Management%20&%20Manipulation/image%206.png)

Bir üst dizine çıkmak için `cd ..` kullanmak yeterli olacaktır

![image.png](File%20Management%20&%20Manipulation/image%207.png)

Bir önceki dizine dönmek içinse `cd -` komutunu yazmamız yeterli olacaktır

![image.png](File%20Management%20&%20Manipulation/image%208.png)

Daha fazlası için 

`cd —help` komutu ile yardım alabilirsiniz

![image.png](File%20Management%20&%20Manipulation/image%209.png)

### Create File and Directory

![image.png](File%20Management%20&%20Manipulation/image%2010.png)

Bilmediğimiz bir komut için `whatis` komutundan yardım alabiliriz.
komutun ne işe yaradığını kısa bir açıklamayla gösterir.

**TOUCH**

Dosya oluşturma

`touch deneme.txt` 

![image.png](File%20Management%20&%20Manipulation/image%2011.png)

Görüldüğü üzere deneme.txt adında boş dosyamız oluştu.
Birden fazla dosya oluşturmak istediğimizde ise aynı yöntem sadece dosya adlarını yan yana yazmamız gerekecektir.

`touch file1.txt file2.txt file3.txt`

![image.png](File%20Management%20&%20Manipulation/image%2012.png)

Belirli bir dizinde dosya oluşturmak içinse

`touch /home/directory/file_name.txt` 

![image.png](File%20Management%20&%20Manipulation/image%2013.png)

**Linux'ta dosya uzantısı zorunlu değildir.**

**`touch` komutu ile oluşturulan bir dosya varsayılan olarak uzantısız oluşturulur**

**MKDİR** 

Dizin oluşturmak için **`mkdir`** komutu kullanırız.

örnek kullanımı;

`mkdir new_directory` 

![image.png](File%20Management%20&%20Manipulation/image%2014.png)

iç içe dizinler oluşturmak istediğimizde -p parametresini kullanırız.

`mkdir -p /home/subdirectory/directory` 

![image.png](File%20Management%20&%20Manipulation/image%2015.png)

daha fazlası için man sayfasına göz atabiliriz.

![image.png](File%20Management%20&%20Manipulation/image%2016.png)

### `echo` ve `cat` Komutları

Linux’ta dosyalarla çalışırken en sık kullanılan komutlardan ikisi **`echo`** ve **`cat`** komutlarıdır.

Bu komutlar genellikle:

- dosya içeriği oluşturmak
- dosya içeriğini görüntülemek
- metin çıktısı üretmek
- script yazarken çıktı vermek

gibi durumlarda sıkça kullanılır.

![image.png](File%20Management%20&%20Manipulation/image%2017.png)

Dosya içine yazmak istersek

![image.png](File%20Management%20&%20Manipulation/image%2018.png)

“>” ile direkt dosyanın içine yazarız ve içindeki veriler silinir veri eklemek için “ >> ” kullanırız

![image.png](File%20Management%20&%20Manipulation/image%2019.png)

`cat` (**concatenate**) komutu dosya içeriğini **terminalde görüntülemek** için kullanılır.

`cat dosya_adı` 

![image.png](File%20Management%20&%20Manipulation/image%2020.png)

Birden fazla görüntülemek için okuncak dosyaları yan yana yazdırabiliriz.

![image.png](File%20Management%20&%20Manipulation/image%2021.png)

Cat ile yeni dosya oluşturup içine veri ekleyebiliriz

`cat > example.txt`

![image.png](File%20Management%20&%20Manipulation/image%2022.png)

CTRL + D ile yazmayı bitiririz.

Dosyaları birleştirmek için;

`cat file1.txt file2.txt > birleşik.txt`

![image.png](File%20Management%20&%20Manipulation/image%2023.png)

**`rm` Command**

Linux'ta `rm` komutu ile silinen dosyalar **geri dönüşüm kutusuna gitmez**, doğrudan sistemden kaldırılır.

![image.png](File%20Management%20&%20Manipulation/image%2024.png)

**Toplu silmek için;**

`rm file1.txt file2.txt file3.txt`

**Dizini silmek için;**

`rm -r directory_name`

![image.png](File%20Management%20&%20Manipulation/image%2025.png)

**Boş Klasör Silmek 2 yolumuz var;**

- `rmdir klasör_adı`
- `rm -r klasör_adı`

**parametreleri;**

## `r` (recursive)

Klasörleri ve içindeki tüm dosyaları siler.

`rm -r folder`

## `f` (force)

Dosyayı **sormadan zorla siler**.

`rm -f file.txt`

## `i` (interactive)

Silmeden önce kullanıcıdan onay ister.

`rm -i file.txt`

## `v` (verbose)

Silinen dosyaları ekrana yazdırır.

`rm -v file.txt`

**!!!PLEASE DONT USE `rm -rf /`   :dddd**

`rm *.txt`  içinde bulunduğumuz dizindeki tüm txt dosyalarını siler.

### File Copying and Moving in Linux (`cp` & `mv`)

- **`cp`** → dosya veya dizin kopyalama
- **`mv`** → dosya veya dizin taşıma / yeniden adlandırma

**CP**

`cp kaynak_dosya hedef_dosya`

Temel kullanımı bu şekilde;

![image.png](File%20Management%20&%20Manipulation/image%2026.png)

“~” Kullanıcımızın home sayfasını temsil eder bunu öğrenmiştik.

backup almak içinde sıkça başvurulan bir komut.

![image.png](File%20Management%20&%20Manipulation/image%2027.png)

Aynı içeriğe sahip iki dosya oluşur.

Dizin kopyalamak için `-r` parametresi gerekir.

`cp -r project backup_project`

man sayfasında detaylı tüm parametrelere bakabiliriz.

![image.png](File%20Management%20&%20Manipulation/image%2028.png)

**MV**

`mv` komutu dosyaları **taşımak veya yeniden adlandırmak** için kullanılır.

`cp`'den farklı olarak **dosyanın kopyası oluşturulmaz**, dosya sadece yer değiştirir.

`mv kaynak hedef`

![image.png](File%20Management%20&%20Manipulation/image%2029.png)

Dosyayı yeniden adlandırmak içinde kullanılır.

![image.png](File%20Management%20&%20Manipulation/image%2030.png)

`mv` Parametreleri

### `i` (interactive)

Üzerine yazmadan önce sorar.

`mv -i file.txt Documents/`

### `v` (verbose)

Taşıma işlemini gösterir.

`mv -v file.txt Documents/`