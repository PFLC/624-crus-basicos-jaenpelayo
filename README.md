
# Aplicación CRUD de PHP

Este repositorio contiene una aplicación PHP CRUD (Create, Read, Update, Delete) simple. Es una demostración básica de cómo integrar PHP con una base de datos MySQL para gestionar datos de usuarios. La aplicación permite a los usuarios agregar, ver, editar y eliminar información de usuario.

## Tecnologías Utilizadas

- **PHP:** Lenguaje de script del lado del servidor utilizado para el desarrollo web.
- **MySQL:** Sistema de gestión de base de datos utilizado para almacenar datos de usuario.
- **HTML & CSS:** Utilizados para estructurar y dar estilo a las páginas web.
- **Tailwind CSS:** Un framework de CSS utilitario para el desarrollo rápido de interfaces de usuario.

## Páginas y Funcionalidades

### 1. Página de Inicio (`display.php`)

![Página de Inicio](images/display.png)

- **Funcionalidad:** Muestra todos los usuarios de la base de datos en un formato de tabla.
- **Características:** 
  - Ver todos los usuarios.
  - Enlaces de navegación para agregar, editar o eliminar información de usuario.

### 2. Agregar Usuario (`user.php`)

![Agregar Usuario](images/add.png)

- **Funcionalidad:** Permite agregar un nuevo usuario a la base de datos.
- **Características:** 
  - Formulario para ingresar detalles del usuario (nombre, correo electrónico, teléfono móvil, contraseña).
  - Validación de datos y envío a la base de datos.

### 3. Editar Usuario (`edit.php`)

![Editar Usuario](images/edit.png)

- **Funcionalidad:** Permite editar detalles de usuarios existentes.
- **Características:** 
  - Formulario prellenado con la información actual del usuario.
  - Actualización de detalles del usuario en la base de datos.

### 4. Eliminar Usuario (`delete.php`)

- **Funcionalidad:** Facilita la eliminación de un usuario de la base de datos.
- **Características:** 
  - Eliminación de información de usuario basada en el ID de usuario.

## Conexión a la Base de Datos (`connect.php`)

- **Propósito:** Establece una conexión con la base de datos MySQL.
- **Credenciales:** Utiliza nombre de host, nombre de usuario, contraseña y nombre de la base de datos para la conexión.

## Cómo Ejecutar

1. Clona el repositorio en tu máquina local.
2. Configura un entorno PHP y MySQL (como XAMPP).
3. Crea la base de datos usando phpmyadmin.
4. Ejecuta la aplicación en un servidor local.

## Nota de Seguridad

Esta aplicación es una demostración básica y no implementa medidas avanzadas de seguridad. Es recomendable utilizar declaraciones preparadas (prepared statements) u ORM para las interacciones con la base de datos para prevenir ataques de inyección SQL.

---

Siéntete libre de contribuir a este proyecto o sugerir mejoras. Para cualquier consulta o problema, por favor abre un issue en este repositorio.

                                                                  investigacion 

Para utilizar PHP en un CRUD (Create, Read, Update, Delete) necesitas seguir algunos pasos básicos. 

Configuración de la base de datos: Primero, necesitas tener una base de datos MySQL (u otro sistema de gestión de bases de datos) configurada. Puedes crear una tabla para almacenar los datos que deseas gestionar con el CRUD.

Conexión a la base de datos: En tu script PHP, necesitarás establecer una conexión a la base de datos. Puedes hacerlo utilizando la extensión mysqli o PDO de PHP.

<?php
$servername = "localhost";
$username = "nombre_usuario";
$password = "contraseña";
$database = "nombre_base_de_datos";

// Crear conexión
$conn = new mysqli($servername, $username, $password, $database);

// Comprobar la conexión
if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}
?>

Operaciones CRUD: Ahora puedes escribir las funciones para realizar las operaciones CRUD en tu base de datos.

Create (Crear): Insertar nuevos registros en la base de datos.

Read (Leer): Leer registros de la base de datos.

Update (Actualizar): Actualizar registros existentes en la base de datos.

Delete (Eliminar): Eliminar registros de la base de datos.

ejemplo basico 

<?php
// Crear un nuevo registro
function createRecord($conn, $nombre, $email) {
    $sql = "INSERT INTO tabla (nombre, email) VALUES ('$nombre', '$email')";
    if ($conn->query($sql) === TRUE) {
        return "Nuevo registro creado con éxito";
    } else {
        return "Error: " . $sql . "<br>" . $conn->error;
    }
}

// Leer registros
function readRecords($conn) {
    $sql = "SELECT id, nombre, email FROM tabla";
    $result = $conn->query($sql);

    if ($result->num_rows > 0) {
        // output data of each row
        while($row = $result->fetch_assoc()) {
            echo "ID: " . $row["id"]. " - Nombre: " . $row["nombre"]. " - Email: " . $row["email"]. "<br>";
        }
    } else {
        echo "0 resultados";
    }
}

