# Laravel Coolify Example

The magic comes from the `nixpacks.toml` file which was based on the one provided by @marcfowler at https://github.com/coollabsio/coolify/discussions/2156

## Steps

The postbuild step handles the cache clear and the artisan migrate, but to get supervisor to work, you can either override the default `[start]` `cmd` with itself plus the command to start supervisor:
```
[start]
cmd = 'node /assets/scripts/prestart.mjs /assets/nginx.template.conf /nginx.conf && (supervisord -c /etc/supervisord.conf & php-fpm -y /assets/php-fpm.conf & nginx -c /nginx.conf)'
```

Or do the following to run supervisor post-build:

Pretty much plug and play, other than the coolify settings, add the command to run supervisor to ensure horizon starts (and restarts if it goes down):
```
supervisord -c /etc/supervisord.conf
```

![Screenshot](https://github.com/Nathanjms/laravel-coolify-example/blob/main/coolify-laravel.png?raw=true)