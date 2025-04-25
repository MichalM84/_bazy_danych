# _bazy_danych

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
imie varchar(255) not null
);
```

**zadanie 4

```

```

