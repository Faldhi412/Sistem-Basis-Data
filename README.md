# Sistem-Basis-Data
Tugas 6 (Setelah MID)

<?php
    $koneksi = mysqli_connect("localhost", "root", "", "db_family");

    if($koneksi){
        //echo "Alhamdulillah sudah terkoneksi";
    }else{
        echo "Aduh, gagal nih gan";
    }
?>
<style type="text/css">
    h1{text-align: center;}
    h2{text-align: center;}
    body{background-image: url("Gambar/bg1.jpg");}
</style>
<br><br><br><h1>Data Keluarga</h1><br>
<center><table border="1" bgcolor="">
    <thead>
        <th>No.</th>
        <th>Nama</th>
        <th>Usia</th>
        <th>Posisi</th>
        <th>Pekerjaan</th>
        <th>Hapus</th>
    </thead>
    <tbody>
        <?php
            $sqlView = "SELECT * FROM `keluarga`";
            $cekView = mysqli_query($koneksi, $sqlView);

            $nomor = 1;
            while($data = mysqli_fetch_array($cekView)){
        ?>
        <tr>
            <td align="center"><?=$nomor ?></td>
            <td align="center"><?=$data[1] ?></td>
            <td align="center"><?=$data[2] ?></td>
            <td align="center"><?=$data[3] ?></td>
            <td align="center"><?=$data[4] ?></td>
            <td><a href="index.php?id=<?=$data[0]?>">Hapus</a></td>
        </tr>
        <?php
            $nomor++; // ++ = nomor+1; 
            }
        ?>
    <!-- /end -->
    </tbody>
</table></center><br><br><br><br><br>
<h1>Masukan Data Keluarga</h1>
<form action="" method="post"><br>
<center><table border="0">
    <tr>
        <td>Nama</td>
        <td>:</td>
        <td><input type="text" name="Nama"></td>
    </tr>
    <tr>
        <td>Usia</td>
        <td>:</td>
        <td><input type="text" name="Usia"></td>
    </tr>
    <tr>
        <td>Posisi</td>
        <td>:</td>
        <td><input type="text" name="Posisi"></td>
    </tr>
    <tr>
        <td>Pekerjaan</td>
        <td>:</td>
        <td><input type="text" name="Pekerjaan"></td>
    </tr>
</table><br></center>
<center><input type="submit" name="registrasi" value="Daftarkan"></center>
</form>
<?php
    if(isset($_POST['registrasi'])){
        $sqlInput = "INSERT INTO `keluarga` (`Nama`,`Usia`,`Posisi`,`Pekerjaan`)
                VALUES ('$_POST[Nama]', '$_POST[Usia]', '$_POST[Posisi]', '$_POST[Pekerjaan]')";
        $cekInput = mysqli_query($koneksi, $sqlInput);
        if($cekInput){
            echo "<script> window.location = 'index.php' </script>";
        }else{
            echo "Data Belum Masuk";
        }
    }

    if(isset($_GET['id'])){
        $sqlDelete = "DELETE FROM `keluarga` WHERE
        `keluarga`.`id` = '$_GET[id]'";
        $cekDelete = mysqli_query($koneksi, $sqlDelete);

        if($cekDelete){
            echo "<script> window.location = 'index.php' </script>";
        }else{
            echo "Gagal Untuk Hapus Data";
        }
    }
?>
