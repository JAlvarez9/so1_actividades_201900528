# Actividad 3


| Nombre                        | Carnet     |
| ------------------------------- | ------------ |
| Jose Fernando Alvarez Morales | 2019000528 |

### Problema:

El problema era que tiraba un error 404, ya que si bien en react internamente se mamejaba por componentes las paginas, para el nginx no podia leer eso, por lo que si colocabamos una url directamente no la encontraba, por el contrario si se corria desde el index.html y luego se iba a las otras rutas.

### Solucion:

Para poder corregir debemos modificar la configuracion del nginx ya que si lo dejamos con la que el maneja por default nos tirara el error antes mencionado. Por lo que debemos crear un `nginx.config` dentro de la caprte root del frntend, en este archivo ya podremos configurar algunos aspectos. Realizaremos un liste en el puerto 80 y le indicaremos como debe manejar las rutas.

```text
server {
    listen  80;

    location / {
        root   /usr/share/nginx/html;
        try_files $uri $uri/ /index.html;
        index  index.html index.htm;
    }

    }
```

Como podremos visualiar le indicamos que esta configuracion se realice direntamente en el `index.html` para qye el nigix pueda utilzar las rutas del react build.

Por ultimo debemos cambiar los cambios dentro de nuestro `Dockerfile`, se necesitaran solamente 2 lineas de codigos, las cuales son

```text
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d
```

Con el comando RUN le decimos que ya no utilice su configuracion por defecto sino que utilice el que nosotros colocamos en la root del frontend, y con el Copy copiamos el archivo que creamos `nginx.config` para luego pueda utiloizarlo.
