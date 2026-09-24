# Taller 2 - Tienda Virtual con SQLite y SQLAlchemy

Versión avanzada de la tienda virtual que usa Flask + SQLAlchemy + SQLite para persistir los productos y categorías en una base de datos real.

## Descripción

Este proyecto toma la lógica del Taller 1 y la mejora con una estructura más profesional:

- base de datos SQLite
- modelos ORM con `Categoria` y `Producto`
- comandos de Flask para inicializar y sembrar datos
- consultas con SQLAlchemy en lugar de leer un JSON a cada petición
- página de categorías con conteo de productos

## Funcionalidades

- Catálogo de productos desde la base de datos
- Filtro por categoría mediante query string
- Detalle de producto por SKU
- Listado de categorías con número de artículos
- Propiedad `disponible` en el modelo de producto
- Carga inicial de datos desde `productos.json`

## Requisitos

- Python 3.10 o superior
- Virtualenv
- Flask
- Flask-SQLAlchemy

## Instalación

```bash
cd ~/proyectos/tienda-virtual
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Si no existe `requirements.txt`, se puede instalar manualmente:

```bash
pip install flask flask-sqlalchemy
```

## Configuración inicial

El proyecto utiliza `config.py` para definir la configuración de la aplicación y la ruta de la base de datos SQLite.

## Crear la base de datos y sembrar datos

```bash
cd ~/proyectos/tienda-virtual
source venv/bin/activate
export FLASK_APP=run.py
flask init-db
flask seed-db
```

Esto crea la base de datos dentro de la carpeta `instance/` y carga los productos desde `app/data/productos.json`.

## Ejecutar la aplicación

```bash
cd ~/proyectos/tienda-virtual
source venv/bin/activate
export FLASK_APP=run.py
python run.py
```

O con Flask:

```bash
flask run
```

Luego abre en el navegador:

- `http://127.0.0.1:5000/`
- `http://127.0.0.1:5000/?categoria=1`
- `http://127.0.0.1:5000/producto/TEC-001`
- `http://127.0.0.1:5000/categorias`

## Comandos útiles de Flask

```bash
flask init-db      # crea las tablas
flask reset-db     # borra y recrea las tablas
flask seed-db      # inserta productos desde JSON
flask shell        # abre un shell interactivo con la app
```

Ejemplo dentro de `flask shell`:

```python
Producto.query.count()
Categoria.query.all()
Producto.query.filter_by(sku="TEC-001").first()
```

## Estructura del proyecto

```text
tienda-virtual/
├── app/
│   ├── __init__.py
│   ├── commands.py
│   ├── extensions.py
│   ├── models.py
│   ├── routes.py
│   ├── data/
│   │   └── productos.json
│   └── templates/
│       ├── base.html
│       ├── index.html
│       ├── detalle.html
│       └── categorias.html
├── instance/
│   └── tienda.db
├── .gitignore
├── README.md
├── config.py
├── requirements.txt
├── run.py
└── venv/
```

## Archivos clave

- `config.py`: configuración global de la aplicación y base de datos.
- `app/models.py`: define los modelos `Categoria` y `Producto`.
- `app/commands.py`: ejecuta `init-db`, `reset-db` y `seed-db`.
- `app/routes.py`: rutas principales y consultas ORM.
- `app/templates/index.html`: catálogo con filtros.
- `app/templates/detalle.html`: detalle del producto.
- `app/templates/categorias.html`: listado de categorías.

## Git

Se recomienda seguir un flujo simple con commits claros:

```bash
git status
git add .
git commit -m "Configura base de datos y modelos SQLAlchemy"
```

## Diferencia con el Taller 1

El Taller 1 usa JSON como almacenamiento. El Taller 2 introduce la persistencia real con SQLite y SQLAlchemy, lo cual es una base importante para proyectos más grandes y escalables.
