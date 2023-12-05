# Tugas3-BigData


## Membuat Resource Azure Synapse Workspace
Sebelumnya, Azure Synapse Workspace digunakan pada tugas ini untuk analisis sederhana. lalu kita akan membuat Resource Azure Synapse Workspace dengan mengisi :
Subscription: Memilih Azure Subscription yang ada diakun azure.
Resource Group: memilih Resource group tempat dari penyimpanan kita.
Region: Memilih wilayah kita (contohnya Southeast Asia).
Select Data Lake Storage Gen2: Memilih From Subscription.
Account Name: Memilih akun dari azure kita.
Setelah itu kita klik Review + Create dan menunggu deploy dari Azure Synapse Workspace

## Menggunakan Synapse Studio untuk Analisis Sederhana
1. Buka terlebih dahulu Synapse Studio.
2. Buat SQL script dan jalankan query ini untuk melihat isi dari file tersebut
   ```
   SELECT
    TOP 100 *
  FROM
    OPENROWSET(
        BULK 'https://bigdatafauzanariq.dfs.core.windows.net/coba/On_Time_Reporting_Carrier_On_Time_Performance_(1987_present)_2016_1.csv',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0'
    ) AS [result]
   ```

