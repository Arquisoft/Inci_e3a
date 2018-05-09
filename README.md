# Sistema de gestión de incidencias del grupo E3A

Este sistema de gestión de incidencias está formado por cuatro módulos: Loader e3a, Agents e3a, InciManager e3a e InciDashBoard e3a. 

## Índice

- [Módulos de sistema](#módulos)
- [Descripción del sistema](#descripción-del-sistema)
- [Despliegue](#despliegue)
- [Autores](#autores)
 
 

### Módulos
| Módulo | | | | 
|---------------------|---|---|---|
| [InciManager e3a](https://github.com/Arquisoft/InciManager_e3a/) | [![Build Status](https://travis-ci.org/Arquisoft/InciManager_e3a.svg?branch=master)](https://travis-ci.org/Arquisoft/InciManager_e3a) | [![Codacy Badge](https://api.codacy.com/project/badge/Grade/fb1e93fdc9694b22bc3493c315e5148d)](https://www.codacy.com/app/jelabra/InciManager_e3a?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Arquisoft/InciManager_e3a&amp;utm_campaign=Badge_Grade)|[![codecov](https://codecov.io/gh/Arquisoft/InciManager_e3a/branch/master/graph/badge.svg)](https://codecov.io/gh/Arquisoft/InciManager_e3a) 
| [Agents e3a](https://github.com/Arquisoft/Agents_e3a/) | [![Build Status](https://travis-ci.org/Arquisoft/Agents_e3a.svg?branch=master)](https://travis-ci.org/Arquisoft/Agents_e3a) | [![Codacy Badge](https://api.codacy.com/project/badge/Grade/52c0a7fa26854206a17e11d781bd421c)](https://www.codacy.com/app/jelabra/Agents_e3a?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Arquisoft/Agents_e3a&amp;utm_campaign=Badge_Grade)|[![codecov](https://codecov.io/gh/Arquisoft/Agents_e3a/branch/master/graph/badge.svg)](https://codecov.io/gh/Arquisoft/Agents_e3a) 
| [Loader e3a](https://github.com/Arquisoft/Loader_e3a/) | [![Build Status](https://travis-ci.org/Arquisoft/Loader_e3a.svg?branch=master)](https://travis-ci.org/Arquisoft/Loader_e3a) | [![Codacy Badge](https://api.codacy.com/project/badge/Grade/6fad6fe134c1434cb0b9384d851821c8)](https://www.codacy.com/app/jelabra/Loader_e3a?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Arquisoft/Loader_e3a&amp;utm_campaign=Badge_Grade)|[![codecov](https://codecov.io/gh/Arquisoft/Loader_e3a/branch/master/graph/badge.svg)](https://codecov.io/gh/Arquisoft/Loader_e3a) | 
| [InciDashBoard e3a](https://github.com/Arquisoft/InciDashboard_e3a/) | [![Build Status](https://travis-ci.org/Arquisoft/InciDashboard_e3a.svg?branch=master)](https://travis-ci.org/Arquisoft/InciDashboard_e3a) |[![Codacy Badge](https://api.codacy.com/project/badge/Grade/6fad6fe134c1434cb0b9384d851821c8)](https://www.codacy.com/app/jelabra/InciDashboard_e3a?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Arquisoft/Loader_e3a&amp;utm_campaign=Badge_Grade) | [![codecov](https://codecov.io/gh/Arquisoft/InciDashboard_e3a/branch/master/graph/badge.svg)](https://codecov.io/gh/Arquisoft/InciDashboard_e3a) |


### Descripción del sistema

Las descripciones concretas se encunetrán en las especificaciones de cada uno de los módulos, con lo que solo describiremos las relaciones entre los módulos mencionados en el apartado anterior:

- El módulo Loader e3a se comunica con la misma base de datos que el módulo Agents e3a. Esta base de datos se encuentra en el servidor mLab, es MongoDB (es decir, no relacional) y se llama agentsdb.
- El módulo Agents e3a, como ya se ha dicho, se conecta con la base de datos agentsdb.
- El módulo InciManager e3a se cómunica con el Agents e3a para validar los datos de todo agente que quiera acceder al primero. Esta comunicación se realiza mediante una petición al segundo de estos módulos por parte del primero. Además, InciManager e3a se cómunica con el módulo InciDashBoard e3a mediante Apache Kafka para mandarle a éste las incidencias recién recibidas.
- El módulo InciDashBoard, recibe de las incidencias más recientes desde Apache Kafka (cuyo servidor se encuentra en CloudKarafka)


## Despliegue

Para el despliegue se ha utilizado el servicio AWS (Amazon Web Service), creando en este tres máquinas Amazon Linux cuyas características básicas son las mismas: 

- 1 vCPUs
- 2.5 GHz
- Intel Xeon Family
- 1 GiB memory

En las máquinas mencionadas se alojan los módulos de las siguiente forma:

- En la primera, el módulo Loader e3a.
- En la segunda, los módulos Agents e3a y InciManager e3a.
- En la tercera, el módulo InciDashBoard e3a.

## Para conectarse a los diferentes módulos se utilizan estos enlaces
http://18.237.112.43:8090 --> InciManager

http://18.237.112.43:8091 --> Agents

http://54.212.241.57:8081 --> InciDashBoard

## Datos de Usuario para acceso a las aplicaciones:
## InciManager:
	- Usuario: Agente1/Agente2/Agente3/Agente4/Agente5/Agente6
	- Contraseña: 123456
	- Kind: person
			*El envío de incidencias por parte de los sensores es automático.

## InciDashBoard:
	- Usuario:
		-  Operario: Id1, Id2, Id3
		-  Administrador: Id4
		-  Analista: Id5
	- Contraseña: 123456

### Autores
- Álvaro Cabrero Barros (@espiguinho)
- Saúl Castillo Valdés (@saulcasti)
- Pelayo Díaz Soto (@PelayoDiaz)
- Amelia Fernández Braña (@ameliafb)
- Francisco Javier Riedemann Wistuba (@FJss23)
