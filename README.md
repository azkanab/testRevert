
# Lesson Learned in Trying Git Revert

## Kesimpulan
*yang works: branch try-revert-3 dan try-revert-5*

1. Command:
```
git revert <commit number> -m 1
```
2. Hanya berlaku di file yang berbeda, kalau file sama commit yang di atasnya akan ikut kehapus. Tapi kalau beda file commit yang di atasnya nggak ikut kehapus

## Contoh Berhasil
*lihat branch try-revert-5*

* Changes commit merge number "1A", ada 2 commit di dalamnya, 1 untuk tambahin love you dan 1 lagi untuk tambahin miss you
File A.js
```
console.log('Love you ' + A)
console.log('Miss you ' + A)
```

* Changes commit merge number "2B", ada 1 commit di dalamnya untuk tambahin miss you
File B.js
```
console.log('Miss you ' + B)
```

* Merge number "1A" duluan baru merge number "2B"

* Ketika kita
```
git revert 1A -m 1
```

Love you dan Miss you di A hilang, tapi Miss you di B nggak hilang. Jadi revertnya seolah-olah tidak menghilangkan commit yang di atasnya, yaitu 2B (kayak nggak bisa revert di tengah-tengah)

## Contoh failed
*lihat branch try-revert-4*

* Changes commit merge number "1A", ada 2 commit di dalamnya untuk tambahin Hello di file A dan file B
    * File A.js
    ```
    console.log('Hello ' + A)
    ```
    * File B.js
    ```
    console.log('Hello ' + B)
    ```

* Changes commit merge number "2B", ada 1 commit di dalamnya untuk tambahin Love you di file B
File B.js
```
console.log('Love you ' + B)
```

* Merge number "1A" duluan baru merge number "2B"

* Ketika kita
```
git revert 1A -m 1
```

Hello di file A dan B hilang, tapi Love you di B **JUGA** hilang. Karena *changesnya sama-sama di file B*. Jadi revertnya seolah-olah menghilangkan commit yang di atasnya, yaitu 2B (kayak **NGGAK** bisa revert di tengah-tengah)