// Actualizar un registro existente
function updateRecord($conn, $id, $nombre, $email) {
    $sql = "UPDATE tabla SET nombre='$nombre', email='$email' WHERE id=$id";
    if ($conn->query($sql) === TRUE) {
        return "Registro actualizado con éxito";
    } else {
        return "Error actualizando el registro: " . $conn->error;
    }
}

// Eliminar un registro
function deleteRecord($conn, $id) {
    $sql = "DELETE FROM tabla WHERE id=$id";
    if ($conn->query($sql) === TRUE) {
        return "Registro eliminado con éxito";
    } else {
        return "Error eliminando el registro: " . $conn->error;
    }
}
?>

Interfaz de usuario: Finalmente, necesitarás crear una interfaz de usuario (generalmente HTML y CSS) que permita a los usuarios interactuar con estas funciones CRUD. Puedes usar formularios HTML para recopilar datos y enviarlos a tu script PHP para procesarlos.
Este es un enfoque básico para implementar un CRUD utilizando PHP y MySQL. Recuerda tener en cuenta la seguridad, como la prevención de ataques de inyección SQL, al manejar datos de usuario en tu aplicación.

las operaciones CRUD y una interfaz de usuario básica utilizando HTML y PHP.

Configuración de la base de datos:
Primero, necesitas crear una tabla en tu base de datos MySQL. Aquí hay un ejemplo de cómo podría ser la definición de la tabla:

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(50),
    email VARCHAR(50)
);
Conexión a la base de datos:
<?php
$servername = "localhost";
$username = "nombre_usuario";
$password = "contraseña";
$database = "nombre_base_de_datos";

// Crear conexión
$conn = new mysqli($servername, $username, $password, $database);

// Comprobar la conexión
if ($conn->connect_error) {
    die("Conexión fallida: " . $conn->connect_error);
}
?>
Operaciones CRUD:
<?php
// Crear un nuevo registro
function createRecord($conn, $nombre, $email) {
    $sql = "INSERT INTO usuarios (nombre, email) VALUES ('$nombre', '$email')";
    if ($conn->query($sql) === TRUE) {
        return "Nuevo registro creado con éxito";
    } else {
        return "Error: " . $sql . "<br>" . $conn->error;
    }
}

// Leer registros
function readRecords($conn) {
    $sql = "SELECT id, nombre, email FROM usuarios";
    $result = $conn->query($sql);

    if ($result->num_rows > 0) {
        // output data of each row
        while($row = $result->fetch_assoc()) {
            echo "ID: " . $row["id"]. " - Nombre: " . $row["nombre"]. " - Email: " . $row["email"]. "<br>";
        }
    } else {
        echo "0 resultados";
    }
}

// Actualizar un registro existente
function updateRecord($conn, $id, $nombre, $email) {
    $sql = "UPDATE usuarios SET nombre='$nombre', email='$email' WHERE id=$id";
    if ($conn->query($sql) === TRUE) {
        return "Registro actualizado con éxito";
    } else {
        return "Error actualizando el registro: " . $conn->error;
    }
}

// Eliminar un registro
function deleteRecord($conn, $id) {
    $sql = "DELETE FROM usuarios WHERE id=$id";
    if ($conn->query($sql) === TRUE) {
        return "Registro eliminado con éxito";
    } else {
        return "Error eliminando el registro: " . $conn->error;
    }
}
?>
Interfaz de usuario:
<!DOCTYPE html>
<html>
<head>
    <title>CRUD de Usuarios</title>
</head>
<body>
    <h2>CRUD de Usuarios</h2>

    <h3>Crear Nuevo Usuario</h3>
    <form action="crear_usuario.php" method="post">
        Nombre: <input type="text" name="nombre"><br>
        Email: <input type="email" name="email"><br>
        <input type="submit" value="Crear Usuario">
    </form>

    <h3>Editar Usuario</h3>
    <form action="editar_usuario.php" method="post">
        ID del Usuario a Editar: <input type="text" name="id"><br>
        Nuevo Nombre: <input type="text" name="nombre"><br>
        Nuevo Email: <input type="email" name="email"><br>
        <input type="submit" value="Editar Usuario">
    </form>

    <h3>Eliminar Usuario</h3>
    <form action="eliminar_usuario.php" method="post">
        ID del Usuario a Eliminar: <input type="text" name="id"><br>
        <input type="submit" value="Eliminar Usuario">
    </form>

    <h3>Lista de Usuarios</h3>
    <?php
    // Mostrar la lista de usuarios
    readRecords($conn);
    ?>

</body>
</html>
Scripts de PHP para procesar los formularios:
Aquí proporcionarías scripts PHP separados para procesar cada uno de los formularios de la interfaz de usuario (crear, editar, eliminar).
