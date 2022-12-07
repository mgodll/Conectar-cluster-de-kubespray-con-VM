# Conectar-cluster-de-kubespray-con-VM
En esta ocasion se mostrara como conectar un cluster de kubespray con un usuario para la instalacion, despliegue, actualización, gestion de aplicaciones

- Cluster_name: mateo
- User_name:    pruebas

# Herramientas necesarias

Antes de proceder con la instalacion se necesitan de unas herramientas previas las cuales son:

- [helm-install](https://github.com/mgodll/Despliegue-y-gestion-de-contenedores-usando-la-herramienta-helm)
- [Kubectl](https://github.com/mgodll/Despliegue-y-gestion-de-contenedores-usando-la-herramienta-helm)

Para esta ocasion se usara el cluster que se explico su despliegue en el repositorio [Cluster_kubespray](https://github.com/mgodll/Despliegue-de-cluster-de-kubernetes-con-la-herramienta-kubespray)

# Requisitos de maquina

Requisitos minimos

| Estructura       | Valores            |
|------------------|--------------------|
|OS usado          | Ubuntu 20.04 LTS   |
|vCPU              | 4                  |
|RAM (GB)          | 8                  |
|Disk (GB)         | 40                 |
|Home user         | pruebas            |
|Number of NICs    | 1 (ens160)         |
|Kubespray Version | v2.19.1            |

# Configuracion del entorno

Para poder conectar el cluster con el usuario es necesario obtener la información del archivo admin.conf del cluster en la ruta `/etc/kubernetes`

```bash
cd /etc/kubernetes
sudo cat admin.conf
```

tendra que aparecer algo de la sigueinte forma

```bash
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUMvakNDQWVhZ0F3SUJBZ0lCQURBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwcmRXSmwKY201bGRHVnpNQjRYRFRJeU1URXlOVEl4TlRZd01Wb1hEVE15TVRFeU1qSXhOVFl3TVZvd0ZURVRNQkVHQTFVRQpBeE1LYTNWaVpYSnVaWFJsY3pDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTXg3CktXVThxbkovcXI2Z09EQ2NUL1VmV1dacHowaFRBSHpZM0ttRXBqZWhLR0dIckNqUUYrckJTQ3dzSXIwcUszUnUKT2xDVXN4UHFVOEtsdmx6NktaUWo1QnVkQzUxV0J1c2I4YW5EVlpkV0tvejRLcnJDczU4VnBURlpYc0FpdmROdgppaUYyamRHY0VySWpOcFFDU213dlpYNWpQdk1CTnl0T25ZMmQ5SEloYTQ3UnRJM1FlN3VwWkV3YzdtU2wxT1hnClFrT0ZMTXhlelJsK09KRzVtV1JqZVp4QnVoMzl1YjQxVWRSZzBSa0p4b29yTnZKekJlRm9XK0dPREJGaUpGOGYKWnBpcy9udTRnMStlYVJNcnlVeTdtczRJUUxhWUVWMnV2Y20raDBtZHVEOHNVQWNPUEkycHhEc1JlMkVWUVg0RwpFbDhYSkw2eGVvcGIyWHRhc0RzQ0F3RUFBYU5aTUZjd0RnWURWUjBQQVFIL0JBUURBZ0trTUE4R0ExVWRFd0VCCi93UUZNQU1CQWY4d0hRWURWUjBPQkJZRUZLYmxGMjF3VDRGZVVWVzRNQkI2V0t1eVVHZ1lNQlVHQTFVZEVRUU8KTUF5Q0NtdDFZbVZ5Ym1WMFpYTXdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBRnA0UVB6R2pRMVZuWUZDRnFWOQpUWjlXYkYydzgyNzdzcW5tQTFaOTFjd1k0QUU2U1RLTFhYM1o2ckpyYTlSUkhlWTB0RVR6QnRkaHlUY0d2eXNICm95blZiVVUyZ1hzOTRRU1k5eWI4UFBoYTRpM2p0ZGRVcGhPNGVSdnVTOXFubVpGZUdsVW5FMGZJSGduMGdwTTcKUytpSmE1Q0RxOTkzL1JLTHJ3aG0xMkQwTjVTYlViWEpHMmNTY2tGenhIZjZ1SDgyWXNaT2MxZHIwcS9uZGNmaAovZmlaTzdCU0ZpOEMrZlRFU2VtNkJQUzdGWFNMMm96aC9nOG00YXp1V2ZPQk1KYkordG5kUVYvSkdhaldNQkdWClN0NHpiUHBZdVk0cHR4cFF3NmRERk1TMkdyYWhWb2ZOT3VrbEE4dXdLdDZMdDBDQkdQWHFyRUFBODVyUG8wMTgKalR3PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    server: https://127.0.0.1:6443
  name: cluster.local
contexts:
- context:
    cluster: cluster.local
    user: kubernetes-admin
  name: kubernetes-admin@cluster.local
current-context: kubernetes-admin@cluster.local
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURJVENDQWdtZ0F3SUJBZ0lJRHVQWkY2K29lYkl3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TWpFeE1qVXlNVFUyTURGYUZ3MHlNekV4TWpVeU1UVTJNRFJhTURReApGekFWQmdOVkJBb1REbk41YzNSbGJUcHRZWE4wWlhKek1Sa3dGd1lEVlFRREV4QnJkV0psY201bGRHVnpMV0ZrCmJXbHVNSUlCSWpBTkJna3Foa2lHOXcwQkFRRUZBQ..... etc
```

Por lo tanto se copiara las informacion del `cat admin.conf` y en la VM del usuario se creara un carpeta con el nombre de .kube y un archivo que tendra como nombre config

```bash
mkdir .kube
vim config
```

>**NOTA** El nombre del archivo config no tiene que ser necesariamente "config" se le puede dar cualquier nombre si se desea

se pega la información y se realizara unas pequeñas modificaciones sobre este de la siguiente forma

```bash
apiVersion: v1
clusters:
- cluster:
+   insecure-skip-tls-verify: true
+   server: https://34.125.167.225:6443
  name: cluster.local
contexts:
- context:
    cluster: cluster.local
    user: kubernetes-admin
  name: kubernetes-admin@cluster.local
current-context: kubernetes-admin@cluster.local
kind: Config
preferences: {}
users:
- name: kubernetes-admin
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURJVENDQWdtZ0F3SUJBZ0lJRHVQWkY2K29lYkl3RFFZSktvWklodmNOQVFFTEJRQXdGVEVUTUJFR0ExVUUKQXhNS2EzVmlaWEp1WlhSbGN6QWVGdzB5TWpFeE1qVXlNVFUyTURGYUZ3MHlNekV4TWpVeU1UVTJNRFJhTURReApGekFWQmdOVkJBb1REbk41YzNSbGJUcHRZWE4wWlhKek1Sa3dGd1lEVlFRREV4QnJkV
```

En donde se borra todo lo del `certificate-authority-data:`, y se reemplaza por `insecure-skip-tls-verify: true`, y la ip del server es la publica de la maquina del cluster

>**NOTA** Es de mencionar que el puerto 6443 es el por defecto dell kubespray y de los cluster, para poder que las maquinas se vean tienen que tener pin y ademas que estos puertos esten abiertos sobre la plataforma en la cual esten montados, para estas pruebas se realizo en la dashboard de GCP (Google Cloud).

Por ultimo se realiza un `kubectl get pods -A` para probar su funcionamiento
