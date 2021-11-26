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
~~~sql
8 -- Retorna atores que atuaram no mesmo filme ordenados por título do filme
select f.title, a.first_name, a.last_name from film f , film_actor fa , actor a where f.film_id  = fa.film_id and a.actor_id = fa.actor_id order by f.title 
~~~
~~~sql
-- 9 Retorna filmes e atores que atuaram no mesmo filme ordenado por ator
select f.title, a.first_name, a.last_name from film f, film_actor fa, actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id order by a.first_name
~~~
~~~sql
-- 10 Retorna filmes de um ator específico
with var (variavel) as (values('scarlett'))
select f.title, a.first_name, a.last_name from film f, film_actor fa, actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id and a.first_name = variavel;
~~~
~~~sql
-- 11 Total de filmes
select count(*) qtd_filmes from film;
~~~
~~~sql
-- 12 Retorna média de duração dos filmes
select avg(length) from film;
~~~
~~~sql
-- 13 Retorna filmes por categorias
select f.title, c.name from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id;
~~~
~~~sql
-- 14 Retorna quantidade de filmes por categoria
select c.name, COUNT(*) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name;
~~~
~~~sql
-- 15 Retorna duração media dos filmes por categoria
select c.name, AVG(f.length) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name;
~~~
~~~sql
-- 16 Retorna quantitativo de filmes por categoria das categorias que tem quantidade de filmes inferior a 57
select c.name, COUNT(*) qtd from film f,category c, film_category fc where f.film_id = fc.film_id AND fc.category_id = c.category_id group by c.name having qtd < 50;
~~~
~~~sql
--- 17 Retorna duração média dos filmes por categoria das categorias com menos de 57 filmes
select c.name, COUNT(*) qtd, AVG(f.length) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name having qtd < 57;
~~~
~~~sql
-- 18 Retorna quantidade de filmes alugados por cliente
select c.first_name, c.last_name, COUNT(*) from  customer c, rental r where c.customer_id = r.customer_id group by (c.customer_id);
~~~
~~~sql
-- 19 Retorna quantidade de filmes alugados por cliente em ordem decrescente de quantidade de filmes alugados
select c.first_name, c.last_name, COUNT(*) qtd from  customer c, rental r where c.customer_id = r.customer_id group by (c.customer_id) order  by qtd desc;
~~~
~~~sql
-- 20 Retorna relação de nomes dos clientes que possuem um filme alugado no momento
select c.first_name, c.last_name from  customer c where exists (select 1 from rental r where c.customer_id = r.customer_id and r.return_date is not null);
~~~
~~~sql
-- 21 Retorna relação de nomes dos clientes que não possuem um filme alugado no momento
select c.first_name, c.last_name from  customer c where not exists (select 1 from rental r where c.customer_id = r.customer_id and r.return_date is not null);
~~~
