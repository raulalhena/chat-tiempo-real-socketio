# Chat Websocket

Creación de chat usando websockets y OAuth de Google.

## Background

Proyecto correspondiente a sprint del bootcamp de NodeJS de la IT Academy.

## Usage

Creación de sala de chat para la comunicación de diferentes usuarios.

Se han creado dos servidores HTTP, uno es la parte del **_Backend (/server, PORT 3000)_** donde se procesan las peticiones y el otro es el **_frontend (/client, PORT 4000)_** donde se gestiona la parte de la interacción con el usuario.

Se puede observar que el código está duplicado tanto en el lado servidor como cliente, esto es para agilizar los tests de cada uno de los servidores, ya que pueden usarse tanto de cliente como de servidor indistintamente.

## API/Component

Descripción de los componentes SERVER y CLIENT.

### Backend (Server) PORT: 3000

### Endpoint: /login

- **POST** - Recepción de datos enviados desde el formulario de login ( _/helpers/login.js - función loginUser(req, res, next)_ ):

  - Recibe:
    - Parametros:
      - username = String \- Requerido
      - password = String \- Requerido
  - Devuelve: JSON

    - code = Number (Código de estado HTML: **_200 OK, 400 SOLICITUD INCORRECTA, 500 ERROR SERVIDOR_**).
    - message = String \- 'success'.

    **Ejemplo:**

    ```JSON
    JSON:
    {
        "code": 200,
        "message": "success",
    }

    ERROR:
    {
        "code": 400,
        "message": "Usuario y/o contraseña incorrectos.",
    }
    ```

### Enpoint: /glogin

- **POST** - Recepción del token de sesión de Google ( _/controllers/logingoogle.js - función loginGoogleUser(req, res, next)_ ):

  - Recibe:
    - Parametros:
      - token = String \- Requerido
  - Devuelve: JSON

    - code = Number (Código de estado HTML: **_200 OK, 400 SOLICITUD INCORRECTA, 500 ERROR SERVIDOR_**).
    - message = String \- 'success'.

    **Ejemplo:**

    ```JSON
    JSON:
    {
        "code": 200,
        "message": "success",
    }
    ```

### Enpoint: /signup

- **POST** - Recepción de datos enviados desde el formulario de login ( _/helpers/login.js - función loginUser(req, res, next)_ ):

  - Recibe:
    - Parametros:
      - username = String \- Requerido
      - password = String \- Requerido
  - Devuelve: JSON

    - _id_ = Objeto \- \_id único de documento MongoDB.
    - username = String \- 'success'.
    - password = String \- Password encriptado

    **Ejemplo:**

    ```JSON
    JSON:
    {
        "_id": "619e89f8d670ae186cdbf172",
        "username": "raul1985",
        "password": "$2b$10$vSdNihZPJ/VGOhuZT4DmreicxAkp.BXOSyxXByuiLU1ln9nVTq9S2",
        "__v": 0
    }
    ```

### Endpoint: /logout

- **GET** - Elimina la sesión de usuario y redirecciona a la pantalla de login ( _/controllers/logout.js - función logout(req, res, next)_ ):

  - Recibe:
    - Parametros:
  - Devuelve: JSON

### Frontend (Client) PORT: 4000

### Endpoint: /

- **GET** - Muestra formulario de login (_/controllers/showLogin.js - función showLogin(req, res)_ ):

  - Recibe:
    - Parametros
  - Devuelve:
    - Render Handlebar: _/views/index.hbs_

### Endpoint: /signup

- **GET** - Muestra formulario de registro de usuario (_/controllers/signup.js - función showSignup(req, res)_ ):

  - Recibe:
    - Parametros
  - Devuelve:
    - Render Handlebar: _/views/signup.hbs_

### Endpoint: /chat

- **GET** - Muestra la sala de chat (_/controllers/chat.js - función showChat(req, res)_ ):

  - Recibe:
    - Parametros
  - Devuelve:
    - Render Handlebar: _/views/chat.hbs_
      - Uso de las variables de sesión: _user y picture_.

## Installation

Para el correcto funcionamiento se requiere de los siguientes tecnologías:

1. NodeJS
2. Express
3. MongoDB
4. Git

Para agilizar el desarrollo se ha utilizado el paquete _nodemon_ que se encuentra en las dependencias de desarrollo del paquete _package.json_.

Para poder instalar todo lo necesario a excepción del servidor MongoDB hay que seguir los siguientes pasos:

### \# Clonar repositorio

```shell
git clone https://github.com/raulalhena/chat-tiempo-real-socketio.git
```

### \# Instalación tanto en la carpeta /server como en /client

```shell
npm install
```

### \# Creación de archivo .env en el directorio raíz de las dos carpetas

```shell
touch .env
```

### \# El archivo .env del SERVIDOR tendrá las siguientes variables:

```shell
DB_HOST = localhost o 127.0.0.1
DB_NAME = nombre_de_bbdd
SESSION_SECRET = Secret de la configuración de OAuth en Google
GOOGLE_CLIENT_ID = ID del cliente de la configuración de OAuth en Google
```

### \# El archivo .env del CLIENTE tendrá las siguientes variables:

```shell
REMOTE_SERVER = http://localhost:3000
SESSION_SECRET = Secret de la configuración de OAuth en Google
GOOGLE_CLIENT_ID = ID del cliente de la configuración de OAuth en Google
```

### \# Ejecución del servidor

```shell
npm run dev
```

## Stack

1. NodeJS
2. Express
3. MongoDB

## Contact info

Contactame a mi email: raul.alhena@gmail.com

## License

GNU General Public License v3.0
[GNU](https://opensource.org/licenses/GPL-3.0)
