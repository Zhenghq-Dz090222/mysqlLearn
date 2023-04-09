##本单元目标
	一、为什么要学习数据库
	二、数据库的相关概念      
		DBMS、DB、SQL
	三、数据库存储数据的特点
	四、初始MySQL
		MySQL产品的介绍        
		MySQL产品的安装          ★        
		MySQL服务的启动和停止     ★
		MySQL服务的登录和退出     ★      
		MySQL的常见命令和语法规范      
	五、DQL语言的学习   ★              
		基础查询        ★             
		条件查询  	   ★			
		排序查询  	   ★				
		常见函数        ★               
		分组函数        ★              
		分组查询		   ★			
		连接查询	 	★			
		子查询       √                  
		分页查询       ★              
		union联合查询	√			
		
	六、DML语言的学习    ★             
		插入语句						
		修改语句						
		删除语句						
	七、DDL语言的学习  
		库和表的管理	 √				
		常见数据类型介绍  √          
		常见约束  	  √			
	八、TCL语言的学习
		事务和事务处理                 
	九、视图的讲解           √
	十、变量                      
	十一、存储过程和函数   
	十二、流程控制结构       

##数据库的好处
	1.持久化数据到本地
	2.可以实现结构化查询，方便管理
	


##数据库相关概念
	1、DB：数据库，保存一组有组织的数据的容器
	2、DBMS：数据库管理系统，又称为数据库软件（产品），用于管理DB中的数据
	3、SQL:结构化查询语言，用于和DBMS通信的语言

##数据库存储数据的特点
	1、将数据放到表中，表再放到库中
	2、一个数据库中可以有多个表，每个表都有一个的名字，用来标识自己。表名具有唯一性。
	3、表具有一些特性，这些特性定义了数据在表中如何存储，类似java中 “类”的设计。
	4、表由列组成，我们也称为字段。所有表都是由一个或多个列组成的，每一列类似java 中的”属性”
	5、表中的数据是按行存储的，每一行类似于java中的“对象”。



##MySQL产品的介绍和安装

###MySQL服务的启动和停止
	方式一：计算机——右击管理——服务
	方式二：通过管理员身份运行
	net start 服务名（启动服务）
	net stop 服务名（停止服务）


###MySQL服务的登录和退出   
	方式一：通过mysql自带的客户端
	只限于root用户

	方式二：通过windows自带的客户端
	登录：
	mysql 【-h主机名 -P端口号 】-u用户名 -p密码

	退出：
	exit或ctrl+C


	
	
	
###MySQL的常见命令 

	1.查看当前所有的数据库
	show databases;
	2.打开指定的库
	use 库名
	3.查看当前库的所有表
	show tables;
	4.查看其它库的所有表
	show tables from 库名;
	5.创建表
	create table 表名(

		列名 列类型,
		列名 列类型，
		。。。
	);
	6.查看表结构
	desc 表名;


	7.查看服务器的版本
	方式一：登录到mysql服务端
	select version();
	方式二：没有登录到mysql服务端
	mysql --version
	或
	mysql --V



###MySQL的语法规范
	1.不区分大小写,但建议关键字大写，表名、列名小写
	2.每条命令最好用分号结尾
	3.每条命令根据需要，可以进行缩进 或换行
	4.注释
		单行注释：#注释文字
		单行注释：-- 注释文字
		多行注释：/* 注释文字  */
	
	
	


###SQL的语言分类
	DQL（Data Query Language）：数据查询语言
		select 
	DML(Data Manipulate Language):数据操作语言
		insert 、update、delete
	DDL（Data Define Languge）：数据定义语言
		create、drop、alter
	TCL（Transaction Control Language）：事务控制语言
		commit、rollback
	



###SQL的常见命令

	show databases； 查看所有的数据库
	use 库名； 打开指定 的库
	show tables ; 显示库中的所有表
	show tables from 库名;显示指定库中的所有表
	create table 表名(
		字段名 字段类型,	
		字段名 字段类型
	); 创建表

	desc 表名; 查看指定表的结构
	select * from 表名;显示表中的所有数据



##DQL语言的学习
###进阶1：基础查询
	语法：
	SELECT 要查询的东西
	【FROM 表名】;

	类似于Java中 :System.out.println(要打印的东西);
	特点：
	1、要查询的东西可以是：表中的字段、常量值、表达式、函数
	2、通过select查询完的结果 ，是一个虚拟的表格，不是真实存在
	
	#1、查询表中的单个字段
	SELECT last_name FROM employees;

	#2、查询表中的多个字段
	SELECT last_name,salary,email FROM employees;	

	#3、查询表中的所有字段
	SELECT * FROM employees;

	#4、查询常量值。注意字符型和日期型的常量必须用单引号引起来，数值型不需要。
	SELECT 100;
	SELECT 'john';

	#5、查询表达式
	SELECT 100*98;

	#6、查询函数
	SELECT VERSION();

	#7、起别名
	/*
	①便于理解
	②如果要查询的字段有重名的情况，使用别名可以区分开来
	*/
	#方式一：式显写出关键字AS
	SELECT 100%98 AS 结果;
	SELECT last_name AS 姓,first_name AS 名 FROM employees;

	#方式二：隐藏关键字AS，使用空格
	SELECT last_name 姓,first_name 名 FROM employees;
	无论使用哪一种方式起别名，若别名中包含空格或者是#等特殊字符，必须将别名用双引号包裹，例如
	SELECT salary AS "out put" FROM employees;

	#8、去重。在字段前添加关键字DISTINCT
	SELECT DISTINCT department_id FROM employees;
	#9、+号的作用仅仅只有一个功能就是运算符。若+运算符的左右两边有一方为字符型，mysql会试图将字符型转换为数值型。如果转换失败则将字符型数值转换成0。特别的若一方为null，则结果一定为null
	#案例：查询员工名和姓连接成一个字段，显示为 姓名
	SELECT last_name+first_name AS 姓名 FROM employees;  /*错误的查询*/
	SELECT CONCAT(last_name,first_name) AS 姓名 FROM employees; 	/*正确的查询，CONCAT函数用于将字符拼接*/




