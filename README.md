# Laravel en Kubernetes

Un ejemplo de como desplegar una aplicación Laravel en Kubernetes usando DigitalOcean.
Puedes leer este [articulo](https://dev.to/gregorip02/como-desplegar-laravel-en-kubernetes-con-digitalocean-2n6f)
donde se explica la función de cada uno de estos manifiestos.

## Guía Básica: Instalación y configuración

``` bash
$ git clone https://gitlab.com/gregorip02/laravel-in-kubernetes.git
$ cd laravel-in-kubernetes
```

Copia el archivo de ejemplo `01-secrets.yml.example` a `01-secrets.yml` y crea tu llave
de Laravel. Para la generación de la llave de Laravel puedes usar:

```bash
$ echo "bas64:$(openssl rand -rand /dev/urandom 32 | base64)"
```

Luego copia el resultado y asocíalo con la variable de entorno **APP_KEY** en el archivo
`01-secrets.yml`. Recuerda que puedes aplicar todos los manifiestos usando:

``` bash
$ kubectl apply -f .
```
