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

<h2>Shell Sort</h2>

<b>Siralamadan cok bir iyilestirme yontemidir.</b>

Shell sort bir baska siralama algoritmasiyla birlikte kullanilir (Ben sadece selection sort ile kullanildigini gordum). Duzensiz bir diziyi tamamen siralamaz fakat daha duzenli bir sekle sokar, bu da birlikte kullanildigi siralama algoritmasinin isini kolaylastirir ve zaman karmasikligini azaltir.

```python
def shell_sort(dizi):
    kopya_dizi = dizi.copy()
    aralik = len(dizi) // 2

    while aralik > 0:

        for i in range(aralik, len(dizi)):

            temp = kopya_dizi[i]

            j = i

            while j >= aralik and kopya_dizi[j - aralik] > temp:
                kopya_dizi[j], kopya_dizi[j -
                                          aralik] = kopya_dizi[j-aralik], kopya_dizi[j]
                j -= aralik

        aralik //= 2

    return kopya_dizi
```

<h3>Karmasiklik</h3>

Worst case: O(n^2)

Best Case: O(n log n)

---

<h2>Heap Sort</h2>

Yigin siralamasi olarak da gecer. Siralama stilimizin minimumdan maksimuma olmasini istersek min heap kullanmamiz gerekir.

Yapilmasi gereken islemler:

- root'daki(en kucuk) degeri silip baska bir listeye ekle.
- min heapify uygula.
- tekrar root'daki degeri silip baska bir listeye ekle.
- tekrar min heapify uygula.

Bu islem min heap'de eleman kalmayana kadar uygulanir. 

<h3>Karmasiklik</h3>

Heap'deki eleman sayisini N olarak dusunursek ve eleman kalmayincaya kadar islem uygulamamiz gerektigi icin N gelir. Min heapify islemini uygulamak icin de log N adima ihtiyac duyariz (agacin derinliginden dolayi). Sonuc olarak <b>N * log N</b> karmasikligimiz olur.

```python
# Python program for implementation of heap Sort

# To heapify subtree rooted at index i.
# n is size of heap

def heapify(arr, n, i):
    largest = i  # Initialize largest as root
    l = 2 * i + 1     # left = 2*i + 1
    r = 2 * i + 2     # right = 2*i + 2

    # See if left child of root exists and is
    # greater than root
    if l < n and arr[largest] < arr[l]:
        largest = l

    # See if right child of root exists and is
    # greater than root
    if r < n and arr[largest] < arr[r]:
        largest = r

    # Change root, if needed
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]  # swap

        # Heapify the root.
        heapify(arr, n, largest)

# The main function to sort an array of given size


def heapSort(arr):
    n = len(arr)

    # Build a maxheap.
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)

    # One by one extract elements
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]  # swap
        heapify(arr, i, 0)
```

<p align="center">
  <img src="https://user-images.githubusercontent.com/31994778/124230253-6a5ad300-db17-11eb-9799-e44bd544ddb1.gif">
  </p>

---

<h2>Merge Sort</h2>

Birlestirme siralamasi olarak da gecer. Bu siralamanin en onemli ozelligi "Divide and Conquer" yani "Parcala ve Fethet" metodunu uygulamasidir.

<b>Burada, siralanmamis bir diziyi kucuk parcalara boluyoruz, her parcayi kendi icinde siraliyoruz, ve siralanmis parcalari birlestiriyoruz.</b>

<p align="center">
  <img width="350" alt="merge_sort" src="https://user-images.githubusercontent.com/31994778/124182817-0eb12b00-dac0-11eb-8d48-f4f6d5977f27.png">
  </p>