###进阶2：条件查询
	条件查询：根据条件过滤原始表的数据，查询到想要的数据。语句内的执行顺序是先执行from语句，然后执行where语句，最后才是执行select语句
	语法：
	select 
		要查询的字段|表达式|常量值|函数
	from 
		表
	where 
		条件(若该条件为字段，则该字段必须在表中存在) ;

	分类：
	一、按条件表达式筛选
		示例：salary>10000
		简单条件运算符：
		> < >= <= = != <>
	
	二、按逻辑表达式筛选，逻辑运算符的作用是连接条件表达式
		示例：salary>10000 && salary<20000
	
		逻辑运算符：
		
		and（&&）:两个条件如果同时成立，结果为true，否则为false
		or(||)：两个条件只要有一个成立，结果为true，否则为false
		not(!)：如果条件成立，则not后为false，否则为true

	三、模糊查询
	模糊查询涉及到的关键字有like，between and，in，is null，is not null
	#1、like一般和通配符搭配使用。通配符%表示0个或多个字符，通配符_表示一个字符
	案例1：查询员工名中包含字母a的员工信息。
	SELECT * FROM employees WHERE last_name LIKE '%a%';
	案例2：查询员工名中第三个字符为e，第五个字符为a的员工名和工资
	SELECT last_name,salary FROM employees WHERE last_name LIKE '__l_d%';
	案例3：查询员工名中第二个字符为_的员工名。可以使用转义字符
	SELECT last_name FROM employees WHERE last_name like '_\_%';
	
	#3、in的用法在条件查询中判断某字段的值是否属于in列表中的某一项，列表中的值类型必须统一。	案例：查询员工的工种编号是IT_PROG、AD_VP、AD_PRES中的一个员工名和工种编号
	SELECT last_name,job_id FROM employees WHERE job_id IN('IT_PROG','AD_VP','AD_PRES');

	#4、is null的用法。在mysql中=不能用于判断null，所以涉及到null值判断的，都必须使用is null或者is not null。
	案例：查询没有奖金的员工名和奖金率
	SELECT last_name,commission_pct FROM employees WHERE is null;
	
	
	
###进阶3：排序查询	
	
	语法：
	select
		要查询的东西
	from
		表
	where 
		条件
	order by 排序的字段|表达式|函数|别名 【asc|desc】
	asc 表示的是升序，是默认的。desc是降序，需要显式的写出
	
	#6、按多个字段排序
	案例：查询员工信息，要求先按工资升序，再按员工编号降序
	SELECT * FROM employees ORDER BY salary ASC,department_id DESC;
	
	
###进阶4：常见函数
	一、单行函数
	1、字符函数
		concat拼接
		substr截取子串
		upper转换成大写
		lower转换成小写
		trim去前后指定的空格和字符
		ltrim去左边空格
		rtrim去右边空格
		replace替换
		lpad左填充
		rpad右填充
		instr返回子串第一次出现的索引
		length 获取字节个数
		
	2、数学函数
		round 四舍五入
		rand 随机数
		floor向下取整
		ceil向上取整
		mod取余
		truncate截断
	3、日期函数
		now当前系统日期+时间
		curdate当前系统日期，不包含时间
		curtime当前系统时间，不包含日期
		str_to_date 将字符转换成日期
		date_format将日期转换成字符
	4、流程控制函数
		1.if()函数有3个参数，等价于C语言中的三目运算符，用于 处理双分支。
		
		2.case函数的使用一：类似switch case 的效果
			case 要判断的字段或表达式
			when 常量1 then 要显示的值1或语句1；
			when 常量2 then 要显示的值2或语句2；
			...
			else 要显示的值n或语句n;
			end
		
			case的实例如下：
			SELECT salary 原始工资,department_id,
			CASE department_id
			WHEN 30 THEN salary*1.1;
			WHEN 40 THEN salary*1.2;
			WHEN 50 THEN salary*1.3;
			ELSE salary
			END AS 新工资
			from employees;
		
		3.case函数的使用二：类似多重if 
			case 
			when 条件1 then 要显示的值1或语句1；
			when 条件2 then 要显示的值2或语句2；
			...
			else 要显示的值n或语句n;
			end
			
			实例如下：
			SELECT salary,
			CASE
			WHEN salary>20000 THEN 'A'
			WHEN salary>15000 THEN 'B'
			WHEN salary>10000 THEN 'C'
			ELSE 'D'
			END AS 工资级别
			FROM employees;
			
	5、其他函数
		version版本
		database当前库
		user当前连接用户



	二、统计函数
	功能：用作统计使用，又称为聚合函数或分组函数或组函数。有如下几类：
		sum() 求和。当参数为null时，不参与运算，即忽略null值
		max() 最大值。当参数为null时，不参与运算，即忽略null值
		min() 最小值。当参数为null时，不参与运算，即忽略null值
		avg() 平均值。当参数为null时，不参与运算，即忽略null值
		count() 计数。只计算不为null的个数。
		和以上各分组函数一同查询的字段要求是group by后的字段
		特点：
		1、以上五个分组函数都忽略null值，除了count(*)
		2、sum和avg一般用于处理数值型
		   max、min、count可以处理任何数据类型
	    3、都可以搭配distinct使用，用于统计去重后的结果
		4、count的参数可以支持：
			字段、*、常量值，一般放1
	
		   建议使用 count(*)进行统计总行数
		案例：
			SELECT SUM(salary) AS 和,AVG(salary) AS 平均,MAX(salary) AS 最高,MIN(salary) AS 最低,COUNT(salary) 个数 FROM employees;
		
		案例：和distinct搭配
			SELECT SUM(DISTINCT salary),SUM(salary) FROM employees;
			SELECT COUNT(DISTINCT salary),COUNT(salary) FROM employees;
			
			
			
