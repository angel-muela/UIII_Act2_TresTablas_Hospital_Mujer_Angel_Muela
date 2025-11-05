¡Claro que sí! Aquí tienes un proyecto Django completo para el "Hospital de la Mujer", siguiendo tus especificaciones.

Proyecto: Hospital de la Mujer
Lenguaje: Python
Framework: Django
Editor: VS Code

1. Procedimiento para crear carpeta del Proyecto: UIII_Hospitaldelamujer_0290

Abre tu terminal (o Git Bash/CMD) en la ubicación deseada y ejecuta:

code
Bash
download
content_copy
expand_less
mkdir UIII_Hospitaldelamujer_0290
2. Procedimiento para abrir VS Code sobre la carpeta UIII_Hospitaldelamujer_0290

Desde la terminal, navega a la carpeta que acabas de crear y ábrela con VS Code:

code
Bash
download
content_copy
expand_less
cd UIII_Hospitaldelamujer_0290
code .

Esto abrirá VS Code con la carpeta UIII_Hospitaldelamujer_0290 como raíz del proyecto.

3. Procedimiento para abrir terminal en VS Code

Dentro de VS Code, ve a Terminal -> New Terminal (o usa el atajo Ctrl + Shift + Ñ).

4. Procedimiento para crear carpeta entorno virtual “.venv” desde terminal de VS Code

En la terminal de VS Code, ejecuta:

code
Bash
download
content_copy
expand_less
python -m venv .venv
5. Procedimiento para activar el entorno virtual.

En Windows:

code
Bash
download
content_copy
expand_less
.venv\Scripts\activate

En macOS/Linux:

code
Bash
download
content_copy
expand_less
source .venv/bin/activate

Verás (.venv) al inicio de la línea de comandos, indicando que el entorno virtual está activo.

6. Procedimiento para activar intérprete de python.

Normalmente, al activar el entorno virtual, VS Code detectará automáticamente el intérprete de Python del entorno. Si no es así, puedes seleccionarlo manualmente:

Abre la paleta de comandos (Ctrl + Shift + P).

Escribe Python: Select Interpreter.

Selecciona la opción que apunte a Python 3.x.x (.venv).

7. Procedimiento para instalar Django

Con el entorno virtual activado, instala Django:

code
Bash
download
content_copy
expand_less
pip install django
8. Procedimiento para crear proyecto backend_Hospitalmujer sin duplicar carpeta.

Desde la raíz de tu proyecto (UIII_Hospitaldelamujer_0290), ejecuta:

code
Bash
download
content_copy
expand_less
django-admin startproject backend_Hospitalmujer .

El . al final es crucial para crear el proyecto directamente en la carpeta actual sin una subcarpeta extra.

9. Procedimiento para ejecutar servidor en el puerto 8023

Para verificar que Django está instalado y el proyecto se creó correctamente, ejecuta el servidor:

code
Bash
download
content_copy
expand_less
python manage.py runserver 8023
10. Procedimiento para copiar y pegar el link en el navegador.

Copia la dirección http://127.0.0.1:8023/ (o http://localhost:8023/) y pégala en tu navegador. Deberías ver la página de bienvenida de Django.

Configuración Inicial del Proyecto y Aplicación

Vamos a crear la estructura completa de archivos y carpetas como se solicitó antes de seguir con el código.

Estructura de Carpetas y Archivos (Paso 29)

code
Code
download
content_copy
expand_less
UIII_Hospitaldelamujer_0290/
├── .venv/
├── backend_Hospitalmujer/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── manage.py
└── app_Hospital/
    ├── migrations/
    │   └── __init__.py
    ├── static/
    ├── templates/
    │   ├── base.html
    │   ├── header.html
    │   ├── navbar.html
    │   ├── footer.html
    │   ├── inicio.html
    │   └── beneficiaria/
    │       ├── agregar_beneficiaria.html
    │       ├── ver_beneficiarias.html
    │       ├── actualizar_beneficiaria.html
    │       └── borrar_beneficiaria.html
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    └── views.py
11. Procedimiento para crear aplicación app_Hospital

Asegúrate de estar en la raíz del proyecto (UIII_Hospitaldelamujer_0290), donde se encuentra manage.py, y ejecuta:

code
Bash
download
content_copy
expand_less
python manage.py startapp app_Hospital
12. Aquí el modelo models.py

