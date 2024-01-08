---
title: Crear contenedores de servicio Redis
shortTitle: Contenedores de servicio de Redis
intro: Puedes usar los contenedores de servicio para crear un cliente Redis en tu flujo de trabajo. En esta guía se muestran ejemplos de cómo crear un servicio Redis para los trabajos que se ejecutan en contenedores o directamente en la máquina ejecutor.
redirect_from:
  - /actions/automating-your-workflow-with-github-actions/creating-redis-service-containers
  - /actions/configuring-and-managing-workflows/creating-redis-service-containers
  - /actions/guides/creating-redis-service-containers
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
type: tutorial
topics:
  - Containers
  - Docker
---

{% data reusables.actions.enterprise-beta %}
{% data reusables.actions.enterprise-github-hosted-runners %}

## Introducción

En esta guía se muestran ejemplos de flujo de trabajo que configuran un contenedor de servicio mediante la imagen `redis` de Docker Hub. El flujo de trabajo ejecuta un script para crear un cliente Redis y rellenar el cliente con datos. Para probar que el flujo de trabajo crea y rellena el cliente Redis, el script imprime los datos del cliente en la consola.

{% data reusables.actions.docker-container-os-support %}

## Prerrequisitos

{% data reusables.actions.service-container-prereqs %}

También puede ser útil tener una comprensión básica de YAML, la sintaxis para {% data variables.product.prodname_actions %}, y Redis. Para obtener más información, consulta:

- "[Aprende sobre las {% data variables.product.prodname_actions %}](/actions/learn-github-actions)"
- "[Comenzar con Redis](https://redislabs.com/get-started-with-redis/)"en la documentación de Redis

## Ejecutar trabajos en contenedores

{% data reusables.actions.container-jobs-intro %}

{% data reusables.actions.copy-workflow-file %}

```yaml{:copy}
name: Redis container example
on: push

jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:10.18-jessie

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      redis:
        # Docker Hub image
        image: redis
        # Set health checks to wait until redis has started
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      # Downloads a copy of the code in your repository before running CI tests
      - name: Check out repository code
        uses: {% data reusables.actions.action-checkout %}

      # Performs a clean installation of all dependencies in the `package.json` file
      # For more information, see https://docs.npmjs.com/cli/ci.html
      - name: Install dependencies
        run: npm ci

      - name: Connect to Redis
        # Runs a script that creates a Redis client, populates
        # the client with data, and retrieves data
        run: node client.js
        # Environment variable used by the `client.js` script to create a new Redis client.
        env:
          # El nombre del host utilizado para comunicarse con el contenedor de servicio Redis
          REDIS_HOST: redis
          # El puerto Redis predeterminado
          REDIS_PORT: 6379
```

### Configurar el trabajo del contenedor

{% data reusables.actions.service-container-host %}

{% data reusables.actions.redis-label-description %}

```yaml{:copy}
jobs:
  # Etiqueta del trabajo del contenedor
  container-job:
    # Los contenedores deben ejecutarse en sistemas operativos basados en Linux
    runs-on: ubuntu-latest
    # Imagen de Docker Hub que `container-job` ejecuta en el contenedor: node:10.18-jessie

    # Contenedores de servicio para ejecutar con `container-job`
    services:
      # Etiqueta utilizada para acceder al contenedor de servicio
      redis:
        # Imagen de Docker Hub
        image: redis
        # Establece revisiones de estado para esperar hasta que Redis haya comenzado
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
```

### Configurar los pasos

{% data reusables.actions.service-template-steps %}

```yaml{:copy}
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: {% data reusables.actions.action-checkout %}

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to Redis
    # Runs a script that creates a Redis client, populates
    # the client with data, and retrieves data
    run: node client.js
    # Environment variable used by the `client.js` script to create a new Redis client.
    env:
      # El nombre del host utilizado para comunicarse con el contenedor del servicio Redis
      REDIS_HOST: redis
      # El puerto Redis predeterminado
      REDIS_PORT: 6379
```

{% data reusables.actions.redis-environment-variables %}

El nombre del host del servicio Redis es la etiqueta que configuraste en tu flujo de trabajo, en este caso, `redis`. Dado que los contenedores Docker en la misma red de puentes definida por el usuario abren todos los puertos por defecto, podrás acceder al contenedor del servicio en el puerto Redis predeterminado 6379.

## Ejecutar trabajos directamente en la máquina del ejecutor

Cuando ejecutes un trabajo directamente en la máquina del ejecutor, deberás asignar los puertos del contenedor de servicios a los puertos del host de Docker. Puedes acceder a los contenedores de servicios desde el host de Docker utilizando `localhost` y el número de puerto del host de Docker.

{% data reusables.actions.copy-workflow-file %}

```yaml{:copy}
name: Redis runner example
on: push

jobs:
  # Label of the runner job
  runner-job:
    # You must use a Linux environment when using service containers or container jobs
    runs-on: ubuntu-latest

    # Service containers to run with `runner-job`
    services:
      # Label used to access the service container
      redis:
        # Docker Hub image
        image: redis
        # Set health checks to wait until redis has started
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          # Maps port 6379 on service container to the host
          - 6379:6379

    steps:
      # Downloads a copy of the code in your repository before running CI tests
      - name: Check out repository code
        uses: {% data reusables.actions.action-checkout %}

      # Performs a clean installation of all dependencies in the `package.json` file
      # For more information, see https://docs.npmjs.com/cli/ci.html
      - name: Install dependencies
        run: npm ci

      - name: Connect to Redis
        # Runs a script that creates a Redis client, populates
        # the client with data, and retrieves data
        run: node client.js
        # Environment variable used by the `client.js` script to create
        # a new Redis client.
        env:
          # El nombre del host utilizado para comunicarse con el contenedor del servicio Redis
          REDIS_HOST: localhost
          # El puerto Redis predeterminado
          REDIS_PORT: 6379
```

