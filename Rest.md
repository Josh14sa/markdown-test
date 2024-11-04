# ARQUITECTURA REST 
**1- PRINCIPIOS DE DISEÑO REST**
* Es una arquitectura ampliamente utilizada para crear interfaces de programación 
de aplicaciones (APIs) basadas en el protocolo HTTP. 
* Las APIs construidas siguiendo los principios de REST se denominan 
comúnmente ‘API RESTful’.
* El concepto de REST fue introducido en el año 2000 por Roy Fielding, quien es 
reconocido por su contribución a la especificación HTTP.

#### Roy Fielding basó la construcción y diseño de REST en los siguientes principios, que se describen a continuación: 
1. **Cliente-servidor:** 
* El cliente y el servidor deben estar completamente separados e independientes. La única 
forma de comunicación debe ser mediante solicitudes HTTP.

2. **Sin estado (stateless):** 
* Nota importante: En un esquema de autorización, el servidor no guarda el "estado" de la 
sesión del usuario. Toda la información de autenticación viaja dentro del token en cada 
solicitud, manteniendo así la arquitectura sin estado.

* Este ejemplo ilustra cómo una API RESTful sin estado maneja la autenticación: el servidor 
no guarda sesiones o información del cliente entre solicitudes; toda solicitud contiene la 
información necesaria para que el servidor pueda procesarla independientemente. 

3. **Identificador único (URI):**
* Todo recurso debe tener un identificador irrepetible, no puede existir dos o más recursos 
con el mismo identificador en la red y estos deben mantener una jerarquía lógica.

4. **Uso correcto de HTTP:**
* REST debe respetar tanto los verbos y códigos de estado para cada operación (GET, 
POST, PUT, DELETE, PATCH, etc.).

**2- REGLAS DE DISEÑO REST**
1. **Uso correcto de verbos y código de estado HTTP.**

- **GET**: Recupera un recurso.
  - **Descripción**: Se utiliza para solicitar la representación de un recurso específico. No debe modificar el estado del recurso en el servidor.
  - **Códigos de Estado**:
    - **200 OK**: Solicitud exitosa, se devuelve el recurso solicitado.
    - **404 Not Found**: El recurso solicitado no se encuentra en el servidor.

- **POST**: Crea un recurso nuevo.
  - **Descripción**: Se utiliza para enviar datos al servidor con el fin de crear un nuevo recurso.
  - **Códigos de Estado**:
    - **201 Created**: Recurso creado exitosamente.
    - **400 Bad Request**: La solicitud tiene un formato incorrecto o faltan datos necesarios para crear el recurso.
    - **500 Internal Server Error**: Error en el servidor al intentar crear el recurso.

- **PUT**: Actualiza un recurso existente.
  - **Descripción**: Se utiliza para modificar un recurso ya existente en el servidor. Si el recurso no existe, algunos servicios pueden crear uno nuevo.
  - **Códigos de Estado**:
    - **200 OK**: El recurso fue actualizado exitosamente.
    - **404 Not Found**: El recurso que se intenta actualizar no existe.
    - **400 Bad Request**: La solicitud tiene un formato incorrecto o datos no válidos.
    - **500 Internal Server Error**: Error en el servidor al intentar actualizar el recurso.

- **DELETE**: Elimina un recurso.
  - **Descripción**: Se utiliza para eliminar un recurso específico del servidor.
  - **Códigos de Estado**:
    - **204 No Content**: El recurso fue eliminado exitosamente, no se devuelve contenido.
    - **404 Not Found**: El recurso que se intenta eliminar no existe.
    - **400 Bad Request**: La solicitud es inválida o no cumple con los requisitos para eliminar el recurso.
    - **500 Internal Server Error**: Error en el servidor al intentar eliminar el recurso.


2. **Versionado del Servicio**
- **GET**: /api/v1/productos   
- **GET**: /api/v2/productos 

3. **Uso de Sustantivos en Puntos Finales y Nombres en Plural**
- **GET**: /api/usuarios  
- **GET**: /api/usuarios/123 

4. **Uso Correcto de Filtrado, Clasificación y Paginación**
- **GET**: /api/productos?categoria=electronica&orden=precio_asc&pagina=1&limite=10

5. **Diseño de URL con Patrones Lógicos y Jerarquía**
- **GET**: /api/productos/1/comentarios con ID 1 
- **POST**: /api/productos/1/comentarios 


**3- SEGURIDAD EN API REST**
1.  Utilización de Cupos y Límites
2. Utilización de Puertas de Enlace (API Gateways)

*Ejemplo*
* Un usuario envía una solicitud a https://miapp.com/api/productos. El API Gateway:
    *  Autentica: Verifica el token o credenciales.
    * Controla el tráfico: Aplica limitación de tráfico para prevenir abusos. 
    * Redirecciona: Enruta la solicitud al servicio correspondiente. 
3. Uso de HTTPS 

*Ejemplo*

* **URL Segura:**
    * https://miapp.com/api/productos 

* **Redirección:** 
    * HTTP/1.1 301 Moved Permanently
    * Location: https://miapp.com/api/productos

4. **Implementación de Autenticación y Autorización**
* Se pueden usar tokens JWT (JSON Web Token) o protocolos de autenticación como OAuth 
2.0. 

*Ejemplo*

* **AUTENTICACIÓN:** 

    * El cliente envía sus credenciales al endpoint de autenticación:

    ```java
    POST /api/auth/login 
    Content-Type: application/json 

    { 
        "username": "user123", 
        "password": "mypassword" 
    }
    ```

   * El servidor valida las credenciales y responde con un token JWT:

    ```java
    HTTP/1.1 200 OK 
    Content-Type: application/json 

    { 
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
    ```

* **AUTORIZACIÓN:** 
    * Para acceder a un recurso protegido, el cliente debe incluir el token en el 
encabezado de la solicitud

    ```java
    GET /api/productos

    Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
    ```

## Enlaces de referencias
[medium.com](https://medium.com/@diego.coder/introducci%C3%B3n-a-las-apis-rest-6b3ad900acc9 "guía para programadores")



