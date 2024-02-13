# deploy-wordpress-on-kubernetes

Hola, este mi primer despliegue de un servicio de wordpress en kubernetes, primero se corrió en un entorno local con docker y después se hizo un kompose de los archivos que creamos de docker.
Este despliegue cuenta con su servicio de **wordpress** exponiendolo mediante un balanceador de carga para que pueda ser accedido desde cualquier parte, este mismo servicio está conectado a su base de datos que corre en **MySQL** y también está conectado a otro servicio de **phpMyAdmin**, este servicio con el fin de poder hacer migraciones de de bases de datos de una manera más sencilla.

Si eres nuevo en esto, al final te dejo una recopilación de los comandos más utilizados en **kubernetes**.

También debes de saber que lo que te dejo está dividido en dos carpetas, lo primero es correr los servicios, de esta manera solo se crean los servicios con su correspondiente **volumen persistente**. Esto se encuentra en la carpeta *wp-deploy* donde solo correrán los servicios en local, lo que sigue es exponer los servicios de mediante un balanceador de carga, solo exponemos el servicio de wordpress o el servicio de phpMyAdmin, puedes o no exponer el servicio de phpMyAdmin, para que pueda ser visto por lo demás debes exponerlo mediante un balanceador de carga, este paso sí debes hacerlo para exponer wordpress. 

Correr servicios en kubernetes:
```bash:
kubectl apply -f wp-deploy/ 
```

Exponer servicio de wordpress:
```bash:
kubectl apply -f expose-services/wordpress-lb.yml
```

Exponer servicio de phpMyAdmin:
```bash:
kubectl apply -f expose-services/phpmyadmin-lb.yml
```

Con estos 3 comandos y los archivos estructurados de esta manera podemos hacer un despliegue de wordpress, lo mejor de todo es que cada servicio corre en un pod, por lo cual son las buenas prácticas de cada recurso se delega a cada servicio.

> [!CAUTION]
> Cambia las contraseñas antes de ejecutar cualquier comando

## Comandos más utilizados para kubernetes

**Para obtener una lista de todos los recursos en el clúster:**

```bash:
kubectl get all
```

**Para obtener una lista de todos los recursos en el clúster en tiempo real:**

```bash:
watch -n1 kubectl get all
```

**Para obtener una lista de todos los pods:**

```bash:
kubectl get pods
```

**Para conectarse a un pod:**

```bash:
kubectl exec -it <nombre-completo-pod> -- bin/bash/
```

**Para obtener una lista de todos los nodos:**

```bash:
kubectl get nodes
```

**Para obtener una lista de todos los servicios:**

```bash:
kubectl get services
```

**Para obtener una lista de todas las deployments:**

```bash:
kubectl get deployments
```

**Para obtener información detallada sobre un pod específico:**

```bash:
kubectl describe pod <nombre-pod>
```

**Para obtener información detallada sobre un nodo específico:**

```bash:
kubectl describe node <nombre-nodo>
```

**Para obtener información detallada sobre un servicio específico:**

```bash:
kubectl describe service <nombre-servicio>
```

**Para obtener información detallada sobre una deployment específica:**

```bash:
kubectl describe deployment <nombre-deployment>
```

**Para mostrar los logs de un pod específico:**

```bash:
kubectl logs <nombre-pod>
```

**Para abrir una terminal en un pod específico:**

```bash:
kubectl exec -it <nombre-pod> -- /bin/bash
```

**Para crear un pod temporal que ejecuta un comando específico:**

```bash:
kubectl run <nombre-pod> --image=busybox --restart=Never -- /bin/sh
```

**Para eliminar un pod específico:**

```bash:
kubectl delete pod <nombre-pod>
```

**Para eliminar un servicio específico:**

```bash:
kubectl delete service <nombre-servicio>
```

**Para eliminar una deployment específica:**

```bash:
kubectl delete deployment <nombre-deployment>
```

**Para crear o actualizar recursos a partir de un archivo YAML:**

```bash:
kubectl apply -f <ruta-archivo-yaml>
```

**Para crear recursos a partir de un archivo YAML:**

```bash:
kubectl create -f <ruta-archivo-yaml>
```

**Para eliminar recursos a partir de un archivo YAML:**

```bash:
kubectl delete -f <ruta-archivo-yaml>
```

**Para editar el archivo YAML de un pod específico:**

```bash:
kubectl edit pod <nombre-pod>
```

**Para editar el archivo YAML de un servicio específico:**

```bash:
kubectl edit service <nombre-servicio>
```

**Para editar el archivo YAML de una deployment específica:**

```bash:
kubectl edit deployment <nombre-deployment>
```

**Para escalar una deployment a 5 réplicas:**

```bash:
kubectl scale deployment <nombre-deployment> --replicas=5
```

**Para mostrar el estado de un rollout de deployment:**

```bash:
kubectl rollout status deployment <nombre-deployment>
```

**Para mostrar el uso de recursos de los nodos en el clúster:**

```bash:
kubectl top nodes
```

**Para mostrar el uso de recursos de los pods en el clúster:**

```bash:
kubectl top pods
```

**Para reenviar un puerto local a un puerto en un pod específico:**

```bash:
kubectl port-forward <nombre-pod> <puerto-local>:<puerto-pod>
```