##进阶5：分组查询
	语法：
		select 统计函数,查询的列(要求该列出现在group by的后面)
		from 表
		【where 筛选条件】
		group by 分组的字段(或者是表达式或者是函数),分组的字段(或者是表达式或者是函数)
		【order by子句】
	注意：
		查询列表必须特殊，要求是统计函数和group by 后出现的字段。
	
	特点：
	1、可以按单个字段分组
	2、和分组函数一同查询的字段最好是分组后的字段
	3、分组筛选
					针对的表		位置			关键字
	分组前筛选：	原始表			group by的前面		where
	分组后筛选：	分组后的结果集	group by的后面		having
	统计函数作为分组条件肯定是放在having子句中。能用分组前筛选的，优先考虑分组前筛选，这有利于提升性能。
	4、可以按多个字段分组，字段之间用逗号隔开
	5、可以支持排序


	#案例1：查询每个工种的最高工资
	分析：看到"每个XX"，就以每个之后的字段为分组依据
	SELECT MAX(salary),job_id FROM employees GROUP BY job_id; 
	
	#案例2：查询每个位置上的部门个数
	SELECT COUNT(*),location_id FROM departments GROUP BY location_id;
	
	#案例3：查询邮箱中包含a字符的每个部门的平均工资
	SELECT AVG(salary),department_id FROM employees WHERE email LIKE "%a%" GROUP BY department_id;
	
	#案例4：查询有奖金的每个领导手下员工的最高工资
	SELECT MAX(salary),manager_id FROM employees WHERE commission_pct IS NOT NULL GROUP BY manager_id;
	
	案例5：查询哪个部门的员工个数大于2
	分析：先查询每个部门的员工个数，然后根据前面的结果进行筛选，查询哪个部门的员工个数大于2
	SELECT COUNT(*),department_id FROM employees GROUP BY department_id HAVING COUNT(*)>2;
	
	案例6：查询每个工种有奖金的员工的最高工资>12000的工种编号和最高工资
	SELECT MAX(salary),job_id FROM employees WHERE commission_pct IS NOT NULL GROUP BY job_id HAVING MAX(salary)>12000;
	
	案例7：查询领导编号>102的每个领导手下的员工最低工资>5000的领导编号	分析：①先查询每个领导手下的员工最低工资，即生成的表的列应该包含manager_id，MIN(salary)这2列，故而需要以manager_id为分组条件进行分组查询
	SELECT manager_id,MIN(salary) FROM employees GROUP BY manager_id;
		  ②添加筛选条件：编号>102。因为编号在原始表中就有，所以采用where子句进行筛选
    SELECT manager_id,MIN(salary) FROM employees WHERE manager_id>102 GROUP BY manager_id;
		  ③继续添加筛选条件：最低工资大于5000。因为最低工资并不在原始表中，所以需要在HAVING子句中对条件进行筛选故而需要以manager_id为分组条件进行分组查询，
		  然后在此次查询的基础上筛选MIN(salary)大于5000的manager_id。
	SELECT manager_id,MIN(salary) FROM employees WHERE manager_id>102 GROUP BY manager_id HAVING MIN(salary)>5000;

	案例：按员工姓名的长度分组，查询每一组的员工个数，筛选员工个数>5的有哪些
	SELECT COUNT(*),LENGTH(last_name) len_name FROM employees GROUP BY LENGTH(last_name) HAVING COUNT(*)>5;
	
	案例：查询每个部门每个工种的员工的平均工资
	分析：该查询是按多个字段分组，仅需在group by子句后接多个分组条件即可，每个条件之间用英文格式的逗号间隔即可
	SELECT department_id,job_id,AVG(salary) FROM employees GROUP BY department_id,job_id;

	案例：查询每个部门每个工种的员工的平均工资，并且按平均工资的高低降序
	SELECT department_id,job_id,AVG(salary) FROM employees GROUP BY department_id,job_id ORDER BY AVG(salary) DESC;



