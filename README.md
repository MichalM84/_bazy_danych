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
create table dzial (
id int auto_increment primary key,
nazwa varchar(255) not null
);
```

**zadanie 4

```sql
INSERT INTO dzial (nazwa) 
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
ALTER TABLE dzial RENAME COLUMN nazwa TO nazwa_dzialu;
ALTER TABLE dzial RENAME COLUMN id TO id_dzialu;
ALTER TABLE pracownik RENAME COLUMN id TO id_pracownika;
```

**zadanie 8

```sql
DELETE FROM pracownik WHERE id_pracownika = 3;
```

## Rozwiązania zadań lab 1, część 2

**zadanie 1

```sql
ALTER TABLE pracownik ADD COLUMN dzial INT;
ALTER TABLE pracownik ADD FOREIGN KEY (dzial) REFERENCES dzial(id_dzialu) ON DELETE RESTRICT;
UPDATE pracownik SET dzial = 1 WHERE id_pracownika = 1;
UPDATE pracownik SET dzial = 2 WHERE id_pracownika = 2;
DELETE FROM dzial WHERE id_dzialu = 1;
 ==> Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails
 (`is_malewiczm`.`pracownik`, CONSTRAINT `pracownik_ibfk_1` FOREIGN KEY (`dzial`) REFERENCES
`dzial` (`id_dzialu`) ON DELETE RESTRICT)

```
**zadanie 2

```sql

```

