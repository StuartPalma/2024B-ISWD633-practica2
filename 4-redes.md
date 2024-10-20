# Redes
Las redes son un componente fundamental que permite la comunicación entre contenedores, así como la comunicación de los contenedores con el mundo exterior. 
![Imagen](img/redes.PNG)
- Bridge: Esta es la red por defecto en Docker. Permite la comunicación entre contenedores en el mismo host. Cada contenedor conectado a la red bridge tiene una IP propia en la subred de la red bridge.
    -  Brige por default: Cuando se ejecuta un contenedor, Docker crea automáticamente una red de tipo bridge por default. Esta red se utiliza para permitir la comunicación entre contenedores en el mismo host. Cada contenedor conectado a esta red obtiene su propia dirección IP en la subred de la red bridge.
    - Bridge creada por nosotros: Un usuario también puede crear sus propias redes de tipo bridge en Docker. Esto puede ser útil para organizar y segmentar los contenedores de una aplicación de manera más controlada. Al crear una red bridge personalizada, se puede especificar un rango de direcciones IP y otras configuraciones de red específicas. Los contenedores conectados a esta red utilizarán las direcciones IP de la subred definida por el usuario.
- Host: Con esta red, los contenedores comparten la red del host en lugar de tener su propia interfaz de red. Esto puede mejorar el rendimiento de red, pero los contenedores pueden entrar en conflicto con los puertos del host si intentan utilizar los mismos puertos.
- None: Con esta red, se deshabilita la configuración de red. Los contenedores que usan esta red tienen su propia red de bucle invertido y no pueden comunicarse con otros contenedores a menos que se conecten explícitamente a una red.

### Crear una red de tipo bridge

```
docker network create <nombre red> -d bridge
```

### Crear un contenedor vinculado a una red

```
docker run -d --name <nombre contenedor> --network <nombre red> <nombre imagen>
```

### Para saber a qué red está conectado un contenedor

```
docker inspect <nombre contenedor>
```
ó
```
docker network inspect <nombre red> 
```

### Vincular contenedor a una red
```
docker network connect <nombre red> <nombre contenedor>
```

### Para desvincular un contenedor de una red
```
docker network disconnect <nombre red> <nombre contenedor>
```

### Para listar las redes existentes
```
docker network ls
```

### Crear los contenedores y las redes que se presentan en el esquema. Usar para todos los contenedores la imagen de nginx:alpine

![Imagen](img/esquema-ejercicio-redes.PNG)

# COLOCAR UNA CAPTURA DE LAS REDES EXISTENTES CREADAS
![Imagen](img/redes.jpeg)

# COLOCAR UNA(S) CAPTURAS(S) DE LOS CONTENEDORES CREADOS EN DONDE SE EVIDENCIE A QUÉ RED ESTÁN VINCULADOS
````

PS C:\Users\User> docker network inspect red
[
    {
        "Name": "red",
        "Id": "de09df73252db9f70a3f5cdb8afe17e26d39b157a7f19934d88f1e2776dddc11",
        "Created": "2024-10-20T21:43:19.651427319Z",        
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.19.0.0/16",
                    "Gateway": "172.19.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "3b9df88bcf1a03b4e63cb5ac62f8341a459bcd25d0584b34c530b3012a6501e1": {
                "Name": "contenedor1",
                "EndpointID": "07a8a0f0190c04e2137e054e492b89e6f92f62823acf0325a30c9f3b5a969b70",
                "MacAddress": "02:42:ac:13:00:02",
                "IPv4Address": "172.19.0.2/16",
                "IPv6Address": ""
            },
            "61efce93b35c15f33f5a88b3ed566ab15c8ddf2460b00caf93be33e7de227480": {
                "Name": "contenedor3",
                "EndpointID": "248269f60ba104a4384972b2fb87bf88b7dc3c0998a86d3f13daa332bf3ae75d",
                "MacAddress": "02:42:ac:13:00:04",
                "IPv4Address": "172.19.0.4/16",
                "IPv6Address": ""
            },
            "8614d4c831a0411fe2006324509af8494da2e5b141f72fefd211b9a69a494475": {
                "Name": "contenedor2",
                "EndpointID": "0da1658097c36a43768cdcffc728aaffccf89cf5f41a391c2a5489b30f5d85d4",
                "MacAddress": "02:42:ac:13:00:03",
                "IPv4Address": "172.19.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
PS C:\Users\User> docker network inspect red2
[
    {
        "Name": "red2",
        "Id": "e99987e640246dc4842d615d47fe773a0e1165b09e32cc4e50b72d7feac1fa83",
        "Created": "2024-10-20T21:53:03.931260908Z",        
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.20.0.0/16",
                    "Gateway": "172.20.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "61efce93b35c15f33f5a88b3ed566ab15c8ddf2460b00caf93be33e7de227480": {
                "Name": "contenedor3",
                "EndpointID": "eb79a2ff2c0f9a5e529b71c02511aab01c70bfb2fc92d0704bdd1f96aeb1abe5",
                "MacAddress": "02:42:ac:14:00:03",
                "IPv4Address": "172.20.0.3/16",
                "IPv6Address": ""
c07d06ea0ecc5addd": {
                "Name": "contenedor4",
                "EndpointID": "f15e6ecceb3ad90a0a4e5ce525dd52e9ad2a2c28b15f55867ca3d959f35e4736",
                "MacAddress": "02:42:ac:14:00:02",
                "IPv4Address": "172.20.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]

````

### Para eliminar las redes creadas
```
docker network rm <nombre de la red>
```