##进阶6：多表连接查询，当查询的字段来自多个表时，会使用多表连接查询
	
	笛卡尔乘积现象：表1有m行，表2有n行，如果连接条件省略或无效则会出现结果为m*n行。
	发生原因：没有有效的连接条件
	解决办法：添加上有效的连接条件
	
	分类：
		按年代分类：
			sql92标准：仅仅支持内连接
			sql99标准[推荐]：支持内连接+外连接(左外和右外)+交叉连接
		按功能分类：
			内连接：
				等值连接
				非等值连接
				自连接
			外连接：用于查询一个表中有，另一个表没有的记录
				左外连接
				右外连接
				全外连接
			交叉连接
			
	一、sql92标准
		#1、等值连接
			①多表等值连接的结果为多表的交集部分。
			②N表连接，至少需要N-1个连接条件。
			③多个表不分主次，没有顺序要求。
			④一般为表起别名，提高阅读性和性能。
			⑤可以搭配前面介绍的所有子句使用，比如排序、分组、筛选。
			
			案例：查询员工名和对应的部门名
			SELECT last_name,department_name FROM employees,departments WHERE employees.department_id=departments.department_id;
			
			案例：查询员工名、工种号、工种名。可以为表起别名，如果为表起了别名，则查询的字段就不能使用原来的表名
			SELECT last_name,e.job_id,job_title FROM employees AS e,jobs AS j WHERE e.job_id=j.job_id;
			
			案例：查询有奖金的员工名、部门名。可以加筛选条件
			SELECT last_name,department_name,commission_pct FROM employees e,departments d WHERE e.department_id=d.department_id AND e.commission_pct IS NOT NULL;
			
			案例：查询城市名中第二个字符为o的部门名和城市名。筛选条件模糊查询
			SELECT department_name,city FROM departments d,locations l WHERE d.location_id=l.location_id AND l.city LIKE '_o%';

			案例：查询每个城市的部门个数。可以加分组
			SELECT COUNT(*),l.city FROM departments d,locations l WHERE d.location_id=l.location_id GROUP BY l.city; 
			
			案例：查询有奖金的每个部门的部门名和部门的领导编号和该部门的最低工资。
			SELECT department_name,d.manager_id,MIN(salary) FROM employees e,departments d WHERE e.department_id=d.department_id AND e.commission_pct IS NOT NULL GROUP BY department_name,d.manager_id;
			
			案例：查询每个工种的工种名和员工的个数，并且按员工个数降序。可以加排序
			SELECT COUNT(*) `count`,job_title FROM employees e,jobs j WHERE e.job_id=j.job_id GROUP BY job_title ORDER BY `count` DESC;
			
			案例：查询员工名、部门名和所在的城市。实现3表连接
			SELECT last_name,department_name,city 
			FROM employees e,departments d,locations l 
			WHERE e.department_id=d.department_id AND d.location_id=l.location_id;
			
		#2、非等值连接
			案例：查询员工的工资和工资级别
			SELECT salary,grade_level FROM employees e,job_grades g WHERE salary BETWEEN g.lowest_sal AND g.highest_sal;
		
		#3、自连接
			案例：查询员工名和上级的名称
			SELECT e.employee_id,e.last_name,m.last_name FROM employees e,employees m WHERE e.manager_id=m.employee_id;
		传统模式下的连接 ：等值连接——非等值连接
		
	
	二、sql99语法：1999年推出的sql语法，通过join关键字实现连接。支持内连接中的等值连接、非等值连接，外连接，交叉连接。
		好处是语句上，连接条件和筛选条件实现了分离，简洁明了！

		语法：	
			select 查询列表
			from 表1 别名 【连接类型】
			join 表2 别名 on 连接条件
			join 表3 别名 on 连接条件
			...
			join 表n 别名 on 连接条件
			【where 筛选条件】
			【group by 分组字段】
			【having 分组后的筛选条件】
			【order by 排序的字段或表达式】
			
		连接类型
			内连接：inner
			外连接：用于查询一个表中有，另一个表没有的记录
				左外连接：left [outer]
				右外连接 right [outer]
				全外连接 full [outer]
			交叉连接：cross
	
	
		（一）内连接
			语法：
				select 查询列表
				from 表1 别名
				inner join 表2 别名 on 连接条件
				join 表3 别名 on 连接条件
				...
				join 表n 别名 on 连接条件
				【where 筛选条件】
				【group by 分组字段】
				【having 分组后的筛选条件】
				【order by 排序的字段或表达式】
			注意：inner可省略
		
			#1、等值连接
				案例：查询员工名、部门名。
				SELECT last_name,department_name FROM employees e INNER JOIN departments d ON e.department_id=d.department_id;
			
				案例：查询名字中包含e的员工名和工种名。添加筛选
				SELECT last_name,job_title FROM employees e INNER JOIN jobs j ON e.job_id=j.job_id WHERE last_name LIKE "%e%";
				
				案例：查询部门个数>3的城市名和部门个数。添加分组和筛选
				SELECT city,COUNT(*) 部门个数 FROM locations l INNER JOIN departments d ON l.location_id=d.location_id GROUP BY city HAVING COUNT(*)>3;
				
				案例：查询哪个部门的员工个数>3的部门名和员工个数，并按个数降序。添加排序
				SELECT department_name,COUNT(*) 员工个数 FROM departments d INNER JOIN employees e ON d.department_id=e.department_id GROUP BY department_name HAVING COUNT(*)>3 ORDER BY COUNT(*) DESC;
				
				案例：查询员工名、部门名、工种名，并按部门名降序。3表连接
				SELECT last_name,department_name,job_title 
				FROM employees e 
				INNER JOIN departments d ON e.department_id=d.department_id 
				INNER JOIN jobs j ON e.job_id=j.job_id;
				ORDER BY department_name DESC;
				
			#2、非等值连接
				案例：查询员工的工资级别
				SELECT salary,grade_level FROM employees e INNER JOIN job_grades g ON salary BETWEEN g.lowest_sal AND g.highest_sal;
				
				案例：查询工资级别的个数>20的个数，并且按工资级别降序
				SELECT COUNT(*),grade_level FROM employees e INNER JOIN job_grades g ON salary BETWEEN g.lowest_sal AND g.highest_sal GROUP BY grade_level HAVING COUNT(*)>20 ORDER BY grade_level DESC;
				
			#3、自连接
				案例：查询姓名中包含字符k的员工的名字、上级的名字
				SELECT e.last_name 员工名,m.last_name 上级名 FROM employees e INNER JOIN employees m ON e.manager_id=m.employee_id WHERE e.last_name LIKE '%k%';
			
			
		（二）外连接：
			应用场景：用于查询一个表中有，另一个表没有的记录。
			特点：
				①、外连接的查询结果为主表中的所有记录。如果从表中有和它匹配的，则显示匹配值，如果从表中没有和它匹配的，则显示null。外连接查询结果=内连接查询结果+主表中有而从表中没有的记录。
				②、左外连接，left join左边的是主表。右外连接，right join右边的是主表。
				③、左外和右外交换两个表的顺序，可以实现同样的效果。
				④、全外连接=内连接的结果+表1中有但表2中没有的+表2中有但表1中没有的
				⑤、交叉连接就是sql92中的笛卡尔乘积
			案例：查询男朋友不在男神表的女神名
			select b.name from beauty b left join boys bo on b.boyfriend_id=bo.id where bo.id is null;
		
			案例：查询哪个部门没有员工
			SELECT d.*,e.employee_id FROM departments d LEFT JOIN employees e ON d.department_id=e.department_id WHERE e.employee_id IS NULL;
		
			案例：查询哪个城市没有部门
			SELECT city FROM locations l LEFT JOIN departments d ON l.location_id=d.location_id WHERE d.department_id IS NULL;
			
			案例：查询部门名为SAL或IT的员工信息
			
			
			
