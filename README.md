# Laravel in Kubernetes

This is the code that I used for my article in dev.to where I explain how to
deploy a Laravel application in kubernetes using DigitalOcean as a cloud provider.

You can read the [article](https://dev.to/gregorip02/como-desplegar-laravel-en-kubernetes-con-digitalocean-2n6f) in Spanish.

## Get started

Clone the manifests.

``` bash
$ git clone https://gitlab.com/gregorip02/laravel-in-kubernetes.git
$ cd laravel-in-kubernetes
```

Then you have to generate a configuration file for your Laravel application.

``` bash
$ cp .env.example .env
```

Modify your environment variables depending on your requirements.
You can use this command to generate a valid application key for laravel:

``` bash
$ echo "base64:$(openssl rand -base64 32)"
```
Then copy the result of this operation and assign it to the environment
variable **APP_KEY** in the `.env` file.

Finally you must generate a secret of kuberntes from the configuration file .env:

``` bash
$ kubectl create secret generic laravel-environment \
  -n laravel-app \
  --from-file=.env \
  --dry-run \
  -o yaml > 01-secrets.yml
```

Finally apply all manifests using a command:

``` bash
$ kubectl apply -f .
```

## Remember

- If you are using minikube you can use the `minikube service list` command to
  obtain the public ip address of your load balancer that will take you to the
  Laravel application.

- If you are using a cloud provider like DigitalOcean using
  `kubectl -n laravel-app get svc -o wide` you can get your public ip address.
