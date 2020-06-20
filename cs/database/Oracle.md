Oracle
===========
Oracle一般在linux/unix。在linux下安装比较麻烦，默认不支持Ubuntu。用Ubuntu, CentOS。
VirtualBox
Oracle 10g不支持Win7？用虚拟机VirtualBox
	安装VirtualBox; 
管理->全局设定->扩展->选择 VirtualBox extension
Error: Can not access the kernel driver
Go to
C:\Program Files\Oracle\VirtualBox\drivers\USB\filter
Select VBoxUSBMon.inf and click the right mouse button. Then pick Install.
Go to
C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv
Select VBoxDrv.inf and click the right mouse button. Then pick install.
VirtualBox should now work again as expected.
新建/导入虚拟机(WinXP)：
设置->系统->硬件加速，去掉“启动VT-x/AMD-V”
	网卡->”桥接网卡”，选有线网卡
虚拟机中：共享文件夹，映射网络驱动器
如果Oracle 安装成功：cmd>sqlplus scott/tiger

Linux上安装Oracle 10g:  http://69520.blog.51cto.com/59520/91156
Fport.exe查看接口（只能在winxp使用）

虚拟机推出时最好选快速休眠；视图->切换到无缝模式
在虚拟机备份Oracel

WinXP in VirtualBox：
只能从原盘ISO安装
加上shared drive:
WinXP->device->insert Guest-addition cd image

Oracle 10.2直接安装到Win7
首先、确保你有该文件夹的完全控制权。（修改：文件夹点右键 属性-〉安全-〉高级-〉所有者-〉改为自己。接着编辑自己的权限为完全控制）
其次、将setup.exe的兼容性改为windows server 2003(server pack 1)。就是右键属性-〉兼容性-〉兼容模式中。
接着、右键，以管理员身份运行。
最后、会出现兼容性问题的提示框。选择运行程序。
Orcl/orcl
解锁Scott/1004

Enterprise Manager Database Control URL - (orcl) : http://localhost:1158/em 数据库配置文件已经安装到 d:\oracle\product\10.2.0,同时其他选定的安装组件也已经安装到 d:\oracle\product\10.2.0\db_1。
iSQL*Plus URL 为: http://localhost:5560/isqlplus iSQL*Plus DBA URL 为: http://localhost:5560/isqlplus/dba 
SQL Plus : (system/orcl/orcl)
SQL> select sysdate from dual;  //看到日期表明安装成功

如果没配置好：
Net Manager: 配置监听程序 Listener
	Oracle Net Configuration Assistant

22.2.	Oracle 简介
Oracle 客户机
Jdbc:oracle:thin:@localhost:1521:orcl，只要一个jar包。SQL developer
Jdbc:oracle:oci:@localhost:1521:orcl ：客户机也必须装oracle，效率高，集群最好用这个。PLSQL Developer

RDBMS:
由实例(n)和数据库组成(1)
	orcl数据库: 路径：product/10.2.0/oradata/orcl
	实例：位于物理内存里的数据结构。一个实例只能与一个数据库连接。大多数情况下，一个数据库只有一个实例对其操作。

Application Cluster集群
Weblogic, Tomcat6都支持集群
 


 

Java通过流（操作系统进程）操作硬盘文件
Commit提交后，Oracle两阶段提交：PGA->SGA, SGA->DB File
Java做错后，commit后无法rollback，但是oracle 闪回可以撤销(day4-23)

表空间(users)对应多个数据文件。
数据文件：*.dbf

逻辑和物理结构
 

注：上图中”数据库”应该是”instance”
数据块： 8k
方案： schema (day4-25)

数据库认证：OCA (day1-3), OCP(day4, 2*5天), OCM

Windows service: OracleServiceORCL

Unlock Scott 
https://localhost:1158/em

通过系统用户登进sql*plus，
cmd> sqlplus/nolog
SQL> conn/as sysdba
或者：Cmd> sqlplus / as sysdba
SQL> alter user scott account unlock;
SQL> disconnect
SQL> conn scott/tiger@orcl
[或者SQL>exit; SQL> sqlplus scott/tiger] 连接上。
SQL> alter user scott identified by 新密码;


1. 管理员登录
c:\>sqlplus sys/你的密码 as sysdba  (密码认证)
c:\>sqlplus / as sysdba             (主机认证  优先)

2. 解锁
SQL>alter user scott account unlock;

3. 改密码
SQL>alter user scott identified by 新密码;

22.3.	基本SQL语句
SQL> spool c:\基本查询.txt（以下是保存到这个文件的内容）
SQL> --清屏
SQL> host cls

SQL> --当前用户
SQL> show user
USER 为 "SCOTT"
SQL> --当前用户下的表
SQL> select * from tab;  //mysql> show tables

TNAME                          TABTYPE  CLUSTERID                               
------------------------------ ------- ----------                               
DEPT                           TABLE                                            
EMP                            TABLE                                            
BONUS                          TABLE                                            
SALGRADE                       TABLE                                            

SQL> --tab: 数据字典(表)
SQL> desc emp
 名称                                      是否为空? 类型
 ----------------------------------------- -------- ----------------------------
 EMPNO                                     NOT NULL NUMBER(4)
 ENAME                                              VARCHAR2(10)
 JOB                                                VARCHAR2(9)
 MGR                                                NUMBER(4)
 HIREDATE                                           DATE
 SAL                                                NUMBER(7,2)
 COMM                                               NUMBER(7,2)
 DEPTNO                                             NUMBER(2)

SQL> --查询员工的所有信息
SQL> select * from emp;

     EMPNO ENAME      JOB              MGR HIREDATE              SAL       COMM 		DEPTNO                                                                      
---------- ---------- --------- ---------- -------------- ---------- ---------- ----------                                                                      
      7369 SMITH      CLERK           7902 17-12月-80            800              20                                                                                                                                                      
      7499 ALLEN      SALESMAN        7698 20-2月 -81           1600        300         30                                                                                                                                                      
      7521 WARD       SALESMAN        7698 22-2月 -81           1250        500        30                                                                                                                                                      
      7566 JONES      MANAGER         7839 02-4月 -81           2975                    20                                                                                                                                                      
      7654 MARTIN     SALESMAN        7698 28-9月 -81           1250       1400         30                                                                                                                                                      
      7698 BLAKE      MANAGER         7839 01-5月 -81           2850                    30                                                                                                                                                      
      7782 CLARK      MANAGER         7839 09-6月 -81           2450                    10                                                                                                                                                      
      7788 SCOTT      ANALYST         7566 13-7月 -87           3000                    20                                                                                                                                                      
      7839 KING       PRESIDENT            17-11月-81           5000                    10                                                                      
      7844 TURNER     SALESMAN        7698 08-9月 -81           1500          0         30                                                                                                                                                      
      7876 ADAMS      CLERK           7788 13-7月 -87           1100                    20                                                                      
      7900 JAMES      CLERK           7698 03-12月-81            950                    30                                                                                                                                                      
      7902 FORD       ANALYST         7566 03-12月-81           3000                    20                                                                      
      7934 MILLER     CLERK           7782 23-1月 -82           1300                    10                                                                      
                                                                                

已选择14行。

SQL> --设置行宽
SQL> set linesize 120
SQL> --设置列宽
SQL> col ename for a8
SQL> col sal for 9999
SQL> /  （重复执行上一条命令select * from emp;）

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

SQL> --通过列名
SQL> select empno,ename,job,mgr,hiredate,sal,comm,deptno
  2  from emp;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

SQL> /*
SQL> SQL优化:
SQL> 1. 尽量使用列名(Orale9i之后，*和列名是一样的 )
SQL> */
SQL> host cls

SQL> --查询员工信息: 员工号  姓名 月薪
SQL> select empno,ename,sal
  2  from emp;

     EMPNO ENAME      SAL                                                                                               
---------- -------- -----                                                                                               
      7369 SMITH      800                                                                                               
      7499 ALLEN     1600                                                                                               
      7521 WARD      1250                                                                                               
      7566 JONES     2975                                                                                               
      7654 MARTIN    1250                                                                                               
      7698 BLAKE     2850                                                                                               
      7782 CLARK     2450                                                                                               
      7788 SCOTT     3000                                                                                               
      7839 KING      5000                                                                                               
      7844 TURNER    1500                                                                                               
      7876 ADAMS     1100                                                                                               

      7900 JAMES      950                                                                                               
      7902 FORD      3000                                                                                               
      7934 MILLER    1300                                                                                               

已选择14行。

SQL> --查询员工信息:员工号  姓名 月薪 年薪
SQL> select empno,ename,sal,sal*12
  2  from emp;

     EMPNO ENAME      SAL     SAL*12                                                                                    
---------- -------- ----- ----------                                                                                    
      7369 SMITH      800       9600                                                                                    
      7499 ALLEN     1600      19200                                                                                    
      7521 WARD      1250      15000                                                                                    
      7566 JONES     2975      35700                                                                                    
      7654 MARTIN    1250      15000                                                                                    
      7698 BLAKE     2850      34200                                                                                    
      7782 CLARK     2450      29400                                                                                    
      7788 SCOTT     3000      36000                                                                                    
      7839 KING      5000      60000                                                                                    
      7844 TURNER    1500      18000                                                                                    
      7876 ADAMS     1100      13200                                                                                    

      7900 JAMES      950      11400                                                                                    
      7902 FORD      3000      36000                                                                                    
      7934 MILLER    1300      15600                                                                                    

已选择14行。

SQL> --查询员工信息:员工号  姓名 月薪 年薪 奖金 年收入
SQL> select empno,ename,sal,sal*12,comm,sal*12+comm
  2  from emp;

     EMPNO ENAME      SAL     SAL*12       COMM SAL*12+COMM                                                             
---------- -------- ----- ---------- ---------- -----------                                                             
      7369 SMITH      800       9600                                                                                    
      7499 ALLEN     1600      19200        300       19500                                                             
      7521 WARD      1250      15000        500       15500                                                             
      7566 JONES     2975      35700                                                                                    
      7654 MARTIN    1250      15000       1400       16400                                                             
      7698 BLAKE     2850      34200                                                                                    
      7782 CLARK     2450      29400                                                                                    
      7788 SCOTT     3000      36000                                                                                    
      7839 KING      5000      60000                                                                                    
      7844 TURNER    1500      18000          0       18000                                                             
      7876 ADAMS     1100      13200                                                                                    

      7900 JAMES      950      11400                                                                                    
      7902 FORD      3000      36000                                                                                    
      7934 MILLER    1300      15600                                                                                    

已选择14行。

SQL> /*
SQL> SQL语句中的null值
SQL> 1. 包含null的表达式都为null
SQL> 2. null!=null
SQL> */
SQL> select empno,ename,sal,sal*12,comm,sal*12+nvl(comm,0)
  2  from emp;

     EMPNO ENAME      SAL     SAL*12       COMM SAL*12+NVL(COMM,0)                                                      
---------- -------- ----- ---------- ---------- ------------------                                                      
      7369 SMITH      800       9600                          9600                                                      
      7499 ALLEN     1600      19200        300              19500                                                      
      7521 WARD      1250      15000        500              15500                                                      
      7566 JONES     2975      35700                         35700                                                      
      7654 MARTIN    1250      15000       1400              16400                                                      
      7698 BLAKE     2850      34200                         34200                                                      
      7782 CLARK     2450      29400                         29400                                                      
      7788 SCOTT     3000      36000                         36000                                                      
      7839 KING      5000      60000                         60000                                                      
      7844 TURNER    1500      18000          0              18000                                                      
      7876 ADAMS     1100      13200                         13200                                                      

      7900 JAMES      950      11400                         11400                                                      
      7902 FORD      3000      36000                         36000                                                      
      7934 MILLER    1300      15600                         15600                                                      

已选择14行。

SQL> --查询奖金为null的员工
SQL> select *
  2  from emp
  3  where comm=null;

未选定行

SQL> select *
  2  from emp
  3  where comm is null;  // 不能用 =null

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择10行。

SQL> host cls

SQL> select *
  2  form emp;
form emp
*
第 2 行出现错误: 
ORA-00923: 未找到要求的 FROM 关键字 


SQL> --c 命令
SQL> 2  //进入第二行
  2* form emp
SQL> c /form/from
  2* from emp
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

SQL> select empno,ename,sal,job
  2  form emp;
form emp
     *
第 2 行出现错误: 
ORA-00923: 未找到要求的 FROM 关键字 


SQL> ed
已写入 file afiedt.buf

  1  select empno,ename,sal,job
  2* from emp
SQL> /

     EMPNO ENAME      SAL JOB                                                                                           
---------- -------- ----- ---------                                                                                     
      7369 SMITH      800 CLERK                                                                                         
      7499 ALLEN     1600 SALESMAN                                                                                      
      7521 WARD      1250 SALESMAN                                                                                      
      7566 JONES     2975 MANAGER                                                                                       
      7654 MARTIN    1250 SALESMAN                                                                                      
      7698 BLAKE     2850 MANAGER                                                                                       
      7782 CLARK     2450 MANAGER                                                                                       
      7788 SCOTT     3000 ANALYST                                                                                       
      7839 KING      5000 PRESIDENT                                                                                     
      7844 TURNER    1500 SALESMAN                                                                                      
      7876 ADAMS     1100 CLERK                                                                                         

     EMPNO ENAME      SAL JOB                                                                                           
---------- -------- ----- ---------                                                                                     
      7900 JAMES      950 CLERK                                                                                         
      7902 FORD      3000 ANALYST                                                                                       
      7934 MILLER    1300 CLERK                                                                                         

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select empno as "员工号",ename "姓名",sal 月薪,job 职位
  2* from emp
SQL> /

    员工号 姓名             月薪 职位                                                                                   
---------- ---------- ---------- ---------                                                                              
      7369 SMITH             800 CLERK                                                                                  
      7499 ALLEN            1600 SALESMAN                                                                               
      7521 WARD             1250 SALESMAN                                                                               
      7566 JONES            2975 MANAGER                                                                                
      7654 MARTIN           1250 SALESMAN                                                                               
      7698 BLAKE            2850 MANAGER                                                                                
      7782 CLARK            2450 MANAGER                                                                                
      7788 SCOTT            3000 ANALYST                                                                                
      7839 KING             5000 PRESIDENT                                                                              
      7844 TURNER           1500 SALESMAN                                                                               
      7876 ADAMS            1100 CLERK                                                                                  

    员工号 姓名             月薪 职位                                                                                   
---------- ---------- ---------- ---------                                                                              
      7900 JAMES             950 CLERK                                                                                  
      7902 FORD             3000 ANALYST                                                                                
      7934 MILLER           1300 CLERK                                                                                  

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select empno as "员工号",ename "姓名",sal 月    薪,job 职位
  2* from emp
SQL> /
select empno as "员工号",ename "姓名",sal 月    薪,job 职位
                                                *
第 1 行出现错误: 
ORA-00923: 未找到要求的 FROM 关键字 


SQL> ed
已写入 file afiedt.buf
// 如果有特殊字符，别名要加双引号。
  1  select empno as "员工号",ename "姓名",sal "月    薪",job 职位
  2* from emp
SQL> /

    员工号 姓名         月    薪 职位                                                                                   
---------- ---------- ---------- ---------                                                                              
      7369 SMITH             800 CLERK                                                                                  
      7499 ALLEN            1600 SALESMAN                                                                               
      7521 WARD             1250 SALESMAN                                                                               
      7566 JONES            2975 MANAGER                                                                                
      7654 MARTIN           1250 SALESMAN                                                                               
      7698 BLAKE            2850 MANAGER                                                                                
      7782 CLARK            2450 MANAGER                                                                                
      7788 SCOTT            3000 ANALYST                                                                                
      7839 KING             5000 PRESIDENT                                                                              
      7844 TURNER           1500 SALESMAN                                                                               
      7876 ADAMS            1100 CLERK                                                                                  

      7900 JAMES             950 CLERK                                                                                  
      7902 FORD             3000 ANALYST                                                                                
      7934 MILLER           1300 CLERK                                                                                  

已选择14行。

SQL> host cls

SQL> --DISTINCT 去掉重复记录
SQL> select deptno from emp;

    DEPTNO                                                                                                              
----------                                                                                                              
        20                                                                                                              
        30                                                                                                              
        30                                                                                                              
        20                                                                                                              
        30                                                                                                              
        30                                                                                                              
        10                                                                                                              
        20                                                                                                              
        10                                                                                                              
        30                                                                                                              
        20                                                                                                              

    DEPTNO                                                                                                              
----------                                                                                                              
        30                                                                                                              
        20                                                                                                              
        10                                                                                                              

已选择14行。

SQL> select DISTINCT deptno from emp;

    DEPTNO                                                                                                              
----------                                                                                                              
        30                                                                                                              
        20                                                                                                              
        10                                                                                                              

SQL> select job from emp;

JOB                                                                                                                     
---------                                                                                                               
CLERK                                                                                                                   
SALESMAN                                                                                                                
SALESMAN                                                                                                                
MANAGER                                                                                                                 
SALESMAN                                                                                                                
MANAGER                                                                                                                 
MANAGER                                                                                                                 
ANALYST                                                                                                                 
PRESIDENT                                                                                                               
SALESMAN                                                                                                                
CLERK                                                                                                                   

JOB                                                                                                                     
---------                                                                                                               
CLERK                                                                                                                   
ANALYST                                                                                                                 
CLERK                                                                                                                   

已选择14行。

SQL> select DISTINCT job from emp;

JOB                                                                                                                     
---------                                                                                                               
CLERK                                                                                                                   
SALESMAN                                                                                                                
PRESIDENT                                                                                                               
MANAGER                                                                                                                 
ANALYST                                                                                                                 

SQL> select DISTINCT deptno,job from emp;

    DEPTNO JOB                                                                                                          
---------- ---------                                                                                                    
        20 CLERK                                                                                                        
        30 SALESMAN                                                                                                     
        20 MANAGER                                                                                                      
        30 CLERK                                                                                                        
        10 PRESIDENT                                                                                                    
        30 MANAGER                                                                                                      
        10 CLERK                                                                                                        
        10 MANAGER                                                                                                      
        20 ANALYST                                                                                                      

已选择9行。

SQL> --DISTINCT作用于后面所有的列
SQL> host cls

SQL> --连接符
SQL> select concat('Hello','  World') from emp;

