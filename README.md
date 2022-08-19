# Curso-MongoDB

En este repositorio, se mostrará una sencilla guía de MongoDB, un SGBD que sirve para crear una API Rest funcional junto a Node.js y Express. La finalidad de este curso es el aprendizaje de nuevas herramientas para el desarrollo de la aplicación que se situa en el siguiente enlace:

-----------------------------

KOMBAT SIMULATOR: https://github.com/Agumeri/Kombat-Simulator-jQueryMobile

-----------------------------

# Introducción: ¿Que es MongoDB?

  MongoDB es un SGBD no relacional open-source orientado a documentos. Es multiplataforma, tiene un rendimiento bastante alto, tiene alta escalabilidad y la disponibilidad de los datos también es alta. Se usa MongoDB cuando la aplicación tenga un crecimiento rápido, se quiera realizar una aplicación con servidores en la nube, los datos no van a tener la misma estructura y la aplicación va a tener muchos usuarios accediendo a los datos simultaneamente.
  
# Estructura de MongoDB

  MongoDB se estrucuta por diferentes capas:
  - El **servidor de mongo**, que es donde lo vamos a tener todo.
  - La **base de datos**, la cual está compuesta por colecciones.
  - Las **colecciones** son los análogos a las tablas de SQL. Dentro de estos tenemos un conjunto de documentos. La principal diferencia con las tablas de una base de datos relacional como puede ser SQL es que Mongo no nos impone un esquema rígido a la hora de almacenar documentos en una colección. 
  - Los **documentos** son los registros de las colecciones, lo que vendría a ser en SQL las filas de cada tabla. Estos tienen un formato de pares de claves y valores. Los valores de estas claves pueden ser String, Number, Array(listas), Date, Boolean y Object. Son análogos a los objetos JSON aunque el nombre que emplean en el ámbito de mongo es BSON (ya que se trata de un JSON en binario).
  
  Un ejemplo de un documento sería el siguiente, que equivaldría a una Persona: 
  {
    "nombre": "Pepito",
    "edad" : 28,
    "telefono": "123456789",
    "DNI": "26321232F"
  }

# Uso de MongoDB
## Instalación MongoDB
  * En Ubuntu, basta con usar la siguiente instrucción en la terminal para instalarlo: 
  ```terminal
  sudo apt install -y mongodb
  ```
  * En Windows (u otro SO, incluso Ubuntu también), accediendo a [esta página](https://www.mongodb.com/download-center/community) podrás descargar el archivo de instalación. Una vez instalado, para iniciar mongo se deberá acceder a la carpeta donde se ha instalado y abrir primero el servidor de mongo, **mongod.exe** y después iniciar **mongo.exe**.
  
*Nota: Lo que queda de guía será enfocado al uso de mongo en Ubuntu, pero las instrucciones usadas para manejar bases de datos con MongoDB serán las mismas tanto en este SO como en el resto.*
  
## Control del servidor de MongoDB

  MongoDB se instala como un servicio de systemmd, lo que significa se se puede administrar con los comandos de systemd. Los más importantes serán los siguientes: 
  
  **Iniciar el servidor**
  ```
  sudo systemctl start mongodb
  ```
  
  **Detener el servidor**
  ```
  sudo systemctl restart mongodb
  ```
  
  **Reiniciar el servidor**
  ```
  sudo systemctl restart mongodb
  ```
  
  **Comprobar el estado del servidor**
  ```
  sudo systemctl status mongodb
  ```

## Instrucciones de MongoDB. Crear, eliminar, manejar y consultar colleciones
  Las siguientes instrucciones son las más comunes en MongoDB. Se utilizarán siempre que se utilizar una base de datos de mongoDB:
  
  * **Mostrar bases de datos existentes**
  ```
  show dbs
  ```
  *Nota: Si la base de datos está vacía, no la muestra al llamar a este comando*
  * **Crear/utilizar una base de datos** 
  ```
  use mibd
  ```
  *Nota: Si no se ha creado la base de datos, se crea automaticamente.*
  * **Ver la base de datos en la que nos encontramos** 
  ```
  db
  ```
  * **Crear una colección e insertar un documento a esta implicitamente**
  ```
  db.usuarios.insertOne({
    "nombre": "Ann",
    "Edad": "48",
    "pais": "Francia",
    "clave": "87654321"
  })
  ```
  * **Crear una colección explicitamente**
  ```
  db.collection("comida")
  ```
  *Nota: Para ver las colecciones una vez creadas usamos --->* ``` show collections ``` 
  
  * **Eliminar una colección**
  ```
  db.comida.drop()
  ```
  * **Eliminar una base de datos**
  *Nota: Nos debemos situar en la base de datos usando ```use [nombreBD]``` para poder eliminarla.
  ```
  db.dropDatabase()
  ```
  * **Consultar elementos de una colección**
  ```
  db.usuarios.find().pretty()
  ```
  *Nota: pretty() lo que hace es que cuando nos muestre la terminal la consulta, esta se vea en un formato más legible.*
  * **Cambiar datos de un documento de una colección**
  ```
  db.usuarios.updateOne({
    "clave": "12345678"
    },
    {
      $set: {'Edad': 30}
    }
    )
  ```
  *Nota: Si deseamos qeu se actualicen todos los que cumplan una condicion (toda la gente con mas de 40 años por ejemplo) deberemos poner un tercer campo ---> ```{multi:true}```
  * **Eliminar un documento de una colección**
  ```db.usuarios.deleteOne({ "clave": "12345678" })```
  
  **Para realizar las consultas específicas en una colleción, lo que debemos hacer es poner los parámetros de busqueda al llamar a find**
  *usuario con 30 años:* ``` db.usuarios.find({"Edad":30})```
  *usuarios con menos de 40 años:* ```db.usuarios.find({"Edad":{$lt:40}})```
  
  Algunos de las operaciones que se pueden realizar son las siguientes: 
  
| Operación | Instrucción |
| ------------- | ------------- |
| Igualdad  | {"Edad": 20 }  |
| Menor que  | {"Edad": {$lt: 20 } }  |
| Menor o igual que  | {"Edad": {$lte: 20 } }  |
| Mayor que  | {"Edad": {$gt: 20 } }  |
| Mayor o igual que  | {"Edad": {$gte: 20 } }  |
| No es igual  | {"Edad": {$ne: 20 } }  |
| AND  | { {key1: value1, key2:value2} }  |
| OR  | { $or: [ {key1: value1, key2:value2} } ] }|

  **Limitar documentos obtenidos** 
  ``` 
  db.usuarios.find().limit(1) 
  ```
  **Devolver los documentos ordenados**
  ```
  db.usuarios.find().sort({"Edad":1})
  ```
  *Nota: si dentro de sort se pone 1, se ordenan de menor a mayor, y con -1 de mayor a menor.*
  
