# 题目一
展示电影ID为2116这部电影各年龄段的平均影评分
```
select u.age as age, avg(r.rate) as avgrate from hive_sql_test1.t_rating r, hive_sql_test1.t_user u 
where r.movieid=2116 and u.userid = r.userid group by u.age
或者
select u.age as age, avg(r.rate) as avgrate from hive_sql_test1.t_rating r join hive_sql_test1.t_user u on (r.userid = u.userid) 
where r.movieid = 2116 group by u.age
```
![8d8d992aa8ea80bf43f2f216b6414d9](https://user-images.githubusercontent.com/4209803/128467212-a9af857b-cc1f-464f-9baf-27caa100b495.png)



# 题目二
找出男性评分最高且评分次数超过50次的10部电影，展示电影名，平均影评分和评分次数
```
select * from (select sex, name, avg(e.rate) as rate,  count(*) as total from 
(select u.sex as sex, m.moviename as name, r.rate as rate from hive_sql_test1.t_rating r, hive_sql_test1.t_user u, hive_sql_test1.t_movie m 
where u.sex='M' and u.userid = r.userid and r.movieid = m.movieid) e group by sex,name order by rate desc) x where x.total > 50 limit 10;
```
![af1bd9933a795337526057c37e16350](https://user-images.githubusercontent.com/4209803/128467186-b3be14c8-0fd4-4b77-a2a7-bf427ba14cea.png)