##进阶7：子查询

	含义：
		一条查询语句中又嵌套了另一条完整的select语句，其中被嵌套的select语句，称为子查询或内查询。
		在外面的查询语句，称为主查询或外查询

	特点：
		1、子查询都放在小括号内
		2、子查询优先于主查询执行，主查询使用了子查询的执行结果
		3、子查询根据查询结果集的行数不同分为以下几类：
			①标量子查询(结果集只有一行一列)
			②列子查询(结果集只有一列多行)
			③行子查询(结果集有一行多列)
			④表子查询(结果集一般为多行多列)
		4、子查询根据出现的位置可以分为以下几类：
			①子查询放在select后面：
				仅仅支持标量子查询
			②子查询放在from后面：
				支持表子查询
			③子查询放在where或having后面：
				支持标量子查询(重点)
				支持列子查询(重点)
				支持行子查询(用的较少)
			④子查询放在exists后面:
				支持表子查询
				
				
			① 单行子查询
				结果集只有一行
				一般搭配单行操作符使用：> < = <> >= <= 
				非法使用子查询的情况：
				a、子查询的结果为一组值
				b、子查询的结果为空
				
			② 多行子查询
				结果集有多行
				一般搭配多行操作符使用：any、all、in、not in
				in： 属于子查询结果中的任意一个就行
				any和all往往可以用其他查询代替
				
				
	一、子查询放在where或having后面
		(1).标量子查询(单行子查询)
		(2).列子查询(多行子查询)
		(3).行子查询(多行多列)
		
		特点：
			子查询都放在小括号内且放在条件的右侧，一般搭配单行操作符合多行操作符(in、any、all)
			
		1、标量子查询	
			案例：谁的工资比Abel高？
			分析：(1)先查询Abel的工资，(2)查询员工的信息，满足salary>(1)的结果
			SELECT last_name FROM employees WHERE salary>(SELECT salary FROM employees WHERE last_name='Abel');
			
			案例：返回job_id与141号员工相同，salary比143员工多的员工的姓名，job_id和工资
			SELECT last_name,job_id,salary FROM employees WHERE job_id=(SELECT job_id FROM employees WHERE employee_id=141) AND salary>(SELECT salary FROM employees WHERE employee_id=143);
		
			案例：返回公司工资最少的员工的last_name，job_id和salary。
			SELECT last_name,job_id,salary FROM employees WHERE salary=(SELECT MIN(salary) FROM employees);
			
			案例：查询最低工资大于50号部门最低工资的部门id和其最低工资。
			SELECT department_id,MIN(salary) FROM employees GROUP BY department_id HAVING MIN(salary)>(SELECT MIN(salary) FROM employees WHERE department_id=50);
		
		
		2、列子查询(一列多行)
			案例：返回location_id是1400或1700的部门中所有员工姓名
			分析：第一步先查询location_id是1400或1700的部门编号，然后再查询员工姓名，要求部门号是第一步查询结果列表中的某一个
			SELECT last_name FROM employees WHERE department_id IN (SELECT DISTINCT department_id FROM departments WHERE location_id IN (1400,1700));
	
			案例：返回其他部门中比job_id为IT_PROG部门任一工资低的员工的工号、姓名、job_id及salary
			SELECT employee_id,last_name,salary FROM employees WHERE job_id!='IT_PROG'  AND salary<ANY (SELECT DISTINCT  salary FROM employees WHERE job_id='IT_PROG');
			
			案例：返回其他部门中比job_id为IT_PROG部门所有工资都低的员工的工号、姓名、job_id及salary
			SELECT employee_id,last_name,salary FROM employees WHERE job_id!='IT_PROG'  AND salary<ALL (SELECT DISTINCT  salary FROM employees WHERE job_id='IT_PROG');
			
			
		3、行子查询(结果集为一行多列)
			案例：查询员工编号最小且工资最高的员工信息
			SELECT * FROM employees WHERE (employee_id,salary)=(SELECT MIN(employee_id),MAX(salary) FROM employees);
			

	二、子查询在select后面，仅仅支持结果集为一行一列的标量子查询
		案例：查询每个部门的员工个数
		SELECT d.*,(SELECT count(*) FROM employees e WHERE e.department_id=d.department_id) 个数 FROM departments d
	
	
	三、子查询在from后面。要求必须起别名。
		案例：查询每个部门的平均工资的工资等级
		SELECT d.department_id,d.ag,grade_level FROM (SELECT department_id,AVG(salary) ag FROM employees GROUP BY department_id) d INNER JOIN job_grades g ON d.ag BETWEEN g.lowest_sal AND g.highest_sal;
		
	
	四、子查询在exists后面。亦称为相关子查询。
		语法：
			exists (完整的查询语句) 
		查询结果：
			1或0。
		案例：查询有员工的部门名
		SELECT department_name FROM departments WHERE EXISTS(SELECT * FROM employees e WHERE d.department_id=e.department_id);
		
		案例：查询没有女朋友的男神的信息
		SELECT bo.* FROM boys bo WHERE NOT EXISTS(SELECT boyfriend_id FROM beauty b WHERE bo.id=b.boyfriend_id)
			
##进阶8：分页查询

	应用场景：
		实际的web项目中需要根据用户的需求提交对应的分页查询的sql语句

	语法：

		select 字段|表达式,...			第7个执行
		from 表							第1个执行
		【join type join 表2			第2个执行
		 on 连接条件					第3个执行
		 where 筛选条件					第4个执行	
		 group by 分组字段				第5个执行
		 having 分组后的筛选条件		第6个执行
		 order by 排序的字段】			第8个执行	
		limit 【起始的条目索引，从0开始】,要显示的条目数;

	特点：

		1.起始条目索引从0开始
		
		2.limit子句放在查询语句的最后，且语句执行时也是最后
		
		3.公式：select * from  表 limit （page-1）*sizePerPage,sizePerPage
		假如:
		每页显示条目数sizePerPage
		要显示的页数 page
		
	案例：查询第11条至25条的员工信息
	SELECT * FROM employees LIMIT 10,15;
	
	案例：查询有奖金的员工信息，并且工资较高的前10名显示出来。
	SELECT * FROM employees WHERE commission_pct IS NOT NULL ORDER BY salary DESC LIMIT 0,10;
	
	
	

