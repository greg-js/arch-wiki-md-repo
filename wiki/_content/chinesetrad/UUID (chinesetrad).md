UUID是"Universally Unique IDentifier"(通用唯一識別碼)的縮寫。

UUID的目的是能在分散式計算系統(distributed systems)在沒有中心調整下有唯一的標示資訊。因此，任何人都可以創造UUID並且用來辨識，並不需要擔心其他人不小心用到相同的UUID。

一個UUID是由16位元組(128位元)組成的數字。因此，理論上可用的UUID有216*8 = 2128 = 25616 或是大約 3.4 × 1038這樣的多。如果在每奈秒(1e-9秒)製造一兆個UUID，也需要百億年才能用完所有的UUID。

UUID包含了32個十六進位數字，並且用"-"分隔成五組，分別是8, 4, 4, 4, 12。 例:`550e8400-e29b-41d4-a716-446655440000`

## 取得磁碟裝置的UUID

有兩種方式取的磁碟裝置的UUID

```
# blkid

```

或

```
# ls -l /dev/disk/by-uuid

```

## 相關資訊

[Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")

## 參考資料

*   [Wikipedia's Article on *Universally Unique Identifier*](https://en.wikipedia.org/wiki/Universally_Unique_Identifier "wikipedia:Universally Unique Identifier")
*   [維基百科](http://zh.wikipedia.org/wiki/Uuid)