# _bazy_danych

Właściciel repozytorium: Michał Malewicz

1. Nagłówki

# Nagłówek poziomu 1 (H1)
## Nagłówek poziomu 1 (H2)
### Nagłówek poziomu 1 (H3)
#### Nagłówek poziomu 1 (H4)
##### Nagłówek poziomu 1 (H5)
###### Nagłówek poziomu 6 (H6)

2. Listy

1. Element1
2. Element2
   1. Element 2.1
  
3. Lista wypunktowana

* punkt 1
* punkt 2
  * punkt 2.1

#Przykładowy format zapisywania rozwiązań

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

...