##进阶9：联合查询：即将多条查询语句的结果合并成一个结果。

	引入：
		union 联合、合并

	应用场景：
		要查询的结果来自于多个表，且多个表没有直接的连接关系，但查询的信息一致时
	语法：

		select 字段|常量|表达式|函数 【from 表】 【where 条件】 union 【all】
		select 字段|常量|表达式|函数 【from 表】 【where 条件】 union 【all】
		select 字段|常量|表达式|函数 【from 表】 【where 条件】 union  【all】
		.....
		select 字段|常量|表达式|函数 【from 表】 【where 条件】

	特点：

		1、多条查询语句的查询的列数必须是一致的
		2、多条查询语句的查询的列的类型几乎相同
		3、union代表去重，union all代表不去重

	案例：查询中国用户中男性的信息及外国用户中男性的用户信息	
	SELECT id,cname,csex FROM t_ca WHERE csex='男' 
	union 
	SELECT t_id,tName,tGender FROM t_ua WHERE tGender='male';
	

##DML语言

###插入

语法：
	insert into 表名(字段名，...)
	values(值1，...);

特点：

	1、字段类型和值类型一致或兼容，而且一一对应
	2、可以为空的字段，可以不用插入值，或用null填充
	3、不可以为空的字段，必须插入值
	4、字段个数和值的个数必须一致
	5、字段可以省略，但默认所有字段，并且顺序和表中的存储顺序一致

###修改

修改单表语法：

	update 表名 set 字段=新值,字段=新值
	【where 条件】
修改多表语法：

	update 表1 别名1,表2 别名2
	set 字段=新值，字段=新值
	where 连接条件
	and 筛选条件


###删除

方式1：delete语句 

单表的删除： ★
	delete from 表名 【where 筛选条件】

多表的删除：
	delete 别名1，别名2
	from 表1 别名1，表2 别名2
	where 连接条件
	and 筛选条件;


方式2：truncate语句

	truncate table 表名


两种方式的区别【面试题】
	
	#1.truncate不能加where条件，而delete可以加where条件
	
	#2.truncate的效率高一丢丢
	
	#3.truncate 删除带自增长的列的表后，如果再插入数据，数据从1开始
	#delete 删除带自增长列的表后，如果再插入数据，数据从上一次的断点处开始
	
	#4.truncate删除不能回滚，delete删除可以回滚


##DDL语句
###库和表的管理

	通用的建库建表语句写法：
	DROP DATABASE IF EXISTS 旧库名;
	CREATE DATABASE 新库名;
	DROP TABLE IF EXISTS 旧表名;
	CREATE TABLE 新表名();
	
	库的管理：

		一、创建库
		create database 库名
		二、删除库
		drop database 库名
		
		
	表的管理：
		#1.创建表
		CREATE TABLE IF NOT EXISTS stuinfo(
			stuId INT,
			stuName VARCHAR(20),
			gender CHAR,
			bornDate DATETIME
			
		
		);

		#2.修改表。关键字：alter

			1、修改列名
			2、修改列的类型或约束
			3、添加新列
			4、删除列
			5、修改表名
		
			#①修改列名(字段名)
			语法：ALTER TABLE 表名 CHANGE COLUMN 旧列名 新列名 新列的类型
			案例：修改studentinfo表中
			ALTER TABLE studentinfo CHANGE COLUMN sex gender CHAR;
			
			#②修改列的类型或约束
			语法：ALTER TABLE 表名 MODIFY COLUMN 列名 新类型
			案例：
			ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;
			
			#③添加新列
			语法：ALTER TABLE 表名 ADD COLUMN 新列名 新列的类型
			案例：
			ALTER TABLE author ADD COLUMN annual DOUBLE
			ALTER TABLE stuinfo ADD COLUMN FOREIGN KEY(majorid) REFERENCES major(id);
			
			#④删除列
			语法：ALTER TABLE 表名 DROP COLUMN 要删除的列名
			案例：
			ALTER TABLE author DROP COLUMN annual;
			
			#⑤修改表名
			语法：ALTER TABLE 旧表名 RENAME [TO] 新表名 
			案例：
			ALTER TABLE author RENAME TO book_author;
		
		
		#3.删除表
		DROP TABLE [IF EXISTS] studentinfo;
		
		#4.表的复制
			1.仅仅复制表的结构
			语法：CREATE TABLE 新表名 LIKE 原表名
			案例：创建一个新表new_author，并将author表的结构复制过来
			CREATE TABLE new_author LIKE author;
			
			2.复制表的结构+数据
			语法：CREATE TABLE 新表名 SELECT * FROM 原表名
			案例：创建一个新表dep1，并将departments表中的所有数据都复制过来。
			CREATE TABLE dep1 SELECT * FROM departments;
	


###常见类型
	数值型：
		整型：Tinyint（1字节）、Smallint（2字节）、Mediumint（3字节）、integer（4字节）、Bigint（8字节）
			1、默认是有符号的，如果想设置无符号需要在其后添加关键字UNSIGNED。形如：INT UNSIGNED 
		小数：
			浮点型：float(M,D)（4字节）、double(M,D)（8字节）。M表示整数部分加上小数部分的总长度，D表示小数点后的位数
			定点型：decimal(M,D)。M表示整数部分加上小数部分的总长度，D表示小数点后的位数。默认为decimal(10,0)
	字符型：
		较短的文本：char(M)固定长度的字符、varchar(M)可变长度的字符。M表示最多的字符数，其中char的M限制为0~255之间的整数且可以省略默认为1，varchar的M限制为0~65535之间的整数且不可省略。
		较长的文本：text、blob（较长的二进制数据）
	日期型：
		date：4字节，最小值1000-01-01，最大值9999-12-31
		datetime：8字节，最小值1000-01-01 00:00:00，最大值9999-12-31 23:59:59
		timestamp：4字节，最小值1970-01-01 08:00:00，最大值2038年的某个时刻
		time：3字节，最小值1000-01-01，最大值2038年的某个时刻
		year：1字节，最小值1901，最大值2155



