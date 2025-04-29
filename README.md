# zadania_bazy_danych

Właściciel repozytorium: Michał Malewicz



## Rozwiązania zadań lab 1, część 1

**zadanie 1**
```sql
create table pracownik (
id int auto_increment primary key,
imie varchar(50) not null,
nazwisko varchar(100) not null,
data_urodzenia date, 
stanowisko enum('sprzedawca', 'magazynier', 'księgowa')
);
```

**zadanie 2**
```sql
#zadanie 2
insert into pracownik values
(default, 'Jan', 'Kowalski', '1990-10-10', 'magazynier'),
(default, 'Tomasz', 'Nowak', '1984-11-11', 'sprzedawca'),
(default, 'Joanna', 'Machalica', '1985-05-28', 'księgowa');
```

**zadanie 3**
```sql
create table dzial (
id int auto_increment primary key,
nazwa varchar(255) not null
);
```

**zadanie 4**

```sql
INSERT INTO dzial (nazwa) 
VALUES
('sprzedaż'),
('księgowość'),
('magazyn');
```

**zadanie 5**

```sql
ALTER TABLE pracownik 
MODIFY stanowisko ENUM('sprzedawca', 'magazynier', 'księgowa') DEFAULT 'sprzedawca';
```

**zadanie 6**

```sql
ALTER TABLE pracownik
ADD COLUMN pensja DECIMAL(7,2);

update pracownik set pensja = 5999.99 where id = 1;
update pracownik set pensja = 7000.00 where id = 2;
update pracownik set pensja = 5000.50 where id = 3;
```

**zadanie 7**

```sql
ALTER TABLE dzial RENAME COLUMN nazwa TO nazwa_dzialu;
ALTER TABLE dzial RENAME COLUMN id TO id_dzialu;
ALTER TABLE pracownik RENAME COLUMN id TO id_pracownika;
```

**zadanie 8**

```sql
DELETE FROM pracownik WHERE id_pracownika = 3;
```

## Rozwiązania zadań lab 1, część 2

**zadanie 1**

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
**zadanie 2**

```sql
create table stanowisko (
id_stanowiska int primary key,
nazwa_stanowiska varchar(100)
);
insert into stanowisko values(1, 'sprzedawca');
insert into stanowisko values(2, 'księgowa');
insert into stanowisko values(3, 'magazynier');
```
**zadanie 3**

```sql
alter table pracownik add stanowisko_temp int;
alter table pracownik add foreign key (stanowisko_temp) references stanowisko(id_stanowiska);

update pracownik set stanowisko_temp = 1 where stanowisko = 'sprzedawca';
update pracownik set stanowisko_temp = 2 where stanowisko = 'księgowa';
update pracownik set stanowisko_temp = 3 where stanowisko = 'magazynier';

alter table pracownik drop column stanowisko;
alter table pracownik rename column stanowisko_temp to stanowisko;
```
**zadanie 4**
```sql
alter table pracownik drop foreign key pracownik_ibfk_1;
alter table pracownik add foreign key (dzial) references dzial(id_dzialu) on delete set null;
```

## Rozwiązania zadań lab 2, część 1

**zadanie 1**
```sql
SELECT nazwisko, imie FROM pracownik ORDER BY nazwisko;
```

**zadanie 2**
```sql
SELECT imie, nazwisko, pensja FROM pracownik WHERE YEAR(data_urodzenia) > 1979;
```


**zadanie 3**
```sql
SELECT * FROM pracownik WHERE pensja BETWEEN 3500 AND 5000;
```
**zadanie 4**
```sql
SELECT * FROM stan_magazynowy WHERE ilosc > 10;
```

**zadanie 5**
```sql
SELECT * FROM towar WHERE nazwa_towaru LIKE 'A%' OR nazwa_towaru LIKE 'B%' OR nazwa_towaru LIKE 'C%';
```

**zadanie 6**
```sql
SELECT * FROM klient WHERE czy_firma = 0;
```

**zadanie 7**
```sql
SELECT * FROM zamowienie ORDER BY data_zamowienia DESC LIMIT 10;
```

**zadanie 8**
```sql
SELECT imie, nazwisko, pensja FROM pracownik ORDER BY pensja LIMIT 5;
```
**zadanie 9**
```sql
SELECT * FROM towar WHERE nazwa_towaru NOT LIKE '%a%' ORDER BY cena_zakupu DESC LIMIT 10;
```
**zadanie 10**
```sql
select 
towar.id_towaru,
towar.nazwa_towaru,
jednostka_miary.nazwa
from towar
inner join stan_magazynowy
on towar.id_towaru = stan_magazynowy.towar
inner join jednostka_miary
on stan_magazynowy.jm = jednostka_miary.id_jednostki
where jednostka_miary.nazwa = 'szt';
```
**zadanie 11**
```sql
create table is_malewiczm.towary_powyzej_100 AS
select *
from __firma_zti.towar
where cena_zakupu >= 100;
```

