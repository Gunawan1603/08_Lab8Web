# 08_Lab8Web

TUGAS PERTEMUAN 10

PEMROGRAMAN WEB

TEKNIK INFORMATIKA

UNIVERSITAS PELITA BANGSA

NAMA  : GUNAWAN

NIM   : 312010191

KELAS : TI.20.B1

DOSEN : Agung Nugroho,S.Kom.,M.Kom

# Pemrograman Web: PHP dan Database MySQL

**Instruksi Praktikum**<br>
1. Persiapkan text editor misalnya VSCode.
2. Buat folder baru dengan nama lab8_php_database pada docroot webserver 
(htdocs)<br>
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.<br>
**Langkah-langkah Praktikum**<br>
**Persiapan :**<br>
Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah 
database server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan 
melalui XAMPP.<br>
**Menjalankan MySQL Server**<br>
Untuk menjalankan MySQL Server dari menu XAMPP Contol.
![08_Lab8Web](Gambar/01.Gambar_XAMPP_Control.jpg)

Gambar 01. XAMPP Control

**Mengakses MySQL Client menggunakan PHP MyAdmin**<br>
Pastikan webserver Apache dan MySQL server sudah dijalankan. Kemudian buka 
melalui browser: http://localhost/phpmyadmin/

**Membuat Database: Studi Kasus Data Barang**
![08_Lab8Web](Gambar/29.Gambar_Tabel_data_barang.jpg)

**Membuat Database**

~~~
CREATE DATABASE latihan 1;
~~~
![08_Lab8Web](Gambar/02.Gambar_CREATE_DATABASE_Latihan1.jpg)

**Membuat Tabel**<br>
~~~
CREATE TABLE data_barang (
 id_barang int(10) auto_increment Primary Key,
 kategori varchar(30),
 nama varchar(30),
 gambar varchar(100),
 harga_beli decimal(10,0),
 harga_jual decimal(10,0),
 stok int(4)
);
~~~
![08_Lab8Web](Gambar/03.Gambar_Code_CREATE_TABLE_data_barang.jpg)

Gambar 02.Tampilan phpMyAdmin

**Menambahkan Data**<br>
~~~
INSERT INTO data_barang (kategori, nama, gambar, harga_beli, harga_jual, stok)
VALUES ('Elektronik', 'HP Samsung Android', 'hp_samsung.jpg', 2000000, 2400000, 5),
('Elektronik', 'HP Xiaomi Android', 'hp_xiaomi.jpg', 1000000, 1400000, 5),
('Elektronik', 'HP OPPO Android', 'hp_oppo.jpg', 1800000, 2300000, 5);
~~~
![08_Lab8Web](Gambar/04.Gambar_Code_Menambahkan_Data.jpg)

![08_Lab8Web](Gambar/05.Gambar_Tampilan_Data_Barang.jpg)

![08_Lab8Web](Gambar/06.Gambar_Print_Tampilan_Data_Barang.jpg)
Gambar 03.Tampilan Data Barang

**Membuat Program CRUD**<br>
Buat folder lab8_php_database pada root directory web server (D:\xampp\htdocs)

![08_Lab8Web](Gambar/07.Gambar_Directory_Lab8.jpg)

Gambar 04. Directory Lab8

Kemudian untuk mengakses direktory tersebut pada web server dengan mengakses URL: 
http://localhost/lab8_php_database/

![08_Lab8Web](Gambar/08.Gambar_Tampilan_Web.jpg)

Gambar 04. Tampilan Web

**Membuat file koneksi database**<br>
Buat file baru dengan nama **koneksi.php**<br>
~~~
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan 1";
$conn = mysqli_connect($host, $user, $pass, $db);
if ($conn == false)
{
 echo "Koneksi ke server gagal.";
 die();
} #else echo "Koneksi berhasil";
?>
~~~
![08_Lab8Web](Gambar/09.Gambar_Code_file_koneksi_database.jpg)

Gambar 05. Code file koneksi database

