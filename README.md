# AOP: Pointcut Declarations

**Problem**
+ How can we reuse a point expression?
  + Want to apply to multiple advices

**Possible Solution**
+ Could do the old copy/paste method

**Ideal Solution**
+ Create a pointcut declaration once
+ Apply it to multiple advices

**Development Process**
1. Create pointcut declaration
2. Apply pointcut declaration to advice(s)

_Step 1:Create pointcut Declaration_
+ Create a pointcut declaration once

```JAVA
@Pointcut("execution(* com.tilmeez.aopdemo.dao.*.*(..))")
private void dorDaoPackage() {}
```
+ `dorDaoPackage` Name of pointcut declaration

_Step 2:Apply to Multiple Advices_
```JAVA
@Aspect
@Component
public class MyDemoLoggingAspect {
  
  @Pointcut("execution(* com.tilmeez.aopdemo.*.*(..))")
  private void forDaoPackage() {}
  
  @Before("forDaoPackage()")
  public void beforeAddAccountAdvice() {
    ...
  }
  
  @Before("forDaoPackage()")
  public void beforeAddAccountAdvice() {
    ...
  }
      
}
```
+ Solved problem of reusing pointcut expressions

**Benefits of Pointcut Declarations**

+ Easily reuse pointcut expressions
+ Update pointcut in one location
+ Can also share and combine pointcut expressions

