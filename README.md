## Comandos SQL da base Filmes para avaliação.

~~~sql
-- Retorna todos os filmes
select * from film f 
~~~

~~~sql
-- Retorna título de filmes
select title from film f 
~~~

~~~sql
-- Retorna filmes com duração menor que 60
select * from film where length < 60
~~~

~~~sql
-- Retorna clientes inativos
select * from customer c where active = 0
~~~

~~~sql
-- Retonar endereço de clientes ativos
select first_name, last_name, address from customer c, address a where active = 1 and c.address_id = a.address_id  
~~~

~~~sql
-- Retorna cliente residentes no Brasil
select first_name, a.address, co.country from customer c, address a, city ct, country co where c.address_id = a.address_id and a.city_id = ct.city_id and ct.country_id = co.country_id and co.country = 'Brazil'
~~~
