# Introducción

El programa Centinela es un programa de tracker para DHIS2 que registra datos de eventos de Efectos adversos supuestamente atribuíbles a la vacunación e inmunización (ESAVI) y efectos adversos de interés especial (EVADIE). Ha sido configurado basado en las directrices generales de la OPS y la OMS para ESAVIS. AGREGAR LINKS A DOCUMENTACIÓN.

El programa cuenta con los catálogos de CIE, MEDDRA y WHODrug y esta mapeado a los requerimientos para transmición de datos a la base de datos mundial de farmacovigilancia.

## Acceso a producción

LINK A LA INSTANCIA

CORREO DE SOPORTE por país/regional?


## Contenido

El paquete del progama centinela cuenta con un componente de entrada de datos con validaciónes y reglas de programa, así como una lista de indicadores calculados basados en los datos ingresados y tableros con visualización de esos datos. 

### Entrada de datos

La entrada de datos está basada en el app core de DHIS2 [Tracker](https://dhis2.org/tracker/) que captura datos individuales longitudinales basados en eventos divididos en etapas no-repetibles. Las etapas han sido configuradas con formularios personalizados. Para información general acerca de como utilizar tracker, ver la [documentación] (https://docs.dhis2.org/en/use/user-guides/dhis-core-version-master/tracking-individual-level-data/tracker-capture.html).

#### Flujo de trabajo

![Diagrama del flujo de trabajo](resources/images/flujo.png) 

#### Etapas
El programa Centinela está dividido en cinco etapas. Para un resúmen de como ingresar datos, véase la guía rápida de uso del programa: LINK A QUICKGUIDE

##### Etapa de clasificación inicial

En esta etapa se determina si el evento es un ESAVI o EVADIE basado en una serie de preguntas. Dependiendo de la clasificación inicial se habilitarán las etapas correspondientes.

##### Etapa EVADIE

Solamente estaría disponible cuando el evento corresponde a un EVADIE.

##### Etapa Notificación ESAVI

La etapa de notificación ESAVI solo está disponible cuando ele vento corresponde a un ESAVI

##### Etapa Investigación ESAVI

La etapa de investigación ESAVI solamente cuando es especificado que el evento requiere una investigación.

#### Etapa Clasificación final

Esta etapa normalmente es accesible solamente a nivel distrito o nacional, y es donde se confirman los resultados del ESAVI y la clasificación final

### Analíticas

DHIS2 calcula indicdores bsados en los datos y genera visualizaciones preconfiguradas que son principalmente mostradas en los tableros de información. Usuarios, dependiendo de su acceso, pueden crear sus propias visualizaciónes, mapas gráficas e indicadores.

Los indicadores en DHIS2 son cálculos basados en elementos de datos, y se dividen en indicadores simples (Numerador/denominador) e indicadores de programa (basados en un conteo por filtros). Elementos de datos que puedan accederse sin tener que incluír calculos o filtros sona gregados automaticamente. Por mas información acerca de indicadores e indicadores de programa en DHIS2 ver la documentación.
 
#### Indicadores de programa
Documentación: https://docs.dhis2.org/en/use/android-app/program-indicators-supported.html 
Lista de indicadores incluídos: XXXXX

#### Indicadores 
Documentación: https://docs.dhis2.org/en/implement/database-design/aggregate-system-design/indicators.html#:~:text=In%20DHIS2%2C%20the%20indicator%20is,do%20not%20have%20a%20denominator.
Lista de indicadores incluídos: XXXXX

#### Tableros

LISTA DE TABLEROS INCLUÌDOS CON DESCRIPCION GENERAL 

##  Acceso, usuarios y roles
 
En DHIS2, el tipo de acceso de un usuario está determinado por tres elementos básicos: 
 
El rol del usuario  
El grupo del usuario  
Las unidades organizativas a las que el usuario tiene acceso

Un usuario podrá  tener más de un rol, y formar parte de más de un grupo de usuarios para de esa manera obtener el acceso necesario para desempeñar su tarea. Por mas información ver [la documentación de DHIS2](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-236/configuring-the-system/users-roles-and-groups.html)

Dentro de un programa, el tipo de acceso es configurable a todo el programa o a cada etapa de programa. Un programa podrá otorgarle distintos niveles de acceso a distintos grupos de usuario. Además, el acceso de búsqueda en general también puede configurarse basado en el programa.



### Configuración de búsqueda

El programa está configurado como protegido para proteger los datos de identificación personal del acceso no autorizado. Esto significa que un usuario puede editar y ver personas que son propiedad de la(s) unidad(es) de la organización a las que el usuario tiene asignado acceso de captura de datos, pero su alcance de búsqueda debe ser más amplio que su alcance de lectura/escritura para garantizar que identificarán cualquier persona ya existente durante una búsqueda, incluso si no pertenecen a su unidad organizativa. Si la búsqueda devuelve una persona que ya exista fuera de su unidad organizativa, se le presenta al usuario la opción de acceder al registro del paciente, debiendo primero justificar el acceso. Este enfoque de la privacidad se conoce como 'romper el cristal' (COMO SE TRADUCE ESTO???) , ya que permite que el usuario tome la decisión de acceder al registro sin permiso o asistencia externa, pero deja un rastro claro para ser auditado. Una vez que el usuario da una razón para romper el vidrio, obtiene la propiedad temporal de la instancia de la entidad rastreada (consulte la Guía del usuario de Tracker para obtener más información).

Los usuarios que completarán la etapa de clasificación final probablemente estarán basados a nivel nacional o de distrito. Para atribuir correctamente los datos a la unidad organizativa donde se administró la inmunización, este usuario a nivel de distrito/nacional debe tener acceso de lectura/escritura a todas las unidades organizativas de las que es responsable.

### Unidades organizativas:

Son configuradas por usuario y por programa determinan el acceso que pueda tener el usuario dentro del organigrama. 
Una persona que tenga acceso a una unidad que tenga mas niveles por debajo, por lo general tendrá también acceso a esos niveles.
Recomendamos que en esta implementación los usuarios de entrada de datos solo tengan acceso a su propia unidad organizativa, y que se determine según su rol que nivel de acceso deberán tener los usuarios que trabajen en capacidad nacional o regional. 



### Roles de usuario:

En los roles de usuario se pueden configurar de manera granular, a que aplicaciones (Por ejemplo, entrada de datos, Mapas, etc) y permisos (por ejemplo, crear, borrar, modificar, etc) tiene acceso.
A nivel de instancia deberá haber al menos un superusuario que tenga acceso a todas o a la mayoría de las acciones. 
Pero por lo general, los roles de usuario solamente deberán tener acceso al mínimo número de acciones necesarias para su función.
Los roles de usuario que recomendamos para esta implementación son los siguientes:


#### **Usuario de Entrada de datos - Tracker (Sin acceso a borrar una TEI)
 
Personas con este rol podrán ingresar datos y registrar personas tracker pero no podrán borrar eventos o registros de personas 


#### **Usuario de Entrada de datos - Tracker**

Personas con este rol podrán ingresar datos y registrar personas tracker y además podrán borrar eventos o registros de personas

#### Supervisor (de país/distrito) *

Este usuario podrá acceder y editar todos los datos dentro de tracker. COmbinar con las org units necesarias para asignarles un distrito/pais 

#### Creación y edición de usuarios
Este rol permitirá crear y editar usuarios existentes. Es recomendado que cada país distribuya este rol como sea conveniente. 


#### Configurador de metadatos
Acceso a la app de mantenimiento para modificar programas, elementos de datos, indicadores, etc. 

#### Superusuario Regional
Acceso a todos los roles. Este acceso debería ser restringido al minimo de usuarios en la instancia de producción  



### Grupos de usuario:

 Los grupos de usuario sirven para dar acceso a los distintos programas (por ejemplo, el programa de ESAVI o el Programa Centinela). Y regular que nivel de acceso tienen los usuarios dentro de ese grupo al programa. 
El nivel de acceso está basado en datos y metadatos, y en poder ver o editar, y deberá ser combinado con el rol de usuario y aceso a la unidad organizativa correspondiente.

Para una implementación regional, se recomiendan las siguientes combinaciones de grupo de usuario / rol / acceso a unidad organizativa, que deberán replicarse para acada programa.


| User group                | Descripción                                                               | Org unit access                                       | Datos                    | Metadatos    | Analytics    | Roles                                                                 |
|---------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|--------------------------|--------------|--------------|-----------------------------------------------------------------------|
| Data entry                | Usuario final                                                             | Unidad propia                                         | Ver y editar (No borrar) | Ver          | Sin acceso   | Usuario de Entrada de datos - Tracker (Sin acceso a borrar una TEI)   |
| Data Entry Supervisor     | Igual que usuario final, pero podrá borrar TEIs ni enrollments            | Unidad propia /distrito                               | Ver y editar ( borrar)   | ver          | ver          | Usuario de Entrada de datos - Tracker Supervisor (de país/distrito) * |
| Data analysis             | Tendrá acceso a visualizaciones e indicadores                             | Unidad propia                                         | Ver                      | Ver          | Ver          | Usuario de Entrada de datos - Tracker                                 |
| Data audit nacional       | Podrá ver todos los datos y quién los ha ingresado pero no editarlos      | Unidades del país                                     | Ver                      | Ver          | Ver          | Supervisor (de país/distrito) *                                       |
| Metadata Admin (OPS)      | Podrá editar los formularios, tableros e indicadores, pero no ver datos   | Todas                                                 | Sin Acceso               | Ver y Editar | Ver y Editar | Configurador de metadatos                                             |
| Administrador de usuarios | Podrá crear y asignar usuarios a distintos roles y unidades organizativas | Unidades del país /Distrito/propias segun corresponda | NO                       | NO           | NO           | Creación y edición de usuarios                                        |
| Superusuario              | Si                                                                        | Todas                                                 | Ver y Editar             | Ver y Editar | Ver y Editar | Todas                                                                 |


