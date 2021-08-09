# INTRODUCTION

## FACTORY.JS

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

## STRATEGY.JS

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

## VISITOR.JS

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
/////////////////////////////////////////////

const sam = new Employee("Sam", 1000)
console.log(sam.getSalary())

function ExtraSalary(emp)
{
  emp.setSalary(emp.getSalary() * 2)
}

sam.accept(ExtraSalary)
console.log(sam.getSalary())
```

## ITERATOR.JS

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

## MEDIATOR.JS

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
