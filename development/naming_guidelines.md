# Naming Conventions and Guidelines

## Introduction

This document outlines the code conventions and guidelines that must be followed when authoring unit tests for new and existing OSC components and features. Each of the topics covered in this section is aligned with the following core principles:

1. Isolation and independency: Tests should not be interdependent. They should run in any order and not propagate failure.
2. Single responsibility: Each test should validate a single unit or aspect of the code.
3. Optimized for reading and maintaining: Tests should be written in a way that is easy to read and maintain. Do not optimize for authoring. A test is usually written once and read many times.
4. Consistency: Test name and format should be consistent across OSC.
5. Environment independent execution: A deployment must not be needed to execute the tests.
6. Run fast: A single test should run in a matter of tens of milliseconds. A test that is taking longer to run might be doing too much or have a hidden environment dependency.

## Conventions

### Naming

#### Class Name

The name of the test class should match the class under test with the addition of the suffix **Test**.

For instance, class under test: `AddDistributedApplianceService.java`

**DO:**

`AddDistributedApplianceServiceTest.java`

**DON'T:**

`AddDistributedApplianceServiceTests.java`

`TestsAddDistributedApplianceService`

`TestAddDistributedApplianceService.java`

`AddDistributedApplianceService.java`

#### Method Name

Keep the following in mind when authoring a unit test: 
* what is being tested
* how it is being tested
* what is the expectation being validated

Keeping these things in mind for each test will result in clear, small, and more maintainable test methods.

The naming convention adopted for the test methods highlights these things, making the test name self-explanatory with no need for additional documentation. Having difficulty naming a test method after these things likely indicates a code smell that might be trying to cover too much on a single unit test.

The test method name should follow this pattern:
```java
testMethodUnderTest_HowIsItTested_WhatItExpects(){}
```

With the exception of (**testMethodUnderTest**), free form is provided to allow for clarity if needed. 

For instance, if you are testing the following method:
```java
void depositCheck(string checkNumber, int value) throws Exception{}
```
**DO:**
```java
testDepositCheck_WithNegativeValue_ThrowsInvalidValueException(){}

testDepositCheck_WithValidValue_ExpectsSuccessDeposit(){}
```
**DON'T:**
```java
testDepositCheckWithNegativeValueThrowsInvalidValueException(){} // no clear separation

testDepositCheckNegativeValue(){} // no clear expectation

testDepositCheck(){} // too vague

testdepositCheck_WithValidValue_ExpectsSuccessDeposit(){} // lower case method name

depositCheck_WithValidValue_ExpectsSuccessDeposit(){} // no test prefix

testDeposit_WithValidValue_ExpectsSuccessDeposit(){} // wrong test method name
