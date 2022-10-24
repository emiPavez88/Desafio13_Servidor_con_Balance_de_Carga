# Servidor con balance de carga
### DAMIÁN CABRIO

## Correr el proyecto localmente
Primero se debe instalar los paquetes desde npm con `npm i`
Para correr el proyecto localmente se debe correr el siguiente comando `npm run dev`. Si se quiere correr el proyecto con un puerto en particular se debe agregar a este comando el parámetro `-p puerto`. Por ejemplo `npm run dev -- -p 2000`.
El proyecto se puede correr en dos modos: Modo fork y modo cluster. Por defecto se utiliza el modo fork, para cambiar el modo utilizar el parámetro `-m` o `-mode` y el modo que se desea utilizar. Al usar el modo cluster, se creará un proceso por cada núcleo del CPU.

También se debe generar y popular un archivo .env, basándose en el archivo .env.example.
Las variables que se deben agregar al archivo .env son: `SESSION_SECRET`, `MONGODB_URL`, `FB_CLIENT_ID`, `FB_CLIENT_SECRET` y `FB_CALLBACK_URL`.

## Rutas del desafío.
Como lo pedía él desafió, se generaron las rutas `/info` y `/api/random?cant=cantidad`, empleando el objeto `process` de Node.js.
- La ruta `/info` devuelve un JSON con la información del entorno de ejecución pedida: Argumentos de entrada, Path de ejecución, Sistema operativo, Process ID, Versión de Node.js, Carpeta del proyecto, Memoria total reservada y número de procesadores.

- La ruta `/api/random` devuelve un JSON con una objeto de números aleatorios como clave, y la cantidad de veces que salieron como valor. La ruta acepta un parámetro `cant`, que indica la cantidad de números aleatorios que se quiere generar (Se verifica que sea un número). Si no se pasa este parámetro, se generan por defecto 100000000 números aleatorios. Al usar la función `fork` para generar los números aleatorios, el procesamiento se realiza en paralelo, y no bloquea la ejecución del proceso principal.

## Outputs de ejecución

### Servidor modo fork con nodemon
$ nodemon src/main.js 

```
[nodemon] 2.0.15
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node src/main.js`
Server on port 8080 || Worker 28932 started! - http://localhost:8080
```

$ tasklist /fi "imagename eq node.exe"

```
Nombre de imagen               PID Nombre de sesión Núm. de ses Uso de memor
========================= ======== ================ =========== ============
node.exe                     16828 Console                    7    59.584 KB
node.exe                     28544 Console                    7    47.212 KB
```

### Servidor modo fork con Node.js

$ node ./src/main.js

```
Server on port 8080 || Worker 31072 started! - http://localhost:8080
```

$ tasklist /fi "imagename eq node.exe"

```
Nombre de imagen               PID Nombre de sesión Núm. de ses Uso de memor
========================= ======== ================ =========== ============
node.exe                     20160 Console                    7   100.160 KB
```

### Servidor modo cluster con nodemon

$ nodemon src/main.js -m cluster
```
[nodemon] 2.0.15
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node src/main.js -p 8080 -m cluster`
Master process PID: 33524
Starting 24 workers...
Server on port 8080 || Worker 28256 started! - http://localhost:8080
Server on port 8080 || Worker 29220 started! - http://localhost:8080
Server on port 8080 || Worker 26444 started! - http://localhost:8080
Server on port 8080 || Worker 31716 started! - http://localhost:8080
Server on port 8080 || Worker 3928 started! - http://localhost:8080
Server on port 8080 || Worker 32656 started! - http://localhost:8080
Server on port 8080 || Worker 33872 started! - http://localhost:8080
Server on port 8080 || Worker 34184 started! - http://localhost:8080
Server on port 8080 || Worker 32248 started! - http://localhost:8080
Server on port 8080 || Worker 3368 started! - http://localhost:8080
Server on port 8080 || Worker 31288 started! - http://localhost:8080
Server on port 8080 || Worker 7072 started! - http://localhost:8080
Server on port 8080 || Worker 33204 started! - http://localhost:8080
Server on port 8080 || Worker 5808 started! - http://localhost:8080
Server on port 8080 || Worker 19628 started! - http://localhost:8080
Server on port 8080 || Worker 11716 started! - http://localhost:8080
Server on port 8080 || Worker 29868 started! - http://localhost:8080
Server on port 8080 || Worker 18572 started! - http://localhost:8080
Server on port 8080 || Worker 3900 started! - http://localhost:8080
Server on port 8080 || Worker 34512 started! - http://localhost:8080
Server on port 8080 || Worker 4708 started! - http://localhost:8080
Server on port 8080 || Worker 13148 started! - http://localhost:8080
Server on port 8080 || Worker 26540 started! - http://localhost:8080
Server on port 8080 || Worker 14420 started! - http://localhost:8080
```

$ tasklist /fi "imagename eq node.exe"

