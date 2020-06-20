Junit
========

assertThat(z, is(8)); // assertThat(T actual, org.hamcrest.Matcher<T> matcher)

junit在eclipse自带的包和引进的包会有冲突。把自带的删掉就好了。

```shell script
assertThat(n, allOf(greaterThan(5), lessThan(10));  //allOf里面的条件都要满足
assertThat(n, anyOf(greaterThan(5), lessThan(10));  
assertThat(n, anything); is, not, 
containsString, endsWith, startsWith, equalTo, equalToIgoringCase, equalToIgnoringWhiteSpace,
closeTo(3.0, 0.3) //3.0 +/- 0.3
greaterThanOrEqualTo, lessThanOrEqualTo
hasEntry, hasItem, hasKey, hasValue
```


failure: 测试失败
error: 程序出错， 2/0

## Annotation
- @Test
- @Test(expected=java.lang.ArithmeticException.class)
- @Test(timeout=100)

- @Ignore  //本次测试忽略该方法
- @Before  //每个测试之前
- @After
- @BeforeClass  //所有测试开始之前，只加载一次
- @AfterClass
static SomeDao dao = null;
Public static void aa() { dao = new SomeDao(); }

@BeforeClass
Public static void beforeClass() { System.out.println("before Class");

## Run multiple tests
Run configuration: 可以选择测试哪些测试方法

### TDD: test driven development 先写测试

Course: Introduction to Testing in Java
Course: Test-Driven Development Practices in Java
Old way: write all functions, then write tests
	Omission of thought in automated unit testing approach
	Benefits of automation missed
	Time crunch encountered in projects
 

From test (red) -> fix test by writing functions -> refactoring

xUnit testing
Class-Under-Test
Method-Under-Test
Test fixture

Don’t have to write all tests before coding. Add more later.
Mockito, DBUnit, PowerMockito
Eclipse: m2e (maven plugin), eclemma(code coverage), subclipe
H2 database: in-memory in process or out of process
	H2w.bat


## Hamcrest
http://blog.csdn.net/neven7/article/details/42489723 
assertThat("myname", startWith("my")
allOf(), anyOf(), both().and(), either().or()
is(), is(not("you")), is(nullValue), is(notNullValue())
everyItem(startsWith("m"), hasItem("me"), hasItems("me", "you")

// numbers
assertThat(n, allOf(greaterThan(5), lessThan(10));  //allOf里面的条件都要满足
assertThat(n, anyOf(greaterThan(5), lessThan(10));  
closeTo(3.0, 0.3) //3.0 +/- 0.3
greaterThanOrEqualTo, lessThanOrEqualTo

assertThat(n, anything); is, not, 

// String
containsString, endsWith, startsWith, equalTo, equalToIgnoringCase, equalToIgnoringWhiteSpace,

// collection
hasEntry, hasItem, hasKey, hasValue


## Mockito
Testing with dependencies creates challenges
	Live database needed
	Multiple developers testing simultaneously
	Incomplete dependency implementation

OrderDao (the interface for database) 
 
Alternative to Mockito.mock( ***.class), use @Mock:
```shell script
Protected @Mock OrderDao mockOrderDao;
@Before
Public void setup() {
	MockitoAnnotations.initiMocks(this);
}
MockSettings.extraInterfaces()
MockSettings.serializable()
MockSettings.name()

Method stubbing
Mockito.when()
	.thenReturn()
	.thenThrow()
Mockito.doThrow(..) returns the Stubber class
```


Delegate calls to the underlying instance with thenCallRealMethod()
Answering: Conditionally respond based on mock operation parameters
Verifications (not required)
	Mockito.verify() is to verify an intended mock operation was called.
VerificationMode allows extra verification of operation
	Times(n)
	atLeastOnce()
	atLeast(n)
	atMost(n)
	never()
Mockito.verify().zeroInteractions()
Mockito.verify().noMoreInteractions()

Mockito feature deep-dive, powerMock

### Matchers
Matchers.eq(..)
Matchers.any(String.class), .anyDouble(), .anySetOf(String.class)
.contains("own"), .starts(), ends()
.same(ref)
thenThrow(..).thenReturn(1);

Argument captor

Mock vs Spies
Mocking interfaces vs Classes
Partial mocking mixes controlled invocation stubs with real method calls
	You can’t mock final methods
	You can’t mock private methods
	Set the state appropriately

### PowerMock
	Mockito covers 80% of usage scenarios. Use powerMock only when necessary.

Mock static method
PowerMockito.mockStatic(WarehouseManagementService.class);

Replacing object instantiation
PowerMockito.whenNew()

Final & Private methods
PowerMockito.mock()

Whitebox
Wrapper around java reflection API, but geared towards testing

Fixture management & data component testing
Limit initialization scope. Find balance between redundant setup and minimum field setup.
Consider a fixture factory or utility class
orderFixture.setId(1); 

## DBUnit

File based dataset

Good naming
	Use domain terminology, natural language, be descriptive
Test behavior not implementation
	Don't try to access private members
	Implementation: exposing private state results in brittle and hard to maintain tests
	Behavior: assert about the result of an operation; you can change the implementation and the test still passes
Don’t repeat yourself
	Café.restorckBeans(ESPRESS_BEANS);  // instead of "7"
Diagnostics
	assertTrue(order.size(), 1);  // not good, not much exception info
=> assertEquals(1, order.size());
	=> assertEquals("wrong quantity of coffee", 1, order.size());



> Always implement things when you actually need them, never when you foresee that you need them. --- Ron Jefferies