### Configurar el trabajo del ejecutador

{% data reusables.actions.service-container-host-runner %}

{% data reusables.actions.redis-label-description %}

El flujo de trabajo asigna el puerto 6379 en el contenedor del servicio Redis al host Docker. Para obtener más información acerca de la palabra clave `ports`, consulta "[Acerca de los contenedores de servicio](/actions/automating-your-workflow-with-github-actions/about-service-containers#mapping-docker-host-and-service-container-ports)".

```yaml{:copy}
jobs:
  # Etiqueta del trabajo del ejecutor
  runner-job:
    # Debes usar un entorno Linux cuando utilices contenedores de servicio o trabajos de contenedor
    runs-on: ubuntu-latest

    # Contenedores de servicio para ejecutar con `runner-job`
    services:
      # Etiqueta usada para acceder al contenedor de servicio
      redis:
        # Imagen de Docker Hub
        image: redis
        # Establece revisiones de estado para esperar hasta que Redis haya comenzado
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          # Asigna el puerto 6379 en el contenedor de servicio al host
          - 6379:6379
```

### Configurar los pasos

{% data reusables.actions.service-template-steps %}

```yaml{:copy}
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: {% data reusables.actions.action-checkout %}

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to Redis
    # Runs a script that creates a Redis client, populates
    # the client with data, and retrieves data
    run: node client.js
    # Environment variable used by the `client.js` script to create
    # a new Redis client.
    env:
      # El nombre del host utilizado para comunicarse con el contenedor del servicio Redis
      REDIS_HOST: localhost
      # El puerto Redis predeterminado
      REDIS_PORT: 6379
```

{% data reusables.actions.redis-environment-variables %}

{% data reusables.actions.service-container-localhost %}

## Probar el contenedor de servicio Redis

Puedes probar tu flujo de trabajo usando el siguiente script, que crea un cliente Redis y rellena el cliente con algunos datos del marcador de posición. Luego, el script imprime los valores almacenados en el cliente Redis en el terminal. Tu script puede usar cualquier lenguaje que desees, pero este ejemplo usa Node.js y el módulo de npm `redis`. Para obtener más información, consulta el [Módulo Redis de npm](https://www.npmjs.com/package/redis).

Puedes modificar *client.js* para incluir cualquier operación de Redis que necesite tu flujo de trabajo. En este ejemplo, el script crea la instancia del cliente Redis, agrega datos de marcador de posición y luego recupera los datos.

{% data reusables.actions.service-container-add-script %}

```javascript{:copy}
const redis = require("redis");

// Crea un nuevo cliente Redis
// Si no se establece REDIS_HOST, el host predeterminado es localhost
// Si no se establece REDIS_PORT, el puerto predeterminado es 6379
const redisClient = redis.createClient({
  host: process.env.REDIS_HOST,
  port: process.env.REDIS_PORT  
});

redisClient.on("error", function(err) {
    console.log("Error " + err);
});

// Establece la clave "octocat" para un valor de "Mona the octocat"
redisClient.set("octocat", "Mona the Octocat", redis.print);
// Establece una clave "octocat", campo para "species" y "value" para "Cat and Octopus"
redisClient.hset("species", "octocat", "Cat and Octopus", redis.print);
// Establece una clave para "octocat", campo para "species" y "value" para "Dinosaur and Octopus"
redisClient.hset("species", "dinotocat", "Dinosaur and Octopus", redis.print);
// Establece una clave para "octocat", campo para "species" y "value" para "Cat and Robot"
redisClient.hset(["species", "robotocat", "Cat and Robot"], redis.print);
// Obtiene todos los campos en la clave "species"

redisClient.hkeys("species", function (err, replies) {
    console.log(replies.length + " replies:");
    replies.forEach(function (reply, i) {
        console.log("    " + i + ": " + reply);
    });
    redisClient.quit();
});
```

El script crea un nuevo cliente Redis utilizando el método `createClient`, que acepta un parámetro de `host` y `port`. El script usa el `REDIS_HOST` y variables de entorno `REDIS_PORT` para establecer la dirección IP y el puerto del cliente. Si `host` y `port` no están definidos, el host predeterminado es `localhost` y el puerto predeterminado es 6379.

El script usa los métodos `set` y `hset` para rellenar la base de datos con algunas claves, campos y valores. Para confirmar que el cliente Redis contiene los datos, el script imprime los contenidos de la base de datos en el registro de la consola.

Cuando ejecutas este flujo de trabajo, deberías ver el siguiente resultado en el paso "Conectar con Redis" que confirma que creaste el cliente Redis y agregaste datos:

```
Reply: OK
Reply: 1
Reply: 1
Reply: 1  
3 replies:
    0: octocat
    1: dinotocat
    2: robotocat
```