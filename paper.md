# Topic : DESIGN PATTERNS

## Context : Discuss any 5 design patterns used in JavaScript with code samples.

## INTRODUCTION :
Design patterns are solutions to common software design problems. It is a blueprint or a template that can be modified to solve a particular problem.

In this paper, I'm going to discuss five design patterns :
1) Factory Design Pattern

2) Strategy Design Pattern

3) Visitor Design Pattern

4) Iterator Design Pattern

5) Mediator Design Pattern

### FACTORY DESIGN PATTERN :

Factory design pattern comes under the creational design pattern. It provides the best way to create an object.
In the Factory Design pattern, we create the object without exposing the creational logic to the user. In a real-world sense, a Factory is a building where things are manufactured and in a programming sense, a Factory is an object that creates or manufactures different objects. Factories allow handling all object creation in a centralized location.

##### FACTORY.JS
```js
function Developer(name){
    this.name = name
    this.type = "Developer"
}
function Tester(name){
    this.name =  name
    this.type = "Tester"
}
function Tech_Support(name){
    this.name = name
    this.type = "Tech Support"
}
function EmployeeFactory(){
    this.create = (name , type) => {
        if( type == 1 )
            return new Developer(name)
        else if( type == 2 )
            return new Tester(name)
        else if( type == 3 )
            return new Tech_Support(name)
    }
}
function print(){
    console.log(this.name + " " + this.type)
}
const employeeFactory = new EmployeeFactory()
const employees = []

employees.push( employeeFactory.create("Sam",1) )
employees.push( employeeFactory.create("War",2) )
employees.push( employeeFactory.create("Sun",3) )

employees.forEach( emp => {
    print.call(emp)
} )
```

In above code, EmployeeFactory creates objects for classes Developer, Tester, Tech_Support.


### STRATEGY DESIGN PATTERN :
Strategy pattern comes under behavioral pattern. It let you define a group of algorithms, put each of them into a separate class, and make them interchangeable.

##### STRATEGY.JS

```js
function Company1(pk){
    this.compute = () => {
        return 1
    }
}
function Company2(pk){
    this.compute = () => {
        return 2
    }
}
function Company3(pk){
    this.compute = () => {
        return 3
    }
}
function Company4(pk){
    this.compute = () => {
        return 4
    }
}

function Task(){
    this.company = ''
    this.setStrategy = company => {
        this.company = company
    }
    this.compute = pk => {
        return this.company.compute(pk)
    }
}

const c1 = new Company1()
const c2 = new Company2()
const c3 = new Company3()
const c4 = new Company4()
const t = new Task()
const pk = 1

t.setStrategy(c1)
console.log("Company 1 :" + t.compute(pk) )

t.setStrategy(c2)
console.log("Company 2 :" + t.compute(pk) )

t.setStrategy(c3)
console.log("Company 3 :" + t.compute(pk) )

t.setStrategy(c4)
console.log("Company 4 :" + t.compute(pk) )
```
In the above code, we can switch from one object to another easily by using a strategy pattern.
- compute() : It's a common function used in all classes.
- setStrategy() : By using this function, we can switch around the objects.

### VISITOR DESIGN PATTERN :
This pattern comes under the behavioral pattern. The visitor pattern allows you to add or provide new operations and methods to an object without actually changing that object itself the new functionality and logic are kept in a separate object known as the visitor object.
##### VISITOR.JS

```js
function Employee(name, salary)
{
  this.name = name
  this.salary = salary
}

Employee.prototype = {
  getSalary: function()
  {
    return this.salary
  },
  setSalary: function(sal)
  {
    this.salary = sal
  },
  accept: function(visitorFunction)
  {
    visitorFunction(this)
  }
}

const sam = new Employee("Sam", 1000)
console.log(sam.getSalary())

function ExtraSalary(emp)
{
  emp.setSalary(emp.getSalary() * 2)
}

sam.accept(ExtraSalary)
console.log(sam.getSalary())
```

### ITERATOR DESIGN PATTERN :
Iterator pattern comes under behavioral pattern.
Iterator design pattern allows to loop over a collection of objects. Iterator pattern allows defining your logic to traverse a collection of objects.

##### ITERATOR.JS

```js
const collection = [10, "String", false, 24.3, null]

function Iterator(collection){
    this.collection = collection
    this.index = 0;
}

Iterator.prototype = {
    hasNext: function() {
        return this.index < this.collection.length
    },
    next: function() {
        return this.collection[this.index++]
    }
}

const it =  new Iterator(collection)
while( it.hasNext() )
    console.log(it.next())
```
In the above code, I had created an iterator that traverses over an array.
It has two methods hasNext() and next().

- hasNext() : returns true if the collection has more elements.
- next() : returns next element in the collection.

### MEDIATOR DESIGN PATTERN :
The mediator pattern comes under the behavioral pattern. This pattern provides a mediator class that handles all communications between different classes. Overall it provides communication between different objects. 
##### MEDIATOR.JS

```js
function Member(name){
    this.name = name
    this.chatroom = null
}

Member.prototype = {
    send: function(message, toMember){
        this.chatroom.send(message, this, toMember)
    },
    receive: function(message, fromMember){
        console.log(`${fromMember.name} to ${this.name}: ${message}`)
    }
}
function Chatroom(){
    this.members = {}
}

Chatroom.prototype = {
    addMember: function(member){
        this.members[member.name] = member
        member.chatroom = this
    },
    send: function(message, fromMember, toMember){
        toMember.receive(message, fromMember)
    }
}

const chat = new Chatroom()

const sam = new Member("Sam")
const sun = new Member("Sun")
const tin = new Member("Tin")

chat.addMember(sam)
chat.addMember(sun)
chat.addMember(tin)

sam.send("Hey Sun",sun)
sun.send("Hello Sam",sam)
tin.send("where are you working ? ",sam)
```

## REFERENCES : 
[Factory Pattern](https://www.youtube.com/watch?v=kuirGzhGhyw&list=PLREW9ZuU80uTfmxo61-acnUYk3P_4plIF&index=4!)


[Strategy Pattern](https://www.youtube.com/watch?v=SicL4fYCz8w&list=PLREW9ZuU80uTfmxo61-acnUYk3P_4plIF&index=6!)


[Visitor Pattern](https://www.youtube.com/watch?v=x-Gx0Ym1Di0&list=PLREW9ZuU80uTfmxo61-acnUYk3P_4plIF&index=11!)


[Iterator Pattern](https://www.youtube.com/watch?v=c85EStPZR8M&list=PLREW9ZuU80uTfmxo61-acnUYk3P_4plIF&index=7!)


[Mediator Pattern](https://www.youtube.com/watch?v=ZuhgOu-DGA4&list=PLREW9ZuU80uTfmxo61-acnUYk3P_4plIF&index=9!)

### Name : Sai Sampath Mahajan
### Email : sai.mahajan.17@mountblue.tech