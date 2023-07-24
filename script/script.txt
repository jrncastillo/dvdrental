-- Aquellas usadas para insertar, modificar y eliminar un Customer, Staff y Actor.
insert into customer (store_id, first_name, last_name, email, address_id , active)
values (1, 'Carlos', 'Garcia', 'cgarcia@gmail.com', 12, 1)

insert into staff (first_name, last_name, address_id, email, store_id , username, password, picture)
values ('Gabriel', 'Balboltin', 3, 'gbalboltin@gmail.com', 1, 'gabbal', '1122334455', null)

insert into actor (first_name, last_name)
values ('Drab', 'Tipp')


update customer 
set email = 'carlosg@gmail.com'
where email = 'cgarcia@gmail.com'

update staff 
set password = '8bGtdfR35ki56HJyu'
where email = 'gbalboltin@gmail.com'

update actor 
set last_name = 'Ttip'
where first_name = 'Drab'


delete from customer 
where email = 'carlosg@gmail.com'

delete from staff 
where email = 'gbalboltin@gmail.com'

delete from actor 
where first_name = 'Drab' and last_name = 'Ttip'


-- Listar todas las “rental” con los datos del “customer” dado un año y mes.
select rental_id, customer.first_name, customer.last_name, customer.email 
from customer
join rental
on customer.customer_id = rental.customer_id 
where to_char(rental_date,'YYYY') = '2005' and to_char(rental_date,'MM') = '06'

-- Listar Número, Fecha (payment_date) y Total (amount) de todas las “payment”.
select payment_id , payment_date, amount
from payment p

-- Listar todas las “film” del año 2006 que contengan un (rental_rate) mayor a 4.0.
select title, rental_rate
from film
where release_year = 2006 and rental_rate > 4

-- Realiza un Diccionario de datos que contenga el nombre de las tablas y columnas,
-- si éstas pueden ser nulas, y su tipo de dato correspondiente.
SELECT
    t1.TABLE_NAME AS tabla_nombre,
    t1.COLUMN_NAME AS columna_nombre,
    t1.COLUMN_DEFAULT AS columna_defecto,
    t1.IS_NULLABLE AS columna_nulo,
    t1.DATA_TYPE AS columna_tipo_dato,
    COALESCE(t1.NUMERIC_PRECISION,
    t1.CHARACTER_MAXIMUM_LENGTH) AS columna_longitud,
    PG_CATALOG.COL_DESCRIPTION(t2.OID,
    t1.DTD_IDENTIFIER::int) AS columna_descripcion,
    t1.DOMAIN_NAME AS columna_dominio
FROM 
    INFORMATION_SCHEMA.COLUMNS t1
    INNER JOIN PG_CLASS t2 ON (t2.RELNAME = t1.TABLE_NAME)
WHERE 
    t1.TABLE_SCHEMA = 'public'
ORDER BY
    t1.TABLE_NAME;