# spring-demo-aop
# AOP: Aspect-Oriented Programming Overview



### AOP - The Business Problem

**Application Architecture**

<img src="https://user-images.githubusercontent.com/80107049/189166402-4bdb4030-0c1c-4904-a483-35de3e079223.png" width = 500 />

**Code for Data Access Object (DAO)**

```JAVA
public void addAccount(Account theAccount, String userId) {
  
  Session currentSession = sessionFactory.getCurrentSession();
  
  currentSession.save(theAccount);
}
```

+ Basic Hibernate code to save an entity


**New Requirement - Logging**
+ Need to add logging to our DAO methods
    + Add some logging statements before the start of method.

**DAO - Add Logging Code**

```JAVA
public void addAccount(Account theAccount, String userId) {
  
  // add code for logging
  
  Session currentSession = sessionFactory.getCurrentSession();
  
  currentSession.save(theAccount);
  
}
```

**New Requirement - Security**
+ Need to add security code to our DAO
    + Make sure user is authorized before running DAO method

**Add Security Code**

```JAVA
public void addAccount(Account theAccount, String userId) {
  
  // add code for logging
  
  // add code for security check
  
  Session currentSession = sessionFactory.getCurrentSession();
  
  currentSession.save(theAccount);
  
}
```

**New Requirement**
+ Let's add it to all of our layers ...

<img src="https://user-images.githubusercontent.com/80107049/189166490-5efd6fa2-90c0-4228-a788-a3e09f1e4abe.png" width=500 />


+ And to for all system , have to do in all the classes


**Two Main Problem**
+ **Code Tangling**
    + For a given method: addAccount(...)
    + We have logging and security code tangled in

+ **Code Scattering**
    + If we need to change logging or security code
    + We have to update ALL classes

**Other possible solutions?**
+ **Inheritance?**
    + Every class would need to inherit from a base class
    + Can all classes extends from your case class? ... plus no multiple inheritance

+ **Delegation?**
    + Classes would delegate logging, security calls
    + Still would need to update classes if we wanted to
        + add/remove logging or security
        + add new feature like auditing, API management, instrumentation


**Aspect-Oriented Programming**
+ Programming technique based on concept of an Aspect
+ Aspect encapsulates cross-cutting logic

> Cross-cutting Concerns
>
+ `Concern` means logic / functionality

**Cross-Cutting Concerns**

<img src="https://user-images.githubusercontent.com/80107049/189166609-21f46f1d-cb95-4ead-b025-2cfe999d1622.png" width=500 />

**Aspect**
+ Aspect can be reused at multiple locations
+ Same aspect/class ... applied based on configuration

<img src="https://user-images.githubusercontent.com/80107049/189166726-99d08b04-871d-4f01-b9f1-e49481b477f4.png" width=500 />

***

### AOP Solution and AOP Use Cases

**AOP Solution**
+ Apply the Proxy design pattern

<img src="https://user-images.githubusercontent.com/80107049/189166810-5087f809-7d9b-4a3b-a134-3e20e06bd21f.png" width= 500 />


**Benefits of AOP**
+ **Code for Aspect is defined in a single class**
    + Much better than being scattered everywhere
    + Promotes code reuse and easier to change

+ **Business code in your application is cleaner**
    + Only applies to business functionality: addAccount
    + Reduces code complexity

+ **Configurable**
    + Based on configuration, apply Aspects selectively to different parts of app
    + No need to make changes to main application code ... very important!!


**Additional AOP Use Cases**

+ **Most common**
    + logging, security, transactions


+ **Audit logging**
    + who,what,when,where

+ **Exception handling**
    + log exception and notify DevOps team via SMS/email

+ **API Management**
    + how many times has a method been called user
    + analytics: what are peak times? what is average load? who is top user?

**AOP: Advantages and Disadvantages**

| **Advantages**                             |
| ------------------------------------------ |
| Reusable modules                           |
| Resolve code tangling                      |
| Resolve code scatter                       |
| Applied selectively based on configuration |


| **Disadvantages**                                              |
| -------------------------------------------------------------- |
| Too many aspects and app flow is hard to follow                |
| Minor performance cost for aspect execution (run-time weaving) |


### Aspect-Oriented Programming (AOP) <br> Spring AOP Support

**AOP Terminology**

