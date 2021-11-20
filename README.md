## Comandos SQL da base Filmes para avaliação.

~~~sql
-- 1 Retorna todos os filmes
select * from film f 
~~~
~~~sql
-- 2 Retorna título de filmes
select title from film f 
~~~
~~~sql
-- 3 Retorna filmes com duração menor que 60
select * from film where length < 60
~~~
~~~sql
-- 4 Retorna clientes inativos
select * from customer c where active = 0
~~~
~~~sql
-- 5 Retonar endereço de clientes ativos
select first_name, last_name, address from customer c, address a where active = 1 and c.address_id = a.address_id  
~~~
~~~sql
-- 6 Retorna cliente residentes no Brasil
select first_name, a.address, co.country from customer c, address a, city ct, country co where c.address_id = a.address_id and a.city_id = ct.city_id and ct.country_id = co.country_id and co.country = 'Brazil'
~~~
~~~sql
-- 7 Retorna filmes e atores no mesmo
select f.title, a.first_name, a.last_name from film f , film_actor fa , actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id 
~~~
