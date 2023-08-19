## How to create your project?

To create your Laravel project you have to run the command:

`docker-compose run --rm composer create-project laravel/laravel .`

This will create a new Laravel project inside the src folder.

You can also copy your existing project inside the `src` folder.

## How to run the project?

To start the project run:

`docker-compose up -d server`

After that, you can visit [http://localhost:8000/](http://localhost:8000/) site

## Small differences

Thanks to "utility containers" there are some command replacements.
Make sure your server is running!

Replacements:
- `php artisan <command>` : `docker-compose run --rm artisan <command>`
- `npm <command>` : `docker-compose run --rm npm <command>` 
