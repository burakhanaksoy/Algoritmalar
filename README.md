<h1>Algoritmalar</h1>

<h2>Binary Search</h2>

`Sirali bir dizide, diziye ortadan girip aranan rakami log2(n) karmasikliginda bulmamizi saglar`

Buradaki "n", dizideki elemen sayisidir.

```python
def binary_search(aranan_no, dizi):
  yuksek_nokta = len(dizi) - 1
  dusuk_nokta = 0
  konum = (yuksek_nokta + dusuk_nokta) / 2
  
  while(yuksek_nokta >= dusuk_nokta):
    if dizi[konum] == aranan_no:
      return True
    elif dizi[konum] > aranan_no:
      yuksek_nokta = konum
    else:
      dusuk_nokta = konum
    
    konum = (yuksek_nokta + dusuk_nokta) / 2
   
   return False
```

<h3>Karmasiklik</h3>

Binary search O(log2(N))'de calisir. Bu da demek oluyor ki, linear search'un worst case'inden(O(n)) cok cok daha iyidir, best case'inden O(log(1))'den kotudur.

<b>Ortalamadan O(n/2) ise cok cok daha iyidir</b>

<p align="center">

</p>
