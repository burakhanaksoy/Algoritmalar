<h1>Algoritmalar</h1>

<h2>Binary Search</h2>

<b>Sirali bir dizide</b>, diziye ortadan girip aranan rakami log2(n) karmasikliginda bulmamizi saglar

<p align="center">
<img width="300" src="https://user-images.githubusercontent.com/31994778/124069460-e1736700-da44-11eb-88b6-3b7ba85ec747.gif">

  </p>

Buradaki "n", dizideki eleman sayisidir.

```python
def binary_search(aranan_no, dizi):
    yuksek_nokta = len(dizi) - 1
    dusuk_nokta = 0
    konum = (yuksek_nokta + dusuk_nokta) // 2

    while(yuksek_nokta >= dusuk_nokta):
        if dizi[konum] == aranan_no:
            return True
        elif dizi[konum] > aranan_no:
            yuksek_nokta = konum - 1
        else:
            dusuk_nokta = konum + 1

        konum = (yuksek_nokta + dusuk_nokta) // 2

    return False
```

<h3>Karmasiklik</h3>

Binary search O(log2(N))'de calisir. Bu da demek oluyor ki, linear search'un worst case'inden(O(n)) cok cok daha iyidir, best case'inden O(log(1))'den kotudur.

<b>Ortalamadan O(n/2) ise cok cok daha iyidir</b>

<p align="center">
<img width="350" src="https://user-images.githubusercontent.com/31994778/123933051-ad436c00-d99a-11eb-811f-f0e194f642ad.png">
</p>

<p align="center">
Binary ve Linear search karsilastirmasi
</p>

---

<h2>Selection Sort</h2>

Selection sort(Secerek siralama), adindan da anlasilacagi uzere <b>bir arama degil, siralama algoritmasidir.</b>

Secerek siralama algoritmasi bir dizideki tum elemanlarin uzerinden gecer ve en kucuk elemani basa alir (Eger buyukten kucuge dizmek istiyorsak). Daha sonra, en bastaki elemana bir daha bakmaz ve dizideki en kucuk ikinci elemani bulur ve 2. sira ile yer degistirir. Son elemana kadar bu sekilde ilerlenir.

```python
def selection_sort(dizi):
    kopya_dizi = dizi.copy()

    for i in range(len(kopya_dizi) - 1):
        minimum = kopya_dizi[i]
        for j in range(i + 1, len(kopya_dizi)):
            if minimum > kopya_dizi[j]:
                min_idx = j
                minimum = kopya_dizi[j]
        kopya_dizi[i], kopya_dizi[min_idx] = kopya_dizi[min_idx], kopya_dizi[i]

    return kopya_dizi
```

<h3>Karmasiklik</h3>

Iki tane for loop olmasi direk olarak O(N^2)'de calistigini soylememiz icin yeterli. Cok efektif bir algoritma degil denebilir.

<p align="center">
  <img width="350" src="https://user-images.githubusercontent.com/31994778/124025430-178af980-d9f9-11eb-88e4-e7fc25c5f299.png">
  </p>

---

<h2>Insertion Sort</h2>

<b>Sokma siralamasi olarak cevirilebilir</b>. Asil amacimiz diziye en bastan girip, gittikce buyuyen bir sub-array gibi dusunup sayilari kendi icinde karsilastirmaktir. 

Ornek olarak, dizi = [3, 5, 1, -1, 2, 0, 11, 213, -231] diyelim.

Burada, oncelikle 3,5. Sonrasinda 3,5,1. Sonrasinda 3,5,1,-1'i kendi iclerinde siralayip, bu listeyi gittikce buyuturuz.

1. Adim -> 3,5
2. Adim -> 3,5,1 -> 3,1,5 -> 1,3,5
3. Adim -> 1,3,5,-1 -> 1,3,-1,5 -> 1,-1,3,5 -> -1,1,3,5 gibi..

