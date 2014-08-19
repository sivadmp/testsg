# Política de desarrollo

La Unidad de Innovación y Desarrollo de la ADSIB sigue esta política para todos sus proyectos de desarrollo de sistemas.

## Metodología de programación

* solo desarrollaremos en lenguajes que tengan estas características:
** Eficiencia para el proyecto: tiempo para llegar al producto final
** Difundido: facilidad de mantenimiento por otras personas
** Entorno servidor: facilidad de desplegar en servidores

* modular: desarrollar por módulos, y con APIs REST / estándar / web servicio
* KISS: poner solo lo necesario en cada módulo. Si no es absolutamente necesaria una funcionalidad, no ponerla. En efecto, una vez desarrollada y utilizada, una funcionalidad dificilmente puede sacada, y entonces se tiene que hacer el mantenimiento para siempre (ie. menor deuda de código posible en cada proyecto).
* elegir tecnologías web, o justificar si se hace desarrollo para una plataforma en particular (Android, Linux...)
* por omisión para sistemas cliente/servidor: Modelo - Vista - Controlador

## Lenguajes del lado del servidor

### PHP

Framework:
* entre phalcon y laravel

Utilitarios de desarrollo:
* Tests unitarios: phpunit
* Integración continua: jenkins + sonar
* Deploy: jenkins

Entorno servidor:
* Versión de PHP: >=5.3
* Servidor de aplicación: Apache2

### Java

Framework de desarrollo:
* Controladores: Spring
* ORM (mapeo de objetos relacional): hibernate

Utilitarios de desarrollo:
* gestión de proyecto: maven
* tests unitarios: JUnit
* tests de integración referencial: ???
* integración continua: Jenkins + Sonar

Entorno servidor:
* versión maquina virtual: openjdk 6 o 7
* servidor de aplicación: Tomcat

### Ruby

Framework de desarrollo:
* ruby on rails

Gemas de desarrollo:
* imágenes: carrierwave
* autenticación de usuarios: devise
* autorización de usuarios: cancan
* preprocesadores/templates de HTML: haml

Utilitarios de desarrollo:
* gestión de proyecto: gema bundler
* tests unitarios: gema rspec
* tests de integración referencial: gema rspec
* deploy: gema capistrano

Entorno servidor:
* versión de ruby: >=2
* servidor de aplicación: passenger con Apache2 (o passenger con nginx, o unicorn)

### Python

Experimental

Framework:
* django?
* falcon?

Entorno servidor:
* version de python: >=2.7
* servidor de aplicaciones: unicorn, passenger?

### Javascript

Experimental

Framework:
* expressJS?

Utilitarios de desarrollo: ?
* experimental: "CoffeeScript":http://coffeescript.org/ lenguaje de programación que se compila en JavaScript

Entorno servidor:
* servidor de aplicaciones: node.js

## Vistas

Para la parte del diseño, utilizar el framework bootstrap
Para la parte de la vistas, se utilizara los frameworks JavaScript
* AngularJS
* ...

## Bases de datos

* Se debe respetar los principios de: eficiencia, ancha difusión y entorno servidor + respetar la norma ANSI SQL 92.
* Modelo de datos: por omisión versionar todo (inmutable). No hacerlo si es insulso.
* Contar con un archivo SQL con los datos de la BD, para ser importados en ambientes de test.
* Opciones: MariaDB/MySQL, PostgreSQL 9.0, SQLite
* experimental: CouchDB, MongoDB, Redis

## BPM Business Process Management

Es una metodología que permite analizar el comportamiento de la organización a través de los procesos.
“Se llama Gestión de procesos de negocio (Business Process Management o BPM en inglés) a la metodología corporativa cuyo objetivo es mejorar la eficiencia a través de la gestión de los procesos de negocio, que se deben modelar, organizar, documentar y optimizar de forma continua.

### *Java*

Para el lenguaje Java existen muchas herramientas, la mas conocida es la librería que es desarrollada por RedHat JBPM
Una lista completa de librerías se encuentra disponible en "workflow-engines":http://java-source.net/open-source/workflow-engines

### *PHP*

* http://camunda.github.io/camunda-bpm-php-sdk/

### *Ruby*

* https://github.com/bokmann/stonepath
* http://ruote.io/
* https://github.com/yamilurbina/processmaker_gem
* https://github.com/bmedici/rbpm

### *JavaScript*

* http://code.google.com/p/oryx-editor/
* http://activiti.org/community.html
* http://www.pleus.net/blog/?p=2142
* https://github.com/dmitryfar/diagram-viewer
* https://github.com/camunda/camunda-bpmn.js

