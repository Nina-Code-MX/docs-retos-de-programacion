# Reto API con Express.js

## 1. Descripción

El objectivo de esta actividad es crear una simple API en tu localhost que pueda recibir peticiones mediante un cliente (curl en la terminal o Postman).

La actividad se enfocará en crear un código simple con TypeScript, este Lenguaje basado en JavaScipt (no confundir con JAVA), es simple pero muy potente, permite crear applicaciones de forma sencilla con pocas lineas de código utilizando librerias de Node.

## 2. Instrucciones

El reto se componde de 4 pasos:

1. Crear un repositorio público (llamarlo como quieras) en Github, debes incluir un `README.md` una Licencia `GNU GENERAL PUBLIC LICENSE V3` y un archivo `.gitignore` para template de Node.
2. Crear una rama o branch llamada `development` (donde trabajaras con el código)
3. Generar una pequeña aplicación utilizando Node/Express.js la cual reciba peticiones externas y pueda responder con información.
4. Guardar los cambios (commit) y enviarlos a la branch de `development` en Github (push).

Lo que se validará es que el código que se ejecute funciona idénticamente en cualquier computadora que se clone, sea Windows, Mac o un Servidor de Linux.

## 3. Pre Requisitos

> ALTO: Para usuario de Windows, se facilitará mucho si instalan [Git Bash](https://gitforwindows.org/) para emular una terminal de Linux y seguir adecuadamente este reto.

### 3.1. Postman

Para poder probar recomiendo tener instalado en tu computadora la aplicación [Postman](https://www.postman.com/downloads/) que es un cliente de peticiones HTTP con interfaz gráfica, podemos probar también usando la Terminal, sin necesidad de un software Extra

### 3.2. Node Version Manager (NVM)

Este administrador de versiones de Node nos permitirá trabajar con diferentes versiones (dependerá mucho de los proyectos con los que trabajes), como no tenemos dependencias, instalaremos node en su última version (LTS o 20 a la fecha)

<details>
  <summary>Usuarios de MacOS</summary>
  
  <p>&nbsp;</p>
  
  Abre una terminal:
  
  ```bash
  brew install nvm
  ```
  
  <p>&nbsp;</p>
</details>

<details>
  <summary>Usuarios de Windows</summary>

  <p>&nbsp;</p>
  
  Descarga el instalador mas reciente en [Github de coreybutler](https://github.com/coreybutler/nvm-windows/releases)

  <p>&nbsp;</p>
</details>

Una vez instalado NVM, instalemos node en la versión 20, abre una terminal:

```bash
#
# La opción `--default` instalara de manera predetermina la version 20, así cada que iniciemos una terminal, automaticamente usara dicha versión.
#
nvm install --default 20
#
# Le indicamos que use la versión 20
#
nvm use 20
#
# Verificamos que la versión de node sea la 20
#
node --version
```

Si por alguna razón la versión no comienza con 20 o algun error al intentar instalarlo, puedes crear un `Issue` en la siguiente dirección https://github.com/Nina-Code-MX/docs-retos-de-programacion/issues

### 3.3. (Opcional) Visual Studio Code

Visual Studio Code ó VSCode, es una IDE o Entorno de Desarrollo Inegrado, facilitará la creación de archivos de código, también cuando estes escibiendo o copiando código te dara sugerencias. Puedes descargarla en aqui: https://code.visualstudio.com/download

## 4. El Código

Ua vez creado el repositorio, clonalo en tu computadora y cambiemos directorio al repositorio recien clonado.

Abre una terminal:

> ALTO: No olvide iniciar el `Agent SSH` y agregar tu llave.

```bash
# EJEMPLO

cd ~/
git clone git@github.com:Nina-Code-MX/docs-retos-de-programacion.git
cd docs-retos-de-programacion
```

> IMPORTANTE: Al directorio del proyecto nos referiremos de ahora en adelante como ROOT o Carpeta ROOT

Creamos una branch para development

```bash
git checkout -b development
```

En la carpeta ROOT, comenzaremos a inicializar el proyecto con npm (node package manager).

Ejecutamos:

```bash
npm init
```

Se ejecutara automaticamente un "Wizard" o un asistente de instalación, donde te preguntará que valores debe ir en cada elemento de la configuración, los únicos importantes a considerar será los siguientes:

```ini
main:    "src/index.ts"
author:  "<Tu Nombre|Correo|Sitio Web>"
license: "GPL-3.0-or-later"
```

Cualquier otro es a tu consideración.

### 4.1. Instalar las Librerias del Proyecto

Las librerias son códigos que ya existen que podemos re-utilizar para no tener que escribir demasiado o código muy complejo. En la carpeta ROOT:

```bash
#
# Instalará TypeScript Globalmente en tu sistema operativo, no solo en este proyecto.
#
npm install --global tsc
#
# Instalará las librerias principales en esta carpeta o proyecto
#
npm install express typescript
#
# Instalará herramientas de ayuda
#
npm install --save-dev typescript @types/express @types/node
```

### 4.2. Iniciar la configuración TypeScript

Para poder compilar sin problemas nuestro código, es necesario darle unos parametros de configuración, para ello en la carpeta de ROOT, crear un archivo llamado `tsconfig.json` y agrega la información abajo:

```json
{
  "compilerOptions": {
    "target": "es2016",
    "module": "commonjs",
    "rootDir": "./src",
    "outDir": "./build",
    "esModuleInterop": true,
    "strict": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*.ts"]
}
```

> IMPORTANTE: Esa es la configuración minima necesaria, existen más parametros que pueden configurar, pero para el objetivo de este reto, lo anterior es suficiente.

### 4.3. Crear el controlador saludos

En la carpeta ROOT crea el siguiete archivo (deberás crear las carpetas necesarias también):

`src/controllers/saludosController.ts`

Adentro, debes agregar el siguiente código:

```typescript
import { Request, Response } from 'express';

export const hola = async (req: Request, res: Response) => {
  res.status(200).json({messages: `Bienvenido a mi api`});
};

export const adios = async (req: Request, res: Response) => {
  res.status(200).json({messages: `Vuelve pronto a mi api`});
};
```

<details>
  <summary>Explicación: saludosController.ts</summary>

  <p>&nbsp;</p>

  - La línea #1 Importara de la libreria express las herramientas de `Request` y `Response`, `Request` contendrá la información solicitada por el cliente, mientras que `Response` será la información que nosotros enviaremos al cliente.
  - La línea #3 a #5 creamos y exportando una función llamada `hola`, que respondera con un estatus `200` y un mensaja dando la bienvenido.
  - La línea $7 a $9 creamos y exportando una función llamada `adios`, que respondera con un estatus `301` y un mensaja despidiendose.

  -> Ver [Códigos de estado de respuesta HTTP](https://developer.mozilla.org/es/docs/Web/HTTP/Status) para más información.
  <p>&nbsp;</p>
</details>

### 4.4. Crear las rutas de saludos

En la carpeta ROOT crear el siguiente archivo (deberás crear las carpetas necesarias también):

`src/routes/saludosRoutes.ts`

```typescript
import { Router } from "express";
import { hola, adios } from "../controllers/saludosController";

const router = Router();

router.get('/hola', hola);
router.get('/adios', adios);

export default router;
```

<details>
  <summary>Explicación: saludosRoutes.ts</summary>

  <p>&nbsp;</p>
  
  - La línea #1 Importará de la libreria express la herramienta `Router`, esta creará las rutas web o del api, que enlazarán a las funciones del controlador.
  - La línea #2 Importará las funciones `hola` y `adios` del controlador `saludosController`, es importante resaltar, que typesciprt no es necesario especificar la extensión del archivo.
  - La línea #4 Creará una variable constante (no puede cambiar una vez definida) que contendrá la información de las rutas.
  - La línea #6 Define que para poder ejecutar la función `hola` debe accederse a la ruta `/hola`.
  - La línea #7 Define que para poder ejecutar la función `adios` debe accederse a la ruta `/adios`.
  - La línea #9 Exporta el objecto `router` con la configuración de las rutas.

  <p>&nbsp;</p>
</details>

### 4.5. Crear ek archivo principal del servidor

En la carpeta ROOT crear el siguiente archivo (deberás crear las carpetas necesarias también):

`src/index.ts`

```typescript
import express from "express";
import saludosRoutes from "./routes/saludosRoutes";

const app = express();
const PORT = 3000;

app.use(express.json());
app.use('/', saludosRoutes);
app.listen(PORT, () => {
  console.log(`Inicie la aplicación en el puerto ${PORT}`);
});
```

<details>
  <summary>Explicación: index.ts</summary>

  <p>&nbsp;</p>

  - La línea #1 Importará en general la libreria `express` con todas sus funcionalidades.
  - La línea #2 Importará la ruta de saludos.
  - La línea #4 Creará una variable constante llamada `app` que inicializará `express()`.
  - La línea #5 Creará una variable constante llamada `PORT` que contendrá el número `3000`, es importante aclarar, que este Puerto no debe estar siendo utilizado por ninguna otra applicación en tu computadora.
  - La línea #7 Agregamos el parametro `use` para indicar que utilize el módulo de JSON de express.
  - La línea #8 Agregamos el parametro `use` para indicar que cuando alguien acceda a `http://localhost:3000` podrá tambien cargar ``http://localhost:3000/hola` y `http://localhost:3000/adios` del archivo `saludosRoutes.ts`
  - La línea #9 Finalmente, iniciamos el mini servidor escuchando en el puerto asignado.
  
  <p>&nbsp;</p>
</details>

## 5. Compilar y ejecutar

Si nuestro archivo `tsconfig.json` es correcto, podemos compilar nuestra aplicación ejecutando en una terminal en la carpeta de ROOT:

```bash
npx tsc
```

El comando anterior, compilará la información y la empaquetara en la carpeta `/build`, ahora es necesario levantar el servidor, en la carpeta de ROOT:


```bash
node build/index.js
```

Esti creara un servidor del app en localhost exponiendo el puerto elejido, ejemplo: `http://localhost:3000/hola` o `http://localhost:3000/adios`

## 6. QA y Testing Manual

Para probar que nuestra aplicación esta funcionando, abrimos la applicación de escritprop `POSTMAN` y creamos una nueva petición:

### 6.1. Validar la ruta `/hola`

1. Tipo `GET`
2. URL `http://localhost:3000/hola`

Al enviar la petición, todo deberia funcionar, la aplicación se ejecutará y mostrará el mensaje: `Bienvenido a mi api` y con un estado de HTTP de 200.

### 6.2. Validar la ruta `/adios`

1. Tipo `GET`
2. URL `http://localhost:3000/adios`

Al enviar la petición, todo deberia funcionar, la aplicación se ejecutará y mostrará el mensaje: `Vuelve pronto a mi api` y con un estado de HTTP de 301.

## 7. Enviar los cambios a Github

Antes de enviar cambios, revisemos nuevamente nuestro archivo `.gitignore`, es importante verificar que la carpeta `/node_modules` y la carpeta `/build` esten agregadas en este archivo.

¿Pero por qué? Te preguntarás. Bueno, para empezar la carpeta de node_modules, contienen millones de archivos, que no queremos agregar al repositorio de Github, ya que, clonandolo y ejecutando `npm install` podremos re generar y descargar nuevamente.

Y la carpeta de `buidl` contiene el código fuente compilado, este código no es relevante, de igual manera, al ejecutar `tsc` en cualquier otro ordenador que haya clonado tu repositorio, compilara nuevamente esos archivos.

Una vez validado, enviar los cambios a Github, puedes hacerlo de dos maneras:

### 7.1. Terminal

En la carpeta root, ejecuta los siguientes comandos:

```bash
git add .
git commit -m "Mi primero código"
git push -u origin development
```

### 7.2. VSCode 

Si estas utilizando VSCode, este viene integrado con una interfaz para Git, podrás ver los archivos creados, modificados, etc. Puedes visualiar los cambios, seleccionar de forma sencilla, agregar un `commit message` y publicar (push) los cambios de manera sencilla.

Lo encontraras con el logotipo de Git en la parte lateral izquiera

## 8. Notas Finales

Si bien este ejemplo solo es informativo, servirá de base para los siguientes retos.

Node o TypeScript no se limitan a las carpetas `controllers` o `routes` esto es simplemente para poder organizar los archivos.

Cualquier duda, hazla llegar a soporte@ninacode.mx

