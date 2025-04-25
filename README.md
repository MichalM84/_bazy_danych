# zadania_bazy_danych

Właściciel repozytorium: Michał Malewicz



## Rozwiązania zadań lab 1, część 1

**Zadanie 1**
```sql
create table pracownik (
id int auto_increment primary key,
imie varchar(50) not null,
nazwisko varchar(100) not null,
data_urodzenia date, 
stanowisko enum('sprzedawca', 'magazynier', 'księgowa')
);
```

**Zadanie 2**
```sql
#zadanie 2
INSERT INTO pracownik values
(default, 'Jan', 'Kowalski', '1990-10-10', 'magazynier'),
(default, 'Tomasz', 'Nowak', '1984-11-11', 'sprzedawca'),
(default, 'Joanna', 'Machalica', '1985-05-28', 'księgowa');
```

**zadanie 3
```sql
create table dział (
id int auto_increment primary key,
nazwa varchar(255) not null
);
```

**zadanie 4

```sql
INSERT INTO dział (nazwa) 
VALUES
('sprzedaż'),
('księgowość'),
('magazyn');
```

**zadanie 5

```sql
ALTER TABLE pracownik 
MODIFY stanowisko ENUM('sprzedawca', 'magazynier', 'księgowa') DEFAULT 'sprzedawca';
```

**zadanie 6

```sql
ALTER TABLE pracownik
ADD COLUMN pensja DECIMAL(7,2);

update pracownik set pensja = 5999.99 where id = 1;
update pracownik set pensja = 7000.00 where id = 2;
update pracownik set pensja = 5000.50 where id = 3;
```

**zadanie 7

```sql
ALTER TABLE dział RENAME COLUMN nazwa TO nazwa_dzialu;
ALTER TABLE dział RENAME COLUMN id TO id_dzialu;
ALTER TABLE pracownik RENAME COLUMN id TO id_pracownika;
```

**zadanie 8

```sql
DELETE FROM pracownik WHERE id_pracownika = 3;
```

## Rozwiązania zadań lab 1, część 2

**zadanie 1

```sql

```