Buka melalui browser untuk menguji koneksi database (untuk menyampilkan pesan 
koneksi berhasil, **uncomment** pada perintah **echo “koneksi berhasil”;**

http://localhost/lab8_php_database/koneksi.php

![08_Lab8Web](Gambar/10.Gambar_Tampilan_tes_Koneksi.jpg)

Gambar 06. Tampilan tes Koneksi

**Membuat file index untuk menampilkan data (Read)**<br>
Buat file baru dengan nama **index.php**
~~~
<?php
include("koneksi.php");

// query untuk menampilkan data
$sql = 'SELECT * FROM data_barang';
$result = mysqli_query($conn, $sql);

?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Data Barang</title>
</head>
<body>
    <div class="container">
        <h1>Data Barang</h1>
        <div class="main">
            <a href="tambah.php">Tambah Barang</a>
            <table>
            <tr>
                <th>Gambar</th>
                <th>Nama Barang</th>
                <th>Katagori</th>
                <th>Harga Jual</th>
                <th>Harga Beli</th>
                <th>Stok</th>
                <th>Aksi</th>
            </tr>
            <?php if($result): ?>
            <?php while($row = mysqli_fetch_array($result)): ?>
            <tr>
                <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=$row['nama'];?>"></td>
                <td><?= $row['nama'];?></td>
                <td><?= $row['kategori'];?></td>
                <td><?= $row['harga_jual'];?></td>
                <td><?= $row['harga_beli'];?></td>
                <td><?= $row['stok'];?></td>
                <td>
                    <a href="ubah.php?id=<?= $row['id_barang'];?>">Ubah</a>
                    <a href="hapus.php?id=<?= $row['id_barang'];?>">Hapus</a> 
                </td>
            </tr>
            <?php endwhile; else: ?>
            <tr>
                <td colspan="7">Belum ada data</td>
            </tr>
            <?php endif; ?>
            </table>
        </div>
    </div>
</body>
</html>
~~~

![08_Lab8Web](Gambar/11.Gambar_Code_index_menampilkan_data.jpg)
![08_Lab8Web](Gambar/11.Gambar_Code_index_menampilkan_data1.jpg)

Gambar 07. Code index menampilkan data

Buka melalui browser 
http://localhost/lab8_php_database/

![08_Lab8Web](Gambar/12.Gambar_Tampilan_index.jpg)

Gambar 08. Tampilan index

**Menambah Data (Create)**
Buat file baru dengan nama **tambah.php**
~~~
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_',$file_gambar['name']);
        $destination = dirname(__FILE__) .'/gambar/' . $filename;
        if(move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }
    
    $sql = 'INSERT INTO data_barang (nama, kategori, harga_jual, harga_beli, stok, gambar) ';
    $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}','{$harga_beli}', '{$stok}', '{$gambar}')";
    $result = mysqli_query($conn, $sql);
    header('location: index.php');
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Tambah Barang</title>
</head>
<body>
<div class="container">
    <h1>Tambah Barang</h1>
    <div class="main">
        <form method="post" action="tambah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" style="margin-left: 20px;" />
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;" >
                    <option value="Komputer">Komputer</option>
                    <option value="Elektronik">Elektronik</option>
                    <option value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" style="margin-left: 40px;" />
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" style="margin-left: 43px;" />
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" style="margin-left: 85px;" />
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>
</body>
</html>
~~~
![08_Lab8Web](Gambar/13.Gambar_Code_Menambah_Data.jpg)
![08_Lab8Web](Gambar/14.Gambar_Code_Menambah_Data1.jpg)
![08_Lab8Web](Gambar/15.Gambar_Code_Menambah_Data2.jpg)

Gambar 09. Code Menambah Data

Buka melalui browser 
http://localhost/lab8_php_database/tambah.php

![08_Lab8Web](Gambar/16.Gambar_Tampilan_Menambah_Data.jpg)

![08_Lab8Web](Gambar/17.Gambar_Tampilan_Menambah_Data1.jpg)

![08_Lab8Web](Gambar/18.Gambar_Tampilan_Menambah_Data2.jpg)

Gambar 10. Tampilan Menambah Barang

**Mengubah Data (Update)**<br>
Buat file baru dengan nama **ubah.php**<br>
~~~
<?php
error_reporting(E_ALL);
include_once 'koneksi.php';