```python
def merge_sort(dizi):

    if len(dizi) > 1:
        orta = len(dizi) // 2
        sol_dizi = dizi[:orta]
        sag_dizi = dizi[orta:]

        merge_sort(sol_dizi)
        merge_sort(sag_dizi)
        merge(dizi, sol_dizi, sag_dizi)

    return dizi


def merge(dizi, sol_dizi, sag_dizi):
    i = 0
    j = 0
    k = 0

    while i < len(sol_dizi) and j < len(sag_dizi):
        if sol_dizi[i] > sag_dizi[j]:
            dizi[k] = sag_dizi[j]
            j += 1
        else:
            dizi[k] = sol_dizi[i]
            i += 1
        k += 1

    while i < len(sol_dizi):
        dizi[k] = sol_dizi[i]
        i += 1
        k += 1

    while j < len(sag_dizi):
        dizi[k] = sag_dizi[j]
        j += 1
        k += 1

    return dizi
```

<h3>Karmasiklik</h3>

<h4>Zaman</h4>
Averaj: O(N * log N)

<b><i>N, dizinin buyuklugudur. Burada, birlestirme isleminde N tane elemani siralayacagimiz ve toplamda log N adimda bu islemi yapacagimiz icin O(N * log N) ifadesi olur. Log N ifadesi, diziyi kac adimda en kucuk parcalarina bolebilecegimizi ifade eder. Mesela 8 elemanli bir dizi 3 adimda, log2 (8), en kucuk parcalarina bolunmus olur.</b></i>

<h4>Yer</h4>

O(N)

---

<h2>Quick Sort</h2>

<b>Hizli siralama</b> olarak da gecer. Taktigi dizi icerisinden ilk elemani pivot olarak alip, geri kalan elemanlari pivot ile karsilastirarak kucuk olanlari pivotun soluna, buyuk olanlari sagina atar. Soldaki dizide kalanlar arasindan tekrar bir pivot secilir ve kucukler soluna, buyukler sagina atilir. Sagdaki dizi icin de ayni islem yapilir. Bu islemler rekursif olarak tekrarlanir ve kucuk gruplar tekrardan birlestirilerek ilk dizi, bu sefer sirali sekilde, olusturulur.

<p align="center">
  <img width = "350" src="https://user-images.githubusercontent.com/31994778/124248785-df380800-db2b-11eb-9f1b-47b638e9fbf8.gif">
  </p>
  
 ```python
def partition(start, end, array):

    # Initializing pivot's index to start
    pivot_index = start
    pivot = array[pivot_index]

    # This loop runs till start pointer crosses
    # end pointer, and when it does we swap the
    # pivot with element on end pointer
    while start < end:

        # Increment the start pointer till it finds an
        # element greater than  pivot
        while start < len(array) and array[start] <= pivot:
            start += 1

        # Decrement the end pointer till it finds an
        # element less than pivot
        while array[end] > pivot:
            end -= 1

        # If start and end have not crossed each other,
        # swap the numbers on start and end
        if(start < end):
            array[start], array[end] = array[end], array[start]

    # Swap pivot element with element on end pointer.
    # This puts pivot on its correct sorted place.
    array[end], array[pivot_index] = array[pivot_index], array[end]

    # Returning end pointer to divide the array into 2
    return end

# The main function that implements QuickSort


def quick_sort(start, end, array):

    if (start < end):

        # p is partitioning index, array[p]
        # is at right place
        p = partition(start, end, array)

        # Sort elements before partition
        # and after partition
        quick_sort(start, p - 1, array)
        quick_sort(p + 1, end, array)

    return array

```

<b>Burada pivotu random secmek, dizinin ilk elemani secmekten daha iyidir, cunku worst case'de dizi zaten sirali verilmis olur ve surekli bir sonraki elemani pivot olarak secersek karmasiklik O(n^2) olur.</b>

<h3>Karmasiklik</h3>

Worst Case: O(n^2)

Best Case: O(N * log N)

<b>Quick sort, merge ve heap sort'dan genelde daha hizlidir. Ek olarak, Quick sort bir in-place sorting algoritmasi, yani extra array olusturmayan, bir algoritma oldugu icin, space karmasikligi merge sort'dan daha avantajlidir.</b>
