# clean-code-practice
Any fool can write code which computer can understand. Good programmers write code that humans can understand.- By Marntin Fowl

## What is clean code ?
Software code written in a systematic manner, so that another coder can easily interpret or modify it.

In programming ask yourself that, whatever I wrote can somebody understand it at first sight ? If not, try to improve it so that it can be maintainable.

Bad code
=========
        Pbag pBag = new Pbag();
        if(p.sts == 1 && pBag.sts(p)) { //process status is 1 (running) and process bag contains the process
            p.sts = 2;
            pBag.removeP(p);
        }
        
        if(user.getStatus().equals(1")) {
            deleteUser(user);
        }
Clean Code
==========
        if(process.isRunning() && processBag.containsProcess(process)) {
            process.setStatusStopped();
            processBag.removeProcess(process);
        }
        
        OR
        
        if(processIsRunning(process, processBag)) {
            killProcess(process, processBag)
        }
        
        if(user.isInactive()) {
            deleteUser(user);
        }

### Write Small Functions (Each function should carry single responsibility)
* Easy to understand
* Easy to debug
* Easy to reuse
* Easy to test (1. reduces too much mocking 2. private functions shouldn't be tested)
* Easy to keep bug free
* Avoid code repetition
* Beautified code
* Separate concepts into there levels of abstraction
* Easy to maintain
* Small functions can replace complex statements with an easy to read function name. Specially for predicates.
        if(predicate) {}

####Small is better - how small function ?
* 5-7 lines of code without logger should be enough. Separate the high cohesive lines into new functions. CTRL + ALT + M (Intellij)

####Small is better - how small class ?
* 10 - 50 -100 lines. towards 100 ? break class to make classes. 
* Avoid putting multiple statements in one line to reduce num of lines. This way complexity increases. Not a good practice.

## SRP (Single Responsibility Principle)
A class/function should carry one responsibility. In other words a class or function should have only one reason to change.
Write small functions (5-7 lines)

## MVC discussion (All skinny)
* Make all layers skinny. Don't keep one fat service, instead create multiple services.
* Models are just data structures. 
* Create dedicated services for repository and then call them from other services. Don't call repository from any random service.
* Entities can contain data as well as logic thus are the real oop objects.
* Don't cross levels of abstractions e.g., model, services, controllers, dates, files. 

## Focus on High level first.
* Write code using non-existent code! Compplete the execution flow with method definition only. Implementation should be the last step to finish the task (Not always).

Naming (methods, classes, variables)
* Variables should be noun - price, currentTrade
* Booleans are predicate -  isScheduled, isRunning
* Methods should start with a verb - getStrategyResult, createSomething, doSomething


## Naming Size (Scope Rule by Uncle Bob)
* Small scope - small variable name, big method name (scope of private methods is within the class only with less usage, so the name should be well descriptive to avoid confusion)
* Big scope - big variable name, small method name
* Naming should be done in such way so that other developer can understand the significance with no effort.

## Parameters
* How many params a method can have - the fewest possible. Max 3, Preferably zero.
* The more parameters' method has ,the more coupled it is.
* In situations where it has to be passed more arguments (cohesive), then try to extract them to an immutable model class.
        
        performTrading(instrument, numberOfUnits, stopLoss, tradeType)
        
  change to 
  
        @Builder
        @Getter
        public class BrokerTradeInput {
            private String instrument;
            private int numberOf Units;
            private BigDecimal stopLoss;
            private TradeType tradeType
        }
        
        performTrading( brokerTradeInput );
        
No boolean and null parameters - instead crate two functions, one for true/null and one for false/value.    

## Comments
* Often, comments are bad. Why ? Because we can't trust them. They might be lying. Can be true today, false tomorrow.
* One two things to trust in programming: 1. Code 2. Tests 
* Often when the code changes, comments don't.

* It's OK to write comment when you absolutely can't express yourself with code. E.g., while writing a complex regex.
* Comments also should be written in case of any critical consequences.
* Comments should be written details way when writing public library.

* Useless javadocs are useless.

### Bad comments
    /**
    * I hope we can improve the function name
    */
    private Result getResultWIthHtml(Result result) {
    }
    
    //first name
    String firstName;
    
    //Creating a new result object
    Result result = new Result();
    

### Should we use exception ?
* Use exceptions instead of error codes. 
* Use your own exceptions not the java ones.Make your exception class as described, so that exception messages are not required unless, very essential.
* Use unchecked/runtime exceptions instead of checked ones.
* Make sure your try & catch are small. Extract them into functions if they are more than 2/3 lines.


### OOPs Objects vs Data Structure Objects

### Composition over Inheritance (Communication between Objects)
* One object can communicate with another object in two ways.
* One object can have the other object as a property - Composition (A has B or HAS-A relation)
* One object can inherit the other object - Inheritance (A is B or IS-A relation)
* In Composition over Inheritance is a programming pattern where composition is preffered than inheritance, because composition leads to flexibility & inheritance rigidity (forces to inherit all the properties. Abstract classes to the rescue).

### Symptoms of bad code
1. Rigidity - Code is hard to change. Any change request by business takes a lot of time.
2. Fragility - When you touch code to change it just inevitably breaks elsewhere.
3. Immobility - Code suffers re-usability. Lack of small functions.
4. Viscosity - environmental issues due to which project is not flexible to handle. Testing/deployment becomes very slow.





