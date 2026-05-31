## Sistema Académico - Gestión de Estudiantes y Profesores

Este proyecto es un sistema de gestión académica desarrollado en Python, diseñado para administrar la información de estudiantes y profesores de manera organizada. Permite realizar operaciones completas de creación, lectura, actualización y eliminación de registros, además de búsquedas avanzadas y generación de estadísticas. Utiliza una estructura modular basada en buenas prácticas de desarrollo, separando modelos, lógica de negocio, almacenamiento e interfaz de usuario, facilitando su mantenimiento y escalabilidad.
---

## Las instrucciones para ejecutar el proyecto localmente (cómo instalar dependencias y cómo correr main.py).

## ✅ Antes de empezar

Asegúrate de tener **Python 3.9 o superior** instalado. Para verificarlo, abre la terminal y escribe:

```bash
python --version
```

Si ves algo como `Python 3.10.x`, estás listo.

---

## ▶️ Cómo correr el proyecto

Sigue estos pasos en orden:

### Paso 1 — Descarga el proyecto

Clónalo con Git:
```bash
git clone <URL-del-repositorio>
cd SistemaEst
```

O si lo descargaste como ZIP, descomprímelo y entra a la carpeta desde la terminal.

---

### Paso 2 — Crea el entorno virtual

El entorno virtual es un espacio aislado para instalar las librerías del proyecto sin afectar tu Python global.

**En Windows:**
```bash
python -m venv .venv
.venv\Scripts\activate
```

**En macOS o Linux:**
```bash
python -m venv .venv
source .venv/bin/activate
```

> 💡 Si usas **PyCharm**, esto se hace automático al abrir el proyecto. Solo acepta cuando el IDE te lo proponga.

Sabrás que está activo porque verás `(.venv)` al inicio de tu terminal.

---

### Paso 3 — Instala las dependencias

```bash
pip install -r requirements.txt
```

> Este proyecto solo usa librerías que vienen incluidas con Python (`json`, `os`, `datetime`), así que es posible que no se instale nada nuevo. Igual ejecuta el comando para estar seguro.

---

### Paso 4 — Ejecuta el programa

```bash
python main.py
```

¡Listo! Verás el menú principal en la terminal.

---

## 🖥️ ¿Qué puedo hacer en el programa?

Al correrlo, aparece este menú:

```
🏫 SISTEMA ACADÉMICO - GESTIÓN INTEGRAL
1️⃣  🎓 Gestión de Estudiantes
2️⃣  👨‍🏫 Gestión de Profesores
3️⃣  📊 Estadísticas Generales
4️⃣  ℹ️  Información del Sistema
0️⃣  🚪 Salir
```

Desde cada módulo puedes **agregar, ver, buscar, editar y eliminar** registros. Los datos se guardan solos en la carpeta `data/`.

---

## ❓ Problemas frecuentes

**"No module named..."**
→ Asegúrate de estar en la carpeta raíz del proyecto (donde está `main.py`) antes de ejecutarlo.

**El entorno virtual no se activa**
→ Verifica que creaste el `.venv` dentro de la carpeta del proyecto y que usas el comando correcto según tu sistema operativo.

---

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