if (isset($_POST['submit']))
{
    $id = $_POST['id'];
    $nama = $_POST['nama'];
    $kategori = $_POST['kategori'];
    $harga_jual = $_POST['harga_jual'];
    $harga_beli = $_POST['harga_beli'];
    $stok = $_POST['stok'];
    $file_gambar = $_FILES['file_gambar'];
    $gambar = null;

    if ($file_gambar['error'] == 0)
    {
        $filename = str_replace(' ', '_', $file_gambar['name']);
        $destination = dirname(__FILE__) . '/gambar/' . $filename;
        if (move_uploaded_file($file_gambar['tmp_name'], $destination))
        {
            $gambar = 'gambar/' . $filename;;
        }
    }

    $sql = 'UPDATE data_barang SET ';
    $sql .= "nama = '{$nama}', kategori = '{$kategori}', ";
    $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok = '{$stok}' ";
    if (!empty($gambar))
        $sql .= ", gambar = '{$gambar}' ";
    $sql .= "WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);

    header('location: index.php');
    }

    $id = $_GET['id'];
    $sql = "SELECT * FROM data_barang WHERE id_barang = '{$id}'";
    $result = mysqli_query($conn, $sql);
    if (!$result) die('Error: Data tidak tersedia');
    $data = mysqli_fetch_array($result);

    function is_select($var, $val) {
        if ($var == $val) return 'selected="selected"';
        return false;
}
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <link href="style.css" rel="stylesheet" type="text/css" />
    <title>Ubah Barang</title>
</head>
<body>
<div class="container">
    <h1>Ubah Barang</h1>
    <div class="main">
        <form method="post" action="ubah.php" enctype="multipart/form-data">
            <div class="input">
                <label>Nama Barang</label>
                <input type="text" name="nama" value="<?php echo $data['nama'];?>" style="margin-left: 20px;"/>
            </div>
            <div class="input">
                <label>Kategori</label>
                <select name="kategori" style="margin-left: 58px;">
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Komputer">Komputer</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Elektronik">Elektronik</option>
                    <option <?php echo is_select ('Komputer', $data['kategori']);?> value="Hand Phone">Hand Phone</option>
                </select>
            </div>
            <div class="input">
                <label>Harga Jual</label>
                <input type="text" name="harga_jual" value="<?php echo $data['harga_jual'];?>" style="margin-left: 40px;"/>
            </div>
            <div class="input">
                <label>Harga Beli</label>
                <input type="text" name="harga_beli" value="<?php echo $data['harga_beli'];?>" style="margin-left: 43px;"/>
            </div>
            <div class="input">
                <label>Stok</label>
                <input type="text" name="stok" value="<?php echo $data['stok'];?>" style="margin-left: 85px;"/>
            </div>
            <div class="input">
                <label>File Gambar</label>
                <input type="file" name="file_gambar" />
            </div>
            <div class="submit">
                <input type="hidden" name="id" value="<?php echo $data['id_barang'];?>" />
                    <input type="submit" name="submit" value="Simpan" />
            </div>
        </form>
    </div>
</div>
</body>
</html>
~~~
![08_Lab8Web](Gambar/19.Gambar_Code_Ubah_Data.jpg)
![08_Lab8Web](Gambar/20.Gambar_Code_Ubah_Data1.jpg)
![08_Lab8Web](Gambar/21.Gambar_Code_Ubah_Data2.jpg)
![08_Lab8Web](Gambar/22.Gambar_Code_Ubah_Data3.jpg)

Gambar 11. Code Ubah Data

Buka melalui browser 
http://localhost/lab8_php_database/

**Tampilan Sebelum**

![08_Lab8Web](Gambar/23.Gambar_Tampilan_Ubah_Data.jpg)

![08_Lab8Web](Gambar/24.Gambar_Tampilan_Ubah_Data1.jpg)

**Tampilan Sesudah**

![08_Lab8Web](Gambar/25.Gambar_Tampilan_Ubah_Data2.jpg)

Gambar 12. Tampilan Ubah Data Barang

**Menghapus Data (Delete)**<br>
Buat file baru dengan nama **hapus.php**
~~~
<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: index.php');
?>
~~~
![08_Lab8Web](Gambar/26.Gambar_Code_Hapus_Data.jpg)

Gambar 13. Code Hapus Data

Buka melalui browser 
http://localhost/lab8_php_database/index.php

**Tampilan Sebelum**

![08_Lab8Web](Gambar/27.Gambar_Tampilan_Hapus_Data.jpg)

**Tampilan Sesudah**

![08_Lab8Web](Gambar/28.Gambar_Tampilan_Hapus_Data1.jpg)

Gambar 14. Tampilan Hapus Data Barang

Cukup Sekian Penjelasan Dari Saya

**TERIMAKASIH**


