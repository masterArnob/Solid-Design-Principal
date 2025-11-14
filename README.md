# SOLID Design Principles

---

## 1. Single Respnsibility Prncipal (SRP):
**The class should have only 1 responsibility and focused on doing onlu that responsibility.**

**Before:**
```php
class AnimalSound
{
    public function dog(){
        return 'dog sound';
    }

    public function cat(){
        return 'cat sound';
    }
}
```

**problem: Multiple responsibilities**

**After**
```php
class dog()
{
    public function dogSound()
    {
        return 'dog sound';
    }
}

class cat
{
    public function catSound()
    {
        return 'cat sound';
    }
}
```
---
## 2. Open Closed Principal (OCP):
**Open for extension but closed for modifications means add new features without changing existing code**

**Before**
```php
class AnimalSound
{
    public function getSound($animal){
        if($animal == 'dog'){
            return 'dog sound';
        }else if($animal == 'cat'){
            return 'cat sound';
        }
    }
}
```
**problem: If I have to add tiger then I have to add more if conditions. I have to modify the existing code that violates the OCP Principal.**

**After:**
```php
interface AnimalInterface
{
    public function sound();
}

class Dog implements AnimalInterface
{
    public function sound(){
        return 'dog sound';
    }
}

class Cat implements AnimalInterface
{
    public function sound(){
        return 'cat sound';
    }
}

class Tiger implements AnimalInterface
{
    public function sound(){
        return 'Tiger sound';
    }
}


class AnimalSound
{
    public function play(AnimalInterface $animal){
        return $animal->sound();
    }
}
```
---
## 3. Liskov Subsitute Principal (LSP):
**Subclass can replace parent class without breaking parent class behaviour.**

**Before**
```php
class Animal
{
    public function fly(){
        return 'flying';
    }
}

class Dog extends Animal {}

class Cat extends Animal {}
```

**Problem: Sub class breaking the parent class behaviour as dog and cat can not fly**

**After:**
```php
class Animal
{
    public function eat(){
        return 'eating';
    }
}


class Dog extends Animal
{
    public function dogSound(){
        return 'dog sound';
    }
}

class Cat extends Animal
{
    public function catSound(){
        return 'cat sound';
    }
}
```

**here sub class is not breaking the parent clas behaviour because dog and cat can make sound also they can eat.**
---
## 4. Interface Segregation Principal (ISP):
**Class should not be forced to use interface that they do not use**

**Before**
```php
interface AnimalInterface
{
    public function run();
    public function fly();
}

class Dog implements AnimalInterface
{
    public function run(){
        // code
    }

    public function fly(){
        // code
    }
}
```
**Problem: Dog can not fly. here dog is forced to implement fly**

**After:**
```php
interface runInterface
{
    public function run();
}

interface flyInterface
{
    public function fly();
}

class Dog implements runInterface
{
    public function run(){
        return 'dog is running';
    }
}

class Bird implements flyInterface
{
    public function run(){
        return 'bird is flying';
    }
}
```
---
## 5. Dependency Inversion Principal (DIP):
**High level module should not be depend on low level module.**

**Before**
```php
class Dog
{
    public function sound(){
        return 'dog sound';
    }
}

class Trainer
{
    public function train(){
        $dog = new Dog();
        return $dog->sound();
    }
}
```

**Problem: High lvl module - Trainer
         Low lvl module - Dog
         Here dog is hard coded towmmorow if i need to train cat then i have to hard coded again that means high lvl module is depend on low lvl module. it violates**

**After:**
```php
interface AnimalInterface
{
    public function sound();
}

class Dog implements AnimalInterface
{
    public function sound(){
        return 'dog sound';
    }
}

class Cat implements AnimalInterface
{
    public function sound(){
        return 'cat sound';
    }
}

class Trainer
{
    public function train(AnimalInterface $animal){
        return $animal->sound();
    }
}
```

**Now trainer can train any animal without hard coded changes**