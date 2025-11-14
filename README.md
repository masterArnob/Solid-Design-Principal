Solid Principal

1. Single Respnsibility Prncipal (SRP):
The class should have only 1 responsibility and focused on doing onlu that responsibility.

Before:
```php
class User
{
    public function UserLogin(){
        // login code
    }
    public function UserRegister(){
        // register code
    }
}
```


After
```php
class UserLogin
{
    public function login(){
        // login code
    }
}

class UserRegister
{
    public function register(){
        // register code
    }
}
```