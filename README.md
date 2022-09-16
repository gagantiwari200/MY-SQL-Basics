# MY SQL Aggregate Function

Create database if not exists inueron;
use inueron;

create table bank_details(
age int,
job varchar(30),
Marital varchar(30),
education varchar(30),
`default` varchar(30),
balance int,
housing varchar(30),
loan varchar(30),
contact varchar(30),
`day` int,
`month`varchar(30),
duration int,
campaign int,
pdays int,
previous int,
poutcome varchar(40),
y varchar(30));
drop table bank_details;
select * from bank_details;

insert into bank_details values(21,"Acountatnt","Single","tertiary","no","1000",214368952,"no","unknown",5,"may",261,1,-1,0,"unknown","no"),
(36,"machenic","Single","tertiary","no","900",21436895,"yes","unknown",5,"may",263,1,-1,0,"unknown","no"),
(23,"Accountant","Single","tertiary","no","800",21436895,"yes","unknown",5,"may",264,1,-1,0,"unknown","no"),
(60,"Blue colour","Married","tertiary","no","400",21436895,"no","unknown",5,"may",264,1,-1,0,"unknown","no"),
(54,"Admin","tertiary","Married","no","800",21436895,"yes","unknown",5,"may",264,1,-1,0,"unknown","no"),
(60,"Blue colour","Married","tertiary","no","900",21436895,"no","unknown",5,"may",264,1,-1,0,"unknown","no"),
(30,"Admin","tertiary","Single","no","550",21436895,"no","unknown",5,"may",264,1,-1,0,"unknown","no"),
(45,"Corporate","Married","tertiary","no","300",21436895,"yes","unknown",5,"may",264,1,-1,0,"unknown","no"),
(59,"Field agent","Married","tertiary","no","1000",21436895,"no","unknown",5,"may",264,1,-1,0,"unknown","no"),
(64,"Office boy","Married","tertiary","no","220",21436895,"yes","unknown",5,"may",264,1,-1,0,"unknown","no"),
(39,"pramoters","Married","tertiary","no","2000",21436895,"no","unknown",5,"may",264,1,-1,0,"unknown","no"),
(40,"machenic","Married","tertiary","no","600",21436895,"yes","unknown",5,"may",263,1,-1,0,"unknown","no");


select count(*) from bank_details;

select * from bank_details;

select age , loan , job from bank_details;

select `default` from bank_details;

select * from bank_details limit 5;

select * from bank_details where age = 24;

select * from bank_details where age = 60;

select * from bank_details	where age = 60 AND job = 'retired';

select * from bank_details where education = ('unknown' or marital = 'single') and balance < 500; 

drop table bank_details;

select distinct job from bank_details;

select * from bank_details order by age desc;


select * from bank_details;

select avg(balance) from bank_details;
select * from bank_details order by balance limit 1;
select * from bank_details order by balance;
select * , min(balance) from bank_details;
select * from bank_details where balance in(select min(balance) from bank_details);
select * from bank_details where balance = (select min(balance) minbalance from bank_details);
select * from bank_details where balance in(select max(balance) from bank_details);
select * from bank_details where balance = (select max(balance) minbalance from bank_details);
select * from bank_details order by balance desc limit	1;

select * from bank_details;
select * from bank_details where loan = 'yes';
select avg(balance) from bank_details where job = 'admin';
select avg(balance) from bank_details where job = 'corporate';
select * from bank_details where job = 'unknown' and age>45;
select * from bank_details where education = 'primary' and job ='unknown';
select * from bank_details where balance < 0;
select * from bank_details where housing = 'NO';
select balance , houseing from bank_details where housing = 'no';

select * from bank_details;
DELIMITER &&
Create procedure GT()
BEGIN
select * from bank_details;
END &&

call GT()

DELIMITER &&
Create procedure bal_max()
BEGIN
select * from bank_details where balance in(select max(balance) from bank_details);
END &&

call bal_max();

DELIMITER &&
Create procedure avg_bal_job_role1(IN `admin` varchar(30))
BEGIN
select avg(balance) from bank_details where job = 'admin';
END &&


call avg_bal_job_role1('admin');


DELIMITER &&
Create procedure avg_bal_job_role2(IN retired varchar(30))
BEGIN
     select avg(balance) from bank_details where job = 'retired';
END &&

call avg_bal_job_role2('retired');

 
call avg_bal_job_role2('unknown');



DELIMITER &&
Create procedure sel_edu_job1(in v1 varchar(30) , in v2 varchar(30) )
BEGIN
      select * from bank_details where education = v1 and job = v2;
END &&

call sel_edu_job1('tertiary' , 'retired');

create view bank_view as select age , job , marital , balance , education from bank_details;


SELECT * FROM inueron.bank_view; 

select avg(balance) from bank_view where job = 'admin';

