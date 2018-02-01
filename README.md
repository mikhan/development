#Guía de desarrollo


## Flujo

- El punto de acceso es el archivo .htaccess, en donde seindica que cualquier solicitud de carpeta no encontrada 
se redirija al archivo index.html

- El archivo index.html carga todos los scripts y stylesheets de módulos y librerías requeridos para visualizar la página. 
Cada módulo define sus componentes, servicios y rutas.

- El archivo main.js inicializa el módulo app

- El módulo contiene el componente `app`, el cual contiene un elemento con la directiva `uiView`

- La direciva `uiView` observa la url y localiza el `state` que coincide con ésta.

- Se compila un elemento utilizando las propiedades template y controller del state y se inserta en el elemento que contiene la directiva uiView
Si en el elemento insertado se encuentra un uiView, se repite este proceso hasta que no haya más uiViews o no se obtenga coincidencia
con los states configurados


## Módulos

### Módulo `main`

Ubicar en el módulo `main` las rutinas para configurar el entorno e inicializar angular.
El módulo `main` no configura rutas ni define componentes o servicios.

### Módulo `app`

Ubicar en el módulo `app` la configuración principal de la aplicación, así como los components y servicios específicos al funcionamiento global de ésta.
Aquí se encontrará toda la lógica para iniciar y terminar sesión.

Declarar el state `app.inicio` para la url "". Este state cargará el componente `<app-inicio/>`, 
Aquí se ubicará la interface de bienvenida al usuario.

Declarar el state `app.dashboard` para la url "/dashboard" y cargar el componente `<app-dashboard/>`
Aquí se ubicará el panel principal de la aplicación con los accesos a los diferentes módulos.

### Archivo `module.js`

Cada módulo contiene en su raiz un archivo `module.js`. La función de este archivo será únicamente declarar el módulo

### Archivo `config.js`

Si es necesario realizar una configuración, declarar variables o constantes, generar un archivo `config.js`
y utilizar el bloque correspondiente para ese propósito. 

### Agrupar en subcarpetas por característica

Ubicar cada archivo en subcarpetas dentro de cada módulo según su función.

- Componentes: /components
- Servicios: /services
- Rutas: /routes


## Estilo de código

### Utilizar sufijos

Utilizar el sufijo `Component` o `Service` en el nombre de la función.

Ejemplo: UsuariosUsuarioComponent

### Utilizar UpperCamelCase

Utilizar el estilo UpperCamelCase al nombrar la función del componente o servicio para denotar que se trata de un constructor.

Ejemplo: UsuariosUsuarioService

## Utilizar modalidad estricta

Especificar `use strict` al inicio de cada documento

### IIFE (Immediately Invoked Function Expression)

Para mantener el código visualmente "limpio" escribir todo sin necesidad de encapsularlo en una IIFE, 
pero encapsularlo al momento de compilar y minificar. 