```python
def insertion_sort(dizi):
    kopya_dizi = dizi.copy()

    for i in range(1, len(kopya_dizi)):
        j = i

        while kopya_dizi[j] < kopya_dizi[j-1] and j > 0:
            kopya_dizi[j], kopya_dizi[j-1] = kopya_dizi[j-1], kopya_dizi[j]
            j -= 1

    return kopya_dizi
```

<h3>Karmasiklik</h3>

Karmasikligimiz O(n^2) dir. Best case'de sirali bir sekilde geldigini dusunebiliriz, bu sekilde O(n) olacaktir.

---

<h2>Bubble Sort</h2>

<b>Kabacik siralamasi</b> olarak da gecer. Bu siralama algoritmasini her seferinde icine iki eleman alan bir baloncugun kayarak siralama yapmasi gibi dusunebiliriz.

```python
def bubble_sort(dizi):
    kopya_dizi = dizi.copy()

    for _ in kopya_dizi:
        for i in range(len(kopya_dizi)-1):
            if kopya_dizi[i] > kopya_dizi[i+1]:
                kopya_dizi[i], kopya_dizi[i+1] = kopya_dizi[i+1], kopya_dizi[i]

    return kopya_dizi
```

<p align="center">
  <img width="300" src="https://user-images.githubusercontent.com/31994778/124068999-306ccc80-da44-11eb-815d-47eefea4eef4.gif">
  </p>
  
  <p align="center">
  Kabarcik siralamasi animasyonu
  <p>
    
<h3>Karmasiklik</h3>

Iki tane for loop olmasindan dolayi direk O(n^2)'dir diyebiliriz.

Worst Case: O(n^2)

Best Case: O(n)'dir. Dizi egerki sirali ise, diziye bir kez girip sirali oldugunu teyit edip iterasyonu durdururuz. Toplamda n kere itere etmis oluruz.

---

<h2>Counting Sort</h2>

<b>Sayarak siralama olarak da gecer.</b> Ozel bir algoritmadir cunku zaman karmasikligini O(n)'de tutar. Fakat space karmasikligindan feragat eder. (O(n+r))

buradaki "n" dizinin buyuklugu, "r" ise sayma icin olusturulan yeni dizinin buyuklugudur.

Bu algoritma tipinde asil amacimiz dizideki sayilarin tekrar etme sayisini yine dizideki sayilarin en buyugune esit buyuklukte bir sayma listesinde tutmak ve 

<p align="center">
<img width="350" alt="Screen Shot 2021-07-01 at 11 15 55 AM" src="https://user-images.githubusercontent.com/31994778/124090682-bd704f80-da5d-11eb-841d-f5f088e34cf0.png">
</p>

```python
def counting_sort(dizi):
    kopya_dizi = dizi.copy()

    sayma_dizisi = [0 for _ in range(max(kopya_dizi)+1)]

    for i in kopya_dizi:
        sayma_dizisi[i] += 1

    # Kumulatif toplam bulma
    for i in range(1, max(kopya_dizi)+1):
        sayma_dizisi[i] += sayma_dizisi[i - 1]

    size = len(kopya_dizi)
    i = size - 1
    output = [0]*size
    while i >= 0:
        output[sayma_dizisi[kopya_dizi[i]] - 1] = kopya_dizi[i]
        sayma_dizisi[kopya_dizi[i]] -= 1
        i -= 1
    kopya_dizi = output

    return kopya_dizi
```

Anlamasi cidden zor bir algoritma. Kumulatif toplami bulmak bize sayiyi sirali dizide nereye koymamiz gerektigini bulmamiza yardimci oluyor.Eger kumulatif toplam degismiyorsa, degismeyen indexlerin sirali dizide olmayacagini soyleyebiliriz.

<h3>Karmasiklik</h3>

Zaman karmasikligi O(n)'dir cunku for donguleri ic ice degil ve maksimum n kere doner.

Yer karmasikligi O(n+r) oluyor.

---

