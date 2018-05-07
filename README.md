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