### *Python*

* https://code.djangoproject.com/wiki/GoFlow
* https://github.com/rbarrois/xworkflows/
* http://sourceforge.net/projects/maymyo/
* http://pyke.sourceforge.net/

### *Suites*

* "Bonita":http://www.bonitasoft.com/ 
* "Processmaker":http://www.processmaker.com/community-2
* "Cuteflow":http://www.cuteflow.org/index.html
* "Joget Workflow":http://www.joget.org/
* "Orchestra":http://orchestra.ow2.org/xwiki/bin/view/Main/

### *Doc. consultada*

* http://holisticsecurity.wordpress.com/2011/07/21/jbpm-bonita-intalio-processmaker-activiti-que-bpm-suite-uso/
* http://openwebstuff.com/best-open-source-bpm-solutions/


## Versionamiento

* versionar todo con git
** utilizar el modelo gitflow: http://nvie.com/posts/a-successful-git-branching-model/
** código en gitlab.geo.gob.bo, luego eventualmente en github.com, bitbucket o softwarelibre.gob.bo según necesidades
** proceso de integración de los commits en la rama principal: con "pull request", revisada y aceptada por los lideres del proyecto. Salvo excepción nunca aceptar su propia PR.

## Gestión de proyecto

* redacción de requerimientos en la wiki + vínculo en las tareas
* asignación de tareas con "issues", con un hito (milestone) y una prioridad
* cada issue debe contar, con el número de versión+(build) del sistema.
* cada issue debe hacer referencia al número de version+(build) en la cual fue resuelto
* números de versiones: utilizar el modelo x.y.z, con x: versión con ruptura de compatibilidad, y: versión menor con nuevas funcionalidades, z: corrección de bug
* despliegue continuo: cada rama tiene su versión de demostración disponible a cada instante en el servidor de prueba (http://css-tricks.com/continuous-integration-continuous-deployment/)
* sistema de "automated rollback": poder volver a una versión anterior del código y de los datos
* redmine/chiliproject/openproject? Debe tener:
** autenticación LDAP o SSO
** integración con gitlab y github
** wiki, issues, gantt, archivos (o relación con owncloud para archivos)
** acceso remoto a las tareas por caldav

## Calidad de código

Idiomas:
* contemplar internacionalización del código fuente, en un principio solo para el idioma español.
* comentarios: en español
* nombres de variables: en español
* mensajes de commit: en español

Pruebas:
* escribir tests unitarios de los métodos críticos
* despliegue continuo: cada commit provoca una construcción del proyecto, con sus tests unitarios
* utilizar herramienta de control del código (Sonar)
* el número de version+(build) debe actualizarse cada que se haga un deploy.
* adicionar el numero de versión+(build) a todos los módulos del sistema. Este número es para hacer seguimiento a las tareas y bugs del sistema.
* experimental: tests de integración, test de interfaz de usuario (testing UI)

## Documentación

* poner mínimamente los archivos siguientes a la raíz del proyecto:
** README.md: presentación del proyecto, vínculos a otras docs
** INSTALL.md: documentación de instalación / compilación / despliegue del proyecto, con requisitos y vínculos a las librerías externas utilizadas
* documentación de desarrollo: generación automática con comentarios en el código (tipo doxygen, sphinx, rdoc, javadoc) + instrucciones en INSTALL.md para compilar la documentación
* comentarios en el código: aparte de los comentarios de documentación, solo poner comentarios cuando es necesario para entender un bloque de código complicado. Sino, el código basta.

## Licencia

* todo con licencia LPG Bolivia: http://www.softwarelibre.gob.bo/licencia.php
* poner un archivo LICENSE.md a la raíz del proyecto, con el contenido de la licencia.
* solo se pueden utilizar librerías de software libre.
* colocar la licencia, en cada archivo del proyecto (siguiendo la misma lógica de la mayoría de los proyectos OpenSource).
* solo usar imágenes, fuentes, etc. de licencia abierta

## Interfaz de usuario

* para sitios públicos: aplicar el principio de "mejora progresiva" (progressive enhancement): por ejemplo estructura HTML funcional sin CSS ni Javascript, y la experiencia del usuario mejora si su navegador permite CSS y JS - Unobtrusive Javascript ("Javascript no obstructivo":http://es.wikipedia.org/wiki/JavaScript_no_obstructivo)
* diseñar la interfaz con "mockups" en formato digital - pencil project
* experimental: CSS: utilizar preprocesadores (SCSS, SASS, STYLUS, KNACSS, LESS)
* experimental: CSS: unidades "em/rem" para las dimensiones
