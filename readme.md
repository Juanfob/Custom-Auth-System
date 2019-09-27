<p align="center"><img src="https://res.cloudinary.com/dtfbvvkyp/image/upload/v1566331377/laravel-logolockup-cmyk-red.svg" width="400"></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/d/total.svg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/v/stable.svg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</p>

# Custom Authentication System

Hemos modificado los archivos:
* LoginController.php
* RegisterController.php
* RedirectifAuthenticated.php
* welcome.blade.php

Con esto redirigimos al usuario dependiendo de la condición definida en estos archivos.

###Path Customization
When a user is successfully authenticated, they will be redirected to the **/home** URI.
You can customize the post-authentication redirect location by defining a
 redirectTo property on the **LoginController, RegisterController, ResetPasswordController, and VerificationController**:

>**protected $redirectTo = '/';**>
>
Next, you should modify the **RedirectIfAuthenticated** middleware's handle method to use your new URI when redirecting the user.

If the redirect path needs custom generation logic you may define a redirectTo method instead of a redirectTo property:
      
      protected function redirectTo()
        {
           return ‘/path’;
        }
 
The redirectTo method will take precedence over the redirectTo property.

### Username Customization
By default, Laravel uses the **email** field for authentication. 
If you would like to customize this, you may define a username method on your **LoginController**:

    public function username()
    {
       return ‘username’;
    }

###  Guard Customization
You may also customize the “guard” that is used to authenticate and register users. To get started, define a guard method on your LoginController, RegisterController, and ResetPasswordController. The method should return a guard instance:

    use Illuminate\Support\Facades\Auth;
    protected function guard()
    {
       return Auth::guard(‘guard-name’);
    }
