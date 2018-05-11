# Pluralsight Effective C# Unit-Testing

## Effective Unit Tests

### Pre-Requisites

- clean code (decoupled, generic when possible)
- testable design (interfaces, dependency injection)
- context-aware (more or fewer tests depending on importance of app)
- solid understanding of unit-testing 

### Qualites

- clear and simple
- high value
- flexible

## Definitions

### Stub
- substitute for a dependency in the code under test that allows code to compile and dependency to return data __but importantly cannot itself directly make test fail__.

### Mock
- ethods were called and in what order that that it can validate an assumption about it's usage and __therefore make a test fail.__

### Fake 
- generic term for mock or stub.

---

## Naming Conventions

### 3-Part naming
- unit of work (main scenario test is covering)
- initial (how scenario is setup, more specific than UOW)
- expected result (how scenario should go)

~~~

Ex. 

UnitOfWork_InitialCondition_ExpectedResult();
UserLogsIn_WithValidCredentials_RedirectsToHome();
UserLogsIn_WithBadPassword_ReturnsError();

Ex.

[TestMethod]
public void UoW_InitialCondition_ExpectedResult()
{
    //Arrange
    // Setup target with dependencies that are needed

    //Act
    // normally one line of code to start test

    //Assert
    // assert statements to check result

}

~~~

#### Benefits
1) easier to organize tests
2) helps you realize new test conditions (just be writing the names)
3) follows convention so you'll understand the usage faster

__useful vs snippet for generating test methods: https://gist.github.com/osmyn/906c917653a30864cb52dee02c36c14e__



### *Test by scenario, not method*


---

### DAMP & DRY Code

__DAMP__ 
- *Descriptive And Meaningful Phrases* promotes the readability of the code
To maintain code, you first need to understand the code. To understand it, you have to read it. Consider for a moment how much time you spend reading code. It's a lot. DAMP *increases maintainability by reducing the time necessary to read and understand the code*.

__DRY__
- *Don't repeat yourself*
Removing duplication ensures that every concept in the system has a single authoritative representation in the code. A change to a single business concept results in a single change to the code. DRY increases maintainability by isolating change (risk) to only those parts of the system that must change.

- keep unit tests and integration tests (calling an external API, hitting a database, etc) in seperate projects so unit tests can run super fast, while integration tests can be run daily (or as needed) since they're slower and more prone to intermittent failures.

---

## Favor composition over inheritance to create testable code (injection easier to mock then inherited behaviors)
- instead of newing up objects within your methods, instead try to inject those into it via parameters
- this allows you to mock these later during your tests

## Tips for Testable Code

### Elements
- classes ask for what they need (in constructor) so they only do what they NEED to do. *The class should ask for the bottom-most thing (list of planes, id, etc) instead of going and getting data itself*
- avoid 'new' (inject your dependency instead)
- avoid global states that multiple objects can modify (makes it harder to test single scenario)
- avoid static methods (difficult to fake)
- add seams to your code (pub props to private variables) so testing can modify these after construction
- composition over inheritance

### SOLID Design
- Single resposibility (makes testing much easier, ask for data, don't get it yourself)
- Open for extension, closed for modification (work with interfaces)
- Liskov substitution princriple (implement interfaces as designed, don't get too clever)
- Interface segregation (don't keep adding to interface)
- Dependency inversion (inject instead of new-ing up)

### What to test?
- test the *riskiest* sections of your code first (sections where errors could occur most often)
- testing the return of a method holds most value, followed closely by object state

### Test Coverage
- test business rules & happy/sad paths
- testing things the compiler would check aren't valuable and create something you might need to change later
- don't worry about 100% code coverage, think about scenarios and real-world situations the code may face.

---

### When to use *Static*?
- static methods are OK if the static of it doesn't change 
- these don't need to be newed-up and can be easily called b/c they never have a state
- these are also easily testable __if it's state doesn't change__
__I.E__ an updateMyString() method that takes in a string and returns the changed string

### Tips for creating easily-changable tests
- maximum of 1 mock per test
- fewer than 10% of tests use mocks
- __RARELY__ directly test a private method (should be available via a seam)
- test via scenario not method (keep tests are dumb as possible)

---

### Are my tests effective?
1. you trust them
2. you maintain them
3. you actually read them (good naming)
4. they don't impede development 

### Unit Testing Checklist
- test name describes the scenario
- contains arrange, act, assert sections
- stays within single project layer
- is a state, value, or interaction test
- fakes all dependencies
- Mock at most 1 dependency per test
- favors the public API (seams) over internal logic
- asserts against single object 