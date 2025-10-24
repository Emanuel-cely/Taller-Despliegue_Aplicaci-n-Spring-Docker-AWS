Cordial saludo
# 🚀 Taller: Despliegue de Aplicación con Spring Boot, Docker y AWS EC2

> 📘 **Resumen:**  
> Este proyecto consiste en crear una aplicacion web usando el micro-framework Spring donde se va a construir un container en Docker, luego se crea una maquina virtual (EC2) en AWS donde se despliga el contenedor previamente clonado de Docker Hub, tambien documentar el proceso completo de compilación, contenedorización y despliegue de una aplicación **Spring Boot** utilizando **Docker**, **Docker Hub** y una **instancia EC2 de AWS**.

### ✅ Requisitos para realizar el proyecto
- Conocimientos en el lenguje de programacion Java y la herramienta Maven.  
- Tener instalado Docker Desktop.
- Tener cuenta en Docker Hub.
- Contar con una cuenta en AWS y creditos para crear una instancia.

A continuacion se explicara lo realizado:

Se crea un proyecto Java usando maven  con el siguiente comando:
- mvn archetype:generate -DgroupId=edu.escuelaing.aygo.conatiner -DartifactId=containerapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

Se crea una aplicacion Spring pequeña donde se crea 2 clases controlador: HelloRestController y RestServiceApplication

Se importa las dependencias de Spark Java donde se agrega el codigo en el file pom.xml
![alt text](image-18.png)

Se asegura que el proyecyo copile con la version 17 de Java
![alt text](image-19.png)

Se asegura que el proyecto compile con el siguiente comando:
- mvn clean install

![alt text](image-3.png)

Se inicializa Spring en este caso con el siguiente comando:
- java -cp "target/classes;target/dependency/*" edu.escuelaing.aygo.conatiner.RestServiceApplication

![alt text](image-8.png)

dando como resuiltado:

![alt text](image-4.png)

--- 

**Imagenes en Docker:**

Se crea una imagen en Docker con el siguiente comando:
- docker build --tag dockersparkprimer .

![alt text](image.png)

Se crea 3 instancias en un contenedor en Docker con el siguiente comando:
- docker run -d -p 34000:33025 --name firstdockercontainer dockersparkprimer

![alt text](image-1.png)

Dando como resultado: 

![alt text](image-5.png)

docker-compose donde se crea una instancia a mongo en otro container quedando de la siguiente manera:
- docker-compose up -d

![alt text](image-2.png)

Se sube la imagen a Docker Hub con el siguiente comando:
- docker tag dockersparkprimer emanuelcely15/ecely-container
- docker push emanuelcely15/ecely-container:latest

![alt text](image-6.png)
![alt text](image-7.png)

---

**Se crea la maquina virtual en AWS:**

Se crea la instancia:

![alt text](image-9.png)

Se conecta y asi se veria la ocnfiguracion general:

![alt text](image-10.png)

Se crea una carpeta donde se alamcena los pares de llaves:

![alt text](image-11.png)

Se conecta a la maquina virtual:

![alt text](image-12.png)

Se instala Docker:
- sudo yum update -y
- sudo yum install docker

![alt text](image-13.png)

Se inicia el servicio de Docker
- sudo service docker start

Se configura el ususario para que no sea necesario usar "sudo", se sale e ingresa de nuevo a la maquina:
- sudo usermod -a -G docker ec2-user

![alt text](image-14.png)

Se crea una instancia del contenedor en Docker Hub a la maquina virtual:
- docker run -d -p 33000:15600 --name firstdockerimageaws emanuelcely15/ecely-container:latest

![alt text](image-15.png)

Se hace los cambios en el apartado de seguridad:

![alt text](image-16.png)

Se verifica que este funcionando en el navegador:

![alt text](image-17.png)

**Muchas gracias.**