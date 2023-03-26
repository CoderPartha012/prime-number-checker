# prime-number-checker
Prime Number Checker using parameterized test in junit

An example of a Prime Number Checker using parameterized tests in JUnit 5👉👉
 
 👉 Step-1: Create the java program to check  for prime or not.
 
  Code: 
 
 public class BusinessLogic {
 
  public Boolean validate(final Integer primeNumber) {
  
    for (int i = 2; i < (primeNumber / 2); i++) {
    
      if (primeNumber % i == 0) {
      
        return false;
        
      }
      
    }
    
    return true;
    
  }
  
}

 Explanation : This is a Java code for a class named BusinessLogic that has a method named validate. The validate method takes an integer parameter named primeNumber and returns a boolean value. The purpose of the validate method is to check whether the input number is a prime number or not.
The algorithm used in this method is a basic one, where the input number is divided by all numbers between 2 and half of the input number. If any of these numbers divide the input number without leaving any remainder, then the input number is not a prime number, and the method returns false. Otherwise, if none of these numbers divide the input number without leaving any remainder, then the input number is a prime number, and the method returns true.
However, there is a small issue with this algorithm. The loop in the code should go up to (primeNumber / 2) + 1, instead of just (primeNumber / 2). This is because if primeNumber is an even number, say 4, then the loop condition will be i < 2, which is not correct. So, changing the loop condition to i <= (primeNumber / 2) will solve this issue.

👉 Step-2:  Create Runner class.
 
  Code: 
 
 import org.junit.runner.JUnitCore;
 
import org.junit.runner.Result;

import org.junit.runner.notification.Failure;

public class Main {

   public static void main(String[] args) {
   
      Result result = JUnitCore.runClasses(TestJunit.class);
      
      for (Failure failure : result.getFailures()) {
      
         System.out.println(failure.toString());
         
      }
      
      System.out.println(result.wasSuccessful());
      
   }
   
}

 Explanation : This Java program runs JUnit tests using the JUnitCore class.
The main() method uses the JUnitCore.runClasses() method to run the TestJunit class, which contains the JUnit tests to be executed.
The Result object returned by the runClasses() method contains information about the test results, including any failures or errors that occurred during the tests.
The for loop in the main() method prints out any failures that occurred during the tests, using the toString() method of the Failure class.
Finally, the program prints out whether all the tests were successful or not, using the wasSuccessful() method of the Result class.
This program can be used to automate the testing process for Java code, making it easier to ensure that the code is working correctly and that any changes or updates to the code do not introduce new bugs or errors.

👉 Step-3:  Create JUnit test class using parameterized tests.
 
  Code: 
 
 import static org.junit.Assert.assertEquals;
 
import java.util.Arrays;

import java.util.Collection;


import org.junit.Before;

import org.junit.Test;

import org.junit.runner.RunWith;

import org.junit.runners.Parameterized;

@RunWith(Parameterized.class)

public class TestJunit {

     private Integer inputNumber;
     private Boolean expectedResult;
     private BusinessLogic logic;

     @Before
     public void initialize() {
        logic = new BusinessLogic();
     }

     public TestJunit(Integer inputNumber, 
        Boolean expectedResult) {
       System.out.println("TestJunit-> inputNumber:"+inputNumber+" expectedResult:"+expectedResult);
        this.inputNumber = inputNumber;
        this.expectedResult = expectedResult;
     }

     @Parameterized.Parameters
     public static Collection<Object[]> primeNumbers() {
       System.out.println("primeNumbers() is called");
        return Arrays.asList(new Object[][] {
           { 2, true },
           { 6, false },
           { 19, true },
           { 22, false },
           { 23, true }
        });
     }

     @Test
     public void testPrimeNumberChecker() {
        System.out.println("Parameterized Number is : " + inputNumber);
        assertEquals(expectedResult, logic.validate(inputNumber));
     }

}

Explanation : This is a JUnit test class that uses parameterized testing to test the functionality of the BusinessLogic class. Parameterized testing allows for running the same test case multiple times with different input values. The first line imports the assertEquals method from the org.junit.Assert class, which is used to compare the actual and expected values of the test. The Arrays and Collection classes are also imported to support parameterized testing. The @RunWith annotation is used to specify the test runner, which in this case is Parameterized.class. Next, three instance variables are declared - inputNumber, expectedResult, and logic. inputNumber and expectedResult are the input values and expected output values of the test, respectively. The logic variable is an instance of the BusinessLogic class, which will be used to execute the test. The @Before annotation is used to initialize the logic object before each test case. The TestJunit constructor is used to assign the input and expected output values to the respective instance variables. The @Parameterized.Parameters annotation is used to specify the input values for the test cases. The primeNumbers() method returns a collection of arrays containing the input and expected output values for each test case. Finally, the @Test annotation is used to specify the test method, testPrimeNumberChecker(), which uses the assertEquals() method to compare the expected and actual output values of the test. The inputNumber instance variable is used as the input parameter for the validate() method of the BusinessLogic class, and the result is compared to the expectedResult variable.
