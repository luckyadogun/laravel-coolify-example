# Laravel Coolify Example with Horizon

The magic comes from the `nixpacks.toml` file, which was based on the one provided by [@marcfowler](https://github.com/marcfowler) at https://github.com/coollabsio/coolify/discussions/2156.

I;ve also added opcache, but to be honest am unsure if it's working (or needed here).

## Steps

The postbuild step handles the cache clear and the artisan migrate, but to get supervisor to work, you can either override the default `[start]` `cmd` with the one provided by Nixpacks and add the command to start supervisor:
```
[start]
cmd = 'node /assets/scripts/prestart.mjs /assets/nginx.template.conf /nginx.conf && (supervisord -c /etc/supervisord.conf & php-fpm -y /assets/php-fpm.conf & nginx -c /nginx.conf)'
```

However, if Nixpacks change this command in the future (unsure how likely this is), this will not update.

Instead, we can do the following to run supervisor post-build:

Add the following to the post-deployment commands section of the project on Coolify dashboard:
```
supervisord -c /etc/supervisord.conf
```

![Screenshot](https://raw.githubusercontent.com/Nathanjms/laravel-coolify-example/main/coolify-laravel.png)
