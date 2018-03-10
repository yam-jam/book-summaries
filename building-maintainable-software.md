# Building Maintainable Software - Ten Guidelines For Future-Proof Code
Author: Joost Visser

## 1 - Introduction
### 1.1 What is maintainability?
* Maintainabilit``y - how easily a system can be modified
* Characteristics of software quality (ISO 25010):
  * Maintainability
  * Functional suitability
  * Performance efficiency
  * Compatibility
  * Usability
  * Reliability
  * Security
  * Portability
* Four types of software maintainance
  * Corrective Maintainence
    * Bugs are discovered and have to be fixed
  * Adaptive Maintenance
    * System has to be adapted to changes in the environment in which it operates
  * Perfective Maintenance
    * Users of the system have new or changed requirements
  * Preventive Maintenance
    * Ways are identified to increase quality or prevent future bugs from occurring

### 1.2 Why is maintainability important?
* Maintainability has significant business impact
* Maintainability is an enabler for other quality characteristics

### 1.3 Three principles of the guidelines in this book
1. Maintainability benefits most from simple guidelines
2. Maintainability is not an afterthought, and every contribution counts
3. Some violations are worse than others

### 1.4 Misunderstandings about maintainability
* Maintainability is language-dependent
* Maintainability is industry-dependent
* Maintainability is the same as the absence of bugs
* Maintainability is a binary quantity

### 1.5 Rating maintainability
* Software Improvement Group (SIG) benchmarks

