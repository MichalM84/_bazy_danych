# zadania_bazy_danych

Właściciel repozytorium: Michał Malewicz



## Rozwiązania zadań lab 1, część 1

** zadanie 1**
```sql
create table pracownik (
id int auto_increment primary key,
imie varchar(50) not null,
nazwisko varchar(100) not null,
data_urodzenia date, 
stanowisko enum('sprzedawca', 'magazynier', 'księgowa')
);
```

** zadanie 2**
```sql
#zadanie 2
INSERT INTO pracownik values
(default, 'Jan', 'Kowalski', '1990-10-10', 'magazynier'),
(default, 'Tomasz', 'Nowak', '1984-11-11', 'sprzedawca'),
(default, 'Joanna', 'Machalica', '1985-05-28', 'księgowa');
```

** zadanie 3
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

** zadanie 7

```sql
ALTER TABLE dzial RENAME COLUMN nazwa TO nazwa_dzialu;
ALTER TABLE dzial RENAME COLUMN id TO id_dzialu;
ALTER TABLE pracownik RENAME COLUMN id TO id_pracownika;
```

** zadanie 8

```sql
DELETE FROM pracownik WHERE id_pracownika = 3;
```

## Rozwiązania zadań lab 1, część 2

** zadanie 1

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
** zadanie 2

```sql
create table stanowisko (
id_stanowiska int primary key,
nazwa_stanowiska varchar(100)
);
insert into stanowisko values(1, 'sprzedawca');
insert into stanowisko values(2, 'księgowa');
insert into stanowisko values(3, 'magazynier');
```
** zadanie 3

```sql
alter table pracownik add stanowisko_temp int;
alter table pracownik add foreign key (stanowisko_temp) references stanowisko(id_stanowiska);

update pracownik set stanowisko_temp = 1 where stanowisko = 'sprzedawca';
update pracownik set stanowisko_temp = 2 where stanowisko = 'księgowa';
update pracownik set stanowisko_temp = 3 where stanowisko = 'magazynier';

alter table pracownik drop column stanowisko;
alter table pracownik rename column stanowisko_temp to stanowisko;
```
** zadanie 4
```sql
alter table pracownik drop foreign key pracownik_ibfk_1;
alter table pracownik add foreign key (dzial) references dzial(id_dzialu) on delete set null;
```

## Rozwiązania zadań lab 2, część 1

** zadanie 1
```sql
SELECT nazwisko, imie FROM pracownik ORDER BY nazwisko;
```

** zadanie 2
```
SELECT imie, nazwisko, pensja FROM pracownik WHERE YEAR(data_urodzenia) > 1979;
```


** zadanie 3
```

```