Abre el archivo app_Hospital/models.py y reemplaza su contenido con el siguiente:

code
Python
download
content_copy
expand_less
# app_Hospital/models.py
from django.db import models

# ==========================================
# MODELO: Beneficiaria
# ==========================================
class Beneficiaria(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    fecha_nacimiento = models.DateField()
    direccion = models.CharField(max_length=255)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    correo = models.EmailField(unique=True, blank=True, null=True)
    numero_expediente = models.CharField(max_length=50, unique=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"

# ==========================================
# MODELO: Personal
# ==========================================
class Personal(models.Model):
    id = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    puesto = models.CharField(max_length=100)
    especialidad = models.CharField(max_length=100, blank=True, null=True)
    telefono = models.CharField(max_length=20, blank=True, null=True)
    correo = models.EmailField(unique=True, blank=True, null=True)
    fecha_contratacion = models.DateField()

    def __str__(self):
        return f"{self.nombre} {self.apellido} - {self.puesto}"

# ==========================================
# MODELO: Consulta
# ==========================================
class Consulta(models.Model):
    id = models.AutoField(primary_key=True)
    beneficiaria = models.ForeignKey(Beneficiaria, on_delete=models.CASCADE, related_name='consultas')
    personal = models.ForeignKey(Personal, on_delete=models.CASCADE, related_name='consultas')
    fecha_consulta = models.DateTimeField(auto_now_add=True)
    motivo = models.TextField()
    diagnostico = models.TextField(blank=True, null=True)
    tratamiento = models.TextField(blank=True, null=True)
    costo = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)

    def __str__(self):
        return f"Consulta de {self.beneficiaria.nombre} el {self.fecha_consulta.strftime('%Y-%m-%d %H:%M')}"
12.5 Procedimiento para realizar las migraciones (makemigrations y migrate)

Desde la terminal en la raíz del proyecto, ejecuta:

code
Bash
download
content_copy
expand_less
python manage.py makemigrations
python manage.py migrate
13. Primero trabajamos con el MODELO: BENEFICIARIA
14. En views.py de app_Hospital crear las funciones con sus códigos correspondientes

Abre el archivo app_Hospital/views.py y reemplaza su contenido con el siguiente:

code
Python
download
content_copy
expand_less
# app_Hospital/views.py
from django.shortcuts import render, redirect, get_object_or_404
from .models import Beneficiaria
from django.views.decorators.http import require_POST

# Función para la página de inicio
def inicio_hospital(request):
    return render(request, 'inicio.html')

# Funciones para Beneficiarias
def agregar_beneficiaria(request):
    if request.method == 'POST':
        nombre = request.POST.get('nombre')
        apellido = request.POST.get('apellido')
        fecha_nacimiento = request.POST.get('fecha_nacimiento')
        direccion = request.POST.get('direccion')
        telefono = request.POST.get('telefono')
        correo = request.POST.get('correo')
        numero_expediente = request.POST.get('numero_expediente')

        Beneficiaria.objects.create(
            nombre=nombre,
            apellido=apellido,
            fecha_nacimiento=fecha_nacimiento,
            direccion=direccion,
            telefono=telefono,
            correo=correo,
            numero_expediente=numero_expediente
        )
        return redirect('ver_beneficiarias')
    return render(request, 'beneficiaria/agregar_beneficiaria.html')

def ver_beneficiarias(request):
    beneficiarias = Beneficiaria.objects.all()
    return render(request, 'beneficiaria/ver_beneficiarias.html', {'beneficiarias': beneficiarias})

def actualizar_beneficiaria(request, pk):
    beneficiaria = get_object_or_404(Beneficiaria, pk=pk)
    return render(request, 'beneficiaria/actualizar_beneficiaria.html', {'beneficiaria': beneficiaria})

@require_POST
def realizar_actualizacion_beneficiaria(request, pk):
    beneficiaria = get_object_or_404(Beneficiaria, pk=pk)
    beneficiaria.nombre = request.POST.get('nombre')
    beneficiaria.apellido = request.POST.get('apellido')
    beneficiaria.fecha_nacimiento = request.POST.get('fecha_nacimiento')
    beneficiaria.direccion = request.POST.get('direccion')
    beneficiaria.telefono = request.POST.get('telefono')
    beneficiaria.correo = request.POST.get('correo')
    beneficiaria.numero_expediente = request.POST.get('numero_expediente')
    beneficiaria.save()
    return redirect('ver_beneficiarias')

@require_POST
def borrar_beneficiaria(request, pk):
    beneficiaria = get_object_or_404(Beneficiaria, pk=pk)
    beneficiaria.delete()
    return redirect('ver_beneficiarias')
15. Crear la carpeta “templates” dentro de “app_Hospital”.

Si aún no lo has hecho, crea la carpeta templates dentro de app_Hospital.

code
Bash
download
content_copy
expand_less
mkdir app_Hospital/templates
16. En la carpeta templates crear los archivos html (base.html, header.html, navbar.html, footer.html, inicio.html).

Crea estos archivos vacíos dentro de app_Hospital/templates/.

17. En el archivo base.html agregar bootstrap para css y js.

Crea y edita app_Hospital/templates/base.html:

code
Html
play_circle
download
content_copy
expand_less
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Hospital de la Mujer{% endblock %}</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <!-- Font Awesome para iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        body {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f8f9fa; /* Color de fondo suave */
        }
        .content {
            flex: 1;
            padding-bottom: 70px; /* Espacio para el footer fijo */
        }
        .footer {
            position: fixed;
            bottom: 0;
            width: 100%;
            background-color: #e9ecef; /* Color del footer */
            color: #495057;
            text-align: center;
            padding: 15px 0;
            box-shadow: 0 -2px 5px rgba(0,0,0,0.1);
        }
        .navbar-custom {
            background-color: #e0f2f7; /* Azul claro muy suave */
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .navbar-brand, .nav-link {
            color: #007bff !important; /* Azul más vibrante para texto principal */
        }
        .dropdown-menu {
            background-color: #e0f2f7;
            border: none;
            box-shadow: 0 5px 10px rgba(0,0,0,0.1);
        }
        .dropdown-item {
            color: #007bff;
        }
        .dropdown-item:hover {
            background-color: #cce7ee;
        }
        .btn-custom-primary {
            background-color: #007bff;
            border-color: #007bff;
            color: white;
        }
        .btn-custom-primary:hover {
            background-color: #0056b3;
            border-color: #0056b3;
        }
        .table-custom th {
            background-color: #d1ecf1;
            color: #0c5460;
        }
        .table-custom tbody tr:nth-child(even) {
            background-color: #f0f8fa;
        }
    </style>
</head>
<body>
    {% include 'navbar.html' %}

    <div class="container mt-4 content">
        {% block content %}
        {% endblock %}
    </div>

    {% include 'footer.html' %}

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
</body>
</html>
18. En el archivo navbar.html incluir las opciones...

Crea y edita app_Hospital/templates/navbar.html:

code
Html
play_circle
download
content_copy
expand_less
<nav class="navbar navbar-expand-lg navbar-custom">
    <div class="container-fluid">
        <a class="navbar-brand" href="{% url 'inicio_hospital' %}">
            <i class="fas fa-hospital-alt me-2"></i>Sistema de Administración Hospital de la Mujer
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item">
                    <a class="nav-link" href="{% url 'inicio_hospital' %}"><i class="fas fa-home me-1"></i>Inicio</a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="beneficiariasDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-female me-1"></i>Beneficiarias
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="beneficiariasDropdown">
                        <li><a class="dropdown-item" href="{% url 'agregar_beneficiaria' %}">Agregar Beneficiaria</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_beneficiarias' %}">Ver Beneficiarias</a></li>
                    </ul>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="personalDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-user-md me-1"></i>Personal
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="personalDropdown">
                        <li><a class="dropdown-item" href="#">Agregar Personal</a></li>
                        <li><a class="dropdown-item" href="#">Ver Personal</a></li>
                    </ul>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="consultasDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-notes-medical me-1"></i>Consultas
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="consultasDropdown">
                        <li><a class="dropdown-item" href="#">Agregar Consulta</a></li>
                        <li><a class="dropdown-item" href="#">Ver Consultas</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</nav>
19. En el archivo footer.html incluir derechos de autor...

Crea y edita app_Hospital/templates/footer.html:

code
Html
play_circle
download
content_copy
expand_less
<footer class="footer">
    <div class="container">
        <span>&copy; {{ current_year }} Derechos de Autor. Creado por Ing. Eliseo Nava, Cbtis 128.</span>
        <br>
        <span>Fecha del Sistema: {{ current_date }}</span>
    </div>
</footer>

{% load static %}
<script>
    document.addEventListener('DOMContentLoaded', function() {
        // Obtener la fecha actual
        const now = new Date();
        const year = now.getFullYear();
        const date = now.toLocaleDateString('es-ES', { day: '2-digit', month: '2-digit', year: 'numeric' });

        // Actualizar el año en el footer
        const yearSpan = document.querySelector('.footer span:first-child');
        if (yearSpan) {
            yearSpan.innerHTML = `&copy; ${year} Derechos de Autor. Creado por Ing. Eliseo Nava, Cbtis 128.`;
        }

        // Actualizar la fecha en el footer
        const dateSpan = document.querySelector('.footer span:last-child');
        if (dateSpan) {
            dateSpan.textContent = `Fecha del Sistema: ${date}`;
        }
    });
</script>

Nota: Para que el current_year y current_date sean dinámicos, tendrías que pasarlos desde el contexto de Django en cada vista, o usar JavaScript como se muestra arriba. Para este ejemplo, he optado por JavaScript para mantener las vistas limpias, ya que es un elemento del footer y no cambia frecuentemente.

20. En el archivo inicio.html se usa para colocar información del sistema más una imagen tomada desde la red sobre un hospital de la mujer.

Crea y edita app_Hospital/templates/inicio.html:

code
Html
play_circle
download
content_copy
expand_less
{% extends 'base.html' %}

{% block title %}Inicio - Hospital de la Mujer{% endblock %}

{% block content %}
<div class="text-center my-5">
    <h1 class="display-4 mb-4">Bienvenido al Sistema de Administración del Hospital de la Mujer</h1>
    <p class="lead">
        Este sistema está diseñado para gestionar de manera eficiente la información de beneficiarias, personal médico y consultas, optimizando los procesos administrativos del Hospital de la Mujer.
    </p>
    <p>
        Nuestro objetivo es proporcionar una herramienta robusta y fácil de usar para mejorar la atención y el seguimiento de nuestras pacientes.
    </p>
</div>

<div class="row justify-content-center mb-5">
    <div class="col-md-8">
        <div class="card shadow-sm">
            <div class="card-body">
                <h5 class="card-title text-center mb-3">Nuestra Misión</h5>
                <p class="card-text">
                    Brindar atención médica integral y especializada a las mujeres, con un enfoque en la calidad, la calidez y el respeto, promoviendo su bienestar y salud en todas las etapas de su vida.
                </p>
                <p class="card-text">
                    Nos comprometemos a utilizar tecnología de vanguardia y un equipo humano altamente capacitado para ofrecer los mejores servicios de salud.
                </p>
            </div>
        </div>
    </div>
</div>

<div class="text-center mb-5">
    <h3>Instalaciones del Hospital de la Mujer</h3>
    <p>Una vista de nuestras modernas instalaciones dedicadas al cuidado de la mujer.</p>
    <img src="https://via.placeholder.com/800x450?text=Hospital+de+la+Mujer" class="img-fluid rounded shadow-lg mt-3" alt="Imagen del Hospital de la Mujer">
    <!-- Puedes reemplazar la URL anterior con una imagen real del Hospital de la Mujer que encuentres en la red -->
</div>
{% endblock %}

Nota: He usado un placeholder de imagen. Puedes reemplazar https://via.placeholder.com/800x450?text=Hospital+de+la+Mujer con la URL de una imagen real de un hospital de la mujer que encuentres en línea.

21. Crear la subcarpeta 'beneficiaria' dentro de app_Hospital\templates.
code
Bash
download
content_copy
expand_less
mkdir app_Hospital/templates/beneficiaria
22. Crear los archivos html con su código correspondiente de (agregar_beneficiaria.html, ver_beneficiarias.html, actualizar_beneficiaria.html, borrar_beneficiaria.html) dentro de app_Hospital\templates\beneficiaria.

app_Hospital/templates/beneficiaria/agregar_beneficiaria.html

code
Html
play_circle
download
content_copy
expand_less
{% extends 'base.html' %}

{% block title %}Agregar Beneficiaria{% endblock %}

{% block content %}
<div class="row justify-content-center">
    <div class="col-md-8">
        <div class="card shadow-sm p-4" style="background-color: #f0f8fa;">
            <h2 class="text-center mb-4" style="color: #007bff;">Agregar Nueva Beneficiaria</h2>
            <form method="post">
                {% csrf_token %}
                <div class="mb-3">
                    <label for="nombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="nombre" name="nombre" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="apellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="apellido" name="apellido" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="fecha_nacimiento" class="form-label">Fecha de Nacimiento:</label>
                    <input type="date" class="form-control" id="fecha_nacimiento" name="fecha_nacimiento" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="direccion" class="form-label">Dirección:</label>
                    <input type="text" class="form-control" id="direccion" name="direccion" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="telefono" class="form-label">Teléfono:</label>
                    <input type="tel" class="form-control" id="telefono" name="telefono" style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="correo" class="form-label">Correo Electrónico:</label>
                    <input type="email" class="form-control" id="correo" name="correo" style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="numero_expediente" class="form-label">Número de Expediente:</label>
                    <input type="text" class="form-control" id="numero_expediente" name="numero_expediente" required style="border-color: #cce7ee;">
                </div>
                <div class="d-grid gap-2">
                    <button type="submit" class="btn btn-custom-primary">Guardar Beneficiaria</button>
                    <a href="{% url 'ver_beneficiarias' %}" class="btn btn-secondary">Cancelar</a>
                </div>
            </form>
        </div>
    </div>
</div>
{% endblock %}

app_Hospital/templates/beneficiaria/ver_beneficiarias.html

code
Html
play_circle
download
content_copy
expand_less
{% extends 'base.html' %}

{% block title %}Ver Beneficiarias{% endblock %}

{% block content %}
<h2 class="text-center mb-4" style="color: #007bff;">Listado de Beneficiarias</h2>

<div class="mb-3 text-end">
    <a href="{% url 'agregar_beneficiaria' %}" class="btn btn-custom-primary"><i class="fas fa-plus-circle me-2"></i>Agregar Nueva Beneficiaria</a>
</div>

{% if beneficiarias %}
<div class="table-responsive">
    <table class="table table-striped table-hover table-custom">
        <thead>
            <tr>
                <th>ID</th>
                <th>Nombre</th>
                <th>Apellido</th>
                <th>Fecha de Nacimiento</th>
                <th>Dirección</th>
                <th>Teléfono</th>
                <th>Correo</th>
                <th>Expediente</th>
                <th>Acciones</th>
            </tr>
        </thead>
        <tbody>
            {% for beneficiaria in beneficiarias %}
            <tr>
                <td>{{ beneficiaria.id }}</td>
                <td>{{ beneficiaria.nombre }}</td>
                <td>{{ beneficiaria.apellido }}</td>
                <td>{{ beneficiaria.fecha_nacimiento|date:"d/m/Y" }}</td>
                <td>{{ beneficiaria.direccion }}</td>
                <td>{{ beneficiaria.telefono|default_if_none:"N/A" }}</td>
                <td>{{ beneficiaria.correo|default_if_none:"N/A" }}</td>
                <td>{{ beneficiaria.numero_expediente }}</td>
                <td>
                    <div class="d-flex">
                        <a href="{% url 'actualizar_beneficiaria' beneficiaria.pk %}" class="btn btn-sm btn-info me-1" title="Editar"><i class="fas fa-edit"></i></a>
                        <form action="{% url 'borrar_beneficiaria' beneficiaria.pk %}" method="post" style="display:inline;" onsubmit="return confirm('¿Está seguro de que desea eliminar a esta beneficiaria?');">
                            {% csrf_token %}
                            <button type="submit" class="btn btn-sm btn-danger" title="Eliminar"><i class="fas fa-trash-alt"></i></button>
                        </form>
                    </div>
                </td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
</div>
{% else %}
<div class="alert alert-info text-center" role="alert">
    No hay beneficiarias registradas aún.
</div>
{% endif %}
{% endblock %}

app_Hospital/templates/beneficiaria/actualizar_beneficiaria.html

code
Html
play_circle
download
content_copy
expand_less
{% extends 'base.html' %}

{% block title %}Actualizar Beneficiaria{% endblock %}

{% block content %}
<div class="row justify-content-center">
    <div class="col-md-8">
        <div class="card shadow-sm p-4" style="background-color: #f0f8fa;">
            <h2 class="text-center mb-4" style="color: #007bff;">Actualizar Beneficiaria</h2>
            <form method="post" action="{% url 'realizar_actualizacion_beneficiaria' beneficiaria.pk %}">
                {% csrf_token %}
                <div class="mb-3">
                    <label for="nombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="nombre" name="nombre" value="{{ beneficiaria.nombre }}" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="apellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="apellido" name="apellido" value="{{ beneficiaria.apellido }}" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="fecha_nacimiento" class="form-label">Fecha de Nacimiento:</label>
                    <input type="date" class="form-control" id="fecha_nacimiento" name="fecha_nacimiento" value="{{ beneficiaria.fecha_nacimiento|date:'Y-m-d' }}" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="direccion" class="form-label">Dirección:</label>
                    <input type="text" class="form-control" id="direccion" name="direccion" value="{{ beneficiaria.direccion }}" required style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="telefono" class="form-label">Teléfono:</label>
                    <input type="tel" class="form-control" id="telefono" name="telefono" value="{{ beneficiaria.telefono|default_if_none:'' }}" style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="correo" class="form-label">Correo Electrónico:</label>
                    <input type="email" class="form-control" id="correo" name="correo" value="{{ beneficiaria.correo|default_if_none:'' }}" style="border-color: #cce7ee;">
                </div>
                <div class="mb-3">
                    <label for="numero_expediente" class="form-label">Número de Expediente:</label>
                    <input type="text" class="form-control" id="numero_expediente" name="numero_expediente" value="{{ beneficiaria.numero_expediente }}" required style="border-color: #cce7ee;">
                </div>
                <div class="d-grid gap-2">
                    <button type="submit" class="btn btn-custom-primary">Actualizar Beneficiaria</button>
                    <a href="{% url 'ver_beneficiarias' %}" class="btn btn-secondary">Cancelar</a>
                </div>
            </form>
        </div>
    </div>
</div>
{% endblock %}

app_Hospital/templates/beneficiaria/borrar_beneficiaria.html
(Este archivo no es estrictamente necesario ya que la eliminación se maneja directamente desde ver_beneficiarias.html con un POST. Sin embargo, si deseas una página de confirmación dedicada, aquí tienes el código. Para este proyecto, el borrar_beneficiaria en ver_beneficiarias.html ya incluye una confirmación JS.)

code
Html
play_circle
download
content_copy
expand_less
{% extends 'base.html' %}

{% block title %}Confirmar Eliminación{% endblock %}

{% block content %}
<div class="row justify-content-center">
    <div class="col-md-6">
        <div class="alert alert-danger text-center shadow-sm" role="alert">
            <h4 class="alert-heading">¿Está seguro de que desea eliminar a esta beneficiaria?</h4>
            <p><strong>ID:</strong> {{ beneficiaria.id }}</p>
            <p><strong>Nombre:</strong> {{ beneficiaria.nombre }} {{ beneficiaria.apellido }}</p>
            <p>Esta acción es irreversible.</p>
            <hr>
            <form action="{% url 'borrar_beneficiaria' beneficiaria.pk %}" method="post">
                {% csrf_token %}
                <button type="submit" class="btn btn-danger me-2"><i class="fas fa-trash-alt me-2"></i>Sí, Eliminar</button>
                <a href="{% url 'ver_beneficiarias' %}" class="btn btn-secondary"><i class="fas fa-times me-2"></i>Cancelar</a>
            </form>
        </div>
    </div>
</div>
{% endblock %}
23. No utilizar forms.py.

Hemos utilizado directamente request.POST.get() en las vistas.

24. Procedimiento para crear el archivo urls.py en app_Hospital con el código correspondiente para acceder a las funciones de views.py para operaciones de CRUD en beneficiarias.

Crea el archivo app_Hospital/urls.py y añade:

code
Python
download
content_copy
expand_less
# app_Hospital/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_hospital, name='inicio_hospital'),
    path('beneficiarias/', views.ver_beneficiarias, name='ver_beneficiarias'),
    path('beneficiarias/agregar/', views.agregar_beneficiaria, name='agregar_beneficiaria'),
    path('beneficiarias/actualizar/<int:pk>/', views.actual

¡Excelente! Aquí están los pasos restantes para completar tu proyecto Django, desde el 25 hasta el 31, incluyendo las configuraciones finales para que todo funcione.

25. Procedimiento para agregar app_Hospital en settings.py de backend_Hospitalmujer

Abre el archivo backend_Hospitalmujer/settings.py. Busca la lista INSTALLED_APPS y añade 'app_Hospital' a ella.

code
Python
download
content_copy
expand_less
# backend_Hospitalmujer/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app_Hospital', # ¡Añade esta línea!
]
26. Realizar las configuraciones correspondiente a urls.py de backend_Hospitalmujer para enlazar con app_Hospital

Abre el archivo backend_Hospitalmujer/urls.py. Importa include y añade una entrada para app_Hospital.

code
Python
download
content_copy
expand_less
# backend_Hospitalmujer/urls.py
from django.contrib import admin
from django.urls import path, include # Importa 'include'

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_Hospital.urls')), # Enlaza la URL raíz a app_Hospital
]
27. Procedimiento para registrar los modelos en admin.py y volver a realizar las migraciones.

Abre el archivo app_Hospital/admin.py y reemplázalo con el siguiente contenido para registrar tus modelos.

code
Python
download
content_copy
expand_less
# app_Hospital/admin.py
from django.contrib import admin
from .models import Beneficiaria, Personal, Consulta

# Registra el modelo Beneficiaria
admin.site.register(Beneficiaria)

# Deja Personal y Consulta comentados por ahora, según la indicación 27
# admin.site.register(Personal)
# admin.site.register(Consulta)

Luego, vuelve a la terminal y ejecuta las migraciones. Aunque no hay cambios en los modelos de Beneficiaria, es una buena práctica si hubieras añadido los otros modelos o si Django detecta algo.

code
Bash
download
content_copy
expand_less
python manage.py makemigrations
python manage.py migrate

Si aún no tienes un superusuario para acceder al panel de administración de Django, créalo ahora:

code
Bash
download
content_copy
expand_less
python manage.py createsuperuser

Sigue las instrucciones en pantalla para crear un nombre de usuario, correo electrónico y contraseña.

27 (segundo punto). Por lo pronto solo trabajar con “Beneficiaria” dejar pendiente # MODELO: PERSONAL y # MODELO: CONSULTA

Ya hemos seguido esta instrucción en los pasos anteriores, tanto en models.py (aunque los modelos están definidos, solo Beneficiaria tiene vistas y URLs implementadas) como en admin.py (donde Personal y Consulta están comentados).

28. Utilizar colores suaves, atractivos y modernos, el código de las páginas web sencillas.

Esto se ha aplicado en los archivos HTML (base.html, etc.) usando clases de Bootstrap y estilos CSS personalizados para lograr una paleta de colores suaves (azules, grises claros) y una interfaz limpia.

28 (segundo punto). No validar entrada de datos.

Según lo solicitado, no se ha implementado validación de datos a nivel de formularios o modelos en las vistas. Los campos HTML tienen required para una validación básica del navegador, pero no hay validación de Django más profunda.

29. Al inicio crear la estructura completa de carpetas y archivos.

Esta instrucción se abordó al principio de la respuesta, guiándote a crear la estructura de directorios y archivos antes de llenarlos con código.

30. Proyecto totalmente funcional.

Con todos los pasos anteriores completados, el módulo de "Beneficiarias" del proyecto debería ser totalmente funcional, permitiendo agregar, ver, actualizar y eliminar registros de beneficiarias.

31. Finalmente ejecutar servidor en el puerto 8036.

Para iniciar tu aplicación web y probarla, asegúrate de que tu entorno virtual esté activado y ejecuta el servidor de Django en el puerto especificado:

code
Bash
download
content_copy
expand_less
python manage.py runserver 8036

¡Felicidades!

Ahora puedes abrir tu navegador y dirigirte a http://127.0.0.1:8036/ (o http://localhost:8036/).

Verás la página de inicio.html.

En la barra de navegación, haz clic en "Beneficiarias" y luego en "Agregar Beneficiaria" para añadir un registro.

Luego, haz clic en "Ver Beneficiarias" para listar las beneficiarias, editarlas o eliminarlas.

También puedes acceder al panel de administración en http://127.0.0.1:8036/admin/ con el superusuario que creaste para gestionar las beneficiarias desde allí.
