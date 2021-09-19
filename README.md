# k8s_4

## Creación de la imagen base backend

El primer paso es la construcción de la imagen base, para esto se deben ejecutar los siguientes comandos:

```
cd 1-Imagen-Backend
docker build -f .docker/Dockerfile -t nombre-usuario/ms-sena:1 .
```
docker build -f .docker/Dockerfile -t nombre-usuario/ms-sena:1 .
Si se desea validar la imagen local, el usuario debe ejecutar la imagen creada en docker:

```
docker run -p 5000:5000 -d nombre-usuario/ms-sena:1
```

Luego, se debe abrir el navegador y ejecutar la siguiente URL para ingresar al swagger `http://localhost:5000/swagger`

Para bublicar la imagen en nuestros dockerHub se deben ejecutar los siguientes comandos:

```
docker login # Desde la consola ingresar el nombre de usuario y la contraseña
docker push nombre-usuario/ms-sena:1
```
## Creación de la imagen base backend

El Segundo paso es la construcción de la imagen base para el front, para esto se deben ejecutar los siguientes comandos:

```
cd 1-Imagen-Frontend
docker build -f .docker/Dockerfile -t nombre-usuario/front-sena:1 .
```
docker build -f .docker/Dockerfile -t nombre-usuario/front-sena:1 .
Si se desea validar la imagen local, el usuario debe ejecutar la imagen creada en docker:

```
docker run -p 4200:4200 -d nombre-usuario/front-sena:1
```

Luego, se debe abrir el navegador  `http://localhost:4200`

Para bublicar la imagen en nuestros dockerHub se deben ejecutar los siguientes comandos:

```
docker login # Desde la consola ingresar el nombre de usuario y la contraseña
docker push nombre-usuario/front-sena:1
```


##  Conexión servicio front con el backend dentro de K8s

### Creación servicio loadbalancer y clusterip


Desde la raíz del repositorio, ingresar a la carpeta:

```
cd 3-Interconexión-Servicios
```
Luego se debe ejecutar los siguientes comandos, para la creación del configmap, del servicio y del despliegue:

```
kubectl apply -f backend.yml
kubectl apply -f frontend.yml
```
Validar que se hayan creado los servicios de manera correcta:


```
kubectl get svc
```

## Manejo de Secretos y Configmap

### Configmap

Desde la raíz del repositorio, ingresar a la carpeta:

```
cd 2-Deploy-Secrets/Configmap
```

Luego se debe ejecutar los siguientes comandos, para la creación del configmap, del servicio y del despliegue:

```
kubectl apply -f configmap.yml
kubectl apply -f deployConfigMap.yml
```

Los comandos anteriores se pueden simplificar, especificando en la ejecución del comando de *apply* la carpeta. Suponiendo que nos encontramos en la carpeta `2-Deploy-Secrets`, se ejecuta el siguiente comando:

```
kubectl apply -f Configmap
```

No olvidar elminiar los recursos creados con el comando `kubectl delete ...`


### Secretos

Desde la raíz del repositorio, ingresar a la carpeta:


```
kubectl apply -f Secrets
```

No olvidar elminiar los recursos creados con el comando `kubectl delete -f Secrets`


Tips para convertir valores de texto plano a base 64, en una terminal se debe ejecutar el siguiente comando:

```
echo -n 'valor a convertir' | base64
```