CONCAT('HELL                                                                                                            
------------                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            

CONCAT('HELL                                                                                                            
------------                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            
Hello  World                                                                                                            

已选择14行。
SQL> select concat('Hello','  World') from dual;

CONCAT('HELL                                                                                                            
------------                                                                                                            
Hello  World                                                                                                            

SQL> --dual:伪表
SQL> select 3+2 from dual;

       3+2                                                                                                              
----------                                                                                                              
         5                                                                                                              

SQL> select 'Hello'||'  World' 一列 from dual;

一列                                                                                                                    
------------                                                                                                            
Hello  World                                                                                                            

SQL> --查询员工信息：***的薪水是****
SQL> select ename||'的薪水是'||sal 一列
  2  from emp;

一列                                                                                                                    
----------------------------------------------------------                                                              
SMITH的薪水是800                                                                                                        
ALLEN的薪水是1600                                                                                                       
WARD的薪水是1250                                                                                                        
JONES的薪水是2975                                                                                                       
MARTIN的薪水是1250                                                                                                      
BLAKE的薪水是2850                                                                                                       
CLARK的薪水是2450                                                                                                       
SCOTT的薪水是3000                                                                                                       
KING的薪水是5000                                                                                                        
TURNER的薪水是1500                                                                                                      
ADAMS的薪水是1100                                                                                                       

JAMES的薪水是950                                                                                                        
FORD的薪水是3000                                                                                                        
MILLER的薪水是1300                                                                                                      

已选择14行。

SQL> host cls
日期和字符只能在单引号中出现
SQL> select * from emp;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

Sqlplus
是orcale提供的SQL工具。它有自己的一些命令。
Sql不能缩写。SQLplus可以缩写
Sql:Select, insert, update, delete
Sqlplus: Set, col, ed, c, desc

Isql *Plus （sqlplus的网页版，只在9i和10g里有）
http://Localhost:5560/isqlplus
OracleOraDb10g_home1TNListener
OracleOraDb10g_home1TNLiSQL*Plus (相当于Tomcat，端口5560)
OracleDBConsoleorcl: Orcale的EM管理器 localhost:1158/em (day4-25)


SQL> save c:\a.sql
已创建 file c:\a.sql
SQL> @c:\a.sql

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

SQL> spool off

22.4.	过滤和排序
SQL> --查询10号部门的员工信息
SQL> select *
  2  from emp
  3  where deptno=10;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

SQL> --字符大小写敏感
SQL> select *
  2  from emp
  3  where ename = 'KING';

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where ename = 'King'
SQL> /

未选定行

SQL> --
SQL> --日期格式敏感
查询入职日期为17-11月-81的员工
默认日期格式 DD-MON-RR
SQL> select *
  2  from emp
  3  where hiredate='17-11月-81';

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where hiredate='1981-11-17'
SQL> /
where hiredate='1981-11-17'
               *
第 3 行出现错误: 
ORA-01861: 文字与格式字符串不匹配 


SQL> select sysdate from dual;

SYSDATE                                                                                                                 
--------------                                                                                                          
19-6月 -13                                                                                                              

SQL> select *
  2  from v$nls_parameters;

PARAMETER                                                                                                               
----------------------------------------------------------------                                                        
VALUE                                                                                                                   
----------------------------------------------------------------                                                        
NLS_LANGUAGE                                                                                                            
SIMPLIFIED CHINESE                                                                                                      
                                                                                                                        
NLS_TERRITORY                                                                                                           
CHINA                                                                                                                   
                                                                                                                        
NLS_CURRENCY                                                                                                            
￥                                                                                                                      

NLS_ISO_CURRENCY                                                                                                        
CHINA                                                                                                                   
                                                                                                                        
NLS_NUMERIC_CHARACTERS                                                                                                  
.,                                                                                                                      
                                                                                                                        
NLS_CALENDAR                                                                                                            
GREGORIAN                                                                                                               
                                                                                                                        
NLS_DATE_FORMAT                                                                                                         
DD-MON-RR                                                                                                               
                                                                                                                        
NLS_DATE_LANGUAGE                                                                                                       
SIMPLIFIED CHINESE                                                                                                      
                                                                                                                        
NLS_CHARACTERSET                                                                                                        
ZHS16GBK                                                                                                                

NLS_SORT                                                                                                                
BINARY                                                                                                                  
                                                                                                                        
NLS_TIME_FORMAT                                                                                                         
HH.MI.SSXFF AM                                                                                                          
                                                                                                                        
NLS_TIMESTAMP_FORMAT                                                                                                    
DD-MON-RR HH.MI.SSXFF AM                                                                                                
                                                                                                                        
NLS_TIME_TZ_FORMAT                                                                                                      
HH.MI.SSXFF AM TZR                                                                                                      
                                                                                                                        
NLS_TIMESTAMP_TZ_FORMAT                                                                                                 
DD-MON-RR HH.MI.SSXFF AM TZR                                                                                            
                                                                                                                        
NLS_DUAL_CURRENCY                                                                                                       
￥                                                                                                                      
                                                                                                                        
NLS_NCHAR_CHARACTERSET                                                                                                  
AL16UTF16                                                                                                               
                                                                                                                        
NLS_COMP                                                                                                                
BINARY                                                                                                                  
                                                                                                                        
NLS_LENGTH_SEMANTICS                                                                                                    
BYTE                                                                                                                    
                                                                                                                        
NLS_NCHAR_CONV_EXCP                                                                                                     
FALSE                                                                                                                   
                                                                                                                        

已选择19行。

SQL> col PARAMETER for a30
SQL> /

PARAMETER                      VALUE                                                                                    
------------------------------ ----------------------------------------------------------------                         
NLS_LANGUAGE                   SIMPLIFIED CHINESE                                                                       
NLS_TERRITORY                  CHINA                                                                                    
NLS_CURRENCY                   ￥                                                                                       
NLS_ISO_CURRENCY               CHINA                                                                                    
NLS_NUMERIC_CHARACTERS         .,                                                                                       
NLS_CALENDAR                   GREGORIAN                                                                                
NLS_DATE_FORMAT                DD-MON-RR                                                                                
NLS_DATE_LANGUAGE              SIMPLIFIED CHINESE                                                                       
NLS_CHARACTERSET               ZHS16GBK                                                                                 
NLS_SORT                       BINARY                                                                                   
NLS_TIME_FORMAT                HH.MI.SSXFF AM                                                                           

NLS_TIMESTAMP_FORMAT           DD-MON-RR HH.MI.SSXFF AM                                                                 
NLS_TIME_TZ_FORMAT             HH.MI.SSXFF AM TZR                                                                       
NLS_TIMESTAMP_TZ_FORMAT        DD-MON-RR HH.MI.SSXFF AM TZR                                                             
NLS_DUAL_CURRENCY              ￥                                                                                       
NLS_NCHAR_CHARACTERSET         AL16UTF16                                                                                
NLS_COMP                       BINARY                                                                                   
NLS_LENGTH_SEMANTICS           BYTE                                                                                     
NLS_NCHAR_CONV_EXCP            FALSE                                                                                    

已选择19行。

SQL> host cls

SQL> select *
  2  from v$nls_parameters;

PARAMETER                      VALUE                                                                                    
------------------------------ ----------------------------------------------------------------                         
NLS_LANGUAGE                   SIMPLIFIED CHINESE                                                                       
NLS_TERRITORY                  CHINA                                                                                    
NLS_CURRENCY                   ￥                                                                                       
NLS_ISO_CURRENCY               CHINA                                                                                    
NLS_NUMERIC_CHARACTERS         .,                                                                                       
NLS_CALENDAR                   GREGORIAN                                                                                
NLS_DATE_FORMAT                DD-MON-RR                                                                                
NLS_DATE_LANGUAGE              SIMPLIFIED CHINESE                                                                       
NLS_CHARACTERSET               ZHS16GBK                                                                                 
NLS_SORT                       BINARY                                                                                   
NLS_TIME_FORMAT                HH.MI.SSXFF AM                                                                           

NLS_TIMESTAMP_FORMAT           DD-MON-RR HH.MI.SSXFF AM                                                                 
NLS_TIME_TZ_FORMAT             HH.MI.SSXFF AM TZR                                                                       
NLS_TIMESTAMP_TZ_FORMAT        DD-MON-RR HH.MI.SSXFF AM TZR                                                             
NLS_DUAL_CURRENCY              ￥                                                                                       
NLS_NCHAR_CHARACTERSET         AL16UTF16                                                                                
NLS_COMP                       BINARY                                                                                   
NLS_LENGTH_SEMANTICS           BYTE                                                                                     
NLS_NCHAR_CONV_EXCP            FALSE                                                                                    

已选择19行。

SQL> alter session set NLS_DATE_FORMAT='yyyy-mm-dd';

会话已更改。

SQL> select * from emp where hiredate='1981-11-17';

     EMPNO ENAME    JOB              MGR HIREDATE     SAL       COMM     DEPTNO                                         
---------- -------- --------- ---------- ---------- ----- ---------- ----------                                         
      7839 KING     PRESIDENT            1981-11-17  5000                    10                                         

SQL> alter session set NLS_DATE_FORMAT='DD-MON-RR';

会话已更改。

=, >, <, >=, <=
赋值 :=
Java: int a=0;
Sql: a number :=0;

SQL> host cls

SQL> --between and 在...之间
SQL> --查询薪水1000~2000之间的员工
SQL> select *
  2  from emp
  3  where sal between 1000 and 2000;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择6行。

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where sal between 2000 and 1000
SQL> /

未选定行

SQL> -- Between and 小值在前 大值在后
SQL> host cls

SQL> --in 在集合中
SQL> --查询部门号是10和20的员工
SQL> select *
  2  from emp
  3  where deptno in (10,20);

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择8行。

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where deptno not in (10,20)
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     

已选择6行。

SQL> --思考题:
SQL> --结论:空值3. 如果集合中含有null，不能使用not in,但可以使用in
SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where deptno not in (10,20,null)
SQL> /

未选定行

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where deptno in (10,20,null)
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择8行。

SQL> host cls

SQL> --like 模糊查询 % _
SQL> --查询名字以S打头的员工
SQL> select *
  2  from emp
  3  where ename like 'S%';

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     

SQL> --查询名字是4个字的员工
SQL> select *
  2  from emp
  3  where ename like '____';

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     

SQL> insert into emp(empno,ename,sal,deptno)
  2  values(1001,'Tom_ABCD',5000,10);

已创建 1 行。

SQL> select * from emp;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      1001 Tom_ABCD                                      5000                    10                                     

已选择15行。

SQL> --查询名字中含有下划线的员工
SQL> select *
  2  from emp
  3  where ename like '%_%';

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      1001 Tom_ABCD                                      5000                    10                                     

已选择15行。

SQL> ed
已写入 file afiedt.buf

转义 escape ‘\’
  1  select *
  2  from emp
  3* where ename like '%\_%' escape '\'
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      1001 Tom_ABCD                                      5000                    10                                     

SQL> rollback;
将本次查询的记录从上一次中删除
Mysql是手动开启事务(start transaction); Oracle是自动开启事务

回退已完成。

SQL> select * from emp;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     

      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。


SQL> host cls

SQL> --优化2: where 从右-->左
where condition1 and condition2
逻辑： and, or, not
SQL> host cls

SQL> --排序 order by
SQL> select *
  2  from emp
  3  order by sal;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     

      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     

已选择14行。

SQL> --a命令  append
注意：a后面有2个空格！！
SQL> a  desc
  3* order by sal desc
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     

      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     

已选择14行。

SQL> --order by后面+ [列名  表达式  别名 序号（第几列）]
SQL> --查询员工信息 按照年薪排序
SQL> select ename,sal,sal*12
  2  from emp
  3  order by sal*12;

ENAME      SAL     SAL*12                                                                                               
-------- ----- ----------                                                                                               
SMITH      800       9600                                                                                               
JAMES      950      11400                                                                                               
ADAMS     1100      13200                                                                                               
WARD      1250      15000                                                                                               
MARTIN    1250      15000                                                                                               
MILLER    1300      15600                                                                                               
TURNER    1500      18000                                                                                               
ALLEN     1600      19200                                                                                               
CLARK     2450      29400                                                                                               
BLAKE     2850      34200                                                                                               
JONES     2975      35700                                                                                               

SCOTT     3000      36000                                                                                               
FORD      3000      36000                                                                                               
KING      5000      60000                                                                                               

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select ename,sal,sal*12 年薪
  2  from emp
  3* order by 年薪
SQL> /

ENAME      SAL       年薪                                                                                               
-------- ----- ----------                                                                                               
SMITH      800       9600                                                                                               
JAMES      950      11400                                                                                               
ADAMS     1100      13200                                                                                               
WARD      1250      15000                                                                                               
MARTIN    1250      15000                                                                                               
MILLER    1300      15600                                                                                               
TURNER    1500      18000                                                                                               
ALLEN     1600      19200                                                                                               
CLARK     2450      29400                                                                                               
BLAKE     2850      34200                                                                                               
JONES     2975      35700                                                                                               

SCOTT     3000      36000                                                                                               
FORD      3000      36000                                                                                               
KING      5000      60000                                                                                               

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select ename,sal,sal*12 年薪
  2  from emp
  3* order by 3
SQL> /

ENAME      SAL       年薪                                                                                               
-------- ----- ----------                                                                                               
SMITH      800       9600                                                                                               
JAMES      950      11400                                                                                               
ADAMS     1100      13200                                                                                               
WARD      1250      15000                                                                                               
MARTIN    1250      15000                                                                                               
MILLER    1300      15600                                                                                               
TURNER    1500      18000                                                                                               
ALLEN     1600      19200                                                                                               
CLARK     2450      29400                                                                                               
BLAKE     2850      34200                                                                                               
JONES     2975      35700                                                                                               

SCOTT     3000      36000                                                                                               
FORD      3000      36000                                                                                               
KING      5000      60000                                                                                               

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select ename,sal,sal*12 年薪
  2  from emp
  3* order by 4
SQL> /
order by 4
         *
第 3 行出现错误: 
ORA-01785: ORDER BY 项必须是 SELECT-list 表达式的数目 


SQL> host cls

SQL> --order by 后面+多列
SQL> select *
  2  from emp
  3  order by deptno,sal;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     

已选择14行。

SQL> --含义： 先按照第一列排序，如果相同，再按照第二列排序，以此类推
SQL> --order by作用于后面所有的列
SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* order by deptno,sal desc
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     

已选择14行。

SQL> --desc只作用于离他最近的一列
SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* order by deptno desc,sal desc
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     

已选择14行。

SQL> host cls

SQL> --查询员工信息，按照奖金排序
SQL> --空值4
SQL> select * from emp order by comm;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     

      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     

已选择14行。

SQL> set pagesize 20
SQL>  select * from emp order by comm;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     

已选择14行。

SQL> select * from emp order by comm desc;

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     

已选择14行。

SQL> ed
已写入 file afiedt.buf

  1  select * 
  2  from emp 
  3  order by comm desc
  4* nulls last
SQL> /

     EMPNO ENAME    JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                     
---------- -------- --------- ---------- -------------- ----- ---------- ----------                                     
      7654 MARTIN   SALESMAN        7698 28-9月 -81      1250       1400         30                                     
      7521 WARD     SALESMAN        7698 22-2月 -81      1250        500         30                                     
      7499 ALLEN    SALESMAN        7698 20-2月 -81      1600        300         30                                     
      7844 TURNER   SALESMAN        7698 08-9月 -81      1500          0         30                                     
      7788 SCOTT    ANALYST         7566 13-7月 -87      3000                    20                                     
      7839 KING     PRESIDENT            17-11月-81      5000                    10                                     
      7876 ADAMS    CLERK           7788 13-7月 -87      1100                    20                                     
      7900 JAMES    CLERK           7698 03-12月-81       950                    30                                     
      7902 FORD     ANALYST         7566 03-12月-81      3000                    20                                     
      7934 MILLER   CLERK           7782 23-1月 -82      1300                    10                                     
      7698 BLAKE    MANAGER         7839 01-5月 -81      2850                    30                                     
      7566 JONES    MANAGER         7839 02-4月 -81      2975                    20                                     
      7369 SMITH    CLERK           7902 17-12月-80       800                    20                                     
      7782 CLARK    MANAGER         7839 09-6月 -81      2450                    10                                     

已选择14行。

SQL> spool off

22.5.	单行函数

SQL> --字符函数
Lower, upper, initcap

SQL> select lower('Hello WORLd') 转小写,upper('Hello WORLd') 转大写,
  2         initcap('hello world') 首字母大写
  3  from dual;

Concat, Substr, length/lengthb, instr, lpad | rpad, trim, replace

转小写      转大写      首字母大写                                              
----------- ----------- -----------                                             
hello world HELLO WORLD Hello World                                             

SQL> --substr(a,b) 从a中，第b位开始取，取右边所有的字符
SQL> select substr('hello world',3) from dual;

SUBSTR('H                                                                       
---------                                                                       
llo world                                                                       

SQL> --substr(a,b,c) 从a中，第b位开始取，取c位
SQL> select substr('hello world',3,4) from dual;

SUBS                                                                            
----                                                                            
llo                                                                             

SQL> host cls

SQL> --length 字符数  lengthb 字节数
SQL> select length('hello world')  字符数,lengthb('hello world')  字节数
  2  from dual;

    字符数     字节数                                                           
---------- ----------                                                           
        11         11                                                           

SQL> ed
已写入 file afiedt.buf

  1  select length('中国')  字符数,lengthb('中国')  字节数
  2* from dual
SQL> /

    字符数     字节数                                                           
---------- ----------                                                           
         2          4                                                           

SQL> host cls

SQL> --instr(a,b) 从a中查找b，找到返回下标，否则返回0
SQL> select instr('hello world','ll') from dual;

INSTR('HELLOWORLD','LL')                                                        
------------------------                                                        
                       3                                                        

SQL> --提示:第二天的课后作业
SQL> host cls

SQL> --lpad 左填充 rpad右填充
SQL> select lpad('abcd',10,'*') 左,rpad('abcd',10,'*') 右
  2  from dual;

左         右                                                                   
---------- ----------                                                           
******abcd abcd******                                                           

SQL> --trim: 去掉前后指定的字符
SQL> select trim('H' from  'Hello WorldH') from dual;

TRIM('H'FR                                                                      
----------                                                                      
ello World                                                                      

SQL> --replace 替换
SQL> select replace('hello world',
  2  'l','*') from dual;

REPLACE('HE                                                                     
-----------                                                                     
he**o wor*d                                                                     

数值函数: Round, trunc (可以是数值，日期)
SQL> host cls

SQL> --四舍五入
SQL> select ROUND(45.926, 2) 一,ROUND(45.926, 1) 二,ROUND(45.926, 0) 三,
  2         ROUND(45.926, -1) 四, ROUND(45.926, -2) 五
  3  from dual;

        一         二         三         四         五                          
---------- ---------- ---------- ---------- ----------                          
     45.93       45.9         46         50          0                          

SQL> ed
已写入 file afiedt.buf

  1  select TRUNC(45.926, 2) 一,TRUNC(45.926, 1) 二,TRUNC(45.926, 0) 三,
  2         TRUNC(45.926, -1) 四, TRUNC(45.926, -2) 五
  3* from dual
SQL> /

        一         二         三         四         五                          
---------- ---------- ---------- ---------- ----------                          
     45.92       45.9         45         40          0                          

SQL> host cls

日期函数: Date, systimestamp
(mysql: date, datetime)
Month_between, add_months, next_day, last_day, round, trunc

SQL> --日期函数
SQL> select sysdate from dual;

SYSDATE                                                                         
--------------                                                                  
19-6月 -13                                                                      

SQL> select to_char(sysdate,'yyyy-mm-dd hh24:mi:ss') from dual;

TO_CHAR(SYSDATE,'YY                                                             
-------------------                                                             
2013-06-19 14:22:23                                                             

SQL> select to_char(systimestamp,'yyyy-mm-dd hh24:mi:ss:ff') from dual;

TO_CHAR(SYSTIMESTAMP,'YYYY-MM                                                   
-----------------------------                                                   
2013-06-19 14:23:22:000000              (microsecond)                                         

SQL> select to_char(systimestamp,'yyyy-mm-dd hh24:mi:ss:ff') from dual;

TO_CHAR(SYSTIMESTAMP,'YYYY-MM                                                   
-----------------------------                                                   
2013-06-19 14:23:24:843000                                                      

SQL> --昨天 今天 明天
SQL> select (sysdate-1) 昨天, sysdate 今天,(sysdate+1) 明天
  2  from dual;

昨天           今天           明天                                              
-------------- -------------- --------------                                    
18-6月 -13     19-6月 -13     20-6月 -13                                        

SQL> host cls

SQL> --计算员工的工龄
SQL> select ename,hiredate,(sysdate-hiredate) 天, (sysdate-hiredate)/7 星期,
  2                        (sysdate-hiredate)/30 月,(sysdate-hiredate)/365 年
  3  from emp;

ENAME      HIREDATE               天       星期         月         年           
---------- -------------- ---------- ---------- ---------- ----------           
SMITH      17-12月-80     11872.6018 1696.08597 395.753392 32.5276761           
ALLEN      20-2月 -81     11807.6018 1686.80025 393.586725 32.3495939           
WARD       22-2月 -81     11805.6018 1686.51454 393.520059 32.3441144           
JONES      02-4月 -81     11766.6018 1680.94311 392.220059 32.2372651           
MARTIN     28-9月 -81     11587.6018 1655.37168 386.253392 31.7468541           
BLAKE      01-5月 -81     11737.6018 1676.80025 391.253392  32.157813           
CLARK      09-6月 -81     11698.6018 1671.22882 389.953392 32.0509637           
SCOTT      13-7月 -87     703435.602   100490.8 23447.8534 1927.22083           
KING       17-11月-81     11537.6018 1648.22882 384.586725 31.6098678           
TURNER     08-9月 -81     11607.6018 1658.22882 386.920059 31.8016487           
ADAMS      13-7月 -87     703435.602   100490.8 23447.8534 1927.22083           

JAMES      03-12月-81     11521.6018 1645.94311 384.053392 31.5660322           
FORD       03-12月-81     11521.6018 1645.94311 384.053392 31.5660322           
MILLER     23-1月 -82     11470.6018 1638.65739 382.353392 31.4263062           

已选择14行。

SQL> select sysdate+hiredate from emp;
select sysdate+hiredate from emp
              *
第 1 行出现错误: 
ORA-00975: 不允许日期 + 日期 


SQL> host cls

SQL> --last_day 日期所在月份的最后一天
SQL> select last_day(sysdate) from dual;

LAST_DAY(SYSDA                                                                  
--------------                                                                  
30-6月 -13                                                                      

SQL> --MONTHS_BETWEEN 返回两个日期相差的月数
SQL> select ename,hiredate,(sysdate-hiredate)/30 一,MONTHS_BETWEEN(sysdate,hiredate) 二
  2  from emp;

ENAME      HIREDATE               一         二                                 
---------- -------------- ---------- ----------                                 
SMITH      17-12月-80     395.753475 390.084008                                 
ALLEN      20-2月 -81     393.586809 387.987234                                 
WARD       22-2月 -81     393.520142 387.922718                                 
JONES      02-4月 -81     392.220142 386.567879                                 
MARTIN     28-9月 -81     386.253475  380.72917                                 
BLAKE      01-5月 -81     391.253475 385.600137                                 
CLARK      09-6月 -81     389.953475 384.342073                                 
SCOTT      13-7月 -87     23447.8535  23111.213                                 
KING       17-11月-81     384.586809 379.084008                                 
TURNER     08-9月 -81     386.920142 381.374331                                 
ADAMS      13-7月 -87     23447.8535  23111.213                                 

ENAME      HIREDATE               一         二                                 
---------- -------------- ---------- ----------                                 
JAMES      03-12月-81     384.053475 378.535621                                 
FORD       03-12月-81     384.053475 378.535621                                 
MILLER     23-1月 -82     382.353475  376.89046                                 

已选择14行。

SQL> --ADD_MONTHS: 加上若干个月
SQL> select ADD_MONTHS(sysdate,100) from dual;

ADD_MONTHS(SYS                                                                  
--------------                                                                  
19-10月-21                                                                      

SQL> host cls

SQL> --next_day
SQL> select next_day(sysdate,'星期三') from dual;

NEXT_DAY(SYSDA                                                                  
--------------                                                                  
26-6月 -13                                                                      

Next_day
SQL> select next_day(sysdate,'星期四') from dual;

NEXT_DAY(SYSDA                                                                  
--------------                                                                  
20-6月 -13                                                                      

SQL> --提示: next_day应用： 每个星期一做数据备份
SQL> --第四天： day04-分布式数据库
SQL> select next_day(sysdate,'礼拜四') from dual;
select next_day(sysdate,'礼拜四') from dual
                        *
第 1 行出现错误: 
ORA-01846: 周中的日无效 
星期日（不是星期天）

SQL> host cls

SQL> select round(sysdate,'month'),  round(sysdate,'year') from dual;

ROUND(SYSDATE, ROUND(SYSDATE,                                                   
-------------- --------------                                                   
01-7月 -13     01-1月 -13                                                       

转换函数
隐式转换：oracle自动转换 where hiredate=’17-11月-81’
	Varchar2 or char -> number
	Varchar2 or char -> date
	Number -> varchar2
	Date -> varchar2
显示转换：
To_char, to_number, to_date, to_char
 
注意格式：
	YYYY, YEAR, MM, MONTH, DY, DAY, DD
常用日期格式：
 
常用数字格式：
 
SQL> --隐式转换的前提： 被转换对象是可以转换的
SQL> --显式转换
SQL> --显示当前时间: 2013-06-19 14:45:23今天是星期三
SQL> select to_char(sysdate,'yyyy-mm-dd hh24:mi:ss"今天是" day') from dual;

TO_CHAR(SYSDATE,'YYYY-MM-DDHH24:MI:                                             
-----------------------------------                                             
2013-06-19 14:46:59今天是 星期三                                                

SQL> --查询员工薪水： 两位小数 货币代码  千位符
SQL> select to_char(sal,'L9,999.99') from emp;

TO_CHAR(SAL,'L9,999                                                             
-------------------                                                             
           ￥800.00                                                             
         ￥1,600.00                                                             
         ￥1,250.00                                                             
         ￥2,975.00                                                             
         ￥1,250.00                                                             
         ￥2,850.00                                                             
         ￥2,450.00                                                             
         ￥3,000.00                                                             
         ￥5,000.00                                                             
         ￥1,500.00                                                             
         ￥1,100.00                                                             

         ￥950.00                                                             
         ￥3,000.00                                                             
         ￥1,300.00                                                             

已选择14行。

SQL> host cls

通用函数
使用于任何数据类型，包括null
nvl(exp1, exp2), 
nvl2(exp1, exp2, exp3)
 nullif, coalesce
SQL> --通用函数
SQL> --nvl2(a,b,c) 当a=null时，返回c，否则返回b
SQL> select sal*12+nvl2(comm,comm,0) from emp;

SAL*12+NVL2(COMM,COMM,0)                                                        
------------------------                                                        
                    9600                                                        
                   19500                                                        
                   15500                                                        
                   35700                                                        
                   16400                                                        
                   34200                                                        
                   29400                                                        
                   36000                                                        
                   60000                                                        
                   18000                                                        
                   13200                                                        

                   11400                                                        
                   36000                                                        
                   15600                                                        

已选择14行。

SQL> host cls

SQL> --NULLIF(a,b) 当a==b时, 返回null，否则返回a
SQL> select nullif('abc','abc') from dual
  2  ;

NUL                                                                             
---                                                                             
                                                                                

SQL> select nullif('abc','abcd') from dual;

NUL                                                                             
---                                                                             
abc                                                                             

SQL> --COALESCE :从左往右找到第一个不为null的值
SQL> select comm,sal,COALESCE(comm,sal) from emp;

      COMM        SAL COALESCE(COMM,SAL)                                        
---------- ---------- ------------------                                        
                  800                800                                        
       300       1600                300                                        
       500       1250                500                                        
                 2975               2975                                        
      1400       1250               1400                                        
                 2850               2850                                        
                 2450               2450                                        
                 3000               3000                                        
                 5000               5000                                        
         0       1500                  0                                        
                 1100               1100                                        

      COMM        SAL COALESCE(COMM,SAL)                                        
---------- ---------- ------------------                                        
                  950                950                                        
                 3000               3000                                        
                 1300               1300                                        

已选择14行。

SQL> host cls

条件表达式 decode
使用if-then-else逻辑
Case: SQL99的语法，比较繁琐: case when else end
Decode: oracle自己的，比较简洁
SQL> --涨工资，总裁1000 经理800 其他400
SQL> select ename,job,sal 涨前薪水,
  2         case job when 'PRESIDENT' then sal+1000
  3                  when 'MANAGER' then sal+800
  4                  else sal+400
  5          end 涨后薪水
  6  from emp;

ENAME      JOB         涨前薪水   涨后薪水                                      
---------- --------- ---------- ----------                                      
SMITH      CLERK            800       1200                                      
ALLEN      SALESMAN        1600       2000                                      
WARD       SALESMAN        1250       1650                                      
JONES      MANAGER         2975       3775                                      
MARTIN     SALESMAN        1250       1650                                      
BLAKE      MANAGER         2850       3650                                      
CLARK      MANAGER         2450       3250                                      
SCOTT      ANALYST         3000       3400                                      
KING       PRESIDENT       5000       6000                                      
TURNER     SALESMAN        1500       1900                                      
ADAMS      CLERK           1100       1500                                      

JAMES      CLERK            950       1350                                      
FORD       ANALYST         3000       3400                                      
MILLER     CLERK           1300       1700                                      

已选择14行。

SQL> select ename,job,sal 涨前薪水,
  2         decode(job,'PRESIDENT',sal+1000,
  3                    'MANAGER',sal+800,
  4                              sal+400) 涨后薪水
  5  from emp;

ENAME      JOB         涨前薪水   涨后薪水                                      
---------- --------- ---------- ----------                                      
SMITH      CLERK            800       1200                                      
ALLEN      SALESMAN        1600       2000                                      
WARD       SALESMAN        1250       1650                                      
JONES      MANAGER         2975       3775                                      
MARTIN     SALESMAN        1250       1650                                      
BLAKE      MANAGER         2850       3650                                      
CLARK      MANAGER         2450       3250                                      
SCOTT      ANALYST         3000       3400                                      
KING       PRESIDENT       5000       6000                                      
TURNER     SALESMAN        1500       1900                                      
ADAMS      CLERK           1100       1500                                      

JAMES      CLERK            950       1350                                      
FORD       ANALYST         3000       3400                                      
MILLER     CLERK           1300       1700                                      

已选择14行。

SQL> spool off

使用decode函数的一个例子：根据80号部门员工的工资，显示税率：
SQL> SELECT last_name, salary, DECODE (TRUNC(salary/2000, 0), 
	0, 0.00,
	1, 0.09,
	2, 0.20,
	3, 0.30,
	4, 0.40,
	5, 0.42,
	6, 0.44,
	0.45) TAX_RATE
FROM employees
WHERE department_id = 80;


分组函数
Group by, having
Avg, count, max, min, sum
SQL> --工资总额
SQL> select sum(sal) from emp;

注意：
Select a, b, c, 分组函数(x)
From ****
Group by a, b, c;
要查询的列要出现在group by里！！反过来不一定：group a, b, c, d

  SUM(SAL)                                                                      
----------                                                                      
     29025                                                                      
SQL> --人数
SQL> select count(*) from emp;

  COUNT(*)                                                                      
----------                                                                      
        14                                                                      

SQL> --平均工资
SQL> select sum(sal)/count(*) 一,avg(sal) 二 from emp;

        一         二                                                           
---------- ----------                                                           
2073.21429 2073.21429                                                           

SQL> --平均奖金: 空值 5
SQL> select sum(comm)/count(*) 一, sum(comm)/count(comm) 二, avg(comm) 三
  2  from emp;

        一         二         三                                                
---------- ---------- ----------                                                
157.142857        550        550                                                

SQL> --空值 5: 组函数自动滤空
SQL> select count(*), count(comm)  from emp;

  COUNT(*) COUNT(COMM)                                                          
---------- -----------                                                          
        14           4                                                          

SQL> select count(*), count(nvl(comm,0))  from emp;

  COUNT(*) COUNT(NVL(COMM,0))                                                   
---------- ------------------                                                   
        14                 14                                                   

SQL> host cls

SQL> --分组数据
SQL> --求每个部门的平均工资
SQL> select deptno,avg(sal)
  2  from emp
  3  group by deptno;

    DEPTNO   AVG(SAL)                                                           
---------- ----------                                                           
        30 1566.66667                                                           
        20       2175                                                           
        10 2916.66667                                                           

SQL> select detpno,job,sum(sal)
  2  from emp
  3  group by deptno,job;
select detpno,job,sum(sal)
       *
第 1 行出现错误: 
ORA-00904: "DETPNO": 标识符无效 


SQL> ed
已写入 file afiedt.buf

  1  select deptno,job,sum(sal)
  2  from emp
  3* group by deptno,job
SQL> /

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        20 CLERK           1900                                                 
        30 SALESMAN        5600                                                 
        20 MANAGER         2975                                                 
        30 CLERK            950                                                 
        10 PRESIDENT       5000                                                 
        30 MANAGER         2850                                                 
        10 CLERK           1300                                                 
        10 MANAGER         2450                                                 
        20 ANALYST         6000                                                 

已选择9行。

SQL> ed
已写入 file afiedt.buf

  1  select deptno,job,sum(sal)
  2  from emp
  3  group by deptno,job
  4* order by 1
SQL> /

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        10 CLERK           1300                                                 
        10 MANAGER         2450                                                 
        10 PRESIDENT       5000                                                 
        20 ANALYST         6000                                                 
        20 CLERK           1900                                                 
        20 MANAGER         2975                                                 
        30 CLERK            950                                                 
        30 MANAGER         2850                                                 
        30 SALESMAN        5600                                                 

已选择9行。

过滤分组having
Where 字句中不能使用组函数。其他一样。

SQL> select deptno,avg(sal)
  2  from emp
  3  group by deptno
  4  having avg(sal)>2000;

    DEPTNO   AVG(SAL)                                                           
---------- ----------                                                           
        20       2175                                                           
        10 2916.66667                                                           

SQL> --求10号部门的平均工资
SQL> select deptno,avg(sal)
  2  from emp
  3  group by deptno
  4  having deptno=10;

    DEPTNO   AVG(SAL)                                                           
---------- ----------                                                           
        10 2916.66667                                                           

SQL> ed
已写入 file afiedt.buf

  1  select deptno,avg(sal)
  2  from emp
  3  where deptno=10
  4* group by deptno
  5  /

    DEPTNO   AVG(SAL)                                                           
---------- ----------                                                           
        10 2916.66667                                                           

SQL> --优化4: 尽量使用where
先过滤再分组效率高
SQL> host cls

SQL> /*
SQL> group by的增强 rollup
报表：小计、总计
group by rollup(a,b)相当于3句：
SQL> group by a,b
SQL> group by a
SQL> group by null

 
SQL> group by deptno,job
SQL> +
SQL> group by deptno
SQL> +
SQL> group by null
SQL> =
SQL> group by rollup(deptno,job)
SQL> 
SQL> group by rollup(a,b)
SQL> =
SQL> group by a,b
SQL> +
SQL> group by a
SQL> +
SQL> group by null
SQL> */
SQL> select deptno,job,sum(sal)
  2  from emp
  3  group by rollup(deptno,job);

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        10 CLERK           1300                                                 
        10 MANAGER         2450                                                 
        10 PRESIDENT       5000                                                 
        10                 8750                                                 
        20 CLERK           1900                                                 
        20 ANALYST         6000                                                 
        20 MANAGER         2975                                                 
        20                10875                                                 
        30 CLERK            950                                                 
        30 MANAGER         2850                                                 
        30 SALESMAN        5600                                                 

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        30                 9400                                                 
                          29025                                                 

已选择13行。

SQL> break on deptno skip 2
Break on deptno: 只显示一次
Skip: 空2行

SQL> select deptno,job,sum(sal)
  2  from emp
  3  group by rollup(deptno,job);

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        10 CLERK           1300                                                 
           MANAGER         2450                                                 
           PRESIDENT       5000                                                 
                           8750                                                 
                                                                                
                                                                                
        20 CLERK           1900                                                 
           ANALYST         6000                                                 
           MANAGER         2975                                                 
                          10875                                                 
                                                                                

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
                                                                                
        30 CLERK            950                                                 
           MANAGER         2850                                                 
           SALESMAN        5600                                                 
                           9400                                                 
                                                                                
                                                                                
                          29025                                                 
                                                                                
                                                                                

已选择13行。

SQL> break on null
SQL> /

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        10 CLERK           1300                                                 
        10 MANAGER         2450                                                 
        10 PRESIDENT       5000                                                 
        10                 8750                                                 
        20 CLERK           1900                                                 
        20 ANALYST         6000                                                 
        20 MANAGER         2975                                                 
        20                10875                                                 
        30 CLERK            950                                                 
        30 MANAGER         2850                                                 
        30 SALESMAN        5600                                                 

    DEPTNO JOB         SUM(SAL)                                                 
---------- --------- ----------                                                 
        30                 9400                                                 
                          29025                                                 

已选择13行。

SQL> spool off


22.6.	多表查询

笛卡尔集：
不一定正确，避免使用
dept					emp*dept					
deptno	dname				empno	ename	sal	deptno	deptno	dname
1	行政部				1000	Tom	5000	1	1	行政部
2	开发部				1001	Mary	3000	2	1	行政部
					1002	Mike	6000	1	1	行政部
					1003	Jerry	4000	1	1	行政部
					1000	Tom	5000	1	2	开发部
emp					1001	Mary	3000	2	2	开发部
empno	ename	sal	deptno		1002	Mike	6000	1	2	开发部
1000	Tom	5000	1		1003	Jerry	4000	1	2	开发部
1001	Mary	3000	2							
1002	Mike	6000	1							
1003	Jerry	4000	1			连接条件	emp.deptno=dept.deptno

连接的类型
Oracle: Equijoin, non-equijoin, outer join, self join
SQL1999: cross joins, natural joins, using clause, full or two sided outer joins
SQL> host cls

SQL> --等值连接
SQL> --查询员工信息： 员工号 姓名 月薪 部门名称
SQL> select e.empno,e.ename,e.sal,d.dname
  2  from emp e,dept d
  3  where e.deptno=d.deptno;

     EMPNO ENAME             SAL DNAME                                          
---------- ---------- ---------- --------------                                 
      7369 SMITH             800 RESEARCH                                       
      7499 ALLEN            1600 SALES                                          
      7521 WARD             1250 SALES                                          
      7566 JONES            2975 RESEARCH                                       
      7654 MARTIN           1250 SALES                                          
      7698 BLAKE            2850 SALES                                          
      7782 CLARK            2450 ACCOUNTING                                     
      7788 SCOTT            3000 RESEARCH                                       
      7839 KING             5000 ACCOUNTING                                     
      7844 TURNER           1500 SALES                                          
      7876 ADAMS            1100 RESEARCH                                       

     EMPNO ENAME             SAL DNAME                                          
---------- ---------- ---------- --------------                                 
      7900 JAMES             950 SALES                                          
      7902 FORD             3000 RESEARCH                                       
      7934 MILLER           1300 ACCOUNTING                                     

已选择14行。

SQL>  --不等值连接
SQL> --查询员工信息： 员工号 姓名 月薪 工资级别
SQL> select * from salgrade;

     GRADE      LOSAL      HISAL                                                
---------- ---------- ----------                                                
         1        700       1200                                                
         2       1201       1400                                                
         3       1401       2000                                                
         4       2001       3000                                                
         5       3001       9999                                                

SQL> select e.empno,e.ename,e.sal,s.grade
  2  from emp e,salgrade s
  3  where e.sal between s.losal and s.hisal;

     EMPNO ENAME             SAL      GRADE                                     
---------- ---------- ---------- ----------                                     
      7369 SMITH             800          1                                     
      7900 JAMES             950          1                                     
      7876 ADAMS            1100          1                                     
      7521 WARD             1250          2                                     
      7654 MARTIN           1250          2                                     
      7934 MILLER           1300          2                                     
      7844 TURNER           1500          3                                     
      7499 ALLEN            1600          3                                     
      7782 CLARK            2450          4                                     
      7698 BLAKE            2850          4                                     
      7566 JONES            2975          4                                     

     EMPNO ENAME             SAL      GRADE                                     
---------- ---------- ---------- ----------                                     
      7788 SCOTT            3000          4                                     
      7902 FORD             3000          4                                     
      7839 KING             5000          5                                     

已选择14行。

SQL> host cls

SQL> --外连接
SQL> --按部门统计员工人数： 部门号 部门名称 人数
SQL> select d.deptno,d.dname,count(e.empno)
  2  from emp e,dept d
  3  where e.deptno=d.deptno
  4  group by d.deptno,d.dname;

    DEPTNO DNAME          COUNT(E.EMPNO)                                        
---------- -------------- --------------                                        
        10 ACCOUNTING                  3                                        
        20 RESEARCH                    5                                        
        30 SALES                       6                                        

SQL> ed
已写入 file afiedt.buf

  1  select d.deptno 部门号,d.dname 部门名称,count(e.empno) 人数
  2  from emp e,dept d
  3  where e.deptno=d.deptno
  4* group by d.deptno,d.dname
SQL> /

    部门号 部门名称             人数                                            
---------- -------------- ----------                                            
        10 ACCOUNTING              3                                            
        20 RESEARCH                5                                            
        30 SALES                   6                                            

SQL> select count(*) from emp;

  COUNT(*)                                                                      
----------                                                                      
        14                                                                      

SQL> select * from dept;

    DEPTNO DNAME          LOC                                                   
---------- -------------- -------------                                         
        10 ACCOUNTING     NEW YORK                                              
        20 RESEARCH       DALLAS                                                
        30 SALES          CHICAGO                                               
        40 OPERATIONS     BOSTON                                                

SQL> select * from emp where deptno=40;

未选定行

SQL> /*
SQL> 希望： 在最后的结果中，包含某些不成立的记录
SQL> 外连接:
SQL> 左外连接: 当where e.deptno=d.deptno不成立的时候,等号左边所代表的表 任然被包含
SQL>         写法: where e.deptno=d.deptno(+)
SQL> 右外连接: 当where e.deptno=d.deptno不成立的时候,等号右边所代表的表 任然被包含
SQL>         写法:where e.deptno(+)=d.deptno
SQL> */
SQL> select d.deptno,d.dname,count(e.empno)
  2  from emp e,dept d
  3  where e.deptno(+)=d.deptno
  4  group by d.deptno,d.dname;

    DEPTNO DNAME          COUNT(E.EMPNO)                                        
---------- -------------- --------------                                        
        10 ACCOUNTING                  3                                        
        40 OPERATIONS                  0                                        
        20 RESEARCH                    5                                        
        30 SALES                       6                                        

SQL> ed
已写入 file afiedt.buf

  1  select d.deptno,d.dname,count(e.empno)
  2  from emp e,dept d
  3  where e.deptno(+)=d.deptno
  4  group by d.deptno,d.dname
  5* order by 1
SQL> /

    DEPTNO DNAME          COUNT(E.EMPNO)                                        
---------- -------------- --------------                                        
        10 ACCOUNTING                  3                                        
        20 RESEARCH                    5                                        
        30 SALES                       6                                        
        40 OPERATIONS                  0                                        

SQL> host cls

SQL> --自连接
SQL> --查询员工信息：***的老板是***
SQL> 
SQL> select * from emp;

SQL> set linesize 120
SQL> col sal for 999
SQL> col sal for 9999
SQL> host cls

SQL> select * from emp;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7369 SMITH      CLERK           7902 17-12月-80       800                    20                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   

      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择14行。

SQL> --自连接：通过表的别名，将同一张表视为多张表
SQL> select e.ename||'的老板是'||b.ename
  2  from emp e,emp b
  3  where e.mgr=b.empno;

E.ENAME||'的老板是'||B.ENAME                                                                                            
----------------------------                                                                                            
FORD的老板是JONES                                                                                                       
SCOTT的老板是JONES                                                                                                      
JAMES的老板是BLAKE                                                                                                      
TURNER的老板是BLAKE                                                                                                     
MARTIN的老板是BLAKE                                                                                                     
WARD的老板是BLAKE                                                                                                       
ALLEN的老板是BLAKE                                                                                                      
MILLER的老板是CLARK                                                                                                     
ADAMS的老板是SCOTT                                                                                                      
CLARK的老板是KING                                                                                                       
BLAKE的老板是KING                                                                                                       

E.ENAME||'的老板是'||B.ENAME                                                                                            
----------------------------                                                                                            
JONES的老板是KING                                                                                                       
SMITH的老板是FORD                                                                                                       

已选择13行。

SQL> select count(*)
  2  from emp e,emp b;

  COUNT(*)                                                                                                              
----------                                                                                                              
       196                                                                                                              
=14*14
自连接不适合做大表操作。指数增长！
SQL> --层次查询
只能有一张表！
 
SQL> desc emp
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 EMPNO                                                             NOT NULL NUMBER(4)
 ENAME                                                                      VARCHAR2(10)
 JOB                                                                        VARCHAR2(9)
 MGR                                                                        NUMBER(4)
 HIREDATE                                                                   DATE
 SAL                                                                        NUMBER(7,2)
 COMM                                                                       NUMBER(7,2)
 DEPTNO                                                                     NUMBER(2)

SQL> select level,empno,ename,sal,mgr
  2  from emp
  3  connect by prior empno=mgr
  4  start with mgr is null
  5  order by 1;

     LEVEL      EMPNO ENAME        SAL        MGR                                                                       
---------- ---------- ---------- ----- ----------                                                                       
         1       7839 KING        5000                                                                                  
         2       7566 JONES       2975       7839                                                                       
         2       7698 BLAKE       2850       7839                                                                       
         2       7782 CLARK       2450       7839                                                                       
         3       7902 FORD        3000       7566                                                                       
         3       7521 WARD        1250       7698                                                                       
         3       7900 JAMES        950       7698                                                                       
         3       7934 MILLER      1300       7782                                                                       
         3       7499 ALLEN       1600       7698                                                                       
         3       7788 SCOTT       3000       7566                                                                       
         3       7654 MARTIN      1250       7698                                                                       

     LEVEL      EMPNO ENAME        SAL        MGR                                                                       
---------- ---------- ---------- ----- ----------                                                                       
         3       7844 TURNER      1500       7698                                                                       
         4       7876 ADAMS       1100       7788                                                                       
         4       7369 SMITH        800       7902                                                                       

已选择14行。

SQL> /*
SQL> 执行的过程:
SQL> 1. KING: start with mgr is null ---> empno=7839
SQL> 2. where mgr = 7839; ---> 7566 7698 7782
SQL> 3. where mgr in (7566 7698 7782)*/
SQL> spool off

22.7.	子查询
SQL> host cls

SQL> --查询工资比SCOTT高的员工信息
SQL> --1. SCOTT的工资
SQL> select sal from emp where ename='SCOTT';

       SAL                                                                      
----------                                                                      
      3000                                                                      

SQL> --2.比3000高的
SQL> set linesize 120
SQL> col sal for 9999
SQL> select * from emp where sal > 3000;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   

SQL> --解决的问题：不能一步求解
SQL> select *
  2  from emp
  3  where sal > (select sal
  4               from emp
  5               where ename='SCOTT');

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   

SQL> /*
SQL> 注意的问题
SQL> 1. 括号
SQL> 2. 合理的书写风格
SQL> 3. 可以主查询的where select from having后面放置子查询
	Select后面必须是单行子查询（只返回一行记录）
SQL> 4. 不可以在主查询的group by后面放置子查询
SQL> 5. 强调from后面的子查询
SQL> 6. 主查询和子查询可以不是同一张表，只要子查询返回的结果 主查询可以使用即可
SQL> 7. 一般不在子查询使用order by，但在Top-N分析问题中 必须使用order by
SQL> 8. 一般先执行子查询，再执行主查询；但相关子查询除外
SQL> 9. 单行子查询只能使用单行操作符 多行子查询只能使用多行操作符
SQL> 10. 子查询中null
SQL> */
SQL> -- 3. 可以主查询的where select from having后面放置子查询
SQL> select ename,sal,(select job from emp where empno=7839) 一列
  2  from emp;

ENAME        SAL 一列                                                                                                   
---------- ----- ---------                                                                                              
SMITH        800 PRESIDENT                                                                                              
ALLEN       1600 PRESIDENT                                                                                              
WARD        1250 PRESIDENT                                                                                              
JONES       2975 PRESIDENT                                                                                              
MARTIN      1250 PRESIDENT                                                                                              
BLAKE       2850 PRESIDENT                                                                                              
CLARK       2450 PRESIDENT                                                                                              
SCOTT       3000 PRESIDENT                                                                                              
KING        5000 PRESIDENT                                                                                              
TURNER      1500 PRESIDENT                                                                                              
ADAMS       1100 PRESIDENT                                                                                              

JAMES        950 PRESIDENT                                                                                              
FORD        3000 PRESIDENT                                                                                              
MILLER      1300 PRESIDENT                                                                                              

已选择14行。

SQL> --5. 强调from后面的子查询
SQL> --查询员工的姓名和薪水
SQL> select *
  2  from (select ename,sal from emp);

ENAME        SAL                                                                                                        
---------- -----                                                                                                        
SMITH        800                                                                                                        
ALLEN       1600                                                                                                        
WARD        1250                                                                                                        
JONES       2975                                                                                                        
MARTIN      1250                                                                                                        
BLAKE       2850                                                                                                        
CLARK       2450                                                                                                        
SCOTT       3000                                                                                                        
KING        5000                                                                                                        
TURNER      1500                                                                                                        
ADAMS       1100                                                                                                        

JAMES        950                                                                                                        
FORD        3000                                                                                                        
MILLER      1300                                                                                                        

已选择14行。

SQL> --查询员工的姓名 薪水 年薪
SQL> ed
已写入 file afiedt.buf

  1  select *
  2* from (select ename,sal,sal*12 annlsal from emp)
SQL> /

ENAME        SAL    ANNLSAL                                                                                             
---------- ----- ----------                                                                                             
SMITH        800       9600                                                                                             
ALLEN       1600      19200                                                                                             
WARD        1250      15000                                                                                             
JONES       2975      35700                                                                                             
MARTIN      1250      15000                                                                                             
BLAKE       2850      34200                                                                                             
CLARK       2450      29400                                                                                             
SCOTT       3000      36000                                                                                             
KING        5000      60000                                                                                             
TURNER      1500      18000                                                                                             
ADAMS       1100      13200                                                                                             

JAMES        950      11400                                                                                             
FORD        3000      36000                                                                                             
MILLER      1300      15600                                                                                             

已选择14行。

SQL> --6. 主查询和子查询可以不是同一张表，只要子查询返回的结果 主查询可以使用即可
SQL> --查询部门名称为SALES的员工信息
SQL> select *
  2  from emp
  3  where deptno=(select deptno
  4                from dept
  5                where dname='SALES');

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   

已选择6行。

SQL> select e.*
  2  from emp e,dept d
  3  where e.deptno=d.deptno and d.dname='SALES';

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   

已选择6行。

上面的结果和子查询结果一致。
SQL> --优化5:理论上，尽量使用多表查询
SQL> host cls

单行子查询
只返回一行
使用单行比较操作符：=, >, >=, <, <=, <>

非法子查询
找出各个部门最低薪水的员工信息
SELECT employee_id, last_name
FROM emloyees
WHERE salary = (SELECT MIN(salary)
				FROM emloyees
				GROUP BY department_id);
错误：子查询返回 多条结果

最好的查解决办法： google

多行子查询：in, any, all
SQL> --in 在集合中
SQL> --查询部门名称是SALES和ACCOUNTING的员工
SQL> select *
  2  from emp
  3  where deptno in (select deptno from dept where dname='SALES' or dname='ACCOUNTING');

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择9行。

SQL> select e.*
  2  from emp e,dept d
  3  where e.deptno=d.deptno and (d.dname='SALES' or d.dname='ACCOUNTING');

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择9行。

SQL> --any: 和集合中 任意一个值比较
SQL> --查询工资比30号部门任意一个员工高的员工信息
SQL> select *\
  2  ;
select *\
        *
第 1 行出现错误: 
ORA-00911: 无效字符 


SQL> select *
  2  from emp
  3  where sal > any (select sal from emp where deptno=30);
大于任意一个值 = 大于最小值！！

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   

      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   

已选择12行。

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where sal > (select min(sal) from emp where deptno=30)
SQL> /

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   

      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择12行。

SQL> --all:和集合的所有值比较
SQL>  --查询工资比30号部门所有员工高的员工信息
SQL> select *
  2  from emp
  3  where sal > all (select sal from emp where deptno=30);

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where sal > (select max(sal) from emp where deptno=30)
SQL> /

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   

SQL> host cls

SQL> --多行子查询中null
SQL> --查询不是老板的员工信息
SQL> select * from emp;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7369 SMITH      CLERK           7902 17-12月-80       800                    20                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   

      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择14行。

子查询的null问题
Not in (Null)
All conditions that compare a null value result in a null!
The NOT In operator is equivalent to <> ALL
办法：where empno not in (select mgr from emp where mgr is not null)

SQL> --是老板的员工
SQL> select *
  2  from emp
  3  where empno in (select mgr from emp);

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   
      7698 BLAKE      MANAGER         7839 01-5月 -81      2850                    30                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   

已选择6行。

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where empno not in (select mgr from emp)
SQL> /

未选定行

SQL> ed
已写入 file afiedt.buf

  1  select *
  2  from emp
  3* where empno not in (select mgr from emp where mgr is not null)
SQL> /

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                                   
      7521 WARD       SALESMAN        7698 22-2月 -81      1250        500         30                                   
      7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                                   
      7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   
      7369 SMITH      CLERK           7902 17-12月-80       800                    20                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   
      7900 JAMES      CLERK           7698 03-12月-81       950                    30                                   

已选择8行。

SQL> spool off

22.8.	集合运算
 
SQL> host cls

SQL> /*
SQL> 查询部门号是10和20的员工信息
SQL> 1. select * from emp where deptno in (10,20);
SQL> 2. select * from emp where deptno=10 or deptno=20;
SQL> 3. 集合运算
SQL>    select * from emp where deptno=10
SQL>    加上
SQL>    select * from emp where deptno=20;
SQL> */
SQL> select * from emp where deptno=10
  2  union
  3  select * from emp where deptno=20;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7369 SMITH      CLERK           7902 17-12月-80       800                    20                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7782 CLARK      MANAGER         7839 09-6月 -81      2450                    10                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7839 KING       PRESIDENT            17-11月-81      5000                    10                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   
      7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                                   

已选择8行。

SQL> select deptno,job,sum(sal) from emp group by rollup(deptno,job);

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
        10 MANAGER         2450                                                                                         
        10 PRESIDENT       5000                                                                                         
        10                 8750                                                                                         
        20 CLERK           1900                                                                                         
        20 ANALYST         6000                                                                                         
        20 MANAGER         2975                                                                                         
        20                10875                                                                                         
        30 CLERK            950                                                                                         
        30 MANAGER         2850                                                                                         
        30 SALESMAN        5600                                                                                         

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        30                 9400                                                                                         
                          29025                                                                                         

已选择13行。

SQL> select deptno,job,sum(sal) from emp group by deptno,job
  2  union
  3  select deptno,sum(sal) from emp group by deptno
  4  union
  5  select sum(sal) from emp;
select deptno,sum(sal) from emp group by deptno
*
第 3 行出现错误: 
ORA-01789: 查询块具有不正确的结果列数 


SQL> /*
SQL> 注意的问题
SQL> 1. 参与运算的各个集合必须列数相同 且类型一致
SQL> 2. 采用第一个集合的表头作为最后的表头
SQL> 3. 如果排序，必须 在每个集合后使用相同order by
SQL> 4. 括号
SQL> */
SQL> select deptno,job,sum(sal) from emp group by deptno,job
  2  union
  3  select deptno,to_char(null),sum(sal) from emp group by deptno
  4  union
  5  select to_number(null),to_char(null),sum(sal) from emp;

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
        10 MANAGER         2450                                                                                         
        10 PRESIDENT       5000                                                                                         
        10                 8750                                                                                         
        20 ANALYST         6000                                                                                         
        20 CLERK           1900                                                                                         
        20 MANAGER         2975                                                                                         
        20                10875                                                                                         
        30 CLERK            950                                                                                         
        30 MANAGER         2850                                                                                         
        30 SALESMAN        5600                                                                                         
        30                 9400                                                                                         
                          29025                                                                                         

已选择13行。

SQL> break on deptno skip 2
SQL> select deptno,job,sum(sal) from emp group by deptno,job
  2  union
  3  select deptno,to_char(null),sum(sal) from emp group by deptno
  4  union
  5  select to_number(null),to_char(null),sum(sal) from emp;

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
           MANAGER         2450                                                                                         
           PRESIDENT       5000                                                                                         
                           8750                                                                                         
                                                                                                                        
        20 ANALYST         6000                                                                                         
           CLERK           1900                                                                                         
           MANAGER         2975                                                                                         
                          10875                                                                                         
                                                                                                                       
        30 CLERK            950                                                                                         
           MANAGER         2850                                                                                         
           SALESMAN        5600                                                                                         
                           9400                                                                                         
                                                                                                                        
                          29025                                                                                         
                                                                                                                        
已选择13行。

SQL> break on null
SQL> host cls

SQL> select deptno,job,sum(sal) from emp group by rollup(deptno,job);

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
        10 MANAGER         2450                                                                                         
        10 PRESIDENT       5000                                                                                         
        10                 8750                                                                                         
        20 CLERK           1900                                                                                         
        20 ANALYST         6000                                                                                         
        20 MANAGER         2975                                                                                         
        20                10875                                                                                         
        30 CLERK            950                                                                                         
        30 MANAGER         2850                                                                                         
        30 SALESMAN        5600                                                                                         
        30                 9400                                                                                         
                          29025                                                                                         

已选择13行。

SQL> set timing on
SQL> select deptno,job,sum(sal) from emp group by rollup(deptno,job);

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
        10 MANAGER         2450                                                                                         
        10 PRESIDENT       5000                                                                                         
        10                 8750                                                                                         
        20 CLERK           1900                                                                                         
        20 ANALYST         6000                                                                                         
        20 MANAGER         2975                                                                                         
        20                10875                                                                                         
        30 CLERK            950                                                                                         
        30 MANAGER         2850                                                                                         
        30 SALESMAN        5600                                                                                         
        30                 9400                                                                                         
                          29025                                                                                         

已选择13行。

已用时间:  00: 00: 00.00
SQL> select deptno,job,sum(sal) from emp group by deptno,job
  2  union
  3  select deptno,to_char(null),sum(sal) from emp group by deptno
  4  union
  5  select to_number(null),to_char(null),sum(sal) from emp;

    DEPTNO JOB         SUM(SAL)                                                                                         
---------- --------- ----------                                                                                         
        10 CLERK           1300                                                                                         
        10 MANAGER         2450                                                                                         
        10 PRESIDENT       5000                                                                                         
        10                 8750                                                                                         
        20 ANALYST         6000                                                                                         
        20 CLERK           1900                                                                                         
        20 MANAGER         2975                                                                                         
        20                10875                                                                                         
        30 CLERK            950                                                                                         
        30 MANAGER         2850                                                                                         
        30 SALESMAN        5600                                                                                         
        30                 9400                                                                                         
                          29025                                                                                         

已选择13行。

已用时间:  00: 00: 00.01
SQL> --优化6: 尽量不要使用集合运算
SQL> set timing off
SQL> host cls

SQL> --交集
SQL> select ename,sal from emp
  2  where sal between 700 and 1300
  3  INTERSECT
  4  select ename,sal from emp
  5  where sal between 1201 and 1400;

ENAME        SAL                                                                                                        
---------- -----                                                                                                        
MARTIN      1250                                                                                                        
MILLER      1300                                                                                                        
WARD        1250                                                                                                        

SQL> select ename,sal from emp
  2  where sal between 700 and 1300
  3  minus
  4  select ename,sal from emp
  5  where sal between 1201 and 1400;

ENAME        SAL                                                                                                        
---------- -----                                                                                                        
ADAMS       1100                                                                                                        
JAMES        950                                                                                                        
SMITH        800                                                                                                        

SQL> spool off

22.9.	查询课堂练习3题 
找到员工工资最高的前三名
找到员工表中薪水大于本部门平均薪水的员工
统计每年入职的员工个数（不许使用子查询）

Top N 问题：rownum行号
SQL> -- rownum 行号  伪列
SQL> select rownum, empno,ename,sal
  2  from emp;

    ROWNUM      EMPNO ENAME        SAL                                                                                  
---------- ---------- ---------- -----                                                                                  
         1       7369 SMITH        800                                                                                  
         2       7499 ALLEN       1600                                                                                  
         3       7521 WARD        1250                                                                                  
         4       7566 JONES       2975                                                                                  
         5       7654 MARTIN      1250                                                                                  
         6       7698 BLAKE       2850                                                                                  
         7       7782 CLARK       2450                                                                                  
         8       7788 SCOTT       3000                                                                                  
         9       7839 KING        5000                                                                                  
        10       7844 TURNER      1500                                                                                  
        11       7876 ADAMS       1100                                                                                  
        12       7900 JAMES        950                                                                                  
        13       7902 FORD        3000                                                                                  
        14       7934 MILLER      1300                                                                                  

已选择14行。

SQL> select rownum,empno,ename,sal
  2  from emp
  3  where rownum<=3
  4  order by sal desc;

    ROWNUM      EMPNO ENAME        SAL                                                                                  
---------- ---------- ---------- -----                                                                                  
         2       7499 ALLEN       1600                                                                                  
         3       7521 WARD        1250                                                                                  
         1       7369 SMITH        800                                                                                  

SQL> /*
SQL> 关于行号
SQL> 1. 按照默认的顺序生成（行号不随排序变化）
SQL> 2. rownum只能使用< <=, 不能> >=
*/
SQL> select rownum, empno,ename,sal
  2  from emp
  3  order by sal desc;

    ROWNUM      EMPNO ENAME        SAL                                                                                  
---------- ---------- ---------- -----                                                                                  
         9       7839 KING        5000                                                                                  
        13       7902 FORD        3000                                                                                  
         8       7788 SCOTT       3000                                                                                  
         4       7566 JONES       2975                                                                                  
         6       7698 BLAKE       2850                                                                                  
         7       7782 CLARK       2450                                                                                  
         2       7499 ALLEN       1600                                                                                  
        10       7844 TURNER      1500                                                                                  
        14       7934 MILLER      1300                                                                                  
         3       7521 WARD        1250                                                                                  
         5       7654 MARTIN      1250                                                                                  

    ROWNUM      EMPNO ENAME        SAL                                                                                  
---------- ---------- ---------- -----                                                                                  
        11       7876 ADAMS       1100                                                                                  
        12       7900 JAMES        950                                                                                  
         1       7369 SMITH        800                                                                                  

已选择14行。

SQL> host cls

SQL> --第一题
SQL> select rownum,empno,ename,sal
  2  from (select * from emp order by sal desc)
  3  where rownum<=3;

    ROWNUM      EMPNO ENAME        SAL                                                                                  
---------- ---------- ---------- -----                                                                                  
         1       7839 KING        5000                                                                                  
         2       7788 SCOTT       3000                                                                                  
         3       7902 FORD        3000                                                                                  

SQL> select rownum,empno,ename,sal
  2  from emp
  3  where rownum>=5 and rownum<=8;

未选定行

行号使用>= 方法
r 已经不是e2的伪列，而是实列（第2次查出的表增加一列 r）！所以可以用where r>5;

SQL> select *
  2  from 	(select rownum r,e1.*
  3  	 from (select * from emp order by sal) e1
  4  	 where rownum <=8
  5  	) e2
  6  where r >=5;

         R      EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                        
---------- ---------- ---------- --------- ---------- -------------- ----- ---------- ----------                        
         5       7654 MARTIN     SALESMAN        7698 28-9月 -81      1250       1400         30                        
         6       7934 MILLER     CLERK           7782 23-1月 -82      1300                    10                        
         7       7844 TURNER     SALESMAN        7698 08-9月 -81      1500          0         30                        
         8       7499 ALLEN      SALESMAN        7698 20-2月 -81      1600        300         30                        

SQL> host cls


SQL> --第二题
SQL> select e.empno,e.ename,e.sal,d.avgsal
  2  from emp e,(select deptno,avg(sal) avgsal from emp group by deptno) d
  3  where e.deptno=d.deptno and e.sal>d.avgsal;

     EMPNO ENAME        SAL     AVGSAL                                                                                  
---------- ---------- ----- ----------                                                                                  
      7698 BLAKE       2850 1566.66667                                                                                  
      7499 ALLEN       1600 1566.66667                                                                                  
      7902 FORD        3000       2175                                                                                  
      7788 SCOTT       3000       2175                                                                                  
      7566 JONES       2975       2175                                                                                  
      7839 KING        5000 2916.66667                                                                                  

已选择6行。

SQL> --相关子查询
将主查询中的某个值  作为参数传递给子查询
SQL> select empno,ename,sal,(select avg(sal) from emp where deptno=e.deptno) avgsal
  2  from emp e
  3  where sal> (select avg(sal) from emp where deptno=e.deptno);

     EMPNO ENAME        SAL     AVGSAL                                                                                  
---------- ---------- ----- ----------                                                                                  
      7499 ALLEN       1600 1566.66667                                                                                  
      7566 JONES       2975       2175                                                                                  
      7698 BLAKE       2850 1566.66667                                                                                  
      7788 SCOTT       3000       2175                                                                                  
      7839 KING        5000 2916.66667                                                                                  
      7902 FORD        3000       2175                                                                                  

已选择6行。

SQL> host cls

SQL> --第三题
SQL> select hiredate from emp;

HIREDATE                                                                                                                
--------------                                                                                                          
17-12月-80                                                                                                              
20-2月 -81                                                                                                              
22-2月 -81                                                                                                              
02-4月 -81                                                                                                              
28-9月 -81                                                                                                              
01-5月 -81                                                                                                              
09-6月 -81                                                                                                              
13-7月 -87                                                                                                              
17-11月-81                                                                                                              
08-9月 -81                                                                                                              
13-7月 -87                                                                                                              
03-12月-81                                                                                                              
03-12月-81                                                                                                              
23-1月 -82                                                                                                              

已选择14行。

SQL> /*
SQL> HIREDATE         count81=0
SQL> ------------------------
SQL> 17-12月-80            0
SQL> 20-2月 -81            1
SQL> 22-2月 -81            1
SQL> 02-4月 -81            1
SQL> 28-9月 -81            1
SQL> 01-5月 -81            1
SQL> 09-6月 -81            1
SQL> 13-7月 -87            0
SQL> 17-11月-81            1
SQL> 08-9月 -81            1
SQL> 13-7月 -87            0
SQL> 03-12月-81            1
SQL> 03-12月-81            1
SQL> 23-1月 -82            0
SQL> ===========================
SQL>                      10
SQL> 
SQL>                     sum(if 是81年 then +1 else +0)
SQL> */
SQL> host cls

SQL> --组函数 行转列  wm_concat
SQL> select deptno,wm_concat(ename) names
  2  from emp
  3  group by deptno;

    DEPTNO                                                                                                              
----------                                                                                                              
NAMES                                                                                                                   
------------------------------------------------------------------------------------------------------------------------
        10                                                                                                              
CLARK,KING,MILLER                                                                                                       
                                                                                                                        
        20                                                                                                              
SMITH,FORD,ADAMS,SCOTT,JONES                                                                                            
                                                                                                                        
        30                                                                                                              
ALLEN,BLAKE,MARTIN,TURNER,JAMES,WARD                                                                                    
                                                                                                                        

SQL> col names for a40
SQL>  select deptno,wm_concat(ename) names
  2   from emp
  3   group by deptno;

    DEPTNO NAMES                                                                                                        
---------- ----------------------------------------                                                                     
        10 CLARK,KING,MILLER                                                                                            
        20 SMITH,FORD,ADAMS,SCOTT,JONES                                                                                 
        30 ALLEN,BLAKE,MARTIN,TURNER,JAMES,WARD                                                                         

SQL> spool off

22.10.	面试题

题1：
create table test1
(id int primary key,
Name varchar(20),
Money int);

Insert into test1 values(1, ‘Tom’, 1000);
Insert into test1 values(2, ‘Mary’, 2000);
Insert into test1 values(3, ‘Mike’, 3000);
Insert into test1 values(4, ‘Jeff’, 4000);

要求：
 

题2：
 


Create table pm_ci
(ci_id varchar(20) primary key,
Stu_ids varchar(100));
Insert into pm_ci values (‘1’, ‘1,2,3,4’);
Insert into pm_ci values (‘2’, ‘1,4’);

Create table pm_stu
(stu_id varchar(20) primary key,
Stu_name varchar(20));
Insert into pm_stu values(‘1’, ‘张三’);
Insert into pm_stu values(‘2’, ‘李四’);
Insert into pm_stu values(‘3’, ‘王五’);
Insert into pm_stu values(‘4’, ‘赵六’);


22.11.	处理数据
课堂练习第3题答案：
SQL> host cls

SQL> select count(*) Total,
  2         sum(decode(to_char(hiredate,'RR'),'80',1,0)) "1980",
  3         sum(decode(to_char(hiredate,'RR'),'81',1,0)) "1981",
  4         sum(decode(to_char(hiredate,'RR'),'82',1,0)) "1982",
  5         sum(decode(to_char(hiredate,'RR'),'87',1,0)) "1987"
  6  from emp;

     TOTAL       1980       1981       1982       1987                          
---------- ---------- ---------- ---------- ----------                          
        14          1         10          1          2                          

SQL> host cls

SQL> /*
SQL> SQL类型
SQL> 1. DML: select, insert, update, delete
(Data Manipulation Lanuage 数据操作语言)
SQL> 2. DDL: create/alter/drop/truncate table, create/drop view/sequence/index/synonym
(Data Definition Language 数据定义语言)
SQL> 
SQL> 3. DCL: commit, rollback
(Data Control Language 数据控制语言)
SQL> */
SQL> host cls

SQL> --插入数据 insert
SQL> insert into emp(empno,ename,sal ,deptno)
  2  values(1001,'Tom',6000,20);

已创建 1 行。

SQL> --隐式/显式插入null
SQL> --地址符   &
SQL> insert into emp(empno,ename,sal,deptno)
  2  values(&empno,&ename,&sal,&deptno);
输入 empno 的值:  1002
输入 ename 的值:  'Mary'
输入 sal 的值:  5000
输入 deptno 的值:  10
原值    2: values(&empno,&ename,&sal,&deptno)
新值    2: values(1002,'Mary',5000,10)

已创建 1 行。

SQL> /
输入 empno 的值:  1003
输入 ename 的值:  'Mike'
输入 sal 的值:  6000
输入 deptno 的值:  30
原值    2: values(&empno,&ename,&sal,&deptno)
新值    2: values(1003,'Mike',6000,30)

已创建 1 行。

SQL> ed
已写入 file afiedt.buf

  1  insert into emp(empno,ename,sal,deptno)
  2* values(&empno,'&ename',&sal,&deptno)
SQL> /
输入 empno 的值:  1004
输入 ename 的值:  Jerry
输入 sal 的值:  5000
输入 deptno 的值:  10
原值    2: values(&empno,'&ename',&sal,&deptno)
新值    2: values(1004,'Jerry',5000,10)

已创建 1 行。

SQL> host ls

SQL> host cls

SQL> select empno,ename,&t
  2  from emp;
输入 t 的值:  sal
原值    1: select empno,ename,&t
新值    1: select empno,ename,sal

     EMPNO ENAME             SAL                                                
---------- ---------- ----------                                                
      1001 Tom              6000                                                
      1002 Mary             5000                                                
      1003 Mike             6000                                                
      1004 Jerry            5000                                                
      7369 SMITH             800                                                
      7499 ALLEN            1600                                                
      7521 WARD             1250                                                
      7566 JONES            2975                                                
      7654 MARTIN           1250                                                
      7698 BLAKE            2850                                                
      7782 CLARK            2450                                                
      7788 SCOTT            3000                                                
      7839 KING             5000                                                
      7844 TURNER           1500                                                
      7876 ADAMS            1100                                                
      7900 JAMES             950                                                
      7902 FORD             3000                                                
      7934 MILLER           1300                                                

已选择18行。

SQL> /
输入 t 的值:  deptno
原值    1: select empno,ename,&t
新值    1: select empno,ename,deptno

     EMPNO ENAME          DEPTNO                                                
---------- ---------- ----------                                                
      1001 Tom                20                                                
      1002 Mary               10                                                
      1003 Mike               30                                                
      1004 Jerry              10                                                
      7369 SMITH              20                                                
      7499 ALLEN              30                                                
      7521 WARD               30                                                
      7566 JONES              20                                                
      7654 MARTIN             30                                                
      7698 BLAKE              30                                                
      7782 CLARK              10                                                
      7788 SCOTT              20                                                
      7839 KING               10                                                
      7844 TURNER             30                                                
      7876 ADAMS              20                                                
      7900 JAMES              30                                                
      7902 FORD               20                                                
      7934 MILLER             10                                                

已选择18行。

SQL> select *
  2  from &t;
输入 t 的值:  dept
原值    2: from &t
新值    2: from dept

    DEPTNO DNAME          LOC                                                   
---------- -------------- -------------                                         
        10 ACCOUNTING     NEW YORK                                              
        20 RESEARCH       DALLAS                                                
        30 SALES          CHICAGO                                               
        40 OPERATIONS     BOSTON                                                

SQL> rollback;

回退已完成。

SQL> host cls

SQL> --批处理
SQL> create table emp10 as select * from emp where 1=2;

表已创建。

SQL> desc emp10
 名称                                      是否为空? 类型
 ----------------------------------------- -------- ----------------------------
 EMPNO                                              NUMBER(4)
 ENAME                                              VARCHAR2(10)
 JOB                                                VARCHAR2(9)
 MGR                                                NUMBER(4)
 HIREDATE                                           DATE
 SAL                                                NUMBER(7,2)
 COMM                                               NUMBER(7,2)
 DEPTNO                                             NUMBER(2)

SQL> select * from emp10;

未选定行

SQL> --一次性从emp中  将所有10号部门的员工插入到emp10
SQL> insert into emp10
  2  select * from emp where deptno=10;

已创建3行。

SQL> select * from emp10;

     EMPNO ENAME      JOB              MGR HIREDATE              SAL       COMM    DEPTNO     
---------- ---------- --------- ---------- -------------- ---------- ---------- ----------                                                                      
      7782 CLARK      MANAGER         7839 09-6月 -81           2450                    10                                                                      
      7839 KING       PRESIDENT            17-11月-81           5000                    10                                                                      
      7934 MILLER     CLERK           7782 23-1月 -82           1300                    10                                                                      
                                                                                

SQL> set linesize 120
SQL> col sal for 9999
SQL> host cls

SQL> --更新数据
SQL> --删除数据
SQL> /*

数据的完整性问题：外键约束
Oracle里任何一个操作都是可逆的。
SQL> delete 和truncate的区别
SQL> 1. delete逐条删除 truncate 先摧毁表 再重建
SQL> 2. **** delete 是DML(可以回滚)，truncate是DDL(不可以回滚)
SQL> 3. delete不会释放空间 truncate会
SQL> 4. delete会产生碎片（要手动开启行移动），truncate不会
SQL> 5. delete可以闪回（day04-23），truncate不可以
SQL> */

测试delete和truncate效率：
SQL> set feedback off
SQL> @c:\sql.sql
SQL> select count(*) from testdelete;

  COUNT(*)                                                                                                              
----------                                                                                                              
      5000                                                                                                              
SQL> set timing on
SQL> delete from testdelete;
已用时间:  00: 00: 00.04
SQL> set timing off
SQL> drop table testdelete purge;
SQL> @c:\sql.sql
SQL> select count(*) from testdelete;

  COUNT(*)                                                                                                              
----------                                                                                                              
      5000                                                                                                              
SQL> set timing on
SQL> truncate table testdelete;
已用时间:  00: 00: 07.87
SQL> set timing off
SQL> host cls

SQL> /*
SQL> Oracle中的事务
性质：ICBC
DDL语句有隐式提交，所以不能回滚（rollback）
SQL> 1. 起始标志: DML语句（自动开启）
SQL> 2. 结束标志: 提交: 	显式提交 commit
SQL>              				隐式提交 正常退出exit ,DDL语句
SQL>              		回滚: 	显式  rollback
SQL>                    			隐式  掉电,宕机，非正常退出
SQL> */

SQL> --保存点
 

SQL> create table testsavepoint
  2  (tid number,tname varchar2(20));
SQL> set feedback on
SQL> insert into testsavepoint values(1,'Tom');
已创建 1 行。

SQL> insert into testsavepoint values(2,'Mary');
已创建 1 行。

SQL> savepoint a;
保存点已创建。

SQL> insert into testsavepoint values(3,'Moke');
已创建 1 行。

SQL> select * from testsavepoint;
       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         1 Tom                                                                                                          
         2 Mary                                                                                                         
         3 Moke                                                                                                         
已选择3行。

SQL> rollback to savepoint a;
回退已完成。

SQL> select * from testsavepoint;
       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         1 Tom                                                                                                          
         2 Mary                                                                                                         
已选择2行。

SQL> commit;
提交完成。
SQL> spool off

事务的隔离级别
Read uncommitted
Read commited (oracle支持，默认)
Repeatable read
Seriablizable (oracle支持，严重影响效率)
问题：oracle有几个隔离级别？3个！
第3个：
Read only（oracle自己的，影响最小）

本地事务、全部事务
Try { 扣钱; 加钱; 提交; 
给对方发短信; 
} Catch  (Exception e) {
Roll back; }

加上“发短信”后就是全局事务（和数据库没关系）。
JTA： Java Transaction API (Tomcat不支持)

22.12.	创建和管理表
常见数据库对象：
表(table)，视图(view)，序列(sequence)，索引(index)，同义词(synonymous)
表
1.	必须有create table 权限
2.	有存储空间
3.	指定：表名，列名（类型，类型大小）

命名规则：
•	表名和列名：
•	必须以字母开头
•	必须在1-30个字符之间
•	必须只能包含A-Z, a-z, 0-9, _, $, 和#
•	必须不能和用户定义的其他对象重名
•	必须不能使Oracle的保留字
•	Oracle默认存储都是存为大写
•	数据库名只能是1~8位，datalink可以是128位，和其他一些特殊字符

默认不能查询另一个用户的表，要使用别的用户名作为前缀。
系统权限，用户权限
 在userA
Select * from userB.employees;
SQL> host cls

SQL> create table test1
  2  (tid number,
  3   tname varchar2(20),
  4   hiredate date default sysdate);

表已创建。

SQL> insert into test1(tid,tname) values(1,'Tom');

已创建 1 行。

SQL> select * from test1;

       TID TNAME                HIREDATE                                                                                
---------- -------------------- --------------                                                                          
         1 Tom                  20-6月 -13                                                                              

已选择 1 行。

SQL> host cls

数据类型
数据类型	描述
VARCHAR2(size)	可变字符数据
CHAR(size)	定长字符数据
NUMBER(p, s)	可变长数值数据
DATE	日期型数据
LONG	可变长字符数据，最大2G
CLOB	字符数据，最大4G
RAW AND LONG RAW	原始的二进制数据
BLOB	二进制数据，最大4G
BFILE	存储外部文件的二进制数据，最大4G
ROWID	行地址


索引就是行地址
SQL> --行地址
SQL> select rowid,empno,ename from emp;

ROWID                   EMPNO ENAME                                                                                     
------------------ ---------- ----------                                                                                
AAANIwAAEAAAAAeAAA       7369 SMITH                                                                                     
AAANIwAAEAAAAAeAAB       7499 ALLEN                                                                                     
AAANIwAAEAAAAAeAAC       7521 WARD                                                                                      
AAANIwAAEAAAAAeAAD       7566 JONES                                                                                     
AAANIwAAEAAAAAeAAE       7654 MARTIN                                                                                    
AAANIwAAEAAAAAeAAF       7698 BLAKE                                                                                     
AAANIwAAEAAAAAeAAG       7782 CLARK                                                                                     
AAANIwAAEAAAAAeAAH       7788 SCOTT                                                                                     
AAANIwAAEAAAAAeAAI       7839 KING                                                                                      
AAANIwAAEAAAAAeAAJ       7844 TURNER                                                                                    
AAANIwAAEAAAAAeAAK       7876 ADAMS                                                                                     
AAANIwAAEAAAAAeAAL       7900 JAMES                                                                                     
AAANIwAAEAAAAAeAAM       7902 FORD                                                                                      
AAANIwAAEAAAAAeAAN       7934 MILLER                                                                                    

已选择14行。

使用子查询创建表

SQL> --保存20号部门的员工
SQL> create table emp20
  2  as
  3  select * from emp where deptno=20;

表已创建。

SQL> select * from emp20;

     EMPNO ENAME      JOB              MGR HIREDATE         SAL       COMM     DEPTNO                                   
---------- ---------- --------- ---------- -------------- ----- ---------- ----------                                   
      7369 SMITH      CLERK           7902 17-12月-80       800                    20                                   
      7566 JONES      MANAGER         7839 02-4月 -81      2975                    20                                   
      7788 SCOTT      ANALYST         7566 13-7月 -87      3000                    20                                   
      7876 ADAMS      CLERK           7788 13-7月 -87      1100                    20                                   
      7902 FORD       ANALYST         7566 03-12月-81      3000                    20                                   

已选择5行。

SQL> --创建表: 员工号  姓名 月薪 年薪 部门名称
SQL> create table empinfo
  2  as
  3  select e.empno,e.ename,e.sal,e.sal*12 annlsal,d.dname
  4  from emp e,dept d
  5  where e.deptno=d.deptno;

表已创建。

SQL> select * from empinfo;

     EMPNO ENAME        SAL    ANNLSAL DNAME                                                                            
---------- ---------- ----- ---------- --------------                                                                   
      7369 SMITH        800       9600 RESEARCH                                                                         
      7499 ALLEN       1600      19200 SALES                                                                            
      7521 WARD        1250      15000 SALES                                                                            
      7566 JONES       2975      35700 RESEARCH                                                                         
      7654 MARTIN      1250      15000 SALES                                                                            
      7698 BLAKE       2850      34200 SALES                                                                            
      7782 CLARK       2450      29400 ACCOUNTING                                                                       
      7788 SCOTT       3000      36000 RESEARCH                                                                         
      7839 KING        5000      60000 ACCOUNTING                                                                       
      7844 TURNER      1500      18000 SALES                                                                            
      7876 ADAMS       1100      13200 RESEARCH                                                                         

     EMPNO ENAME        SAL    ANNLSAL DNAME                                                                            
---------- ---------- ----- ---------- --------------                                                                   
      7900 JAMES        950      11400 SALES                                                                            
      7902 FORD        3000      36000 RESEARCH                                                                         
      7934 MILLER      1300      15600 ACCOUNTING                                                                       

已选择14行。

SQL> host cls

修改表
alter table add/modify/drop/rename

SQL> --修改表： 追加新列 修改列 删除列 重名列
SQL> desc test1
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 TID                                                                        NUMBER
 TNAME                                                                      VARCHAR2(20)
 HIREDATE                                                                   DATE

SQL> alter table test1 add image blob;

表已更改。

SQL> desc test1
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 TID                                                                        NUMBER
 TNAME                                                                      VARCHAR2(20)
 HIREDATE                                                                   DATE
 IMAGE                                                                      BLOB

SQL> alter table test1 modify tname varchar2(40);

表已更改。

SQL> desc test1
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 TID                                                                        NUMBER
 TNAME                                                                      VARCHAR2(40)
 HIREDATE                                                                   DATE
 IMAGE                                                                      BLOB

SQL> alter table test1 drop column image;

表已更改。

SQL> desc test1
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 TID                                                                        NUMBER
 TNAME                                                                      VARCHAR2(40)
 HIREDATE                                                                   DATE

SQL> alter table test1 rename tname to username;
alter table test1 rename tname to username
                         *
第 1 行出现错误: 
ORA-14155: 缺失 PARTITION 或 SUBPARTITION 关键字 


SQL> alter table test1 rename column tname to username;

表已更改。

SQL> desc test1
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 TID                                                                        NUMBER
 USERNAME                                                                   VARCHAR2(40)
 HIREDATE                                                                   DATE

SQL> host cls

删除表 drop table [purge]
并没有被删掉，只是在回收站；如果要restore, 需要闪回。
SQL> -- 删除表
SQL> select * from tab;

TNAME                          TABTYPE  CLUSTERID                                                                       
------------------------------ ------- ----------                                                                       
DEPT                           TABLE                                                                                    
TESTSAVEPOINT                  TABLE                                                                                    
EMP                            TABLE                                                                                    
BONUS                          TABLE                                                                                    
SALGRADE                       TABLE                                                                                    
EMP10                          TABLE                                                                                    
TESTDELETE                     TABLE                                                                                    
TEST1                          TABLE                                                                                    
EMP20                          TABLE                                                                                    
EMPINFO                        TABLE                                                                                    

已选择10行。

SQL> drop table test1;

表已删除。

SQL> select * from tab;

TNAME                          TABTYPE  CLUSTERID                                                                       
------------------------------ ------- ----------                                                                       
BIN$UKc1E0vyQ0C1ZcDR8cUI4w==$0 TABLE                                                                                    
DEPT                           TABLE                                                                                    
TESTSAVEPOINT                  TABLE                                                                                    
EMP                            TABLE                                                                                    
BONUS                          TABLE                                                                                    
SALGRADE                       TABLE                                                                                    
EMP10                          TABLE                                                                                    
TESTDELETE                     TABLE                                                                                    
EMP20                          TABLE                                                                                    
EMPINFO                        TABLE                                                                                    

已选择10行。

SQL> --Oracle的回收站
SQL> show recyclebin
ORIGINAL NAME    RECYCLEBIN NAME                OBJECT TYPE  DROP TIME                                                  
---------------- ------------------------------ ------------ -------------------                                        
TEST1            BIN$UKc1E0vyQ0C1ZcDR8cUI4w==$0 TABLE        2013-06-20:15:23:20                                        
SQL> purge recyclebin;

回收站已清空。

SQL> show recyclebin
SQL> --drop table test1 purge; --> 不经过回收站直接删除
SQL> select * from TESTSAVEPOINT;

       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         1 Tom                                                                                                          
         2 Mary                                                                                                         

已选择2行。

SQL> host cls

SQL> drop table TESTSAVEPOINT;

表已删除。

SQL> show recyclebin
ORIGINAL NAME    RECYCLEBIN NAME                OBJECT TYPE  DROP TIME                                                  
---------------- ------------------------------ ------------ -------------------                                        
TESTSAVEPOINT    BIN$b9zRUzdaQfuXXqNhykffVA==$0 TABLE        2013-06-20:15:26:10                                        
SQL> select * from TESTSAVEPOINT;
select * from TESTSAVEPOINT
              *
第 1 行出现错误: 
ORA-00942: 表或视图不存在 

SQL> select * from tab;

TNAME                          TABTYPE  CLUSTERID                                                                       
------------------------------ ------- ----------                                                                       
BIN$b9zRUzdaQfuXXqNhykffVA==$0 TABLE                                                                                    
DEPT                           TABLE                                                                                    
EMP                            TABLE                                                                                    
BONUS                          TABLE                                                                                    
SALGRADE                       TABLE                                                                                    
EMP10                          TABLE                                                                                    
TESTDELETE                     TABLE                                                                                    
EMP20                          TABLE                                                                                    
EMPINFO                        TABLE                                                                                    

已选择9行。

SQL> select * from BIN$b9zRUzdaQfuXXqNhykffVA==$0;
select * from BIN$b9zRUzdaQfuXXqNhykffVA==$0
                                        *
第 1 行出现错误: 
ORA-00933: SQL 命令未正确结束 


SQL> select * from "BIN$b9zRUzdaQfuXXqNhykffVA==$0";

       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         1 Tom                                                                                                          
         2 Mary                                                                                                         

已选择2行。

SQL> --注意： 管理员没有回收站
SQL> host cls

重命名表
Rename dept to dept2


SQL> --检查性约束
NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK
主键最快（not null, unique）,本身就是索引。
外键：必须是副表的主键
两个方法删除有关联的表：
On delete cascade: 删除父表时，级联删除子表记录
On delete set null: 将子表的外键null（这个好）
给约束起名字：
Constraint em_salary_min check(salary>1000);

如果约束很多，将创建表和创建约束分开做
alter table dep add ( constraint pk_deptno primary key(dno));

SQL> create table test2
  2  (tid number,
  3   tname varchar2(20),
  4   gender varchar2(4) check (gender in ('男','女')),
  5   sal number check (sal > 0)
  6  );

表已创建。

SQL> insert into test2 values(1,'Tom', '男', 5000);

已创建 1 行。

SQL> insert into test2 values(2,'Tom', '啊', 5000);
insert into test2 values(2,'Tom', '啊', 5000)
*
第 1 行出现错误: 
ORA-02290: 违反检查约束条件 (SCOTT.SYS_C005636) 
（这个就是约束的名字）

SQL> update test2 set gender='啊' where tid=1;
update test2 set gender='啊' where tid=1
*
第 1 行出现错误: 
ORA-02290: 违反检查约束条件 (SCOTT.SYS_C005636) 


SQL> host cls

SQL> create table myperson
  2  (pid varchar2(18) constraint myperson_PK primary key,
  3   pname varchar2(40) constraint myperson_Name_notnull not null,
  4   gender varchar2(4) constraint myperson_Gender check (gender in ('男','女')),
  5   email varchar2(40) constraint myperson_Email_unique unique
  6                      constraint myperson_Email_notnull not null,
  7   deptno number constraint myperson_FK references dept(deptno) ON DELETE CASCADE
  8  );

表已创建。

SQL> insert into myperson values('p001','Tom','男','tom@126.com',10);

已创建 1 行。

SQL> insert into myperson values('p002','Tom','男','tom@126.com',10);
insert into myperson values('p002','Tom','男','tom@126.com',10)
*
第 1 行出现错误: 
ORA-00001: 违反唯一约束条件 (SCOTT.MYPERSON_EMAIL_UNIQUE) 


SQL> 
SQL> spool off

22.13.	视图
和create table 一样。
目的：简化查询，保护数据，但不能提高性能。相当于对象的封装。
不建议通过视图对表进行修改（因为有很多限制）。

使用下面的语法格式创建视图：
CREATE [OR REPLACE] [FORCE|NOFORCE] VIEW view
	[(alias[, alias] …) ]
AS subquery
[WITH CHECK OPTION [CONSTRAINT constraint]]
[WITH READ ONLY [CONSTRAINT constraint]];

FORCE: 子查询不一定存在
NOFORCE: 子查询存在（默认）
WITH READ ONLY: 只能做查询操作

删除视图：drop VIEW view;

SQL> host cls

SQL> --视图
SQL> create view empview
  2  as
  3  select e.empno,e.ename,e.sal,e.sal*12 annlsal,d.dname
  4  from emp e,dept d
  5  where e.deptno=d.deptno;
create view empview
            *
第 1 行出现错误: 
ORA-01031: 权限不足 

Cmd> sqlplus / as sysdba
Sql> grant create view to scott;

SQL> /

视图已创建。

SQL> select * from tab;

TNAME                          TABTYPE  CLUSTERID                                                                       
------------------------------ ------- ----------                                                                       
BIN$b9zRUzdaQfuXXqNhykffVA==$0 TABLE                                                                                    
MYPERSON                       TABLE                                                                                    
TEST2                          TABLE                                                                                    
EMPVIEW                        VIEW                                                                                     
DEPT                           TABLE                                                                                    
EMP                            TABLE                                                                                    
BONUS                          TABLE                                                                                    
SALGRADE                       TABLE                                                                                    
EMP10                          TABLE                                                                                    
TESTDELETE                     TABLE                                                                                    
EMP20                          TABLE                                                                                    
EMPINFO                        TABLE                                                                                    

已选择12行。

SQL> select * from EMPVIEW;

     EMPNO ENAME        SAL    ANNLSAL DNAME                                                                            
---------- ---------- ----- ---------- --------------                                                                   
      7369 SMITH        800       9600 RESEARCH                                                                         
      7499 ALLEN       1600      19200 SALES                                                                            
      7521 WARD        1250      15000 SALES                                                                            
      7566 JONES       2975      35700 RESEARCH                                                                         
      7654 MARTIN      1250      15000 SALES                                                                            
      7698 BLAKE       2850      34200 SALES                                                                            
      7782 CLARK       2450      29400 ACCOUNTING                                                                       
      7788 SCOTT       3000      36000 RESEARCH                                                                         
      7839 KING        5000      60000 ACCOUNTING                                                                       
      7844 TURNER      1500      18000 SALES                                                                            
      7876 ADAMS       1100      13200 RESEARCH                                                                         
      7900 JAMES        950      11400 SALES                                                                            
      7902 FORD        3000      36000 RESEARCH                                                                         
      7934 MILLER      1300      15600 ACCOUNTING                                                                       

已选择14行。

SQL> desc EMPVIEW
 名称                                                              是否为空? 类型
 ----------------------------------------------------------------- -------- --------------------------------------------
 EMPNO                                                             NOT NULL NUMBER(4)
 ENAME                                                                      VARCHAR2(10)
 SAL                                                                        NUMBER(7,2)
 ANNLSAL                                                                    NUMBER
 DNAME                                                                      VARCHAR2(14)

SQL> create or replace view empview
  2  as
  3  select e.empno,e.ename,e.sal,e.sal*12 annlsal,d.dname
  4  from emp e,dept d
  5  where e.deptno=d.deptno
  6  with read only
  7  ;

视图已创建。

SQL> host cls


22.14.	序列
提供主键值。
序列->数组->内存：提高效率

CREATE SEQUENCE sequence
	[INCREMENT BY n]
	[START WITH n]
	[{MAXVALUE n | NOMAXVALUE}]
	[{MINVALUE n | NOMINVALUE}]
	[{CYCLE | NOCYCLE}]
	[{CACHE n | NOCACHE}];

指针指向数组第一个值的前面一个地址。
NextVal 使用在CurrVal之前

ALTER SEQUENCE dept_deptid_seq
	INCREMENT BY 20
	MAXVALUE 999999
	NOCACHE
	NOCYCLE;
Sequence altered.

Drop sequence dept_deptid_seq;

SQL> --sequence
SQL> create sequence myseq;
序列已创建。
SQL> create table tableA(tid number,tname varchar2(20));
表已创建。
SQL> select myseq.currval from dual;
select myseq.currval from dual
       *
第 1 行出现错误: 
ORA-08002: 序列 MYSEQ.CURRVAL 尚未在此会话中定义 

SQL> select myseq.nextval from dual;
   NEXTVAL                                                                                                              
----------                                                                                                              
         1                                                                                                              

已选择 1 行。
SQL> select myseq.currval from dual;
   CURRVAL                                                                                                              
----------                                                                                                              
         1                                                                                                              

已选择 1 行。
SQL> insert into tableA values(myseq.nextval,'aaa' );

已创建 1 行。
SQL> /
已创建 1 行。
SQL> /
已创建 1 行。
SQL> commit;

提交完成。

SQL> select * from tableA;

       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         2 aaa                                                                                                          
         3 aaa                                                                                                          
         4 aaa                                                                                                          

已选择3行。

SQL> /*
SQL> 序列的不连续影响因素：
SQL> 1. 序列是公有对象（不要共用一个序列）
SQL> 2. 掉电（序列在内存里）
SQL> 3. 回滚
SQL> */
SQL> insert into tableA values(myseq.nextval,'aaa' );

已创建 1 行。

SQL> /

已创建 1 行。

SQL> rollback;

回退已完成。

SQL> insert into tableA values(myseq.nextval,'aaa' );

已创建 1 行。

SQL> select * from tableA;

       TID TNAME                                                                                                        
---------- --------------------                                                                                         
         2 aaa                                                                                                          
         3 aaa                                                                                                          
         4 aaa                                                                                                          
         7 aaa                                                                                                          

已选择4行。

SQL> host cls

22.15.	索引
 

什么时候建索引
1.	数值分布很广
2.	列经常在where条件中出现
3.	被访问数据量很大，需要的很小2%-4%
4.	表不经常更新

Oracle中的索引
B树索引（=二叉树，默认）
位图索引
 

Drop index ind;

Bigtable + mapreduce + *** = 云计算 hadoop

SQL> --index
SQL> create index myindex on emp(deptno);

索引已创建。

SQL> host cls

22.16.	同义词 -->   别名
可以代表任何一个数据库对象。

语法：
CREATE [PUBLIC] SYNONYM synonym
FOR object;


银行给你的可能是视图，甚至是synonym。
分布式操作：day04

先需要权限：
Cmd> sqlplus hr/hr;
SQL> grant select on EMPLOYEES to scott;
SQL> conn / as sysdba
SQL> grant create synonym to scott;

SQL> select count(*)
  2  from hr.EMPLOYEES;
from hr.EMPLOYEES
        *
第 2 行出现错误: 
ORA-00942: 表或视图不存在 


SQL> /

  COUNT(*)                                                                                                              
----------                                                                                                              
       107                                                                                                              

已选择 1 行。

SQL> create synonym  hremp for hr.EMPLOYEES;
create synonym  hremp for hr.EMPLOYEES
*
第 1 行出现错误: 
ORA-01031: 权限不足 


SQL> /

同义词已创建。

SQL> select * from hremp;

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        198 Donald               OConnell                  DOCONNEL                  650.507.9833         21-6月 -99    
SH_CLERK         2600                       124            50                                                           
                                                                                                                        
        199 Douglas              Grant                     DGRANT                    650.507.9844         13-1月 -00    
SH_CLERK         2600                       124            50                                                           
                                                                                                                        
        200 Jennifer             Whalen                    JWHALEN                   515.123.4444         17-9月 -87    
AD_ASST          4400                       101            10                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        201 Michael              Hartstein                 MHARTSTE                  515.123.5555         17-2月 -96    
MK_MAN          13000                       100            20                                                           
                                                                                                                        
        202 Pat                  Fay                       PFAY                      603.123.6666         17-8月 -97    
MK_REP           6000                       201            20                                                           
                                                                                                                        
        203 Susan                Mavris                    SMAVRIS                   515.123.7777         07-6月 -94    
HR_REP           6500                       101            40                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        204 Hermann              Baer                      HBAER                     515.123.8888         07-6月 -94    
PR_REP          10000                       101            70                                                           
                                                                                                                        
        205 Shelley              Higgins                   SHIGGINS                  515.123.8080         07-6月 -94    
AC_MGR          12000                       101           110                                                           
                                                                                                                        
        206 William              Gietz                     WGIETZ                    515.123.8181         07-6月 -94    
AC_ACCOUNT       8300                       205           110                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        100 Steven               King                      SKING                     515.123.4567         17-6月 -87    
AD_PRES         24000                                      90                                                           
                                                                                                                        
        101 Neena                Kochhar                   NKOCHHAR                  515.123.4568         21-9月 -89    
AD_VP           17000                       100            90                                                           
                                                                                                                        
        102 Lex                  De Haan                   LDEHAAN                   515.123.4569         13-1月 -93    
AD_VP           17000                       100            90                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        103 Alexander            Hunold                    AHUNOLD                   590.423.4567         03-1月 -90    
IT_PROG          9000                       102            60                                                           
                                                                                                                        
        104 Bruce                Ernst                     BERNST                    590.423.4568         21-5月 -91    
IT_PROG          6000                       103            60                                                           
                                                                                                                        
        105 David                Austin                    DAUSTIN                   590.423.4569         25-6月 -97    
IT_PROG          4800                       103            60                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        106 Valli                Pataballa                 VPATABAL                  590.423.4560         05-2月 -98    
IT_PROG          4800                       103            60                                                           
                                                                                                                        
        107 Diana                Lorentz                   DLORENTZ                  590.423.5567         07-2月 -99    
IT_PROG          4200                       103            60                                                           
                                                                                                                        
        108 Nancy                Greenberg                 NGREENBE                  515.124.4569         17-8月 -94    
FI_MGR          12000                       101           100                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        109 Daniel               Faviet                    DFAVIET                   515.124.4169         16-8月 -94    
FI_ACCOUNT       9000                       108           100                                                           
                                                                                                                        
        110 John                 Chen                      JCHEN                     515.124.4269         28-9月 -97    
FI_ACCOUNT       8200                       108           100                                                           
                                                                                                                        
        111 Ismael               Sciarra                   ISCIARRA                  515.124.4369         30-9月 -97    
FI_ACCOUNT       7700                       108           100                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        112 Jose Manuel          Urman                     JMURMAN                   515.124.4469         07-3月 -98    
FI_ACCOUNT       7800                       108           100                                                           
                                                                                                                        
        113 Luis                 Popp                      LPOPP                     515.124.4567         07-12月-99    
FI_ACCOUNT       6900                       108           100                                                           
                                                                                                                        
        114 Den                  Raphaely                  DRAPHEAL                  515.127.4561         07-12月-94    
PU_MAN          11000                       100            30                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        115 Alexander            Khoo                      AKHOO                     515.127.4562         18-5月 -95    
PU_CLERK         3100                       114            30                                                           
                                                                                                                        
        116 Shelli               Baida                     SBAIDA                    515.127.4563         24-12月-97    
PU_CLERK         2900                       114            30                                                           
                                                                                                                        
        117 Sigal                Tobias                    STOBIAS                   515.127.4564         24-7月 -97    
PU_CLERK         2800                       114            30                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        118 Guy                  Himuro                    GHIMURO                   515.127.4565         15-11月-98    
PU_CLERK         2600                       114            30                                                           
                                                                                                                        
        119 Karen                Colmenares                KCOLMENA                  515.127.4566         10-8月 -99    
PU_CLERK         2500                       114            30                                                           
                                                                                                                        
        120 Matthew              Weiss                     MWEISS                    650.123.1234         18-7月 -96    
ST_MAN           8000                       100            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        121 Adam                 Fripp                     AFRIPP                    650.123.2234         10-4月 -97    
ST_MAN           8200                       100            50                                                           
                                                                                                                        
        122 Payam                Kaufling                  PKAUFLIN                  650.123.3234         01-5月 -95    
ST_MAN           7900                       100            50                                                           
                                                                                                                        
        123 Shanta               Vollman                   SVOLLMAN                  650.123.4234         10-10月-97    
ST_MAN           6500                       100            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        124 Kevin                Mourgos                   KMOURGOS                  650.123.5234         16-11月-99    
ST_MAN           5800                       100            50                                                           
                                                                                                                        
        125 Julia                Nayer                     JNAYER                    650.124.1214         16-7月 -97    
ST_CLERK         3200                       120            50                                                           
                                                                                                                        
        126 Irene                Mikkilineni               IMIKKILI                  650.124.1224         28-9月 -98    
ST_CLERK         2700                       120            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        127 James                Landry                    JLANDRY                   650.124.1334         14-1月 -99    
ST_CLERK         2400                       120            50                                                           
                                                                                                                        
        128 Steven               Markle                    SMARKLE                   650.124.1434         08-3月 -00    
ST_CLERK         2200                       120            50                                                           
                                                                                                                        
        129 Laura                Bissot                    LBISSOT                   650.124.5234         20-8月 -97    
ST_CLERK         3300                       121            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        130 Mozhe                Atkinson                  MATKINSO                  650.124.6234         30-10月-97    
ST_CLERK         2800                       121            50                                                           
                                                                                                                        
        131 James                Marlow                    JAMRLOW                   650.124.7234         16-2月 -97    
ST_CLERK         2500                       121            50                                                           
                                                                                                                        
        132 TJ                   Olson                     TJOLSON                   650.124.8234         10-4月 -99    
ST_CLERK         2100                       121            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        133 Jason                Mallin                    JMALLIN                   650.127.1934         14-6月 -96    
ST_CLERK         3300                       122            50                                                           
                                                                                                                        
        134 Michael              Rogers                    MROGERS                   650.127.1834         26-8月 -98    
ST_CLERK         2900                       122            50                                                           
                                                                                                                        
        135 Ki                   Gee                       KGEE                      650.127.1734         12-12月-99    
ST_CLERK         2400                       122            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        136 Hazel                Philtanker                HPHILTAN                  650.127.1634         06-2月 -00    
ST_CLERK         2200                       122            50                                                           
                                                                                                                        
        137 Renske               Ladwig                    RLADWIG                   650.121.1234         14-7月 -95    
ST_CLERK         3600                       123            50                                                           
                                                                                                                        
        138 Stephen              Stiles                    SSTILES                   650.121.2034         26-10月-97    
ST_CLERK         3200                       123            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        139 John                 Seo                       JSEO                      650.121.2019         12-2月 -98    
ST_CLERK         2700                       123            50                                                           
                                                                                                                        
        140 Joshua               Patel                     JPATEL                    650.121.1834         06-4月 -98    
ST_CLERK         2500                       123            50                                                           
                                                                                                                        
        141 Trenna               Rajs                      TRAJS                     650.121.8009         17-10月-95    
ST_CLERK         3500                       124            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        142 Curtis               Davies                    CDAVIES                   650.121.2994         29-1月 -97    
ST_CLERK         3100                       124            50                                                           
                                                                                                                        
        143 Randall              Matos                     RMATOS                    650.121.2874         15-3月 -98    
ST_CLERK         2600                       124            50                                                           
                                                                                                                        
        144 Peter                Vargas                    PVARGAS                   650.121.2004         09-7月 -98    
ST_CLERK         2500                       124            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        145 John                 Russell                   JRUSSEL                   011.44.1344.429268   01-10月-96    
SA_MAN          14000             .4        100            80                                                           
                                                                                                                        
        146 Karen                Partners                  KPARTNER                  011.44.1344.467268   05-1月 -97    
SA_MAN          13500             .3        100            80                                                           
                                                                                                                        
        147 Alberto              Errazuriz                 AERRAZUR                  011.44.1344.429278   10-3月 -97    
SA_MAN          12000             .3        100            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        148 Gerald               Cambrault                 GCAMBRAU                  011.44.1344.619268   15-10月-99    
SA_MAN          11000             .3        100            80                                                           
                                                                                                                        
        149 Eleni                Zlotkey                   EZLOTKEY                  011.44.1344.429018   29-1月 -00    
SA_MAN          10500             .2        100            80                                                           
                                                                                                                        
        150 Peter                Tucker                    PTUCKER                   011.44.1344.129268   30-1月 -97    
SA_REP          10000             .3        145            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        151 David                Bernstein                 DBERNSTE                  011.44.1344.345268   24-3月 -97    
SA_REP           9500            .25        145            80                                                           
                                                                                                                        
        152 Peter                Hall                      PHALL                     011.44.1344.478968   20-8月 -97    
SA_REP           9000            .25        145            80                                                           
                                                                                                                        
        153 Christopher          Olsen                     COLSEN                    011.44.1344.498718   30-3月 -98    
SA_REP           8000             .2        145            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        154 Nanette              Cambrault                 NCAMBRAU                  011.44.1344.987668   09-12月-98    
SA_REP           7500             .2        145            80                                                           
                                                                                                                        
        155 Oliver               Tuvault                   OTUVAULT                  011.44.1344.486508   23-11月-99    
SA_REP           7000            .15        145            80                                                           
                                                                                                                        
        156 Janette              King                      JKING                     011.44.1345.429268   30-1月 -96    
SA_REP          10000            .35        146            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        157 Patrick              Sully                     PSULLY                    011.44.1345.929268   04-3月 -96    
SA_REP           9500            .35        146            80                                                           
                                                                                                                        
        158 Allan                McEwen                    AMCEWEN                   011.44.1345.829268   01-8月 -96    
SA_REP           9000            .35        146            80                                                           
                                                                                                                        
        159 Lindsey              Smith                     LSMITH                    011.44.1345.729268   10-3月 -97    
SA_REP           8000             .3        146            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        160 Louise               Doran                     LDORAN                    011.44.1345.629268   15-12月-97    
SA_REP           7500             .3        146            80                                                           
                                                                                                                        
        161 Sarath               Sewall                    SSEWALL                   011.44.1345.529268   03-11月-98    
SA_REP           7000            .25        146            80                                                           
                                                                                                                        
        162 Clara                Vishney                   CVISHNEY                  011.44.1346.129268   11-11月-97    
SA_REP          10500            .25        147            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        163 Danielle             Greene                    DGREENE                   011.44.1346.229268   19-3月 -99    
SA_REP           9500            .15        147            80                                                           
                                                                                                                        
        164 Mattea               Marvins                   MMARVINS                  011.44.1346.329268   24-1月 -00    
SA_REP           7200             .1        147            80                                                           
                                                                                                                        
        165 David                Lee                       DLEE                      011.44.1346.529268   23-2月 -00    
SA_REP           6800             .1        147            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        166 Sundar               Ande                      SANDE                     011.44.1346.629268   24-3月 -00    
SA_REP           6400             .1        147            80                                                           
                                                                                                                        
        167 Amit                 Banda                     ABANDA                    011.44.1346.729268   21-4月 -00    
SA_REP           6200             .1        147            80                                                           
                                                                                                                        
        168 Lisa                 Ozer                      LOZER                     011.44.1343.929268   11-3月 -97    
SA_REP          11500            .25        148            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        169 Harrison             Bloom                     HBLOOM                    011.44.1343.829268   23-3月 -98    
SA_REP          10000             .2        148            80                                                           
                                                                                                                        
        170 Tayler               Fox                       TFOX                      011.44.1343.729268   24-1月 -98    
SA_REP           9600             .2        148            80                                                           
                                                                                                                        
        171 William              Smith                     WSMITH                    011.44.1343.629268   23-2月 -99    
SA_REP           7400            .15        148            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        172 Elizabeth            Bates                     EBATES                    011.44.1343.529268   24-3月 -99    
SA_REP           7300            .15        148            80                                                           
                                                                                                                        
        173 Sundita              Kumar                     SKUMAR                    011.44.1343.329268   21-4月 -00    
SA_REP           6100             .1        148            80                                                           
                                                                                                                        
        174 Ellen                Abel                      EABEL                     011.44.1644.429267   11-5月 -96    
SA_REP          11000             .3        149            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        175 Alyssa               Hutton                    AHUTTON                   011.44.1644.429266   19-3月 -97    
SA_REP           8800            .25        149            80                                                           
                                                                                                                        
        176 Jonathon             Taylor                    JTAYLOR                   011.44.1644.429265   24-3月 -98    
SA_REP           8600             .2        149            80                                                           
                                                                                                                        
        177 Jack                 Livingston                JLIVINGS                  011.44.1644.429264   23-4月 -98    
SA_REP           8400             .2        149            80                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        178 Kimberely            Grant                     KGRANT                    011.44.1644.429263   24-5月 -99    
SA_REP           7000            .15        149                                                                         
                                                                                                                        
        179 Charles              Johnson                   CJOHNSON                  011.44.1644.429262   04-1月 -00    
SA_REP           6200             .1        149            80                                                           
                                                                                                                        
        180 Winston              Taylor                    WTAYLOR                   650.507.9876         24-1月 -98    
SH_CLERK         3200                       120            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        181 Jean                 Fleaur                    JFLEAUR                   650.507.9877         23-2月 -98    
SH_CLERK         3100                       120            50                                                           
                                                                                                                        
        182 Martha               Sullivan                  MSULLIVA                  650.507.9878         21-6月 -99    
SH_CLERK         2500                       120            50                                                           
                                                                                                                        
        183 Girard               Geoni                     GGEONI                    650.507.9879         03-2月 -00    
SH_CLERK         2800                       120            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        184 Nandita              Sarchand                  NSARCHAN                  650.509.1876         27-1月 -96    
SH_CLERK         4200                       121            50                                                           
                                                                                                                        
        185 Alexis               Bull                      ABULL                     650.509.2876         20-2月 -97    
SH_CLERK         4100                       121            50                                                           
                                                                                                                        
        186 Julia                Dellinger                 JDELLING                  650.509.3876         24-6月 -98    
SH_CLERK         3400                       121            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        187 Anthony              Cabrio                    ACABRIO                   650.509.4876         07-2月 -99    
SH_CLERK         3000                       121            50                                                           
                                                                                                                        
        188 Kelly                Chung                     KCHUNG                    650.505.1876         14-6月 -97    
SH_CLERK         3800                       122            50                                                           
                                                                                                                        
        189 Jennifer             Dilly                     JDILLY                    650.505.2876         13-8月 -97    
SH_CLERK         3600                       122            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        190 Timothy              Gates                     TGATES                    650.505.3876         11-7月 -98    
SH_CLERK         2900                       122            50                                                           
                                                                                                                        
        191 Randall              Perkins                   RPERKINS                  650.505.4876         19-12月-99    
SH_CLERK         2500                       122            50                                                           
                                                                                                                        
        192 Sarah                Bell                      SBELL                     650.501.1876         04-2月 -96    
SH_CLERK         4000                       123            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        193 Britney              Everett                   BEVERETT                  650.501.2876         03-3月 -97    
SH_CLERK         3900                       123            50                                                           
                                                                                                                        
        194 Samuel               McCain                    SMCCAIN                   650.501.3876         01-7月 -98    
SH_CLERK         3200                       123            50                                                           
                                                                                                                        
        195 Vance                Jones                     VJONES                    650.501.4876         17-3月 -99    
SH_CLERK         2800                       123            50                                                           
                                                                                                                        

EMPLOYEE_ID FIRST_NAME           LAST_NAME                 EMAIL                     PHONE_NUMBER         HIRE_DATE     
----------- -------------------- ------------------------- ------------------------- -------------------- --------------
JOB_ID         SALARY COMMISSION_PCT MANAGER_ID DEPARTMENT_ID                                                           
---------- ---------- -------------- ---------- -------------                                                           
        196 Alana                Walsh                     AWALSH                    650.507.9811         24-4月 -98    
SH_CLERK         3100                       124            50                                                           
                                                                                                                        
        197 Kevin                Feeney                    KFEENEY                   650.507.9822         23-5月 -98    
SH_CLERK         3000                       124            50                                                           
                                                                                                                        

已选择107行。

SQL> host cls

SQL> select count(*) from hremp;

  COUNT(*)                                                                                                              
----------                                                                                                              
       107                                                                                                              

已选择 1 行。

SQL> spool off


22.17.	PLSQL 程序设计
PL/SQL developer: new Test window (not SQL window)
Helloworld
set serveroutput on

declare
  --说明部分
begin
  --程序
  dbms_output.put_line('Hello World');
exception
-- 例外处理语句
end;
/
(/表示推出编辑并执行)

-- 查看程序包的结构
SQL>desc dbms_output 

PL/SQL
Procedure Language / SQL
PL/SQL 是Oracle对sql语言的过程华扩展。在sql语言中增加了过程处理语句（如分支，循环），使SQL语言具有过程处理能力。
PL/SQL是纯面向过程的。
PL/SQL比JDBC, C++等都快。
Java调用PL/SQL就可以了。
Transact-SQL(SQL server)

变量
说明变量（char, varchar2, date, number, boolean, long）
var1 		char(15);
married 		Boolean := true;
psal 			number(7,2)
my_name 	emp.ename%type;	-- 与emp.ename的类型一样
emp_rec		emp%rowtype


记录型变量表示一行。
记录变量分量的引用：
Emp_rec.ename:=’ADAMS’;

例子：引用型变量.sql
set serveroutput on
declare 
  --定义引用型变量
  pename emp.ename%type;
  psal   emp.sal%type;
begin
  --查询7839的姓名和薪水
  select ename,sal into pename,psal from emp where empno=7839;
  -- 打印
  dbms_output.put_line(pename||'的薪水是'||psal);
end;
/

例子：记录型变量
set serveroutput on
declare
  --记录型变量 代表一行
  emp_rec emp%rowtype;
begin
  select * into emp_rec from emp where empno=7839;
  dbms_output.put_line(emp_rec.ename||'的薪水是'||emp_rec.sal);
end;
/

IF-THEN-ELSIF
IF … THEN;
…;
ENDIF

IF … THEN …;
ELSE …;
END IF;

IF … THEN …;
ELSEIF … THEN …;
ELSE …;
END IF;


例子：IF
set serveroutput on

--接收键盘输入
--num: 地址值，在该地址上，存了输入的值
accept num prompt '请输入一个数字';

declare
  --定义变量保存输入的数字
  --隐式转换
  pnum number := &num;
begin

  if pnum = 0 then dbms_output.put_line('您输入的是0');
    elsif pnum = 1 then dbms_output.put_line('您输入的是1');
    elsif pnum = 2 then dbms_output.put_line('您输入的是2');
    else dbms_output.put_line('其他数字');
  end if;
end;
/

循环
第二种好点：容易控制光标（后面讲到）
WHILE total <= 25000
LOOP
…
Total := total + salary;
END LOOP;

LOOP
EXIT [WHEN …];
… …
END LOOP

FOR I IN 1..3
LOOP
… …;
END LOOP


例子：循环
set serveroutput on

declare
  pnum number := 1;
begin
  loop
    --退出循环
    exit when pnum > 10;
        dbms_output.put_line(pnum);
    --加一
    pnum := pnum + 1;
  end loop;
end;
/

22.18.	Cursor光标 == ResultSet (JDBC)
说明光标语法：
CURSOR光标名[(参数名 数据类型[, 参数名 数据类型]…)]
		IS SELECT 语句;
用于存储一个查询返回的多行数据
	Cursor cl is select ename from emp;
打开光标： open c1;
取一个光标值：fetch c1 into pjob; (取一行到变量中, 其类型必须与job一致)
关闭光标：	close c1;

注意：光标指向第一条记录！
例子：光标
--使用游标查询员工姓名和工资，并打印

/*
1. 光标的属性
%isopen: 是否打开
%rowcount: 行数
%notfound: 没有记录

2. 默认允许一次打开300个光标(修改光标： 第四天 管理方案)
SQL> show parameters cursor

NAME                                 TYPE        VALUE
------------------------------------ ----------- -------
cursor_sharing                       string      EXACT
cursor_space_for_time                boolean     FALSE
open_cursors                         integer     300
session_cached_cursors               integer     20
*/

set serveroutput on

declare
  --定义光标代表员工集合
  cursor cemp is select ename,sal from emp;
  pename emp.ename%type;
  psal   emp.sal%type;
begin
  open cemp;
  
  loop
    --取一个员工
    fetch cemp into pename,psal;    
    --退出条件
    exit when cemp%notfound;
    dbms_output.put_line(pename||'的薪水是'||psal);
  end loop;  
  close cemp;
end;
/

22.19.	21. 综合例子
--涨工资 总裁1000 经理800 其他400

set serveroutput on

declare
  cursor cemp is select empno,empjob from emp;
  pempno emp.empno%type;
  pjob   emp.empjob%type;
begin
  rollback;
  open cemp;
  loop
    --取一个员工 涨工资
    fetch cemp into pempno,pjob;
    exit when cemp%notfound;    
    --判断职位
    if pjob = 'PRESIDENT' then update emp set sal=sal+1000 where empno=pempno;
      elsif pjob = 'MANAGER' then update emp set sal=sal+800 where empno=pempno;
      else update emp set sal=sal+400 where empno=pempno;
    end if;
  end loop;
  close cemp;  
  --事务的隔离级别
  commit;  
  dbms_output.put_line('涨工资完成');
end;
/


--查询某个部门中员工的姓名

set serveroutput on

declare
  --带参数的光标
  cursor cemp(dno number) is select ename from emp where deptno=dno;
  pename emp.ename%type;
begin
  open cemp(20);
  loop  
    fetch cemp into pename;
    exit when cemp%notfound;    
    dbms_output.put_line(pename);
  end loop;
  close cemp;
end;
/

Cemp(dno number) ??


22.20.	例外
Java里如何知道谁调用某段代码？手动抛异常。

系统例外
没有finally!

系统 定义例外
	No_data_found
	Too_many_rows
	Zero_Divide
	Value_error
	Timeout_on_resource

与java不一样，PL/SQL要catch所有意外，不要抛。

例子：系统例外
declare
  pnum number;
begin
  pnum := 1/0;

exception
  when Zero_Divide then dbms_output.put_line('1:0不能做被除数');
                        dbms_output.put_line('2:0不能做被除数');
  when Value_error then dbms_output.put_line('算术或转换错误');                 
  when others then dbms_output.put_line('其他例外');      
end;
/

自定义例外
No_data_found exception;
Raise no_data (java: throws new Exception(e))

例子：
DECLARE
v_job char(10);
v_sal emp.sal%type
No_data exception;
Cursor c1 is select distinct job from emp order by job;

BEGIN
Open c1;
Fetch c1 into v_job;
IF c1%notFound then raise no_data;
END IF;
Close c1;

EXCEPTION
WHEN no_data THEN insert into emplog values(‘fetch语句没有获得数据或数据已经处理完’);
END


例子：自定义例外
declare
  cursor cemp is select ename from emp where deptno=50;
  pename emp.ename%type;
  
  --自定义例外
  no_emp_found exception;
begin
  open cemp;

  --取一个员工
  fetch cemp into pename;
  
  if cemp%notfound then
    --抛出例外
    raise no_emp_found;
  end if;

  --当抛出例外，自动关闭
  close cemp;
  
exception
  when no_emp_found then dbms_output.put_line('没有找到员工');
  when others then dbms_output.put_line('其他例外');   
end;
/




22.21.	面试题答案 面试题eg1
第一题
SQL> Select id, name, money, (select money from test1 where id=t.id-1) money1
From test1 t;

第二题
SQL> select c.ci_id, s.stu_name
	From pm_ci c, pm_stu s
	Where instr(c.stu_ids, s.stu_id) > 0

SQL> Select ci_id, wm_concat(stu_name) names
from select c.ci_id, s.stu_name
	From pm_ci c, pm_stu s
	Where instr(c.stu_ids, s.stu_id) > 0
Group by ci_id

思考题：
如果选课的stu_ids有”11, 22”等
Instr会把stu_id为1和2的也包括进去！

22.22.	瀑布模型
 
3年左右写代码：获得经验
往上发展：需求分析，architect


22.23.	实例1统计每年入职的员工个数
/*
实例1：统计每年入职的员工个数。

SQL语句
1. select to_char(hiredate,'RR') from emp; --> 光标  --> 循环(notfound)
2. count80 number := 0;
   count81 number := 0;
   count82 number := 0;
   count87 number := 0;
*/
set serveroutput on 

declare
  cursor cemp is select to_char(hiredate,'RR') from emp;
  phiredate varchar2(4);
  
  --计数器
  count80 number := 0;
  count81 number := 0;
  count82 number := 0;
  count87 number := 0;
begin
  open cemp;
  loop
    --取一个员工
    fetch cemp into phiredate;
    exit when cemp%notfound;

    --判断年份
    if phiredate = '80' then count80:=count80+1;
      elsif phiredate = '81' then count81:=count81+1;
      elsif phiredate = '82' then count82:=count82+1;
      else count87:=count87+1;
    end if;

  end loop;
  close cemp;
  
  dbms_output.put_line('Total:'||(count80+count81+count82+count87));
  dbms_output.put_line('80:'||count80);
  dbms_output.put_line('81:'||count81);
  dbms_output.put_line('82:'||count82);
  dbms_output.put_line('87:'||count87);
end;
/

实例2
/*
为员工长工资。从最低工资调起每人长10％，但工资总额不能超过5万元,
请计算长工资的人数和长工资后的工资总额，并输出输出长工资人数及工资总额。

SQL语句:
1. select empno,sal from emp order by sal;-->光标 -->循环(1. > 5w  2. 涨完)
2. countEmp number := 0;
3. 长工资后的工资总额: *. select sum(sal) from emp
                    *.  涨后=涨前+sal*0.1 (*)
                    
练习： 工资<5w                    
*/
set serveroutput on
declare
  cursor cemp is select empno,sal from emp order by sal;
  pempno emp.empno%type;
  psal   emp.sal%type;
  
  --人数
  countEmp number := 0;
  
  --工资总额
  salTotal number;
begin
  --初始的工资总额
  select sum(sal) into salTotal from emp;

  open cemp;
  loop
    --第一个退出条件
    exit when salTotal> 50000;
    
    --取一个员工
    fetch cemp into pempno,psal;
    
    --第二个退出条件
    exit when cemp%notfound;
    
    --涨工资
    update emp set sal =sal *1.1 where empno=pempno;
    
    --人数
    countEmp := countEmp+1;
        
     --工资总额
    salTotal := salTotal + psal *0.1;
  end loop;
  close cemp;
  commit;  
  dbms_output.put_line('人数:'||countEmp||'  工资总额:'||salTotal);

end;
/


实例3
/*
用PL/SQL语言编写一程序，实现按部门分段（6000以上、(6000，3000)、3000元以下)
统计各工资段的职工人数、以及各部门的工资总额(工资总额中不包括奖金)
部门	小于3000数	3000-6000	大于6000	工资总额
10	2	1	0	8750
20	3	2	0	10875
30	6	0	0	9400



SQL语句
1. 部门: select deptno from dept; --> 光标 --> 循环
2. 部门中员工的薪水: select sal from emp where deptno=??? --> 带参数的光标 -->  循环
3. count1 number; count2 number; count3 number;
4. 部门工资总额: salTotal number;
               select sum(sal) into salTotal from emp where deptno=???
5.最后创建一张表（msg1）保存数据

*/
set serveroutput on

declare
  --部门
  cursor cdept is select deptno from dept;
  pdeptno dept.deptno%type;
  
  --部门中员工的薪水
  cursor cemp(dno number) is select sal from emp where deptno=dno;
  psal emp.sal%type;
  
  --计数器
  count1 number; count2 number; count3 number;
  
  --部门的工资总额
  salTotal number;
begin
  open cdept;
  loop
    --取一个部门
    fetch cdept into pdeptno;
    exit when cdept%notfound;
    
    --初始化 
    count1:=0;count2:=0;count3:=0;
    
    --部门的工资总额
    select sum(sal) into salTotal from emp where deptno=pdeptno;
    
    --部门中员工的薪水
    open cemp(pdeptno);
    loop
      --取一个员工的薪水cl
      fetch cemp into psal;
      exit when cemp%notfound;
      
      --判断
      if psal< 3000 then count1:=count1+1;
        elsif psal>=3000 and psal<6000 then count2:=count2+1;
        else count3:=count3+1;
      end if;        

    end loop;
    close cemp;
    
    -- 保存当前结果
    insert into msg1 values(pdeptno,count1,count2,count3,nvl(salTotal,0));

  end loop;
  close cdept;  
  commit;  
  dbms_output.put_line('完成');
end;
/

22.24.	Oracle 分页
 

Page 类
1.	集合：该页上显示的对象
2.	记录数
3.	当前页码
4.	当前起始页码
5.	总记录数
6.	总页码
7.	url: 当前地址


22.25.	数据字典

前缀	说明
USER	用户自己的
ALL	用户可以访问到的
DBA	管理员视图
V$	性能相关的数据



Dictionary

User_objects, all_objects
User_tables
User_tab_columns
User_constraints
User_cons_constraints
User_synonyms


给表加注释
SQL> Comment on table emp is “this is a employee table”;
SQL> User_tab_comments

Session_privs: 当前回话的权限

User_source: 源代码(PL/SQL)

22.26.	Java 调用存储过程和存储函数


死锁：ThreadDump：得到死锁或性能瓶颈
	 *   win: Ctrl+Break
	 *   linux: kill -3 pid

调用Procedure
create [or replace] PROCEDURE 过程名(参数列表)  
AS 
        PLSQL子程序体；
查询并返回某个员工的姓名 月薪和职位

思考: out参数太多???
*/
create or replace procedure queryEmpInfo(eno in number,
                                         pename out varchar2,
                                         psal   out number,
                                         pjob   out varchar2)
as
begin
  select ename,sal,empjob into pename,psal,pjob from emp where empno=eno;

end;


/
/*
 *  思考: 1. 能在mysql运行吗?
 *        2. 光标是否close?
 */
public class TestOracle {
/*
 * create or replace procedure queryEmpInfo(eno in number,
                                         pename out varchar2,
                                         psal   out number,
                                         pjob   out varchar2)
 */

@Test
public void testProcedure(){
	//{call <procedure-name>[(<arg1>,<arg2>, ...)]}
	String sql = "{call queryEmpInfo(?,?,?,?)}";
	
	Connection conn = null;
	CallableStatement call = null;
	try {
		conn = JDBCUtils.getConnection();
		call = conn.prepareCall(sql);
		
		//对于in参数，赋值
		call.setInt(1, 7839);
		
		//对于out参数,申明
		call.registerOutParameter(2, OracleTypes.VARCHAR);
		call.registerOutParameter(3, OracleTypes.NUMBER);
		call.registerOutParameter(4, OracleTypes.VARCHAR);
		
		//执行
		call.execute();
		
		//取出结果
		String name = call.getString(2);
		double sal = call.getDouble(3);
		String job = call.getString(4);
		
		System.out.println(name);
		System.out.println(sal);
		System.out.println(job);
	} catch (Exception e) {
		e.printStackTrace();
	}finally{
		JDBCUtils.release(conn, call, null);
	}
}

调用存储函数
CREATE [OR REPLACE] FUNCTION 函数名(参数列表) 
 RETURN  函数值类型
AS
PLSQL子程序体；

查询某个员工的年收入

create or replace function queryEmpIncome(eno in number)
return number
as
  psal emp.sal%type;
  pcomm emp.comm%type;
begin

  select sal,comm into psal,pcomm from emp where empno=eno;

  return psal*12+nvl(pcomm,0);
end;
/

/*
 * create or replace function queryEmpIncome(eno in number)
return number
 */

@Test
public void testFunction(){
	// {?= call <procedure-name>[(<arg1>,<arg2>, ...)]}
	String sql = "{?=call queryEmpIncome(?)}";
	
	Connection conn = null;
	CallableStatement call = null;
	try {
		conn = JDBCUtils.getConnection();
		call = conn.prepareCall(sql);

		//对于out参数,申明
		call.registerOutParameter(1, OracleTypes.NUMBER);			
		
		//对于in参数，赋值
		call.setInt(2, 7839);
		
		//执行
		call.execute();
		
		//取出结果
		double income = call.getDouble(1);
		System.out.println(income);
	}catch (Exception e) {
		e.printStackTrace();
	}finally{
		JDBCUtils.release(conn, call, null);
	}
}	



在out参数中使用cursor
解决的问题：返回值是一个集合

查询某个部门中 所有员工的所有信息

--软件PL/SQL -> create package ->mypackage.
--包头
CREATE OR REPLACE PACKAGE MYPACKAGE AS 
  type empcursor is ref cursor;
  procedure queryEmpList(dno in number,empList out empcursor);
END MYPACKAGE;

--软件PL/SQL -> create package body
--包体
CREATE OR REPLACE PACKAGE BODY MYPACKAGE AS
  procedure queryEmpList(dno in number,empList out empcursor) AS
  BEGIN
    open empList for select * from emp where deptno=dno;
  END queryEmpList;
END MYPACKAGE;


@Test
public void testCursor(){
	String sql = "{call MYPACKAGE.queryEmpList(?,?)}";
	
	Connection conn = null;
	CallableStatement call = null;
	ResultSet rs = null;
	try {
		conn = JDBCUtils.getConnection();
		call = conn.prepareCall(sql);
		
		//对于in参数，赋值
		call.setInt(1, 20);
		
		//对于out参数,申明
		call.registerOutParameter(2, OracleTypes.CURSOR);
		
		//执行
		call.execute();
		
		//取出结果
		rs = ((OracleCallableStatement)call).getCursor(2);
		while(rs.next()){
			String name = rs.getString("ename");
			double sal = rs.getDouble("sal");
			
			System.out.println(name+"的薪水是"+sal);
		}
		
	} catch (Exception e) {
		e.printStackTrace();
	}finally{
		JDBCUtils.release(conn, call, rs);
	}
}

22.27.	Trigger触发器
/*
create [or replace] PROCEDURE 过程名(参数列表)  
AS 
        PLSQL子程序体；

为指定的员工涨100块钱  并打印涨前和涨后的薪水
*/
create or replace procedure raiseSalary(eno in number)
as
  psal emp.sal%type;
begin
  --涨前薪水
  select sal into psal from emp where empno=eno;
  
  --涨100
  update emp set sal=sal+100 where empno=eno;
  
  --要不要commit???
  
  dbms_output.put_line('涨前:'||psal||'   涨后:'||(psal+100));

end;
/


/*
成功插入员工后，自动输出“成功插入一个新员工”
   CREATE  [or REPLACE] TRIGGER  触发器名
   {BEFORE | AFTER}
   {DELETE | INSERT | UPDATE [OF 列名]}
   ON  表名
   PLSQL 块

*/
create or replace trigger sayNewEmp
after insert
on emp
begin
  dbms_output.put_line('成功插入一个新员工');
end;
/

触发器场景1：安全性检查
/*
实施复杂的安全性检查

禁止在非工作时间 往emp表中插入数据
   CREATE  [or REPLACE] TRIGGER  触发器名
   {BEFORE | AFTER}
   {DELETE | INSERT | UPDATE [OF 列名]}
   ON  表名
   PLSQL 块

周末:to_char(sysdate,'day') in ('星期六','星期日')
上班前 下班后: to_number(to_char(sysdate,'hh24')) not between 9 and 18
*/
create or replace trigger securityEmp
before insert
on emp
begin
  if to_char(sysdate,'day') in ('星期六','星期日') or 
      to_number(to_char(sysdate,'hh24')) not between 9 and 18 then 
      
    raise_application_error(-20001,'不能在非工作时间插入数据');

  end if;
end;
/

触发器场景2：数据确认
/*
数据确认

涨后的薪水不能少于涨前的薪水
   CREATE  [or REPLACE] TRIGGER  触发器名
   {BEFORE | AFTER}
   {DELETE | INSERT | UPDATE [OF 列名]}
   ON  表名
   [FOR EACH ROW [WHEN(条件) ] ]
   PLSQL 块

*/
create or replace trigger checksal
before update
on emp
for each row
begin
    --if 涨后的薪水< 涨前的薪水 then 
    if :new.sal < :old.sal then   
      raise_application_error(-20002,'涨后的薪水不能少于涨前的薪水.涨前:'||:old.sal||'  涨后:'||:new.sal);
    end if;
end;
/


22.28.	查询练习
Sqltest-mysql
韩顺平-java-SqlServer

create table dept
(depno int primary key,
dname nvarchar(30),
loc nvarchar(30))

create table emp
(empno int primary key,
ename nvarchar(30),
job nvarchar(30),
mgr int,
hiredate datetime,
sal numeric(10,2),
comm numeric(10,2),   -- bonus
deptno int foreign key references dept(deptno))
-- foregin key references: only one primary key, and the same type

--简单查询
--查询smith的薪水，工作，所在部门
select sal, job, deptno from emp where ename='smith';  --‘SMITH’不区分大小写。ORACLE区分大小写！

select distinct deptno from emp;		--"distinct" removes duplicates
select ename, sal*13 'annual salary' from emp;		-- "annual salary": alias of "sal；as可以省略；不区分单、双引号，无引号
select ename, sal*13+isnull(comm,0)*13 'annual salary' from emp;	-- isnull(comm,0)

select * from emp where hiredate>'1982-1-1'

select * from emp sal>2000 and sal <2500
select * from emp where sal between 2000 and 2500		-- >= and <=

select ename, sal from emp where ename like 'S%'		-- name start with "S"
--显示第3个字符为大写O的所有员工姓名和工资
select ename, sal from emp where ename like '__O%';  --the third letter is "O"; 与oracle一样

select * from emp where empno=123 or empno=345 or empno=800;	-- no efficient
select * from emp where empno in (123, 345, 800);		-- better

--没有老板的员工
select * from emp where mgr is null;		-- employee without a manager

--工资高于500或者岗位为manager的雇员，同时还要满足他们的姓名首写字母为j
select * from emp where (sal>500 or job='manager') and (ename like 'J%'); 

select * from emp order by sal asc;			-- "asc" by default, "desc"

select * from emp order by deptno, sal desc;

--统计每个人的年薪，并从低到高排序
select  ename, (sal+isnull(comm,0))*13 from emp order by (sal+isnull(comm,0))*13;		-- works fine but duplicate calculation
select  ename, (sal+isnull(comm,0))*13 salary from emp order by salary;				-- use alias

--复杂查询
select min(sal) from emp;	--
-- 最低工资和该员工的名字display salary and name of those employee with lowest salary
select ename, min(sal) from emp;	--this is wrong; MySQL可以？？
select ename, sal from emp where sal=(select min(sal) from emp);
--sql优化原则：将简易查询尽量写在右边

select avg(sal) 'average salary', sum(sal) 'total salary' from emp;

--total number of employee
select count(*) from emp;

--显示高于平均工资的员工的名字、工资
select ename, sal from emp where sal>(select avg(sal) from emp);
-- how to also show average salary in the third column?
select ename, sal, (select avg(sal) from emp) from emp where sal>(select avg(sal) from emp); --不太好

--show every dept's average salary and highest salary
select avg(sal), deptno, max(sal) from emp group by deptno
--再显示部门名称
-- select e.avg(sal), e.deptno, d.deptname, e.max(sal) from emp e, dept d where e.deptno=d.deptno group by deptno


--show every job in every dept's average salary, minimum salary...
select avg(sal), min(sal), deptno, job from emp group by deptno, job order by deptno;

--show deptno and average salary of those average salar less than 2000 in each department
--"having" together with "group by": furhter filter results after grouped, and by order of salary.
select avg(sal), deptno from emp group by deptno having avg(sal)<2000 order by avg(sal) asc;
MySQL: SELECT AVG(sal) s, deptno FROM emp GROUP BY deptno HAVING s<3000 ORDER BY s ASC;
--多表查询
--two tables
select ename, sal, loc from emp, dept where dept.dname='sales' and emp.detno=dept.deptno;

select ename, sal, loc, deptno from emp, dept where dept.dname='sales' and emp.detno=dept.deptno;  --wrong, deptno is in both tables.
select ename, sal, loc, emp.deptno from emp, dept where dept.dname='sales' and emp.detno=dept.deptno;
select ename, sal, loc, e.deptno from emp e, dept d, e.deptno where d.dname='sales' and e.detno=d.deptno;

--show deptno, name and salary of deptno is 10
select d.dname, e.ename, e.sal from emp e, dept d where d.deptno=10 and e.deptno=d.deptno;		--must have "and e.deptno=d.deptno"

select d.dname, e.sal, e.ename from emp e, dept d where e.deptno=d.deptnno order by d.dname;

------------------------------ self link 自连接-------------------------------
--show an employee 's manager's name
select ename from emp where empno=(select mgr from emp where ename='ford');

--show every employee's name and his manager's name
--take emp as if it is two tables: worker, boss
select worker.ename, boss.ename from emp worker, emp boss where worker.mgr=boss.empno


----------------------------embeded select--------------------------------
--show all at the same dept with Smith
select * from emp where deptno = (select deptno from emp where ename='Smith');

--show all that have the same job in dept 10
--how to exclude people already in dept 10?
select * from emp where job in (select distint job from emp where deptno=10)		-- use "in" when there are several results
SELECT * FROM emp WHERE job IN (SELECT DISTINCT job FROM emp WHERE deptno=10) AND deptno !=10

--show all employee with salary higher than the dept's average salary
selet emp.ename, emp.sal, temp.a from (select avg(sal) a, dept from emp group by dept) temp 
where emp.sal>temp.a and emp.deptno=temp.deptno;	--use alias
--MySQL
SELECT e.ename, e.sal, t.a 
FROM (SELECT AVG(sal) a, deptno FROM emp e GROUP BY deptno) t, emp e 
WHERE e.sal>t.a AND e.deptno=t.deptno;

--最早的4名员工
select top 4 * from emp order by hiredate;
select * from emp order by hiredate;
mysql: SELECT * FROM emp ORDER BY hiredate LIMIT 5;
oracle: selet * from (select rownum, ename, sal from emp order by hiredate) h where h.rownum<=5;

-- top 6 *: choose 5-10 by excluding the first 4
select top 6 * from emp where empno not in (select top 4 empno from emp order by hiredate) order by hiredate;
mysql: SELECT * FROM emp ORDER BY hiredate LIMIT 4, 6;	--start from 0! Include 4, get 6 records

-- show 11-13
select top 3 * from emp where empno not in (select top 10 empno from emp order by hiredate) order by hiredate;


-------------------------------------large data test----------------------------------------
--identity(1,1): testID auto increase by 1 from 1
create table test(
testID int primary key identity(1,1),
testName varchar(30),
testPass varchar(30))

mysql: PRIMARY KEY auto_increment

insert into test (testName, testPass) values ('shunping', 'shunping');
select count(*) from test;
insert into test (testName, testPass) select testName, testPass from test;

select top 6 * from test where testID not in (select top 999 testID from test);
drop table test

----------------------how to remove duplicates from the table---------------------------------
create table cat(
catID int,
catName varchar(40))

insert into cat values (2,'bb');
select * from cat

select distinct *  into #temp from cat		--1. put distict records into temporary table #temp
delete from cat								--2. erase all data in table cat
insert into cat select * from #temp			--3. copy #temp to table cat
drop table #temp							--4. delete the table #temp

--外连接
---------------------- left foreign link, right foreign link------------------------
--show every employee and their boss's names
--inner link: show only matched
select w.ename, b.ename from emp w, emp b where w.mgr=b.empno

--how to also show people without boss
--left foreign link: show all recorder in left table; if no record found in right table, show NULL
select w.ename, b.ename from emp w left join emp b on w.mgr=b.empno

--约束
----------------------entry control: not null, unique, primary key, foreign key, check, default
--testName varchar(30) not null,
--insert into test1 (testage) values (3);								--testname and testpass are NULL
--insert into test1 (testname, testpass, testage) values('','',5)		--testname and testpass are not filled yet.

--primary key (testID, testname);		--复合主键, duplicate: testID and testname are the same at the same time
-- sal int check (sal>=1000 and sal <=2000)
--mesDate datetime default getdate()		--default

--------------------control example----------------
create table goods(
goodsID nvarchar(50) primary key,
goodsName nvarchar(80) not null,
unitprice numeric(10,2) check (unitprice>0),
category nvarchar(3) check(category in ('food','grocery')),
provider nvarchar(50)
)

create table customer(
customerID nvarchar(50) primary key,
cusname nvarchar(50) not null,
address nvarchar(100),
email nvarchar(100) unique,
sex nchar(1) check (sex in ('man','woman')) default 'man',
ID nvarchar(18))

create table purchase(
customerID nvarchar(50) foreign key references customer(customerID),
goodsID nvarchar(50) foreign key references goods(goodsID),
nums int check (nums>0))

select * from goods

--数据库备份/恢复
----------------------------back up database--------------
--Method 1. in SQL server Management studio
--right click the database name->task->detach ->*.mdf and *.ldf
--attach 
--Method 2. right click the database name->task->backup
--Method 3.
backup database liangshan to disk='f:/sp.bak';
restore database liangshan from disk='f:/sp.bak';

--------------------CRUD, java

select * from emp


--作业
-----------------------------homework-----------------------
选择部门30中所有员工
列出所有clerk的姓名，编号和部门号
找出comm高于工资的员工
SELECT * FROM emp WHERE comm>sal;

找出comm高于工资60%的员工 
select * from emp where isnull(comm,0)>sal*0.6

找出部门10中所有经理和部门20中所有办事员的详细资料
SELECT * FROM emp 
WHERE (deptno=10 AND job='manager') 
OR (deptno=20 AND job='clerk');

找出部门10中所有经理和部门20中所有办事员的详细资料，以及既不是经理又不是办事员但工资大于或等于2000的所有员工详细资料
SELECT * FROM emp 
WHERE (deptno=10 AND job='manager') 
OR (deptno=20 AND job='clerk') 
OR (job NOT IN ('manager', 'clerk') AND sal>=2000);

找出收取comm员工的不同工作
select distict job from emp where comm >0 -- comm is not null or isnull(comm, 0)>0
SELECT DISTINCT job FROM emp 
WHERE comm IS NOT NULL;		// comm>0

找出不收取comm或者comm小于100的员工的不同工作
select distict job from emp where comm <100 or comm is null

--find employees hired in the last 3 days of each month
--oracle has a funtion to return the last day of month: last_day()

--empolyees hired 12 years ago
select * from emp where datediff(year, hiredate, getdate())>12;		--didn't consider days
select ename, hiredate from emp where datediff(year, hiredate, getdate())>10;

--first letter of name to capital
select upper(substring(ename,1,1))+lower(substring(ename,2,len(ename))) from emp;

--name has 5 letters
select * from emp where ename like '_____';  --five “_”
select* from emp where len(ename)=5;

--first 3 letters of name
select substring(ename, 1,3) from emp;

--replace A with a in names
select replace(ename, 'A',  'a') from emp

select ename, hiredate from emp order by hiredate;
select ename, job, sal from emp order by job desc, sal;

--date's year and month
select ename, datepart(year, hiredate) y, datepart(month, hiredate) m from emp order by m, y;


--至少有一个员工的部门--dept has at least two employees
select count(*), deptno from emp group by deptno having count(*)>2

--工资比’smith’多的所有员工

--所有员工的姓名及其直接上级的姓名，其受雇日期晚于上级
select w.ename, b.ename from emp w, emp b where w.mgr=b.empno and w.hiredate>b.hiredate;

--dept name and its employee's names, also dept without any empolyees
select d.dname, e.ename, e.job from emp e right join dept d on e.deptno=d.deptno;
SELECT d.dname, e.ename, e.job
FROM dept d LEFT JOIN emp e 
ON d.deptno=e.deptno;

--列出所有clerk的姓名和其部门名称
SELECT e.ename, d.dname 
FROM emp e, dept d 
WHERE e.job='clerk' AND e.deptno=d.deptno;

--jobs with lowest salary > 1500
select min(sal), job from emp group by job having min(sal)>1500;
SELECT job, MIN(sal) 
FROM emp 
GROUP BY job HAVING MIN(sal)>1500;

--names from dept "sales"
select ename, 'sales' from emp where deptno=(select deptno from dept where dname='sales');


select * from emp where sal>(select avg(sal) from emp);
SELECT * FROM emp WHERE sal> AVG(sal); --错AVG()是分组函数，不能直接用！

与scott从事相同工作的所有员工
SELECT * FROM emp 
WHERE job = (SELECT job FROM emp WHERE ename='scott');

列出工资等于部门30中员工工资的所有工资的姓名和工资
select ename, sal from emp where sal>(select max(sal) from emp where deptno=30)
SELECT ename, sal FROM emp 
WHERE sal>ALL(SELECT sal FROM emp WHERE deptno=30)

--列出每个部门中的员工数量，平均工资和平均服务期限
select count(*), avg(sal), avg(datediff(year, hiredate, getdate())), deptno from emp group by deptno
SELECT COUNT(*), AVG(sal), AVG(YEAR(CURDATE())-YEAR(hiredate)), deptno 
FROM emp GROUP BY deptno;

--列出从事同一种工作但属于不同部门的员工的组合
SELECT a.ename, a.job, a.deptno, b.ename, b.job, b.deptno 
FROM emp a, emp b 
WHERE a.job=b.job AND a.deptno<>b.deptno;

--列出所有部门的详细信息和人数
--dept's info with number of employees in each dept, replace null with 0 
select d2.dname, d2.loc, isnull(d1.c,0) from dept d2 left join (select 
count(*) c, deptno from emp group by deptno) d1 on d2.deptno=d1.deptno;
SELECT IFNULL(c,0), d.deptno, d.dname 
FROM dept d LEFT JOIN (SELECT COUNT(*) c, deptno FROM emp GROUP BY deptno) t
ON d.deptno=t.deptno;

--列出各种工作的最低工资
select min(sal) from emp group by job;

--找出经理的最低工资manager's lowest salary
select min(sal) from emp where job='manager';
SELECT MIN(t.sal) FROM (SELECT b.sal FROM emp e, emp b WHERE e.mgr=b.empno) t;

--列出所有员工的年工资，按年薪从低到高排序 all annual salary, order
select (sal+isnull(comm,0))*12 'Annual Sallary', ename from emp order by 'Annual Sallary'
SELECT (sal+IFNULL(comm,0))*12 n FROM emp ORDER BY n;

作业2
一张表test，有3个字段，id, name, parentid。写sql抓出爷爷的id和name
SELECT DISTINCT e2.empno, e2.ename, e2.job FROM emp e2, 
(SELECT DISTINCT b.empno empno, b.mgr mgr, b.ename FROM emp e, emp b WHERE e.mgr=b.empno) p 
WHERE e2.empno=p.mgr;
(先查出经理的no和，他的经理 -> 临时表)

一张表student (sid, name), 另一张选课表taken(sid, cid), 第3张表couse(cid, cname)。找出选了所有课程的学生。
Select s.sid, s.name from student s, taken t, course c group by s.sid having s.sid=t.sid and count(*) = (select count(*) from course);
Select s.sid, s.name 
from student s, (select sid, count(*) tc from taken group by sid) t, course, c
where s.sid=t.sid and t.tc=(select count(*) from course)

一张表person(id, name, age)。找出年龄最接近的2个人。如下记录：
1, a, 18; 2, b, 20; 3, c, 25; 4, d, 26
输出3, 4
