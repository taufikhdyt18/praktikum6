
# Praktikum6 <img src=https://logos-download.com/wp-content/uploads/2016/05/MySQL_logo_logotype.png width="130px" >
```
NIM     : 312310576
NAMA    : TAUFIK HIDAYAT
KELAS   : TI.23.A6
MATKUL  : BASIS DATA
DOSEN   : Agung Nugroho, S.Kom., M.Kom.
```



# ERD KARYAWAN
Berikut adalah representasi Entity Relationship Diagram (ERD) berdasarkan deskripsi yang Anda berikan:

```
                 +----------------+
                 |    Departemen  |
                 +----------------+
                 | id (PK)        |
                 | nama_departemen|
                 +----------------+
                        |       ^
                        |       |
         +--------------+       +--------------+
         |                                     |
         |                                     |
+----------------+                  +-----------------+
|    Karyawan    |                  |    Proyek       |
+----------------+                  +-----------------+
| id (PK)        |                  | id (PK)         |
| nama_karyawan  |                  | nama_proyek     |
| departemen_id  |------------------| departemen_id   |
| manager_id     |                  +-----------------+
+----------------+
       |  ^
       |  |
       |  |
+--------------+
|   Supervisor |
+--------------+
| id (PK)      |
| departemen_id|
| karyawan_id  |
+--------------+
```

Pada ERD di atas, terdapat empat entitas utama yaitu "Departemen", "Karyawan", "Proyek", dan "Supervisor". Relasi antara entitas-entitas tersebut dijelaskan sebagai berikut:

1. Tabel "Karyawan" memiliki relasi many-to-one dengan tabel "Departemen". Hal ini ditunjukkan oleh atribut "departemen_id" di tabel "Karyawan" yang mengacu pada atribut "id" di tabel "Departemen".
2. Tabel "Karyawan" juga memiliki relasi many-to-one dengan tabel "Karyawan" (alias "Manager"). Ini ditunjukkan oleh atribut "manager_id" di tabel "Karyawan" yang mengacu pada atribut "id" di tabel "Karyawan" itu sendiri.
3. Tabel "Proyek" memiliki relasi many-to-one dengan tabel "Departemen". Hal ini ditunjukkan oleh atribut "departemen_id" di tabel "Proyek" yang mengacu pada atribut "id" di tabel "Departemen".
4. Terdapat tabel many-to-many "Karyawan_Proyek" yang menghubungkan karyawan dengan proyek yang sedang dikerjakan atau pernah dikerjakan. Tabel ini menghubungkan antara atribut "id" dari tabel "Karyawan" dan atribut "id" dari tabel "Proyek".
5. Tabel "Supervisor" memiliki relasi many-to-one dengan tabel "Departemen" dan tabel "Karyawan". Hal ini ditunjukkan oleh atribut "departemen_id" di tabel "Supervisor" yang mengacu pada atribut "id" di tabel "Departemen", serta atribut "karyawan_id" di tabel "Supervisor" yang mengacu pada atribut "id" di tabel "Karyawan".

ERD tersebut memberikan gambaran visual mengenai hubungan antara entitas-entitas dalam basis data yang Anda deskripsikan.


# MEMBUAT TABEL 
```SQL
-- Membuat tabel Departemen
CREATE TABLE Departemen (
  id INT PRIMARY KEY,
  nama_departemen VARCHAR(255)
);

-- Membuat tabel Karyawan
CREATE TABLE Karyawan (
  id INT PRIMARY KEY,
  nama_karyawan VARCHAR(255),
  departemen_id INT,
  manager_id INT,
  FOREIGN KEY (departemen_id) REFERENCES Departemen(id),
  FOREIGN KEY (manager_id) REFERENCES Karyawan(id)
);

-- Membuat tabel Proyek
CREATE TABLE Proyek (
  id INT PRIMARY KEY,
  nama_proyek VARCHAR(255),
  departemen_id INT,
  FOREIGN KEY (departemen_id) REFERENCES Departemen(id)
);

-- Membuat tabel Many-to-Many Karyawan_Proyek
CREATE TABLE Karyawan_Proyek (
  karyawan_id INT,
  proyek_id INT,
  PRIMARY KEY (karyawan_id, proyek_id),
  FOREIGN KEY (karyawan_id) REFERENCES Karyawan(id),
  FOREIGN KEY (proyek_id) REFERENCES Proyek(id)
);

-- Membuat tabel Supervisor
CREATE TABLE Supervisor (
  id INT PRIMARY KEY,
  departemen_id INT,
  karyawan_id INT,
  FOREIGN KEY (departemen_id) REFERENCES Departemen(id),
  FOREIGN KEY (karyawan_id) REFERENCES Karyawan(id)
);
```


Setelah tabel-tabel terbuat, Anda dapat menggunakan perintah SQL untuk menghubungkan tabel-tabel tersebut. Berikut ini adalah contoh kode program untuk membuat hubungan antar tabel:

1. Menambahkan karyawan ke departemen:
```sql
-- Contoh data pada tabel Departemen
INSERT INTO Departemen (id, nama_departemen) VALUES (1, 'Departemen A');
INSERT INTO Departemen (id, nama_departemen) VALUES (2, 'Departemen B');

-- Contoh data pada tabel Karyawan
INSERT INTO Karyawan (id, nama_karyawan, departemen_id, manager_id) VALUES (1, 'Karyawan A', 1, 2);
INSERT INTO Karyawan (id, nama_karyawan, departemen_id, manager_id) VALUES (2, 'Karyawan B', 1, NULL);
INSERT INTO Karyawan (id, nama_karyawan, departemen_id, manager_id) VALUES (3, 'Karyawan C', 2, NULL);
```

2. Menambahkan proyek ke departemen:
```sql
-- Contoh data pada tabel Proyek
INSERT INTO Proyek (id, nama_proyek, departemen_id) VALUES (1, 'Proyek A', 1);
INSERT INTO Proyek (id, nama_proyek, departemen_id) VALUES (2, 'Proyek B', 1);
INSERT INTO Proyek (id, nama_proyek, departemen_id) VALUES (3, 'Proyek C', 2);
```

3. Menghubungkan karyawan dengan proyek pada tabel Many-to-Many Karyawan_Proyek:
```sql
-- Contoh data pada tabel Karyawan_Proyek
INSERT INTO Karyawan_Proyek (karyawan_id, proyek_id) VALUES (1, 1);
INSERT INTO Karyawan_Proyek (karyawan_id, proyek_id) VALUES (1, 2);
INSERT INTO Karyawan_Proyek (karyawan_id, proyek_id) VALUES (2, 1);
INSERT INTO Karyawan_Proyek (karyawan_id, pro

yek_id) VALUES (3, 3);
```

Dengan menggunakan kode program di atas, Anda dapat membuat tabel-tabel dan menghubungkannya sesuai dengan deskripsi yang Anda berikan. Pastikan untuk menyesuaikan data yang ingin Anda masukkan ke dalam tabel sesuai kebutuhan Anda.

## SELESAI 
