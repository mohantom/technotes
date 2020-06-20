Spring
---------


## AOP
AOP 的概念
   1、切面 （Aspect, 比如Hibernate的Transaction（事务）也是一个切面）
        事务、日志、安全性框架、权限等都是切面。不是目标方法的都是切面。
	横切性关注点的抽象。与类相似，但类是对物体特征的抽象。
各人做事物、日志、安全的时候都不知道其他的存在、怎么写的，直到在客户端测试时。耦合性降低。如果有变化，只需要改各个模块就可以了。
   2、通知 advice
      切面中的方法就是通知 (logging(), security(), etc)
   3、目标类: target
joinpoint (连接点)： 被拦截到的点
   4、切入点 Pointcut： 对哪些joinpoint进行拦截的定义
         只有符合切入点，才能让通知和目标方法结合在一起
   5、织入 weaving：
         形成代理对象的方法的过程（将aspects应用到target对象并导致Proxy对象创建的过程）
         代理对象的方法 = 通知(切面方法) + 目标方法
   6、引入 introduction: 在不修改目标类的情况下，在运行期为类动态的添加一些方法或Field。

好处：
   事务、日志、安全性框架、权限、目标方法之间完全是松耦合的(loose coupled)

```shell script
@Aspect
public class MyInterceptor {
	@Pointcut("execution (* cn.itcast.service.impl.PersonServiceBean.*(..))")
	private void anyMethod() {
	}// 声明一个切入点

	@Before("anyMethod() && args(userName)")	//只拦截有个String参数的方法执行
	public void doAccessCheck(String userName) {
		System.out.println("前置通知:" + userName);
	}

	@AfterReturning(pointcut = "anyMethod()",returning="result") //目标方法的返回值
	public void doAfterReturning(String result) {
		System.out.println("后置通知:"+ result);
	}
	@After("anyMethod()")
	public void doAfter() {
		System.out.println("最终通知");
	}
	@AfterThrowing(pointcut="anyMethod()",throwing="e")
	public void doAfterThrowing(Exception e) {
		System.out.println("例外通知:"+ e);
	}
	
	@Around("anyMethod()")
	public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
		//if(){//判断用户是否在权限
		System.out.println("进入方法");
		Object result = pjp.proceed();	//这个之后再执行目标方法
		System.out.println("退出方法");
		//}
		return result;
	}	
}

```


## Transactional
```shell script
RuntimeException (unchecked exception, eg, throw new Exception("e")): 默认事务会回滚
Checked exception (try catch 语句): 默认事务不会回滚 
@Transactional(rollbackFor=Exception.class)//会回滚
@Transactional(noRollbackFor=Exception.class)//不会回滚
	public void delete(Integer personid) {
		jdbcTemplate.update("delete from person where id=?", new Object[] { personid }, new int[] { java.sql.Types.INTEGER });
	throw new RuntimeException("运行期例外");
	}

	@Transanctional(propagation=Propagation.NOT_SUPPORTED) //不需要事务
	@SuppressWarnings("unchecked")
	public List<Person> getPersons() {
		return (List<Person>) jdbcTemplate.query("select * from person", new PersonRowMapper());
	}
```

@Transactional
	可以写在方法上。
		对本方法有效
	可以定在类上。
		对本类中所有public方法有效。
		对子类的中方法有效。
		对父类声明的方法无效。



事务传播属性
•	REQUIRED: 如果已经处在一个事务中则加入，否则自己创建一个新的事务。
•	NOT_SUPPORTED: 不需要事务。如果关联到一个事务，容器不会为它开启事务。如果方法在一个事务中被调用，该事务会被挂起，方法调用结束后，原先的事务会恢复执行。
•	REQUIREDSNEW: 不管是否存在事务，总发起一个新的事务。如果已经运行在一个事务中，原有事务会被挂起。
•	MANDATORY: 只能在一个已经存在的事务中执行，不能自己发起事务。如果没有事务的环境下被调用，会抛出异常。
•	SUPPORTS: 如果在某个事务内被调用，则加入；如果在事务外，则运行在没有事务的环境下。
•	NEVER: 制定业务方法绝对不能在事务范围内执行。否则抛出异常。
•	NESTED: 如果一个活动的事务存在，则运行在一个嵌套的事务中。如果没有活动的事务，则按REQUIRED属性执行。使用一个单独的事务，拥有多个可以回滚的保存点。内部事务的会滚不会对外部事务造成影响。它只对DataSourceTransactionManager事务管理器有效。


Course: Architecting Web Applications with Spring
---------------

## Spring configuration
```shell script
@Transactional
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(classes = ApplicationConfiguration.class)
@Sql({"/insert-data.sql"})
@Sql(scripts = "/clean-up.sql", executionPhase= AFTER_TEST_METHOD)
@ActiveProfiles("test")
public abstract class AbstractTest{ }
```


use @Autowired to inject the object

## security
authentication (who you are), authorization (what you are allowed to do)
apply plugin: 'spring-boot'


Testability, maintainablility, scalability, complexity, business focus
Everything is POJO.
Essentially a glorified HashMap, can be used as a registry

applicationContext.xml
autowire: byType, byname, constructor