###常见约束
	约束是一种限制，用于创建表时限制表中的数据，为了保证数据的一致性。
	添加约束的时机：
		1.创建表时：
			CREATE TABLE 表名(
				字段名 字段类型 约束
			)
		2.修改表时：
			ALTER TABLE book MODIFY COLUMN pubdate TIMESTAMP;
	
	
	约束分为6大类：
		NOT NULL：非空，用于保证该字段的值不能为空
		DEFAULT：默认，用于保证该字段有默认值
		PRIMARY KEY：主键，用于保证该字段的值具有唯一性，并且非空
		UNIQUE：唯一，用于保证该字段的值具有唯一性，但可以为空
		CHECK：检查约束，mysql中不支持。
		FOREIGN KEY：外键，用于限制两个表的关系，用于保证该字段的值必须来自于主表的关联列的值
		
	约束根据所在位置的不可，又可分为2类：
		列级约束：6大约束语法上都支持，但外键约束没有效果
		CREATE TABLE 表名(
			字段名 字段类型 列级约束
		)
		CREATE TABLE stuinfo(
				id INT PRIMARY KEY,
				stuName VARCHAR(20) NOT NULL,
				gender CHAR(1),
				seat INT UNIQUE,
				age INT DEFAULT 18
			)
		
		表级约束：除了非空、默认，其他都支持
		CREATE TABLE 表名(
			字段名 字段类型 
			字段名 字段类型,
			字段名 字段类型,
			表级约束
		)
		CREATE TABLE stuinfo(
				id INT,
				stuName VARCHAR(20),
				gender CHAR(1),
				seat INT,
				age INT,
				majorid INT,
				
				[CONSTRAINT 约束名] PRIMARY KEY(id),
				[CONSTRAINT 约束名] UNIQUE(seat)
				[CONSTRAINT 约束名] FOREIGN KEY(majorid) REFERENCES major(id) 
			)
		[CONSTRAINT 约束名]可以省略不写
		
	主键和唯一的对比：
				保证唯一性			是否允许为空		一个表中可以有多少个		是否允许组合
		主键		√					×					至多有1个					√，但不推荐
		唯一		√					√					可以有多个					√，但不推荐
	
	外键：
		1、要求在从表设置外键关系
		2、从表的外键列的类型和主表的关联列的类型要求一致，名称无要求
		3、主表的关联列必须是一个key（一般是主键或唯一）
		4、插入数据时，必须先插入主表，再插入从表。删除数据时必须先删除从表，再删除主表。
		案例：向表emp2中添加列dept_id，并在其中定义FOREIGN KEY约束，与之关联的列是dept2表中的id列。
			ALTER TABLE emp2 ADD COLUMN dept_id INT;
			ALTER TABLE emp2 ADD CONSTRAINT fk_emp2_dept2 FOREIGN KEY(dept_id) REFERENCES dep2(id);
	
	标识列：又称为自增长列，可以不用手动的插入值，系统提供默认的序列值
		关键字：AUTO_INCREMENT。
		标识列不必须和主键搭配，但要求是一个key；一个表中仅能有1个标识列
	
		
		

##数据库事务
###含义
	通过一组逻辑操作单元（一组DML——sql语句），将数据从一种状态切换到另外一种状态

###特点
	（ACID）
	原子性：要么都执行，要么都回滚
	一致性：保证数据的状态操作前和操作后保持一致
	隔离性：多个事务同时操作相同数据库的同一个数据时，一个事务的执行不受另外一个事务的干扰
	持久性：一个事务一旦提交，则数据将持久化到本地，除非其他事务对其进行修改

相关步骤：

	1、开启事务
	2、编写事务的一组逻辑操作单元（多条sql语句）
	3、提交事务或回滚事务

###事务的分类：

隐式事务，没有明显的开启和结束事务的标志

	比如
	insert、update、delete语句本身就是一个事务


显式事务，具有明显的开启和结束事务的标志

		1、开启事务
		取消自动提交事务的功能
		
		2、编写事务的一组逻辑操作单元（多条sql语句）
		insert
		update
		delete
		
		3、提交事务或回滚事务
###使用到的关键字

	set autocommit=0;
	start transaction;
	commit;
	rollback;
	
	savepoint  断点
	commit to 断点
	rollback to 断点


###事务的隔离级别:

事务并发问题如何发生？

	当多个事务同时操作同一个数据库的相同数据时
事务的并发问题有哪些？

	脏读：一个事务读取到了另外一个事务未提交的数据
	不可重复读：同一个事务中，多次读取到的数据不一致
	幻读：一个事务读取数据时，另外一个事务进行更新，导致第一个事务读取到了没有更新的数据
	
如何避免事务的并发问题？

	通过设置事务的隔离级别
	1、READ UNCOMMITTED
	2、READ COMMITTED 可以避免脏读
	3、REPEATABLE READ 可以避免脏读、不可重复读和一部分幻读
	4、SERIALIZABLE可以避免脏读、不可重复读和幻读
	
设置隔离级别：

	set session|global  transaction isolation level 隔离级别名;
查看隔离级别：

	select @@tx_isolation;
	


##视图
含义：理解成一张虚拟的表

视图和表的区别：
	
		使用方式	占用物理空间
	
	视图	完全相同	不占用，仅仅保存的是sql逻辑
	
	表	完全相同	占用

视图的好处：


	1、sql语句提高重用性，效率高
	2、和表实现了分离，提高了安全性

###视图的创建
	语法：
	CREATE VIEW  视图名
	AS
	查询语句;
###视图的增删改查
	1、查看视图的数据 ★
	
	SELECT * FROM my_v4;
	SELECT * FROM my_v1 WHERE last_name='Partners';
	
	2、插入视图的数据
	INSERT INTO my_v4(last_name,department_id) VALUES('虚竹',90);
	
	3、修改视图的数据
	
	UPDATE my_v4 SET last_name ='梦姑' WHERE last_name='虚竹';
	
	
	4、删除视图的数据
	DELETE FROM my_v4;
###某些视图不能更新
	包含以下关键字的sql语句：分组函数、distinct、group  by、having、union或者union all
	常量视图
	Select中包含子查询
	join
	from一个不能更新的视图
	where子句的子查询引用了from子句中的表
