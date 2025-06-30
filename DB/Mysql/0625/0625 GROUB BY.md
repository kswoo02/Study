-- GROUP BY
-- 직원수를 조회하시오
select count(*) from emp;

-- 부서별 직원수
select deptno, count(*) from emp group by deptno;

-- 년도별 직원수 1980,1981만 조회
select year(hiredate), count(*) from emp 
where year(hiredate) in (1980, 1981) group by year(hiredate)


-- 입사월별 직원수 조회
-- 2명 이상인 월만 조회 
select month(hiredate), count(*) from emp 
where month(hiredate) in (3,4)
group by month(hiredate)
having count(*) >=2 ;

-- 부서별 월급의 평균을 구하시오
select deptno, avg(sal), sum(sal), min(sal), max(sal) from emp
group by deptno;

-- job 별 근속 연수의 평균을 구하시오
select job, avg(year(curdate()) - year(hiredate)) from emp 
group by job

-- ALLEN이 속한 부서의 직원들 월급의 최대보다 많이 받는 직원조회
select ename, deptno, sal from emp
where sal > (select max(sal) from emp where deptno = (SELECT deptno FROM emp WHERE ename = 'ALLEN'));

select * from emp
where sal > ALL (select sal from emp
where deptno in (select deptno from emp where ename = 'ALLEN'));

-- group by
SELECT ename, deptno, sal FROM emp
WHERE sal > (
    SELECT MAX(sal)
    FROM emp
    WHERE deptno = (SELECT deptno FROM emp WHERE ename = 'ALLEN')
    GROUP BY deptno
);


-- 
select deptno, avg(year(curdate())-year(hiredate)) as avg_year
from emp
group by deptno
having avg_year > (select avg(year(curdate())-year(hiredate)) from emp
where deptno in (select deptno from emp 
where ename = "SCOTT"));

--
select avg(year(curdate())-year(hiredate)) from emp
where deptno in (select deptno from emp 
where ename = "SCOTT");


-- 별별 부서별, job 별 월급의 평균
select deptno, job, count(*), avg(sal) from emp group by deptno, job;

select count(distinct job) from emp;

select deptno, job, avg(sal) from emp
where deptno in(10,20)
group by deptno, job
with rollup
order by deptno;
-- -------------------------------------

select * from (
	select ename, sal,
	case
		when sal <= 1000 then 'low'
		when sal <= 2000 then 'mid'
		when sal <= 3000 then 'high'
		else 'none'
	end as level
	from emp
) e where e.level in ('low','high');


-- 직원들의 월급평균과 월급의 차를 구하시오

select avg(sal) from emp;
select ename,(select avg(sal) from emp) - sal from emp;
-- 
SELECT ename, sal,
    (SELECT ROUND(AVG(sal), 2) FROM emp) AS overall_avg_sal,
	sal - (SELECT AVG(sal) FROM emp) AS difference
FROM
    emp;
    
-- 각 부서의 평균 월급보다 많이 받는 직원을 조회하시오
select ename, sal from emp 
select deptno, avg(sal) from emp group by deptno;
(select ename, avg(sal) from emp) - sal from emp;

SELECT ename, sal, deptno FROM emp e1
WHERE e1.sal > (SELECT AVG(sal)
FROM emp e2 WHERE e2.deptno = e1.deptno);

-- 각 부서의 평균을 구한다
select * from(
	select deptno, avg(sal) as avg_sal,
		case
			when avg(sal) <= 1500 then '하위'
			when avg(sal) <= 2000 then '중위'
			else 0
		end as grade
	from emp group by deptno) e where e.grade = '중위';


