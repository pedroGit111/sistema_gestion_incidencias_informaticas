# Sistema de Gestión de Incidencias Informáticas

Este proyecto es una aplicación de consola en Java que permite a los técnicos de soporte autenticar su acceso, gestionar empleados, registrar incidencias, cambiar su estado y generar informes. Utiliza JDBC para conectarse a una base de datos MySQL y sigue el patrón Modelo-Vista-Controlador (MVC).

##  Requisitos del Sistema
Java 8 o superior
MySQL o MariaDB
JDBC Driver MySQL (si no usas Maven)
Eclipse, IntelliJ o cualquier IDE compatible con Java

##  Configuración de la Base de Datos
Abre tu gestor de base de datos (MySQL Workbench, phpMyAdmin o consola).
Ejecuta el script SQL script_incidencias.sql ubicado en la carpeta bd/.

### Script SQL básico incluido:
sql
CREATE DATABASE IF NOT EXISTS sistema_incidencias;
USE sistema_incidencias;

CREATE TABLE IF NOT EXISTS tecnicos (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre_usuario VARCHAR(50) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL
);

CREATE TABLE IF NOT EXISTS empleados (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nombre VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL
);

CREATE TABLE IF NOT EXISTS incidencias (
  id INT PRIMARY KEY AUTO_INCREMENT,
  id_empleado INT NOT NULL,
  descripcion TEXT NOT NULL,
  prioridad VARCHAR(10) CHECK (prioridad IN ('Alta', 'Media', 'Baja')),
  estado VARCHAR(20) CHECK (estado IN ('Abierta', 'En proceso', 'Cerrada')),
  fecha_creacion DATE NOT NULL,
  fecha_resolucion DATE,
  FOREIGN KEY (id_empleado) REFERENCES empleados(id)
);


 Asegúrate de ejecutar primero la instrucción:
> sql
> USE sistema_incidencias;
> 

##  Cómo usar la aplicación

### 1. Ejecutar el programa
Abre Main.java y ejecútalo desde tu IDE.
Se te pedirá ingresar un usuario y contraseña de técnico ya existente en la tabla tecnicos.

### 2. Navegar por el menú principal
Una vez autenticado, verás el siguiente menú:


=== Menú Principal ===
1. Gestionar Empleados
2. Gestionar Incidencias
3. Ver Incidencias por Estado
4. Ver Historial de un Empleado
5. Ver Informes Generales
6. Cerrar Sesión


### 3. Opciones disponibles
*Gestionar Empleados*: Crear, ver, actualizar y eliminar empleados.
*Gestionar Incidencias*: Registrar nuevas incidencias, listarlas, cambiar su estado y eliminarlas.
*Ver Incidencias por Estado*: Filtra incidencias por estado ('Abierta', 'Cerrada', etc).
*Ver Historial de un Empleado*: Muestra todas las incidencias asociadas a un empleado por su ID.
*Ver Informes Generales*:
  - Total de incidencias abiertas y cerradas por empleado.
  - Cantidad de incidencias abiertas por prioridad.
  - Tiempo promedio de resolución de incidencias.

### 4. Ejemplo de salida de informe

Empleado: Juan Pérez - Incidencias Abiertas: 3 - Cerradas: 5
Prioridad Alta: 4 incidencias abiertas
Tiempo promedio de resolución: 2.3 días


##  Estructura de Carpetas
modelo/ → Clases Java con la estructura de datos.
dao/ → Acceso a base de datos (JDBC).
controlador/ → Lógica de negocio y coordinación entre capas.
vista/ → Menús interactivos por consola.
util/ → Validaciones comunes.
bd/ → ScredStatement` para evitar inyecciones SQL.

##  Autor
[Nombre del estudiante aquí] – Proyecto de examen – Junio 2025
ipt de base de datos.

##  Notas
Incluye validaciones, autenticación, consultas JOIN e informes agregados.
Proyecto ejecutable en bucle hasta cierre de sesión.
Consultas optimizadas mediante `Prepar