# 문제 
-- ALLEN과 같은 달에 입사한 직원들에게 월급의 10%를 보너스로 지급하려고 한다.
-- 조회내용
-- ename, sal, hiremonth, bonus


select ename, sal, hiremonth from emp
where month(hiredat) 
in (select month(hiredate) from emp where ename = 'ALLEN');
-- 
SELECT
    ename,
    sal,
    MONTH(hiredate) AS hiremonth,
    sal * 0.1 AS bonus 
FROM
    emp
WHERE
    MONTH(hiredate) = (
        SELECT MONTH(hiredate) FROM emp WHERE ename = 'ALLEN'
    );
    
-- 오늘 날짜를 기준으로 가장 오래 근무한 사원 5명을 조회한다
-- 근무년이 40년 이상이면 보너스를 (근속년수 * 100) 지급
-- 근무년이 43년 이상이면 보너스를 (근속년수 * 200) 지급
-- 근무년이 45년 이상이면 보너스를 (근속년수 * 300) 지급
-- ename, years, bonus     
   
select ename, year(curdate())-year(hiredate) as years,
	case
		when year(curdate())-year(hiredate) >= 40 then (year(curdate())-year(hiredate)) *100
		when year(curdate())-year(hiredate) >= 40 then (year(curdate())-year(hiredate)) *200
		when year(curdate())-year(hiredate) >= 40 then (year(curdate())-year(hiredate)) *300
		else 0
	end as bonus
from emp
order by years desc limit 5;


-- 오늘 날짜를 기준으로 입사일 기준으로 가장 오래 근무한 직원들 8명의
-- 근무한 월을 조회하시오

SELECT ename, hiredate,
    TIMESTAMPDIFF(MONTH, hiredate, CURRENT_DATE()) AS worked_months
FROM emp
ORDER BY hiredate ASC LIMIT 8;

    
    
    
    