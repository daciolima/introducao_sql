## Comandos SQL da base Filmes para avaliação.

```sql
-- 1 Retorna todos os filmes
select * from film f 
```
```sql
-- 2 Retorna título de filmes
select title from film f 
```
```sql
-- 3 Retorna filmes com duração menor que 60
select * from film where length < 60
```
```sql
-- 4 Retorna clientes inativos
select * from customer c where active = 0
```
```sql
-- 5 Retonar endereço de clientes ativos
select first_name, last_name, address from customer c, address a where active = 1 and c.address_id = a.address_id  
```
```sql
-- 6 Retorna cliente residentes no Brasil
select first_name, a.address, co.country from customer c, address a, city ct, country co where c.address_id = a.address_id and a.city_id = ct.city_id and ct.country_id = co.country_id and co.country = 'Brazil'
```
```sql
-- 7 Retorna filmes e atores no mesmo
select f.title, a.first_name, a.last_name from film f , film_actor fa , actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id 
```
```sql
8 -- Retorna atores que atuaram no mesmo filme ordenados por título do filme
select f.title, a.first_name, a.last_name from film f , film_actor fa , actor a where f.film_id  = fa.film_id and a.actor_id = fa.actor_id order by f.title 
```
```sql
-- 9 Retorna filmes e atores que atuaram no mesmo filme ordenado por ator
select f.title, a.first_name, a.last_name from film f, film_actor fa, actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id order by a.first_name
```
```sql
-- 10 Retorna filmes de um ator específico
with var (variavel) as (values('scarlett'))
select f.title, a.first_name, a.last_name from film f, film_actor fa, actor a where f.film_id = fa.film_id and a.actor_id = fa.actor_id and a.first_name = variavel;
```
```sql
-- 11 Total de filmes
select count(*) qtd_filmes from film;
```
```sql
-- 12 Retorna média de duração dos filmes
select avg(length) from film;
```
```sql
-- 13 Retorna filmes por categorias
select f.title, c.name from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id;
```
```sql
-- 14 Retorna quantidade de filmes por categoria
select c.name, COUNT(*) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name;
```
```sql
-- 15 Retorna duração media dos filmes por categoria
select c.name, AVG(f.length) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name;
```
```sql
-- 16 Retorna quantitativo de filmes por categoria das categorias que tem quantidade de filmes inferior a 57
select c.name, COUNT(*) qtd from film f,category c, film_category fc where f.film_id = fc.film_id AND fc.category_id = c.category_id group by c.name having qtd < 50;
```
```~sql
--- 17 Retorna duração média dos filmes por categoria das categorias com menos de 57 filmes
select c.name, COUNT(*) qtd, AVG(f.length) from film f,category c, film_category fc where f.film_id = fc.film_id and fc.category_id = c.category_id group by c.name having qtd < 57;
```
```sql
-- 18 Retorna quantidade de filmes alugados por cliente
select c.first_name, c.last_name, COUNT(*) from  customer c, rental r where c.customer_id = r.customer_id group by (c.customer_id);
```
```sql
-- 19 Retorna quantidade de filmes alugados por cliente em ordem decrescente de quantidade de filmes alugados
select c.first_name, c.last_name, COUNT(*) qtd from  customer c, rental r where c.customer_id = r.customer_id group by (c.customer_id) order  by qtd desc;
```
```sql
-- 20 Retorna relação de nomes dos clientes que possuem um filme alugado no momento
select c.first_name, c.last_name from  customer c where exists (select 1 from rental r where c.customer_id = r.customer_id and r.return_date is not null);
```
```sql
-- 21 Retorna relação de nomes dos clientes que não possuem um filme alugado no momento
select c.first_name, c.last_name from  customer c where not exists (select 1 from rental r where c.customer_id = r.customer_id and r.return_date is not null);
```
### MAIS 10 CONSULTAS
```sql
-- 22 Retorna quantidade de filme que contei um determinada palavra
select count(*) qtd FROM film f WHERE description like '%Student%'
```
```sql
-- 23 Retorna todos os filmes e suas respectivas categorias onde o rate do fil é superio a 3.00
select f.title, c.name from film f, category c, film_category fc where f.rental_rate > 3.00 and f.film_id = fc.film_id and fc.category_id = c.category_id
```
```sql
-- 24 Retorna lista de atores que participaram do mesmo filme
select * from actor a inner join actor_info ai2 on a.actor_id  = ai2.actor_id where ai2.film_info like '%LORD ARIZONA%'
```
```sql
-- 25 Retorna os 10 primeiros clientes com quantia inferior a 3
select c.first_name, p.amount from customer c , payment p where c.customer_id = p.customer_id and p.amount < 3.00 limit 10
```
```sql
-- 26 Retorna atores, filmes e suas categorias dos filmes em determinada lingua
select a.first_name, f.title, c.name,  l.name from language l, film f , film_actor fa, actor a, film_category fc , category c 
where l.language_id  = f.language_id and fa.film_id = f.film_id and fc.category_id = c.category_id 
and a.actor_id = fa.actor_id and l.name like '%English%' 
```
```sql
-- 27 Retorna o numero de vezes que um determinado ator participou de um filme.
select COUNT(*) as qtd_ator_participou from film_list fl where fl.actors like '%NICK STALLONE%'
```
```sql
-- 28 Retorna quantidade de cliente de clientes de uma determinada filial
select count(*) from store s , customer c where s.store_id = c.store_id and s.store_id = 1
```
```sql
-- 29 Retorna clientes de uma determinada filial e que mora em um determinado país
select * from customer_list cl where cl.country like '%Japan%' and sid = 2
``` 
```sql
-- 30 Retorna país que mais tem clientes que alugam filme
select max(c3.country) as pais_que_mais_aluga from rental r , customer c, address a , city c2 , country c3 
where r.customer_id = c.customer_id and c.address_id = a.address_id and a.city_id = c2.city_id 
``` 
```sql
-- 31 Retorna a quantidade de filmes de Drama alugados por uma determinada cidade
select count(*) from film f , film_category fc, category c, rental r , customer c4 , address a , city c2 , country c3 
where f.film_id = fc.film_id and fc.category_id = c.category_id and c."name" like '%Drama%' and r.customer_id = c4.customer_id 
and c4.address_id = a.address_id and a.city_id = c2.city_id and c2.city like '%Juazeiro do Norte%'
```

### Diagrama ER
![plot](DIagramaER.png)
