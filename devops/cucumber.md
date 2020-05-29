# Cucumber

- plugin: Natural
- chrome plugin: tidy gherkin; 
- DataTable data, data.raw(); 
- parameterized variable with Examples; 
- @RegTest, @SmokeTest, @SanityTest, @MobileTest => 
- CucumberOptions(tags="@SmokeTest"); 
- Background keywork, in feature file similar to @BeforeEach; 
- @Before("@MobileTest") => remove Background section;
- dryRun=true (do not run test, only check if all features are implemented), monochrome=true (for pretty printing output), 
- restrict=true (to check missing implementation); 
- mvn test (need surefire plugin)
