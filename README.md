# Supported tags and respective Dockerfile links

- [`0.2.0`, `0.3.3` (*0.3.3/Dockerfile*)](https://github.com/Accenture/adop-nginx/blob/master/Dockerfile.md)

# Build Status

[![Build Status](https://travis-ci.org/Accenture/adop-nginx.svg?branch=master)](https://travis-ci.org/Accenture/adop-nginx)

# What is adop-nginx?

adop-nginx provides Nginx with LDAP support. Nginx is a high performance reverse proxy. This image also has the LDAP authentiction module installed.

> [wikipedia.org/wiki/Nginx](https://en.wikipedia.org/wiki/Nginx)

![logo](https://raw.githubusercontent.com/docker-library/docs/master/nginx/logo.png)

# How to use this image

      $ docker run --name <your-container-name> -dt \
        -v /resources/configuration/:/etc/nginx/:ro \
        -v /resources/release_note:/usr/share/nginx/html/:ro \
        -v /var/log:/var/log 
        -p 443:443 \
        -p 80:80 \
        accenture/adop-nginx:VERSION
        
## Configuration

The nginx configuration is externalised and stored the 'resources' directory.

Runtime configuration can be provided using environment variables:

* NGINX_PORT, 80(default) or 443 (for ssl)
* NGINX_SSL, off(default) or on
* LDAP_PROTOCOL, ldap(default) or ldaps
* LDAP_SERVER, the LDPA URI, i.e. ldap-host:389
* LDAP_USERNAME, the LDAP BASE_DN
* LDAP_PASSWORD, the password to use connecting to LDAP service using the provided username 
* LDAP_USER_BASE_DN, the LDAP user BASE_DN
* LDAP_GROUP_ATTRIBUTE, LDAP object field attribute the defines group appartenence. 
* LDAP_USER_ID_ATTRIBUTE, LDAP object field attribute the defines the user identifier. 
* LDAP_USER_OBJECT_CLASS, LDAP user object class

### Custom HTML (landing page) and NGINX configuration

Both html and nginx configuration folders are being overwritten on every container start (to enforce configuration persitency). If you want to customize this and do not overwrite the data, specify these environment variables:

* CUSTOM_CONF, flag - whether to allow NGINX config files customization, default `false`
* CUSTOM_HTML, flag - whether to allow NGINX HTML files customization, default `false`

## SSL configuration
If you have certificates, set `NGINX_PORT` to `443` and `NGINX_SSL` to `on` and add your certificates to the volume under ssl directory as `host.crt` and `host.key`:

```
# Assuming host.crt and host.key are in the current working directory, perform the following steps
$ docker volume inspect nginx_config
[
    {
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/nginx_config/_data",
        "Name": "nginx_config",
        "Options": {},
        "Scope": "local"
    }
]

$ ls "/var/lib/docker/volumes/nginx_config/_data"
fastcgi.conf          fastcgi_params          koi-utf  mime.types          naxsi_core.rules  naxsi-ui.conf.1.4.1  nginx.conf.default  scgi_params          sites-available  ssl           uwsgi_params.default
fastcgi.conf.default  fastcgi_params.default  koi-win  mime.types.default  naxsi.rules       nginx.conf           proxy_params        scgi_params.default  sites-enabled    uwsgi_params  win-utf

$ cp host* /var/lib/docker/volumes/nginx_config/_data/ssl/
$ docker restart proxy
```

# License
Please view [licence information](LICENCE.md) for the software contained on this image.

# Supported Docker versions

This image is officially supported on Docker version 1.9.1.
Support for older versions (down to 1.6) is provided on a best-effort basis.

# User feedback

## Documentation
Documentation for this image is available in the [Nginx documentation page](http://nginx.org/en/docs/). 
Additional documentaion can be found under the [`docker-library/docs` GitHub repo](https://github.com/docker-library/docs). Be sure to familiarize yourself with the [repository's `README.md` file](https://github.com/docker-library/docs/blob/master/README.md) before attempting a pull request.

## Issues
If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/Accenture/adop-nginx/issues).

## Contribute
You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/Accenture/adop-nginx/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