+ **Aspect:** module of code for a cross-cutting concern (logging, security, ...)
+ **Advice:** What action is taken and when it should be applied
+ **Join Point:** When to apply code during program execution
+ **Pointcut:** A predicate expression for where advice should be applied

**Advice Types**
+ **Before advice:** run before the method
+ **After finally advice:** run after the method (finally)
+ **After returning advice:** run after the method (success execution)
+ **After throwing advice:** run after method (id exception throw)
+ **Around advice:** run before and after method

**Weaving**
+ Connecting aspects to target objects to create an advised object
+ Different types of waving
    + Compile-time, load-time or run-time

+ Regarding performance: run-time weaving is the slowest

**AOP Frameworks**
+ Two leading AOP frameworks Java
    + Spring AOP
    + AspectJ

**Spring AOP support**
+ Spring provides AOP support
+ Key component of Spring
+ Security, transactions, caching etc
+ Use run-time weaving of aspects
    + Proxy pattern

**AspectJ**
+ Original AOP framework, released in 2001
    + www.eclipse.org/aspectj

+ Provides complete support for AOP
+ Rich support for
    + join points: method-level, constructor, field
    + code weaving: compile-time,post compile-time and load-time

**Spring AOP Comparison**

| **Advantages**                                       |
| ---------------------------------------------------- |
| Simpler to user than AspectJ                         |
| Uses Proxy pattern                                   |
| Can migrate to AspectJ when using @Aspect annotation |


| **Disadvantages**                                              |
| -------------------------------------------------------------- |
| Only support method-level join points                          |
| Can only apply aspects to beans created by Spring app context  |
| Minor Performance cost for aspect execution (run-time weaving) |


**AspectJ Comparison**

| **Advantages**                                       |
| ---------------------------------------------------- |
| Support all join points                              |
| Works with any POJO, not just beans from app context |
| Faster performance compared to Spring AOP            |
| Complete AOP support                                 |


| **Disadvantages**                                    |
| ---------------------------------------------------- |
| Compile-time weaving required extra compilation step |
| AspectJ pointcut syntax can become complex           |

**Compating Spring AOP and AspectJ**
+ Spring AOP supports
    + Method-level join points
    + Run-time code weaving(slower than AspectJ)

+ AspectJ support
    + join points: method-level, constructor, field
    + weaving: compile-time, post compile-time and load-time

+ Spring AOP is a light implementation of AOP
+ Solves common problems in enterprise applications
+ Start with Spring AOP ... easy to get started with
+ If we have complex requirements then move to AspectJ

**Additional Resources**
+ Spring Reference Manual: www.spring.io
+ **AspecJ in Action**
    + by Raminvas Laddad

+ **Aspect-Oriented Development with Use Cases**
    + by lavar Jacobson and Pan-Wei Ng

**Our Spring AOP Roadmap**
+ Create **Aspects**
+ Develop **Advices**
    + *Before, After returning, After throwing, After finally, Around*
+ Create **Pointcut** expressions
+ Apply it to our CRM project (Spring MVC + Hibernate)


***

**@Before Advice - Interaction**

<img src="https://user-images.githubusercontent.com/80107049/189166999-3d5f8ae1-a542-48a7-92a7-132a3c736f82.png" width=500 />


**Advice Interaction**

<img src="https://user-images.githubusercontent.com/80107049/189167094-92361b20-a5d1-41bf-90e8-7d58a30a96a5.png" width=400 />


**@Before Advice - Use Cases**

+ **Most common**
    + logging, security, transactions

+ **Audit logging**
    + who, what, when, where

+ **API Management**
    + how many times has a method been called user
    + analytics: what are peak time? what is average load? who is top user?

**Development Process - @Before**

1. Create target object: AccountDAO
2. Create Spring Java Config class
3. Create main app
4. Create an Aspect with @Before advice


_Step 1:Create Target Object:AccountDAO_

```JAVA
@Component
public class AccountDAO {
  
  public void addAccount() {
    
    System.out.println("DOING MY DB WORK: ADDING AN ACCOUNT");
  }
}
```
+ `@Component` is Spring component

_Step 2:Create Spring Java Config class_

```JAVA
@Configuration
@EnableAspectJAutoProxy
@ComponentScan("com.tilmeez.aopdemo")
public class DemoConfig {
  
}
```

