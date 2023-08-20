## How to create your project?

To create your Laravel project first create the `src` folder inside the root folder. After that run this command:
```
docker-compose run --rm composer create-project laravel/laravel .
```

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

```
docker-compose up -d server
```

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

Inside the hmr, we define the host on which we want to set Hot Module Replacement.
Since we will be publishing our site locally, the value will be localhost.

After all these steps run this command to start publishing your Vite code:

```
docker-compose run --rm --service-ports npm run dev
```

The flag `--service-ports` is important because it will expose ports according to those defined in the `docker-compose.yaml` and `src/vite.config.js` files.
By default `vite` expose port `5173`.

Finish, you can visit [http://localhost:8000/](http://localhost:8000/) site

## Extra tips

- After making some changes in the `routes` folder make sure that you clear the cache before trying your newly added routes. You can do it by typing in CMD the following command:

```
docker-compose run --rm artisan optimize
```
