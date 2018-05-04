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