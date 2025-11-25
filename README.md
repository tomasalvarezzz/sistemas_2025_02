# Proyecto Sistemas - La Picá

Este repositorio contiene la solución de software propuesta para el control operativo de "La Picá", incluyendo módulos para **Login, Caja (Ventas), Cocina (Inventario)** y **Administración (KPIs/CRUD de Productos)**.

## 1. Requisitos del Sistema

Para ejecutar la aplicación, se requiere el siguiente entorno:
* **Motor de Base de Datos:** MySQL Server (versión 8.0 o superior recomendada).
* **Lenguaje de Programación:** Python 3.x.
* **Librerías Python:** `PyQt5`, `pymysql`.

## 2. Configuración de la Base de Datos (SQL)

El sistema utiliza una base de datos relacional llamada `db_la_pica`. Sigue los siguientes pasos para su inicialización:

### Paso 2.1: Crear la Base de Datos y Tablas

1.  Abre un cliente MySQL (MySQL Workbench, consola, etc.).
2.  Ejecuta completamente el archivo **`Sentencias_lapica.sql`**.

Este script realiza las siguientes acciones:
* Crea la base de datos `db_la_pica`.
* Crea todas las tablas relacionales (`Usuarios`, `Insumos`, `Ventas`, `Recetas`, etc.).
* Inserta los datos iniciales necesarios (usuarios de prueba, insumos de stock, platos del menú) para que el sistema funcione inmediatamente.

### Paso 2.2: Configuración de Conexión

Es **CRUCIAL** modificar la función `get_connection()` en el archivo **`main.py`** para que coincida con tus credenciales de MySQL:

```python
def get_connection():
    """Establece conexión con la base de datos MySQL"""
    try:
        return pymysql.connect(
            host='localhost',
            user='root',
            password='TU_CONTRASEÑA_MYSQL',   # <--- REEMPLAZA ESTO
            database='db_la_pica',
            autocommit=False
        )
    except pymysql.Error as e:
        print(f"Error grave de conexión: {e}")
        return None

```

## Paso 3: Instalación de Dependencias

Asegúrate de tener Python instalado.
Luego, instala las librerías necesarias ejecutando el siguiente comando en tu terminal: Bashpip install PyQt5 pymysql

### Paso 4. Ejecución del Software

Una vez configurada la conexión y las dependencias, ejecuta el archivo principal:Bashpython main.py
La aplicación se iniciará mostrando la ventana de Login.

### 5. Cuentas de Acceso de Prueba

El archivo SQL inicializa cuentas de usuario con diferentes roles para las pruebas:
| Rol | Usuario | Contraseña | Ventana de Acceso |
| :--- | :--- | :--- | :--- |
| **Administrador** | `admin` | `admin123` | AdminWindow (KPIs y CRUD Productos) |
| **Cajero** | `caja` | `caja123` | CajaWindow (Ventas e Historial) |
| **Cocina** | `cocina` | `cocina123` | CocinaWindow (Inventario y Movimientos) |

**Nota de Seguridad: La contraseña del supervisor requerida para anular ventas en el módulo de Caja es admin123.**

### 6. Secuencia de Uso Típica

**Login**: El usuario inicia sesión con su rol (caja, cocina o admin).
**Cocina**: El personal registra las Mermas/Pérdidas o Compras/Reposiciones en el Tab Movimientos para mantener el stock actual al día.
**Caja**: El cajero registra las ventas usando el Tab Nueva Venta, seleccionando productos, cantidades y finalizando la transacción.
**Administrador**: El dueño/gerente accede a la vista de KPIs para monitorear el desempeño (Venta Total, Ticket Promedio, Quiebres de Stock).

### 7. Archivos del Proyecto

**main.py**: Código principal de la lógica de negocio y las ventanas.
**Sentencias_lapica.sql**: Script para crear y poblar la Base de Datos.
**admin.ui, ventas.ui, cocina.ui, login.ui**: Archivos de diseño de interfaz gráfica (PyQt/Qt Designer).
**cocina.ui**: Interfaz gráfica para el módulo de cocina.
**ventas.ui**: Interfaz gráfica para el módulo de caja.
**admin.ui**: Interfaz gráfica para el módulo de administración.
