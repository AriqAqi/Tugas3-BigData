# Tugas3-BigData
## Azure Data Lake Storage Gen2 Setup
Repositori ini menyediakan panduan langkah demi langkah untuk menyiapkan akun penyimpanan yang dapat digunakan dengan Azure Data Lake Storage Gen2. Ikuti langkah-langkah di bawah untuk membuat akun penyimpanan dengan namespace hierarki dan mengaktifkan kemampuan Data Lake Storage.

## langkah-langkah
### 1. Buat Akun Penyimpanan
-Buka portal Azure.
-Navigasi ke halaman "Create a resource."
-Pada tab "Basics," pilih jenis akun antara dua opsi. Untuk kemampuan Data Lake Storage Gen2, pilih akun blok blob premium. Pilih "Premium" dan dalam dropdown "Premium account type," pilih "Block blobs."

![image](https://github.com/AriqAqi/Tugas3-BigData/assets/84063377/8e88bdfe-0195-4999-b87f-906533a80372)

-Di tab "Advanced," aktifkan pengaturan namespace hierarki.

![image](https://github.com/AriqAqi/Tugas3-BigData/assets/84063377/c2d70b71-7a09-4678-a7d0-96c7a771a81e)

### 2. Salin Data Sumber ke Akun Penyimpanan
-Buka akun penyimpanan baru Anda di portal Azure.
-Pilih "Storage browser" -> "Blob containers" -> "Add container" dan buat kontainer baru dengan nama data.
-Di browser penyimpanan, unggah data  ke dalam kontainer data.
![Screenshot 2023-12-05 153831](https://github.com/AriqAqi/Tugas3-BigData/assets/84063377/9cb67155-84f0-4cad-a22c-3858badf0517)

## Membuat Resource Azure Synapse Workspace
Sebelumnya, Azure Synapse Workspace digunakan pada tugas ini untuk analisis sederhana. lalu kita akan membuat Resource Azure Synapse Workspace dengan mengisi :
-Subscription: Memilih Azure Subscription yang ada diakun azure.
-Resource Group: memilih Resource group tempat dari penyimpanan kita.
-Region: Memilih wilayah kita (contohnya Southeast Asia).
-Select Data Lake Storage Gen2: Memilih From Subscription.
-Account Name: Memilih akun dari azure kita.
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
- SELECT TOP 100 * untuk memilih 100 baris pertama.
- FROM OPENROWSET untuk membaca data dari sumber eksternal.
- BULK untuk menentukan sumber data dari eksternal.
- FORMAT = 'CSV' untuk menentukan bahwa data yang dibaca adalah dalam format CSV.
- PARSER_VERSION = '2.0' adalah versi parser yang digunakan untuk membaca data.

3. Membuat query untuk analisis sederhana
      ```
   SELECT
    C16, COUNT(*) AS Banyaknya
   FROM
    OPENROWSET(
        BULK 'https://bigdatafauzanariq.dfs.core.windows.net/coba/On_Time_Reporting_Carrier_On_Time_Performance_(1987_present)_2016_1.csv',
        FORMAT = 'CSV',
        PARSER_VERSION = '2.0'
    ) AS [result]
      GROUP BY C16
   ```
   ![image](https://github.com/AriqAqi/Tugas3-BigData/assets/115605338/ea7c05f0-7c6e-4f39-b9a9-cd42af4080e6)
   
   Berikut output dari hasil query yang diatas, yang menghitung setiap OriginCityName disetiap data yang ada.
