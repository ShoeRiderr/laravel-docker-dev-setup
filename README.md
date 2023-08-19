## How to create your project?

To create your Laravel project you have to run the command:

`docker-compose run --rm composer create-project laravel/laravel .`

This will create a new Laravel project inside the src folder.

You can also copy your existing project inside the `src` folder.

## Small differences

Thanks to "utility containers" there are some command replacements.
Make sure your server is running!

Replacements:
- `php artisan <command>` : `docker-compose run --rm artisan <command>`
- `npm <command>` : `docker-compose run --rm npm <command>` 

## How to run the project?

Start by configuring the generating and configuring the .evn file according to the following steps:
1. in the root directory run cp src/.env.example .env
2. inside the .env file change replace following variables with the following fields:
   `
     DB_CONNECTION=mysql
     DB_HOST=mysql
     DB_PORT=3306
     DB_DATABASE=homestead
     DB_USERNAME=homestead
     DB_PASSWORD=secret
`

### If you clone the project inside of the src folder you have to also run these commands:
1. docker-compose run --rm artisan composer install
2. cp src/.env.example src/.env
3. docker-compose run --rm artisan key:generate

After that in CMD run:

`docker-compose up -d server`

### Setup for Vue and React Apps (for Vite setup)

To show your js framework content you have to configure `vite.config.js` file.
For Vue setup the content of the file will look like this:
```
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import vue from '@vitejs/plugin-vue'

export default defineConfig({
    server: {
        host: '0.0.0.0',
        hmr: {
            host: 'localhost'
        },
    },
    plugins: [

        vue(),

        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});
```

The most important is this part:

```
server: {
   host: '0.0.0.0',
   hmr: {
      host: 'localhost'
   },
},
```

Inside the hmr we define the host on which we want to set Hot Module Replacement.
Since we will publish our site locally so the value will be localhost.

Finish, you can visit [http://localhost:8000/](http://localhost:8000/) site