###视图逻辑的更新
	#方式一：
	CREATE OR REPLACE VIEW test_v7
	AS
	SELECT last_name FROM employees
	WHERE employee_id>100;
	
	#方式二:
	ALTER VIEW test_v7
	AS
	SELECT employee_id FROM employees;
	
	SELECT * FROM test_v7;
###视图的删除
	DROP VIEW test_v1,test_v2,test_v3;
###视图结构的查看	
	DESC test_v7;
	SHOW CREATE VIEW test_v7;

##存储过程

含义：一组经过预先编译的sql语句的集合
好处：

	1、提高了sql语句的重用性，减少了开发程序员的压力
	2、提高了效率
	3、减少了传输次数

分类：

	1、无返回无参
	2、仅仅带in类型，无返回有参
	3、仅仅带out类型，有返回无参
	4、既带in又带out，有返回有参
	5、带inout，有返回有参
	注意：in、out、inout都可以在一个存储过程中带多个
###创建存储过程
语法：

	create procedure 存储过程名(in|out|inout 参数名  参数类型,...)
	begin
		存储过程体

	end

类似于方法：

	修饰符 返回类型 方法名(参数类型 参数名,...){

		方法体;
	}

注意

	1、需要设置新的结束标记
	delimiter 新的结束标记
	示例：
	delimiter $

	CREATE PROCEDURE 存储过程名(IN|OUT|INOUT 参数名  参数类型,...)
	BEGIN
		sql语句1;
		sql语句2;

	END $

	2、存储过程体中可以有多条sql语句，如果仅仅一条sql语句，则可以省略begin end

	3、参数前面的符号的意思
	in:该参数只能作为输入 （该参数不能做返回值）
	out：该参数只能作为输出（该参数只能做返回值）
	inout：既能做输入又能做输出


#调用存储过程
	call 存储过程名(实参列表)
##函数


###创建函数

学过的函数：LENGTH、SUBSTR、CONCAT等
语法：

	CREATE FUNCTION 函数名(参数名 参数类型,...) RETURNS 返回类型
	BEGIN
		函数体
	
	END

###调用函数
	SELECT 函数名（实参列表）





###函数和存储过程的区别

			关键字		调用语法	返回值			应用场景
	函数		FUNCTION	SELECT 函数()	只能是一个		一般用于查询结果为一个值并返回时，当有返回值而且仅仅一个
	存储过程	PROCEDURE	CALL 存储过程()	可以有0个或多个		一般用于更新


##流程控制结构

###系统变量
一、全局变量

作用域：针对于所有会话（连接）有效，但不能跨重启

	查看所有全局变量
	SHOW GLOBAL VARIABLES;
	查看满足条件的部分系统变量
	SHOW GLOBAL VARIABLES LIKE '%char%';
	查看指定的系统变量的值
	SELECT @@global.autocommit;
	为某个系统变量赋值
	SET @@global.autocommit=0;
	SET GLOBAL autocommit=0;

二、会话变量

作用域：针对于当前会话（连接）有效

	查看所有会话变量
	SHOW SESSION VARIABLES;
	查看满足条件的部分会话变量
	SHOW SESSION VARIABLES LIKE '%char%';
	查看指定的会话变量的值
	SELECT @@autocommit;
	SELECT @@session.tx_isolation;
	为某个会话变量赋值
	SET @@session.tx_isolation='read-uncommitted';
	SET SESSION tx_isolation='read-committed';

###自定义变量
一、用户变量

声明并初始化：

	SET @变量名=值;
	SET @变量名:=值;
	SELECT @变量名:=值;
赋值：

	方式一：一般用于赋简单的值
	SET 变量名=值;
	SET 变量名:=值;
	SELECT 变量名:=值;


	方式二：一般用于赋表 中的字段值
	SELECT 字段名或表达式 INTO 变量
	FROM 表;

使用：

	select @变量名;

二、局部变量

声明：

	declare 变量名 类型 【default 值】;
赋值：

	方式一：一般用于赋简单的值
	SET 变量名=值;
	SET 变量名:=值;
	SELECT 变量名:=值;


	方式二：一般用于赋表 中的字段值
	SELECT 字段名或表达式 INTO 变量
	FROM 表;

使用：

	select 变量名



二者的区别：

			作用域			定义位置		语法
用户变量	当前会话		会话的任何地方		加@符号，不用指定类型
局部变量	定义它的BEGIN END中 	BEGIN END的第一句话	一般不用加@,需要指定类型

###分支
一、if函数
	语法：if(条件，值1，值2)
	特点：可以用在任何位置

二、case语句

语法：

	情况一：类似于switch
	case 表达式
	when 值1 then 结果1或语句1(如果是语句，需要加分号) 
	when 值2 then 结果2或语句2(如果是语句，需要加分号)
	...
	else 结果n或语句n(如果是语句，需要加分号)
	end 【case】（如果是放在begin end中需要加上case，如果放在select后面不需要）

	情况二：类似于多重if
	case 
	when 条件1 then 结果1或语句1(如果是语句，需要加分号) 
	when 条件2 then 结果2或语句2(如果是语句，需要加分号)
	...
	else 结果n或语句n(如果是语句，需要加分号)
	end 【case】（如果是放在begin end中需要加上case，如果放在select后面不需要）


特点：
	可以用在任何位置

三、if elseif语句

语法：

	if 情况1 then 语句1;
	elseif 情况2 then 语句2;
	...
	else 语句n;
	end if;

特点：
	只能用在begin end中！！！！！！！！！！！！！！！


三者比较：
			应用场合
	if函数		简单双分支
	case结构	等值判断 的多分支
	if结构		区间判断 的多分支


###循环

语法：


	【标签：】WHILE 循环条件  DO
		循环体
	END WHILE 【标签】;
	
特点：

	只能放在BEGIN END里面

	如果要搭配leave跳转语句，需要使用标签，否则可以不用标签

	leave类似于java中的break语句，跳出所在循环！！！
	


































