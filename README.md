# Taller de trabajo individual en patrones arquitecturales

Students are tasked with developing a simple CRUD (Create, Read, Update, Delete) system for managing real estate properties. The goal is to build a basic web application that allows users to perform the following operations on property listings:

- Create new property listings.
- Read or view a list of all properties and individual property details.
- Update existing property details.
- Delete property listings


## 📌 Características


# Funcionalidades Principales

Este sistema CRUD permite gestionar anuncios de propiedades inmobiliarias. Los usuarios pueden crear, leer, actualizar y eliminar propiedades a través de una interfaz web sencilla y un backend implementado con Spring Boot.


- Crear: Permite a los usuarios agregar nuevos anuncios de propiedades con detalles como dirección, precio, tamaño y descripción.
- Leer: Muestra una lista de todas las propiedades disponibles y permite ver los detalles individuales de cada propiedad.
- Actualizar: Permite editar la información de una propiedad existente.
- Eliminar: Permite eliminar una propiedad de la base de datos.

Despliegue de los servicios de backend y base de datos en servidores separados dentro de de AWS
  
```bash
Despliegue en AWS
```

Se ejecuta localmente en contenedores Docker y también puede ser desplegada en una máquina virtual en AWS.


## 🛠️ Requisitos
- Java 11 o superior
- Git
- Maven
- Docker
- AWS EC2
- MySQL


## 🚀 Instalación y Ejecución
### 1️⃣ Clonar el repositorio
```bash
git clone https://github.com/Juanse2347/AREP_T5
cd AREP_T5
```

### 2️⃣ Compilar el proyecto con Maven
```bash
mvn clean install
```

![Image](https://github.com/user-attachments/assets/0a5c2877-e890-4901-a25a-0cfa24bdb6ee)


### 3️⃣ Ejecutar el servidor 

```bash
mvn spring-boot:run
```

![image](https://github.com/user-attachments/assets/03293b31-728d-4a8c-ac17-72b71f5412c0)



## 🔍 Diseño de Clases 

Clases Principales

> [!IMPORTANT]
>  - **Property**: Representa la entidad de propiedad con los atributos id, address, price, size, y description.
>  - **PropertyService**: Contiene la lógica del negocio para gestionar las operaciones CRUD de las propiedades.
>  - **PropertyController**: Proporciona los endpoints RESTful para interactuar con el frontend.


![image](https://github.com/user-attachments/assets/a10ca6fa-8513-4c8c-a72d-7a8d74b1d3c9)


# 🔍 Sistema Arquitectónico

El sistema consta de tres componentes principales:


- **Frontend (HTML, JavaScript)**: Proporciona la interfaz de usuario para interactuar con las propiedades (crear, leer, actualizar, eliminar).
- **Backend (Spring Boot)**: Proporciona la API RESTful para gestionar las propiedades, implementando los métodos POST, GET, PUT y DELETE.
- **Base de Datos (MySQL en AWS RDS)**: Almacena los datos de las propiedades y asegura su persistencia.


## 🚀 Despliegue AWS

Creamos las dos instancias en AWS EC2.

![image](https://github.com/user-attachments/assets/3f41dff7-e699-4053-9087-8e3b3a2a4d3d)


Ahora configura el grupo de seguridad de la instancia EC2 para permitir el tráfico entrante en el puerto 8080 (o el puerto que hayas configurado en tu aplicación Spring Boot).


![image](https://github.com/user-attachments/assets/0855c555-704d-4d8c-85bc-4e6784f21c97)


Asegúrate de que la base de datos MySQL esté accesible desde la instancia EC2.


Desplegamos nuestro codigo en AWS

1. Subimos el proyecto a AWS

```bash
scp -i key.pem target/app.jar ec2-user@IP_EC2:/home/ec2-user/
```

2. Conectamos a nuestra instancia EC2

```bash
ssh -i key.pem ec2-user@IP_EC2
```

3. Ejecutamos la aplicacion 

```bash
java -jar /home/ec2-user/app.jar
```

4. Y para finalizar accedemos a la aplicacion

```bash
http://EC2_PUBLIC_IP:8080/index.html
```

Que se veria de la siguiente manera

![image](https://github.com/user-attachments/assets/932d8b33-db0c-460c-adad-ec8b921410fe)


## 🚀 Configuración de la Base de Datos

Creamos una base de datos en MySQL

```sql
CREATE DATABASE propertydb;
CREATE USER 'arep'@'%' IDENTIFIED BY 'Arep2025@';
GRANT ALL PRIVILEGES ON propertydb.* TO 'arep'@'%';
FLUSH PRIVILEGES;
```

Creamos los atributos y datos para nuestra tabla:


```sql
CREATE TABLE properties (
  id BIGINIT AUTO_INCREMENT PRIMARY KEY,
  address VARCHAR(255) NOT NULL,
  price DOUBLE NOT NULL,
  size INT NOT NULL,
  description VARCHAR(255) NOT NULL
);
```

Que agregamos a nuestra instancia en AWS, de la siguiente manera:

![image](https://github.com/user-attachments/assets/f3384e11-d0c7-46b3-9d54-af24b4b134bc)


Ahora abrimos los puertos de entrada del security group de la máxima virtual para acceder al servicio

![image](https://github.com/user-attachments/assets/752d80f0-d46e-4e39-944c-958d4ab4c810)



## 🔍 Pruebas de Estilo de Codificacion ##

Con el siguiente comando realizamos las pruebas de estilo de codificación son aquellas que verifican que el código sigue las convenciones y buenas prácticas del equipo o la comunidad

```bash
mvn checkstyle:check
```

![Image](https://github.com/user-attachments/assets/6c5a4c16-9c71-463d-9629-59f5c976213a)


## :office: Desplieqgue ##

Vamos a ejecutar el servidor como un proceso en segundo plano o configurar un servicio systemd, de la siguiente manera:

```bash
mvn spring-boot:run
```

## :cd: Construido con ## 

 - Java - Lenguaje principal utilizado
 - Maven - Para la gestión de dependencias y automatización
 - Docker - Plataforma de código abierto que permite crear, ejecutar, administrar y actualizar contenedores


## :busts_in_silhouette: Contribuciones ##

Lea [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) para obtener detalles sobre nuestro código de conducta y el proceso para enviarnos solicitudes de extracción.

## :school_satchel: Control de Versiones ##

Usamos [SemVer](http://semver.org/) para controlar las versiones.

## :bust_in_silhouette: Autor ##

* **Juan Sebastian Sanchez** - *Trabajo Inicial* - [Juanse2347](https://github.com/Juanse2347)


## 📄 Licencia
Este proyecto está bajo la licencia [LICENSE](LICENSE). ¡Siéntete libre de contribuir! 😊


## :wave: Expresiones de Gratitud ##

- Inspiracion
- Compromiso