+ `@Cofiguration` Spring Pure Java Configuration
+ `@EnableAspectJAutoProxy`Spring AOP Proxy Support
+ `@ComponentScan("com.tilmeez.aopdemo")` Component scan for components and aspects, Recurse package

_Step 3: Create main app_

```JAVA
public class MainDemoAoo {
  
  public static void main(String[] args) {
    
    // read spring config Java Class
    AnnotaionConfApplicationContext context =
      new AnnotationConfApplicationConext(DemoConfig.class);
    
    // get the bean from spring container
    AccountDAO theDAO = cotext.getBean("accountDAO", AccountDAO.class);
    
    // call the business method
    theDAO.addAccount();
    
    // clase the context
    context.closs();
  }
}
```

_Step 4:Create an Aspect with @Before advice_


<img src="https://user-images.githubusercontent.com/80107049/189167187-49fc7086-6ee0-460a-9b47-a9cb9b1fff47.png" width=500 />


+ Pointcut expression: Run this code BEFORE - target object method: "public void addAccount()"


**Best Practices: Aspect and Advices**

+ Keep the code small
+ Keep the code fast
+ Do not perform any expresive / slow operations
+ Get in and out as QUICKLY as possible



***

**AOP Terminology**
+ **Pointcut:** A predicate expression for where advice should be applied

**Pointcut Expression Language**
+ Spring AOP uses AspectJ's pointcut expression language
+ We will start with execution pointcuts
    + Applies to execution of methods

**Match on Method Name**

```JAVA 
execution(modifiers-pattern? return-type-pattern declaring-type-pattern?
          method-name-pattern(param-pattern) throws-pattern?)
```

+ `modifiers-pattern?` Modifiers:(Spring AOP only support public)
+ `return-type-pattern` Return type: void, boolean, String, `List<Customer>`, ...
+ `declaring-type-pattern?` Declaring type: the class name
+ `method-name-pattern(param-pattern)` Method name to match `param-pattern` Parameter types to match
+ `throws-pattern?` Exception types to match

<br>

+ The pattern is optional if it has "?"


**Pointcut Expresion Examples**

_Match on method names in class_
+ Match only **addAccount()** method in **AccountDAO** class

<img src="https://user-images.githubusercontent.com/80107049/189168249-3e6c044e-8d21-4331-9278-fce018a748e0.png" width=800/>

_Match on methods names_
+ Match any **addAccount()** method in **any** class

<img src="https://user-images.githubusercontent.com/80107049/189168176-bd67be15-5812-4045-bc57-13e0485e4988.png" width=800/>

_Match on method names (using wildcards)_
+ Match methods **staring** with **add** in any class

<img src="https://user-images.githubusercontent.com/80107049/189168093-cbc3a3c4-4883-493a-9dbf-f913107d101d.png" width=800/>

+ Match methods starting with **processCreditCard** in any class

```JAVA
@Before("execution(public VerificationResult processCreaditCard*())")
```
+ Here return type is VerificationResult

+ Use wildcards on return type

```JAVA
@Before("execution(public * processCreditCard*())")
```

+ Modifier is optional ... so don't have to list it

```JAVA
@Before("execution(* processCreditCard())")
```


***


**Parameter Pattern Wildcards**
+ For param-patterm
  + **()** - matches a method with no arguments
  + **(\*)** - matches a method with one argument of any type
  + **(..)** - matches a method with 0 or more arguments of any type


**Pointcut Expression Examples**

_Match on method ~~parameters~~_

+ Match **addAcount** methods with **no arguments**

<img src="https://user-images.githubusercontent.com/80107049/189195392-68682e5a-1d12-4656-b8d3-b42bc1dab7a9.png" width=800/>


_Match on method ~~parameters~~_
+ Match **addAcount** methods that have **Account** param

<img src="https://user-images.githubusercontent.com/80107049/189186988-b98d049c-7907-4d0f-92c5-41fd7d178557.png" width=800 />

_Match on method ~~parameters~~ (using wildcards)_
+ Match **addAccount** methods with **any number of arguments**

<img src="https://user-images.githubusercontent.com/80107049/189186856-d4f8ba17-e244-416c-8f18-219c4be019f1.png" width=800 />



_Match on methods in a ~~package~~_

+ Match any method in our DAO package:**com.tilmeez.aopdemo.dao**

<img src="https://user-images.githubusercontent.com/80107049/189186420-4735bc37-78ee-497f-bde1-383a174b3a3d.png" width=800 />