**zadanie 12**
```sql
create table is_malewiczm.pracownik_50_plus
like __firma_zti.pracownik;

insert into is_malewiczm.pracownik_50_plus
select *
from __firma_zti.pracownik
where timestampdiff (year, data_urodzenia, CURDATE()) >= 50;
```

## Rozwiązania zadań lab 2, część 2

**zadanie 1**
```sql
select p.imie, p.nazwisko, d.nazwa
from pracownik p
join dzial d on p.dzial = d.id_dzialu;
```
**zadanie 2**
```sql
select t.nazwa_towaru, k.nazwa_kategori, sm.ilosc
from towar t
join kategoria k on t.kategoria = k.id_kategori
join stan_magazynowy sm on t.id_towaru = sm.towar
order by sm.ilosc desc;
```

**zadanie 3**
```sql
select z.*, sz.nazwa_statusu_zamowienia
from zamowienie z
join status_zamowienia sz on z.status_zamowienia = sz.id_statusu_zamowienia
where sz.id_statusu_zamowienia = 6;
```

**zadanie 4**
```sql
select *
from klient k
join adres_klienta ak on k.id_klienta = ak.klient
join typ_adresu ta on ak.typ_adresu = ta.id_typu
where ta.nazwa = 'podstawowy' and ak.miejscowosc = 'Olsztyn';
```


**zadanie 5**
```sql
select jm.nazwa
from jednostka_miary jm
left join stan_magazynowy sm on jm.id_jednostki = sm.jm
where sm.jm is null;
```

**zadanie 6**
```sql
SELECT z.numer_zamowienia, t.nazwa_towaru, pz.ilosc, pz.cena
FROM zamowienie z
JOIN pozycja_zamowienia pz ON z.id_zamowienia = pz.zamowienie
JOIN towar t ON pz.towar = t.id_towaru
WHERE YEAR(z.data_zamowienia) = 2018;
```

**zadanie 7**
```sql
CREATE TABLE is_malewiczm.towary_full_info AS 
SELECT t.nazwa_towaru, t.cena_zakupu, k.nazwa_kategori AS kategoria, sm.ilosc, jm.nazwa AS jednostka_miary
FROM towar t
JOIN kategoria k ON t.kategoria = k.id_kategori
JOIN stan_magazynowy sm ON t.id_towaru = sm.towar
JOIN jednostka_miary jm ON sm.jm = jm.id_jednostki;
```
**zadanie 8**
```sql
select pz.*, z.data_zamowienia
from pozycja_zamowienia pz
join (
    select id_zamowienia, data_zamowienia
    from zamowienie
    order by data_zamowienia asc
    limit 5
) as z on pz.zamowienie = z.id_zamowienia
order by z.data_zamowienia asc, pz.zamowienie;
```
**zadanie 9**
```sql
SELECT z.*
FROM zamowienie z
JOIN status_zamowienia sz ON z.status_zamowienia = sz.id_statusu_zamowienia
WHERE sz.nazwa_statusu_zamowienia != 'zrealizowane';
```
**zadanie 10**
```sql
SELECT *
FROM adres_klienta
WHERE kod NOT REGEXP '^[0-9]{2}-[0-9]{3}';
```
## Rozwiązania zadań lab 3, część 1

**zadanie 1**

```sql
SELECT imie, nazwisko, YEAR(data_urodzenia) AS rok_urodzenia
FROM pracownik;
```

**zadanie 2**

```sql
SELECT imie, nazwisko, (YEAR(CURDATE()) - YEAR(data_urodzenia)) AS wiek
FROM pracownik;
```

**zadanie 3**

```sql
SELECT d.nazwa, COUNT(p.id_pracownika) AS liczba_pracownikow
FROM dzial d
LEFT JOIN pracownik p ON d.id_dzialu = p.dzial
GROUP BY d.nazwa;
```

**zadanie 4**
```sql
select k.nazwa_kategori, count(t.nazwa_towaru) as liczba_produktow
from kategoria k 
inner join towar t on t.kategoria=k.id_kategori 
group by k.id_kategori;
```


**zadanie 5**
```sql
SELECT k.nazwa_kategori, GROUP_CONCAT(t.nazwa_towaru ORDER BY t.nazwa_towaru SEPARATOR ', ') AS produkty
FROM kategoria k
LEFT JOIN towar t ON k.id_kategori = t.kategoria
GROUP BY k.nazwa_kategori;
```

**zadanie 6**
```sql
SELECT ROUND(AVG(pensja), 2) AS srednia_pensja
FROM pracownik;
```

**zadanie 7** 
```sql
SELECT ROUND(AVG(pensja), 2) AS srednia_pensja
FROM pracownik
WHERE TIMESTAMPDIFF(YEAR, data_zatrudnienia, CURDATE()) >= 10;
#dałem 10 lat dla sprawdzenia bo wszyscy pracują więcej niż 5 lat i wychodzi taki sam wynik jak w zadaniu 6
```
