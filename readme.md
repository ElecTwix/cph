This project has been prepared for the subject of **Database Design** of the degree of **Computer Programming** of the University of Ege, Turkey.

# Project Name: **Database Design for a University**
## Requirements for HW:
General:
- A student can have more than one meal.
- There can be more than one department in a campus.
- There can be more than one cafeteria in a campus.
- A student can have a maximum of one student number.
- A student can pay more than one tuition fee.
- A counselor has one registered campus.
- A student can have more than one absence record.
- Each student can have a maximum of one absence record for a course.
- Each student can have a maximum of one success grade from a course.
- A course can have more than one course content.
- A course content can have more than one course material.
- A course can have a maximum of one classroom.
- A campus has a single location.
- A student can have a maximum of one registration.
- Not every staff member must be a teaching assistant.
- A classroom can be found in a maximum of one campus.
- More than one course can be held in a classroom.
- A student cannot take a course if they do not renew their registration.
- A student cannot renew their registration if they do not pay tuition.
- Every counselor is a staff member.
- A course can only be given to students in the campus where it is registered.
- A course can only be given by the teaching assistant of that course.
- A student can only register for courses in the same campus.

 -----

Unfortunately, Turkish Language is a requirement for the project which caused table names and column names to be in Turkish.


## Project Standards
- Camel Case Naming Convention
- Ascii table characters

## Project Contains
- Joint Tables
- Many-to-Many Relationships
- Many-to-One Relationships
- One-to-One Relationships
- Foreign Keys
- Unique Keys

![diagram](https://raw.githubusercontent.com/ElecTwix/cph/main/diagram.png)

## Installation

1. Install PostgreSQL.

2. Create a database named "University".


3. Create Tables run script or execute the provided SQL Query.

- 3A. Execute Script inside psql
```bash
\i -d $DataBaseName -a -f init.sql
```

- 3B. Execute the Provided SQL Query.

```sql
``CREATE TABLE Kampus (
  KampusID INT IDENTITY(1,1) NOT NULL,
  KampusAdi VARCHAR(50) NOT NULL,
  Lokasyon VARCHAR(50) NOT NULL,
  CONSTRAINT PK_Kampus PRIMARY KEY (KampusID)
);

CREATE TABLE Danisman (
  DanismanID INT IDENTITY(1,1) NOT NULL,
  BolumID INT NOT NULL,
  PersonalID INT NOT NULL,
  CONSTRAINT PK_Danisman PRIMARY KEY (DanismanID),
  CONSTRAINT FK_Danisman_Bolum FOREIGN KEY (BolumID) REFERENCES Bolum (BolumID),
  CONSTRAINT FK_Danisman_Personal FOREIGN KEY (PersonalID) REFERENCES Personel (PersonalID)
);

CREATE TABLE Yemekhane (
  YemekhaneID INT IDENTITY(1,1) NOT NULL,
  KampusID INT NOT NULL,
  CONSTRAINT PK_Yemekhane PRIMARY KEY (YemekhaneID),
  CONSTRAINT FK_Yemekhane_Kampus FOREIGN KEY (KampusID) REFERENCES Kampus (KampusID)
);

CREATE TABLE Yemek (
  YemekID INT IDENTITY(1,1) NOT NULL,
  YemekhaneID INT NOT NULL,
  AnaYemek VARCHAR(50) NOT NULL,
  Corba VARCHAR(50) NOT NULL,
  GunlukEkstra VARCHAR(50) NOT NULL,
  CONSTRAINT PK_Yemek PRIMARY KEY (YemekID),
  CONSTRAINT FK_Yemek_Yemekhane FOREIGN KEY (YemekhaneID) REFERENCES Yemekhane (YemekhaneID)
);

CREATE TABLE Siparis (
  SiparisID INT IDENTITY(1,1) NOT NULL,
  OgrenciNo INT NOT NULL,
  YemekID INT NOT NULL,
  CONSTRAINT PK_Siparis PRIMARY KEY (SiparisID),
  CONSTRAINT FK_Siparis_Ogrenci FOREIGN KEY (OgrenciNo) REFERENCES OgrenciBilgi (OgrNo),
  CONSTRAINT FK_Siparis_Yemek FOREIGN KEY (YemekID) REFERENCES Yemek (YemekID)
);

CREATE TABLE Bolum (
  BolumID INT IDENTITY(1,1) NOT NULL,
  BolumAdi VARCHAR(50) NOT NULL,
  KampusID INT NOT NULL,
  CONSTRAINT PK_Bolum PRIMARY KEY (BolumID),
  CONSTRAINT FK_Bolum_Kampus FOREIGN KEY (KampusID) REFERENCES Kampus (KampusID)
);

CREATE TABLE Personel (
  PersonalID INT IDENTITY(1,1) NOT NULL,
  Ad VARCHAR(50) NOT NULL,
  Soyad VARCHAR(50) NOT NULL,
  Maas INT NOT NULL,
  Pozisyon VARCHAR(50) NOT NULL,
  KampusID INT NOT NULL,
  CONSTRAINT PK_Personel PRIMARY KEY (PersonalID),
  CONSTRAINT FK_Personel_Kampus FOREIGN KEY (KampusID) REFERENCES Kampus (KampusID)
);

CREATE TABLE OgretimGorevlisi (
  GorevliID INT IDENTITY(1,1) NOT NULL,
  DersID INT NOT NULL,
  PersonalID INT NOT NULL,
  CONSTRAINT PK_OgretimGorevlisi PRIMARY KEY (GorevliID),
  CONSTRAINT FK_OgretimGorevlisi_Ders FOREIGN KEY (DersID) REFERENCES Dersler (DersID),
  CONSTRAINT FK_OgretimGorevlisi_Personal FOREIGN KEY (PersonalID) REFERENCES Personel (PersonalID)
);

CREATE TABLE OgrenciBilgi (
  OgrNo INT IDENTITY(1,1) NOT NULL,
  OgrAdi VARCHAR(50) NOT NULL,
  OgrSoyadi VARCHAR(50) NOT NULL,
  BolumID INT NOT NULL,
  OgrenciDogumTarihi DATE NOT NULL,
  DevamID INT NOT NULL,
  DanismanID INT NOT NULL,
  KayitID INT NOT NULL,
  CONSTRAINT PK_OgrenciBilgi PRIMARY KEY (OgrNo),
  CONSTRAINT FK_OgrenciBilgi_Bolum FOREIGN KEY (BolumID) REFERENCES Bolum (BolumID),
  CONSTRAINT FK_OgrenciBilgi_Danisman FOREIGN KEY (DanismanID) REFERENCES Danisman (DanismanID)
);
```

3. Ready to go!
