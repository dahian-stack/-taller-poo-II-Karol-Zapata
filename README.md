## Sistema Académico - Gestión de Estudiantes y Profesores
Sistema desarrollado en Python bajo una estructura organizada y modular, siguiendo buenas prácticas de desarrollo y Programación Orientada a Objetos. Permite gestionar la información de estudiantes, profesores, y en futuras versiones materias y calificaciones.

## Estructura del Proyecto y Descripción de Archivos

```
Desempeno.Inst_Eva/
├── main.py                     → Archivo principal de ejecución
├── data/                       → Almacena los archivos JSON con la información
│   ├── students.json          → Datos de estudiantes (generado automáticamente)
│   └── teachers.json          → Datos de profesores (generado automáticamente)
├── src/                       → Código fuente del sistema
│   ├── __init__.py            → Archivo para reconocer el directorio como paquete
│   ├── models/                → Definición de las clases / modelos de datos
│   │   ├── __init__.py
│   │   ├── student.py         → Modelo y lógica de la entidad Estudiante
│   │   └── teacher.py         → Modelo y lógica de la entidad Profesor
│   ├── storage/               → Manejo de persistencia de datos
│   │   ├── __init__.py
│   │   └── json_storage.py    → Lectura, escritura y gestión de archivos JSON
│   ├── services/              → Lógica de negocio, reglas y operaciones CRUD
│   │   ├── __init__.py
│   │   ├── student_service.py → Servicios y reglas para gestión de estudiantes
│   │   └── teacher_service.py → Servicios y reglas para gestión de profesores
│   └── ui/                    → Interfaz de usuario, menús y entrada de datos
│       ├── __init__.py
│       ├── menu.py            → Interfaz y menú del módulo Estudiantes
│       └── teacher_menu.py    → Interfaz y menú del módulo Profesores
├── requirements.txt           → Dependencias del proyecto
└── README.md                  → Este archivo, documentación general
```

---

## Detalle de Contenido por Archivo

### `main.py`
- **Ubicación:** Raíz del proyecto
- **Contenido:**
  - Importa los módulos de interfaz de usuario
  - Define la clase `AcademicSystemMenu` con el menú principal
  - Gestiona la navegación entre módulos: Estudiantes, Profesores, Estadísticas y Salida
  - Manejo de errores y excepciones generales del sistema
- **Función:** Es el punto de entrada que conecta todos los componentes y arranca la aplicación.

---

### Carpeta `src/models/`

#### `student.py`
- **Contenido:**
  - Clase `Student` con atributos: `id`, `name`, `age`, `grade`, `email`, `created_at`
  - Método `to_dict()`: Convierte el objeto a diccionario para guardar en JSON
  - Método de clase `from_dict()`: Crea un objeto `Student` desde datos de diccionario
  - Método `__str__()`: Representación legible de los datos
- **Función:** Define la estructura y características de un estudiante.

#### `teacher.py`
- **Contenido:**
  - Clase `Teacher` con atributos: `id`, `name`, `specialty` (especialidad), `email`, `salary` (salario opcional), `created_at`
  - Métodos `to_dict()`, `from_dict()` y `__str__()` con la misma lógica que el modelo de estudiante
- **Función:** Define la estructura y características de un profesor.

#### `__init__.py`
- Archivo vacío que indica a Python que esta carpeta es un paquete importable.

---

### Carpeta `src/storage/`

#### `json_storage.py`
- **Contenido:**
  - Clase `JSONStorage` encargada de toda la lectura y escritura
  - Métodos:
    - `_ensure_data_directory()`: Crea la carpeta `data/` si no existe
    - `load_students()`: Lee y carga datos desde el archivo JSON
    - `save_students()`: Guarda la lista de objetos en formato JSON
    - `file_exists()`, `get_file_info()`: Utilidades de verificación
  - Manejo de errores: Archivos corruptos, respaldo automático, excepciones
- **Función:** Capa de persistencia reutilizable para cualquier entidad (estudiantes, profesores, etc.).

#### `__init__.py`
- Archivo vacío de configuración de paquete.

---

### Carpeta `src/services/`

#### `student_service.py`
- **Contenido:**
  - Clase `StudentService` que conecta el modelo con el almacenamiento
  - Inyección de dependencias: Recibe el almacenamiento o usa uno por defecto
  - Operaciones CRUD completas:
    - `add_student()`: Con validaciones de nombre, edad, correo único
    - `get_all_students()`, `get_student_by_id()`
    - `update_student()`: Con respaldo de datos y rollback si hay error
    - `delete_student()`: Con confirmación y restauración
  - Búsquedas: por término, grado, rango de edad
  - Estadísticas: total, promedio de edad, distribución por grados
- **Función:** Contiene **toda la lógica de negocio** y reglas para gestionar estudiantes. No interactúa directamente con la pantalla ni con el archivo, coordina todo.

#### `teacher_service.py`
- **Contenido:**
  - Clase `TeacherService` siguiendo el mismo patrón que `StudentService`
  - Validaciones específicas: especialidad obligatoria, salario no negativo, correo único
  - Búsquedas: por especialidad, rango de salario
  - Estadísticas: promedio salarial, cantidad por especialidad
  - Reutiliza `JSONStorage` apuntando al archivo `teachers.json`
- **Función:** Lógica de negocio y reglas para la gestión completa de profesores.

#### `__init__.py`
- Archivo vacío de configuración de paquete.

---

### Carpeta `src/ui/`

#### `menu.py`
- **Contenido:**
  - Clase `StudentMenu` con la interfaz de usuario del módulo de estudiantes
  - Menú principal y submenús de navegación
  - Métodos para entrada de datos con validación de tipos
  - Funciones para mostrar listados, detalles, estadísticas
  - Métodos `handle_*()` que conectan las opciones del menú con los servicios
- **Función:** Todo lo que el usuario ve y utiliza para interactuar con la información de estudiantes.

#### `teacher_menu.py`
- **Contenido:**
  - Clase `TeacherMenu` idéntica en estructura a `StudentMenu`
  - Menús adaptados a los campos del profesor (especialidad, salario)
  - Formato especial para mostrar salarios y estadísticas económicas
- **Función:** Interfaz completa para la gestión visual de profesores.

#### `__init__.py`
- Archivo vacío de configuración de paquete.

---

### Carpeta `data/`
> *Esta carpeta se crea automáticamente al ejecutar el sistema por primera vez*

- **`students.json`:** Almacena en formato JSON la lista completa de estudiantes registrados.
- **`teachers.json`:** Almacena en formato JSON la lista completa de profesores registrados.

---

### Otros archivos

#### `requirements.txt`
- Lista las librerías necesarias para que el proyecto funcione.
- Actualmente no requiere librerías externas, usa solo librerías estándar de Python.

#### `README.md`
- Este mismo archivo. Contiene la descripción, estructura y documentación de todo el proyecto.