### 1.6 An overview of the maintainability guidelines
* [Write short units of code](#2---write-short-units-of-code)
* [Write simple units of code](#3---write-simple-units-of-code)
* [Write code once](#4---write-code-once)
* [Keep unit interfaces small](#5---keep-unit-interfaces-small)
* [Separate concerns in modules](#6---separate-concerns-in-modules)
* [Couple architecture components loosely](#7---couple-architecture-components-loosely)
* [Keep architecture components balanced](#8---keep-architecture-components-balanced)
* [Keep your codebase small](#9---keep-your-code-base-small)
* [Automate development pipeline and tests](#10---automate-tests)
* [Write clean code](#11---write-clean-code)

## 2 - Write short units of code
* Limit the length of code units to 15 lines of code
	* Do this by not writing units that are longer than 15 lines of code in the first place, or by splitting long units into multiple smaller units until each unit has at most 15 lines of code
	* This improves maintainability because small units are easy to understand, easy to test, and easy to reuse

### 2.1 - Motivation
* Short units are easy to test
* Short units are easy to analyze
* Short units are easy to reuse

### 2.2 - How to apply the guideline
* When writing a new unit
* When extending a unit with new functionality
* Using refactoring techniques to apply the guideline
	* Extract method
	* Replace method with method object

### 2.3 - Common objections to writing short units
* Having more units is bad for performance
* Code is harder to read when spread out
* Guideline encourages improper formatting
* This unit is impossible to split up
* There is no visible advantage in splitting units

## 3 - Write simple units of code
* Limit the number of branch points per unit to 4
	* Do this by splitting complex units into simpler ones and avoiding complex units altogether
	* This improves maintainability because keeping the number of branch points low makes units easier to modify and test

### 3.1 - Motivation
* Simple units are easier to modify
* Simple units are easier to test

### 3.2 - How to apply the guideline
* Dealing with conditional chains
	* Use a map data structure
	* Refactoring pattern: Replace conditional with polymorphism
* Dealing with nesting
	* Refactoring pattern: Replace nested conditional with guard clauses

### 3.3 - Common objections to writing simple units of code
* High complexity cannot be avoided
* Splitting up methods does not reduce complexity

## 4 - Write code once
* Do not copy code
	* Do this by writing reusable, generic code and/or calling existing methods instead
	* This improves maintainability because when code is copied, bugs need to be fixed at multiple places, which is inefficient and error-prone

### 4.1 - Motivation
* Duplicated code is harder to analyze
* Duplicated code is harder to modify

### 4.2 - How to apply the guideline
* Extract superclass refactoring technique

### 4.3 - Common objections to avoiding code duplication
* Copying from another codebase should be allowed
* Slight variations, and hence duplication, are unavoidable
* This code will never change
* Duplicates of entire files should be allowed as backups
* Unit tests are covering me
* Duplication in string literals are unavoidable and harmless

## 5 - Keep unit interfaces small
* Limit the number of parameters per unit to at most 4
	* Do this by extracting parameters into objects
	* This improves maintainability because keeping the number of parameters low makes units easier to understand and reuse

### 5.1 - Motivation
* Small interfaces are easier to understand and reuse
* Methods with small interfaces are easier to modify

### 5.2 - How to apply the guideline
* Data transfer objects or parameter objects
* Replace method with method object

### 5.3 - Common objections to keeping unit interfaces small
* Parameter objects with large interfaces
* Refactoring large interfaces does not improve my situation
* Frameworks or libraries prescribe interfaces with long parameter lists

## 6 - Separate concerns in modules
* Avoid large modules (classes) in order to achieve loose coupling between them
	* Do this by assigning responsibilities to separate modules and hiding implementation details behind interfaces
	* This improves maintainability because changes in a loosely coupled codebase are much easier to oversee and execute than changes in a tightly coupled codebase

### 6.1 - Motivation
* Small, loosely coupled modules allow developers to work on isolated parts of the codebase
* Small, loosely coupled modules ease navigation through the codebase
* Small, loosely coupled modules prevent no-go areas for new developers

### 6.2 - How to apply the guideline
* Split classes to separate concerns
* Hide specialized implementations behind interfaces
* Replace custom code with third-party libraries/frameworks

### 6.3 - Common objections to separating concerns
* Loose coupling conflicts with reuse
* Jave interfaces are not just for loose coupling
* High fan-in of utility classes is unavoidable
* Not all loose coupling solutions increase maintainability

## 7 - Couple architecture components loosely
* Achieve loose coupling between top-level components
	* Do this by minimizing the relative amount of code within modules that is exposed to (i.e., can receive calls from) modules in other components
	* This improves maintainability because independent components ease isolated maintenance

### 7.1 - Motivation
* Low component dependence allows for isolated maintenance
* Low component dependence separates maintenance responsibilities
* Low component dependence eases testing

### 7.2 - How to apply the guideline
* Limit the size of modules that are the component's interface
* Define component interfaces on a high level of abstraction. This limits the types of requests that cross component borders. That avoids requests that "know too much" about the implementation details
* Avoid throughput code, because it has the most serious effect on testing functionality: In other words, avoid interface modules that put through calls to other components. If throughput code exists, analyze the concerned modules in order to solve calls that are put through to other components
* Abstract Factory Design Pattern

### 7.3 - Common objections to loose component coupling
* Component dependence cannot be fixed because the components are entangled
* No time to fix
* Throughput is a requirement

## 8 - Keep architecture components balanced
* Balance the number and relative size of top-level components in your code
	* Do this by organizing source code in a way that the number of components is close to 9 (between 6 and 12) and that the components are of approximately equal size
	* This improves maintainability because balanced components ease locating code and allow for isolated maintenance

### 8.1 - Motivation
* A good component balance eases finding and analyzing code
* A good component balance better isolates maintenance effects
* A good component balance separates maintenance responsibilities

### 8.2 - How to apply the guideline
* The number of top level system components should ideally be 9, and generally between 6 and 12
* The components' volume in terms of source code should be roughy equal
* Decide on the right conceptual level for grouping functionality into components
* Clarify the system's domains and apply those consistently

### 8.3 - Common objections to balancing components
* Component imbalance works just fine
* Entanglement is impairing component balance

## 9 - Keep your code base small
* Keep your codebase as small as feasible
	* Do this by avoiding codebase growth and actively reducing system size
	* This improves maintainability because having a small product, project, and team is a success factor

### 9.1 - Motivation
* A project that sets out to build a large codebase is more likely to fail
* Large codebases are harder to maintain
* Large systems have higher defect density

### 9.2 - How to apply the guideline
* Functional measures
	* Fight scope creep
		* Avoid "nice-to-have" functionality that doesn't add much value to the business or user
	* Standardize functionality
* Technical measures
	* Do not copy and paste code
	* Refactor existing code
	* Use third-party libraries and frameworks
	* Split up a large system

### 9.3 - Common objections to keeping the codebase small
* Reducing the codebase size is impeded by productivity measures
* Reducing the codebase size is impeded by the programming language
* System complexity forces code copying
* Splitting the codebase is impossible because of platform architecture
* Splitting the codebase leads to duplication
* Splitting the codebase is impossible because of tight coupling

## 10 - Automate tests
* Automate tests for your codebase
	* Do this by writing automated tests using a test framework
	* This improves maintainability because automated testing makes development predictable and less risky

### 10.1 - Motivation
* Automated testing makes testing repeatable
* Automated testing makes development efficient
* Automated testing makes code predictable
* Tests document the code that is tested
* Writing tests make you write better code

### 10.2 - How to apply the guideline
* Types of testing
	* Unit test
	* Integration test
	* End-to-end test
	* Regression test
	* Acceptance test
* Getting started with jUnit tests
* General principles for writing good unit tests
	* Test both normal and special cases
	* Maintain tests just like nontest (production code)
	* Write tests that are isolated: their outcomes should reflect only the behaviour of the subject being tested
* Measure coverage to determine whether there are enough tests
	* at least 80%

### 10.3 - Common objections to automating tests
* We still need manual testing
* I am not allowed to write unit tests
* Why should we invest in unit tests when the current coverage is low?

## 11 - Write clean code
* Write clean code
	* Do this by not leaving code smells behind after development work
	* This improves maintainability because clean code is maintainable code

### 11.1 - Leave no trace
Boy Scout Rule - leave the campground cleaner than you found it.

### 11.2 - How to apply the guideline
1. Leave no unit-level code smells behind
	* [No long units](#2---write-short-units-of-code)
	* [No complex units](#3---write-simple-units-of-code)
	* [No units with large interfaces](#5---keep-unit-interfaces-small)
2. Leave no bad comments behind
3. Leave no code in comments behind
4. Leave no dead code behind
5. Leave no long identifier names behind
6. Leave no magic constants behind
7. Leave no badly handled exceptions behind
	* Always catch exceptions
	* Catch specific exceptions
	* Translate specific exceptions to general messages before showing them to end users

### 11.3 - Common objections to writing clean code
* Comments are our documentation
* Exception handling causes code additions
* Why only these coding guidelines?

