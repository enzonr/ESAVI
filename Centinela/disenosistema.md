# Seguridad


##  Los desafíos/premisas a responder son:



* cómo lograr un nivel de seguridad adecuado para la base de datos con datos sensibles (personales y de salud) de una organización internacional, con el objetivo de prevenir brechas de seguridad y daño reputacional (encriptación de BBDD no sería posible; encriptación de datos personales presentes como tracked entity attributes es posible, pero tiene consecuencias negativas en la búsqueda desde Tracker; encriptación de data elements no sería posible?)
* cómo lograr que los países sólo puedan ver los datos correspondientes a su país, sin importar el nivel de acceso/tipo de rol que se les provea. Debería respetar las OrgUnits de cada país, pero quedar también muy claro en otras configuraciones como Search settings, etc.
* cómo lograr que PAHO vea los datos de todos los países, pero no vea los datos de identificación de pacientes y profesionales (nombre, apellido, ID nacional, dirección, teléfono, email, entre otros).
* cómo elaborar una política de seguridad de OPS para DHIS2. Pedir ejemplos de documentos/políticas de seguridad (reales) de otras organizaciones en situaciones similares: PSI, países, etc.


##  Acceso, usuarios y roles
 
En DHIS2, el tipo de acceso de un usuario está determinado por tres elementos básicos: 
 
El rol del usuario  
El grupo del usuario  
Las unidades organizativas a las que el usuario tiene acceso.

 
Un usuario podrá  tener más de un rol, y formar parte de más de un grupo de usuarios para de esa manera obtener el acceso necesario para desempeñar su tarea.
 
Por mas información ver [la documentación de DHIS2](https://docs.dhis2.org/en/use/user-guides/dhis-core-version-236/configuring-the-system/users-roles-and-groups.html)


## Unidades organizativas:

Son configuradas por usuario y determinan el acceso que pueda tener el usuario dentro del organigrama. 
Una persona que tenga acceso a una unidad que tenga mas niveles por debajo, por lo general tendrá también acceso a esos niveles.
Recomendamos que en esta implementación los usuarios de entrada de datos solo tengan acceso a su propia unidad organizativa, y que se determine según su rol que nivel de acceso deberán tener los usuarios que trabajen en capacidad nacional o regional. 


## Roles de usuario:

En los roles de usuario se pueden configurar de manera granular, a que aplicaciones (Por ejemplo, entrada de datos, Mapas, etc) y permisos (por ejemplo, crear, borrar, modificar, etc) tiene acceso.
A nivel de instancia deberá haber al menos un superusuario que tenga acceso a todas o a la mayoría de las acciones. 
Pero por lo general, los roles de usuario solamente deberán tener acceso al mínimo número de acciones necesarias para su función.
Los roles de usuario que recomendamos para esta implementación son los siguientes:


#### **Usuario de Entrada de datos - Tracker (Sin acceso a borrar una TEI)
 
**Personas con este rol podrán ingresar datos y registrar personas tracker pero no podrán borrar eventos o registros de personas 

Acceso (add/update public):
Etapa de programa 
Valor de datos 

Acceso (add/update private): 
Informe de evento  
Mapa 
Tabla de eventos 
Tablero 
Visualización 
 
Acceso (Delete)

Informe de evento (privte) 
Mapa (private) 
Tabla de eventos (private) 
Mapa (Private) 
Visualización (private) 
Valor de datos (Public) 
 
Aplicaciones: 
Tracker Capture app 
 
Tracker(Rastreador) 
Search tracked entity instance in all Org units 
Update tracked entities 
 
Importar/exportar: 
-sin acceso 
Sistema: 
-sin acceso


#### **Usuario de Entrada de datos - Tracker**

Personas con este rol podrán ingresar datos y registrar personas tracker y además podrán borrar eventos o registros de personas

Acceso (add/update public): 
Etapa de programa 
Valor de datos 
 
 
Acceso (add/update private): 
Informe de evento  
Mapa 
Tabla de eventos 
Tablero 
Visualización

Acceso (Delete)

Informe de evento (private) 
Mapa (private) 
Tabla de eventos (private) 
Mapa (Private) 
Visualización (private) 
Valor de datos (Public) 
 
Aplicaciones: 
Tracker Capture app 
 
Tracker(Rastreador) 
Delete enrollment and associated events 
Delete tracked entity instance and associated enrollments and events 
Search tracked entity instance in all Org units 
Update tracked entities 
 
Importar/exportar: 
-sin acceso 
Sistema: 
-sin acceso 



#### Supervisor (de país/distrito) *

Este usuario podrá acceder y editar todos los datos dentro de tracker. COmbinar con las org units necesarias para asignarles un distrito/pais \
- 
- 
- 
- 


#### Creación y edición de usuarios
Este rol permitirá crear y editar usuarios existentes. Es recomendado que cada país distribuya este rol como sea conveniente. \
- 
- 
- 


#### Configurador de metadatos
Acceso a la app de mantenimiento para modificar programas, elementos de datos, indicadores, etc. 

-
-
-
- 


#### Superusuario Regional
Acceso a todos los roles. Este acceso debería ser altamente restringido en la instancia de producción \
  
X 
Y 
Z 



## Grupos de usuario:

 Los grupos de usuario sirven para dar acceso a los distintos programas (por ejemplo, el programa de ESAVI o el Programa Centinela). Y regular que nivel de acceso tienen los usuarios dentro de ese grupo al programa. 
El nivel de acceso está basado en datos y metadatos, y en poder ver o editar, y deberá ser combinado con el rol de usuario y aceso a la unidad organizativa correspondiente.

Para una implementación regional, se recomiendan las siguientes combinaciones de grupo de usuario / rol / acceso a unidad organizativa:


| User group                | Descripción                                                               | Org unit access                                       | Datos                    | Metadatos    | Analytics    | Roles                                                                 |
|---------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|--------------------------|--------------|--------------|-----------------------------------------------------------------------|
| Data entry                | Usuario final                                                             | Unidad propia                                         | Ver y editar (No borrar) | Ver          | Sin acceso   | Usuario de Entrada de datos - Tracker (Sin acceso a borrar una TEI)   |
| Data Entry Supervisor     | Igual que usuario final, pero podrá borrar TEIs ni enrollments            | Unidad propia /distrito                               | Ver y editar ( borrar)   | ver          | ver          | Usuario de Entrada de datos - Tracker Supervisor (de país/distrito) * |
| Data analysis             | Tendrá acceso a visualizaciones e indicadores                             | Unidad propia                                         | Ver                      | Ver          | Ver          | Usuario de Entrada de datos - Tracker                                 |
| Data audit nacional       | Podrá ver todos los datos y quién los ha ingresado pero no editarlos      | Unidades del país                                     | Ver                      | Ver          | Ver          | Supervisor (de país/distrito) *                                       |
| Metadata Admin (OPS)      | Podrá editar los formularios, tableros e indicadores, pero no ver datos   | Todas                                                 | Sin Acceso               | Ver y Editar | Ver y Editar | Configurador de metadatos                                             |
| Administrador de usuarios | Podrá crear y asignar usuarios a distintos roles y unidades organizativas | Unidades del país /Distrito/propias segun corresponda | NO                       | NO           | NO           | Creación y edición de usuarios                                        |
| Superusuario              | Si                                                                        | Todas                                                 | Ver y Editar             | Ver y Editar | Ver y Editar | Todas                                                                 |