# Guía de desarrollo

### Agreupar por módulo y tipo


### Utilizar conveciones en nombre de eventos del componente

Utilizar nombres de eventos fijos que denoten la característica del evento.

- **onChange.** Emitido cuando la información del componente ha cambiado o en caso de una lista, cuando un elemento ha sido agregado, eliminado o modificado.

```javascript
//usuarios/components/template.html
<usuarios-usuario
  ng-repeat="item in $ctrl.lista"
  on-change="$ctrl.actualizarItem(item, $event.data)"></usuarios-usuario>
  
//usuarios/components/usuario/component.js
...
function UsuariosUsuarioComponent(UsuariosUsuarioService){

  ...

  function actualizar(){
    UsuariosUsuarioService.put($ctrl.idUsuario, $ctrl.data)
      .then(function(response){
        //Utilizamos el objeto $event para adjuntar toda la información emitida por el componente
        var event = {data: response.data};

        $ctrl.onChange({$event: event});
      });
  }
}
```

- **onClose.** Emitido cuando la información del componente ha cambiado o en caso de una lista, cuando un elemento ha sido agregado, eliminado o modificado.

```javascript
//usuarios/components/lista/template.html
<div ng-repeat="item in $ctrl.items">
  
<usuarios-lista-item

  on-change="$ctrl.actualizarItem(item, $event.data)"></usuarios-usuario>
</div>
  
//usuarios/components/usuario/component.js
...
function UsuariosUsuarioComponent(UsuariosUsuarioService){

  ...

  function actualizar(){
    UsuariosUsuarioService.put($ctrl.idUsuario, $ctrl.data)
      .then(function(response){
        //Utilizamos el objeto $event para adjuntar toda la información emitida por el componente
        var event = {data: response.data};

        $ctrl.onChange({$event: event});
      });
  }
}
```

### Utilizar sufijos

Utilizar el sufijo `Component` o `Service` en el nombre de la función. 

Ejemplo: UsuariosUsuarioComponent

### Utilizar UpperCamelCase

Utilizar el estilo UpperCamelCase al nombrar la función del componente o servicio para denotar que se trata de un constructor. 

Ejemplo: UsuariosUsuarioService

## Ejemplos

### Componente

```javascript
//usuarios/components/usuario/component.js
"use strict";

angular.module("usuarios")
  .component("usuariosUsuario", {
    templateUrl: "/usuarios/components/usuario/template.html",
    controller: UsuariosUsuarioComponent,
    bindings:{
      idUsuario: "<"
    }
  });
  
function UsuariosUsuarioComponent(UsuariosUsuarioService){
  var $ctrl = this;//Referencia al controlador
  
  $ctrl.$onInit = $onInit;//Utilizar hook $onInit para inicializar el componente
  $ctrl.actualizar = actualizar;//Definir al inicio del controlador sus métodos
  $ctrl.actualizando = false;//Definir al inicio del controlador sus variables
  $ctrl.error = null;
  $ctrl.usuario = undefined;
  
  function $onInit(){
    UsuariosUsuarioService.get($ctrl.idUsuario)
      .then(function(response){
        $ctrl.usuario = response.data;
      });
  }
  
  function actualizar(){
    if($ctrl.actualizando)
      return;
      
    $ctrl.actualizando = true;
    $ctrl.error = null;
    
    UsuariosUsuarioService.put($ctrl.idUsuario, $ctrl.data)
      .then(function(response){
        $ctrl.data = response.data;
      })
      .catch(function(response){
        $ctrl.error = response.data;
      })
      .finally(function(response){
        $ctrl.actualizando = false;
      });
  }
}
```

### Ruta

```javascript
/** usuarios/services/usuario/service.js **/
"use strict";

angular.module("usuarios")
  .config(function($stateProvider){
    $stateProvider.state("usuarios.usuario", {
      url: "/usuarios/{id_usuario}",
      template: "<usuarios-usuario id-usuario='idUsuario'/>",
      controller: function($scope, $stateParams){
        $scope.idUsuario = $stateParams.id_usuario
      }
    });
  });
```
