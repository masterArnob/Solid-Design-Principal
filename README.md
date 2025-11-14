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

2. Open Closed Principal (OCP):
Open for extension but closed for modifications means add new features without changing existing code

before
```php
class Auth
{
    public function login($login_type){
        if($login_type == 'email'){
            // login code
        }else if($login_type == 'google'){
            // login code 
        }else if($login_type == 'fb'){
            // login code
        }
    }
}
```
problem: If I have to add GitHub login then I have to add more if conditions. I have to modify the existing code that violates the OCP Principal.

After:
```php
interface LoginInterface
{
    public function login();
}

class EmailLogin implements LoginInterface
{
    public function login(){
        // email login code
    }
}

class GoogleLogin implements LoginInterface
{
    public function login(){
        // google logn code
    }
}


class GitHub implements LoginInterface
{
    public function login(){
        // github logn code
    }
}


class Auth
{
    public function authenticate(LoginInterface $method){
        return $LoginInterface->login();
    }
}


class controller
{
    $auth = new Auth();
    echo $auth->authenticate(new EmailLogin());
    echo $auth->authenticate(new GoogleLogin());
    echo $auth->authenticate(new FacebookLogin());
}
```