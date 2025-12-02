# lab8web
Nama: Ahmad Ibnu Abdillah
NIM: 312410489
# Kode dan Dokumentasi
```
<?php
$host = "localhost";
$user = "root";
$pass = "";
$db = "latihan1";
$conn = mysqli_connect($host, $user, $pass, $db);
if ($conn == false)
{
 echo "Koneksi ke server gagal.";
 die();
} #else echo "Koneksi berhasil";
?>

```
```
<meta charset="UTF-8">
 <link href="style.css" rel="stylesheet" type="text/css" />
 <title>Data Barang</title>
</head>
<body>
 <div class="container">
 <h1>Data Barang</h1>
 <div class="main">
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
 <td><img src="gambar/<?= $row['gambar'];?>" alt="<?=
$row['nama'];?>"></td>
 <td><?= $row['nama'];?></td>
 <td><?= $row['kategori'];?></td>
 <td><?= $row['harga_beli'];?></td>
 <td><?= $row['harga_jual'];?></td>
 <td><?= $row['stok'];?></td>
 <td><?= $row['id_barang'];?></td>
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
```
![img](https://github.com/AhmadIbnuAbdillah/img8/blob/8d55f618d7eb98d65109c04e69be46a6f2988593/Screenshot%202025-12-02%20221145.png)
```
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
 $sql = 'INSERT INTO data_barang (nama, kategori,harga_jual, harga_beli,
stok, gambar) ';
 $sql .= "VALUE ('{$nama}', '{$kategori}','{$harga_jual}',
'{$harga_beli}', '{$stok}', '{$gambar}')";
 $result = mysqli_query($conn, $sql);
 header('location: index.php');
}
```
![img](https://github.com/AhmadIbnuAbdillah/img8/blob/8d55f618d7eb98d65109c04e69be46a6f2988593/Screenshot%202025-12-02%20221205.png)
```
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
 $sql .= "harga_jual = '{$harga_jual}', harga_beli = '{$harga_beli}', stok
= '{$stok}' ";
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
```
![img](https://github.com/AhmadIbnuAbdillah/img8/blob/8d55f618d7eb98d65109c04e69be46a6f2988593/Screenshot%202025-12-02%20221222.png)
```
<?php
include_once 'koneksi.php';
$id = $_GET['id'];
$sql = "DELETE FROM data_barang WHERE id_barang = '{$id}'";
$result = mysqli_query($conn, $sql);
header('location: index.php');
?>
```
![img](https://github.com/AhmadIbnuAbdillah/img8/blob/8d55f618d7eb98d65109c04e69be46a6f2988593/Screenshot%202025-12-02%20221255.png)