```
Nombre de imagen               PID Nombre de sesión Núm. de ses Uso de memor
========================= ======== ================ =========== ============
node.exe                     16828 Console                    7    58.672 KB
node.exe                     28544 Console                    7    43.280 KB
node.exe                      3248 Console                    7    33.020 KB
node.exe                     33524 Console                    7    74.216 KB
node.exe                     32248 Console                    7    73.740 KB
node.exe                     31716 Console                    7    73.984 KB
node.exe                     11716 Console                    7    74.140 KB
node.exe                     29220 Console                    7    73.728 KB
node.exe                     34184 Console                    7    73.168 KB
node.exe                      3928 Console                    7    73.380 KB
node.exe                     33872 Console                    7    74.364 KB
node.exe                      3900 Console                    7    73.608 KB
node.exe                     28256 Console                    7    73.988 KB
node.exe                     32656 Console                    7    73.144 KB
node.exe                      4708 Console                    7    73.608 KB
node.exe                      5808 Console                    7    73.784 KB
node.exe                     26540 Console                    7    74.372 KB
node.exe                     29868 Console                    7    73.664 KB
node.exe                     33204 Console                    7    73.944 KB
node.exe                     31288 Console                    7    74.004 KB
node.exe                     26444 Console                    7    73.820 KB
node.exe                     14420 Console                    7    73.356 KB
node.exe                      3368 Console                    7    73.800 KB
node.exe                      7072 Console                    7    73.560 KB
node.exe                     34512 Console                    7    74.012 KB
node.exe                     13148 Console                    7    73.440 KB
node.exe                     18572 Console                    7    73.416 KB
node.exe                     19628 Console                    7    73.324 KB
```

### Servidor modo cluster con Node.js

$ node ./src/main.js -m cluster
```
Master process PID: 33312
Starting 24 workers...
Server on port 8080 || Worker 22900 started! - http://localhost:8080
Server on port 8080 || Worker 28268 started! - http://localhost:8080
Server on port 8080 || Worker 30440 started! - http://localhost:8080
Server on port 8080 || Worker 33384 started! - http://localhost:8080
Server on port 8080 || Worker 35488 started! - http://localhost:8080
Server on port 8080 || Worker 16012 started! - http://localhost:8080
Server on port 8080 || Worker 15644 started! - http://localhost:8080
Server on port 8080 || Worker 8096 started! - http://localhost:8080
Server on port 8080 || Worker 24584 started! - http://localhost:8080
Server on port 8080 || Worker 30516 started! - http://localhost:8080
Server on port 8080 || Worker 23620 started! - http://localhost:8080
Server on port 8080 || Worker 29252 started! - http://localhost:8080
Server on port 8080 || Worker 3700 started! - http://localhost:8080
Server on port 8080 || Worker 12508 started! - http://localhost:8080
Server on port 8080 || Worker 29872 started! - http://localhost:8080
Server on port 8080 || Worker 19852 started! - http://localhost:8080
Server on port 8080 || Worker 18912 started! - http://localhost:8080
Server on port 8080 || Worker 36760 started! - http://localhost:8080
Server on port 8080 || Worker 33380 started! - http://localhost:8080
Server on port 8080 || Worker 30220 started! - http://localhost:8080
Server on port 8080 || Worker 16724 started! - http://localhost:8080
Server on port 8080 || Worker 14520 started! - http://localhost:8080
Server on port 8080 || Worker 31220 started! - http://localhost:8080
Server on port 8080 || Worker 34136 started! - http://localhost:8080
```

$ tasklist /fi "imagename eq node.exe"

```
Nombre de imagen               PID Nombre de sesión Núm. de ses Uso de memor
========================= ======== ================ =========== ============
node.exe                     16828 Console                    7    58.960 KB
node.exe                     28544 Console                    7    43.320 KB
node.exe                     33312 Console                    7    73.444 KB
node.exe                     28268 Console                    7    72.576 KB
node.exe                     33384 Console                    7    72.744 KB
node.exe                     16724 Console                    7    72.824 KB
node.exe                     16012 Console                    7    73.304 KB
node.exe                     35488 Console                    7    73.248 KB
node.exe                      8096 Console                    7    72.752 KB
node.exe                     29252 Console                    7    73.344 KB
node.exe                     22900 Console                    7    72.884 KB
node.exe                     15644 Console                    7    74.020 KB
node.exe                     30440 Console                    7    72.316 KB
node.exe                      3700 Console                    7    72.716 KB
node.exe                     23620 Console                    7    73.128 KB
node.exe                     24584 Console                    7    73.484 KB
node.exe                     29872 Console                    7    73.460 KB
node.exe                     30220 Console                    7    73.196 KB
node.exe                     18912 Console                    7    73.240 KB
node.exe                     34136 Console                    7    72.944 KB
node.exe                     14520 Console                    7    73.292 KB
node.exe                     30516 Console                    7    73.712 KB
node.exe                     19852 Console                    7    72.184 KB
node.exe                     36760 Console                    7    74.012 KB
node.exe                     12508 Console                    7    72.584 KB
node.exe                     31220 Console                    7    73.488 KB
node.exe                     33380 Console                    7    72.792 KB
```

## PM2

### PM2 en modo fork

$ pm2 start src/main.js  



### PM2 en modo cluster

$ pm2 start src/main.js -i max


## NGINX

Se creó un archivo ecosystem.json con la configuración de ejecución que debe utilizar PM2 para ejecutar el servidor, y ser vinculado con NGINX.
El comando que se debe correr es: `pm2 start ecosystem.json`
Luego de correr este comando, se debe correr NGINX con el archivo de configuración que se encuentra en la carpeta 'nginx' o debajo. Como la ubicación de NGINX y el proyecto van a ser diferentes a las mías, se debe modificar el parámetro 'root' dentro del archivo, con la ruta a la carpeta public del proyecto.

```
worker_processes  1;

events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    keepalive_timeout  65;

    upstream node_app{
        server localhost:8082;
        server localhost:8083;
        server localhost:8084;
        server localhost:8085;
    }

    server {
        listen       80;
        server_name  nginx_node;
        root /ruta/del/proyecto/public; #Esta ruta se debe cambiar por la ruta del proyecto

        location / {
            proxy_pass http://node_app;
        }
    }
}
```