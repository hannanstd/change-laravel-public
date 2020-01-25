# Change laravel public folder:

1- rename `public` folder to `public_html`.  
2- create new folder next-to `public_html` and name it `laravel-core`.  
3- move all files and folders except `.public_html, .idea, .git, .gitattributes, .gitignore` into `laravel-core` folder.  
4- edit `index.php` in `public_html` folder and change `__DIR__.'/../` to `__DIR__.'/../laravel-core/`. (2 case)  
5- edit `server.php` in `laravel-core` folder and change `/public` to `/../public_html`. (2 case)  
6- edit `AppServiceProviver.php` and add below code in `register` method:  
```php
$this->app->bind('path.public', function() {
  return realpath(base_path().'/../public_html');
});
```

7- edit `webpack.mix.js` and change `mix.` to `mix.setPublicPath('../public_html/').` and change all `public/` to `../public_html/` like below:  
```javascript
mix.setPublicPath('../public_html/')
    .sass("resources/scss/app.scss", "../public_html/css/main.css")
    ....
```
8- edit `.gitignore` and change all `public/` to `public_html/` and add `/laravel-core/` before others.  
9- run `git rm -rf --cached .` in terminal to update `.gitignore`.  
```
/.idea
/.git
/.gitattributes
/.gitignore
/public_html
  /index.php
/laravel-core
  /server.php
  /webpack.mix.js
  /app
    /Providers
      /AppServiceProviver.php
```
