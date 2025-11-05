Proyecto: Hospital de la Mujer - Guía Completa
1. Procedimiento para crear carpeta del Proyecto: UIII_Hospitaldelamujer_0290
Abre tu terminal (o línea de comandos) y ejecuta el siguiente comando para crear la carpeta principal del proyecto:
code
Bash
mkdir UIII_Hospitaldelamujer_0290
cd UIII_Hospitaldelamujer_0290
2. Procedimiento para abrir VS Code sobre la carpeta UIII_Hospitaldelamujer_0290
Desde la terminal, asegúrate de estar dentro de la carpeta UIII_Hospitaldelamujer_0290 y luego ejecuta:
code
Bash
code .
Esto abrirá VS Code con la carpeta del proyecto cargada.
3. Procedimiento para abrir terminal en VS Code
Dentro de VS Code, puedes abrir la terminal yendo a Terminal > New Terminal o usando el atajo de teclado Ctrl + Shift + Ñ (Windows/Linux) o ` (macOS).
4. Procedimiento para crear carpeta entorno virtual “.venv” desde terminal de VS Code
En la terminal de VS Code, ejecuta:
code
Bash
python -m venv .venv
5. Procedimiento para activar el entorno virtual.
Windows:
code
Bash
.venv\Scripts\activate
macOS/Linux:
code
Bash
source .venv/bin/activate
Verás (.venv) al inicio de tu prompt, indicando que el entorno virtual está activo.
6. Procedimiento para activar intérprete de python.
VS Code debería detectarlo automáticamente al activar el entorno virtual. Si no es así, presiona Ctrl + Shift + P (o Cmd + Shift + P) para abrir la paleta de comandos, busca "Python: Select Interpreter" y elige la opción que apunte a .\.venv\Scripts\python.exe (Windows) o ./.venv/bin/python (macOS/Linux).
7. Procedimiento para instalar Django
Con el entorno virtual activado, instala Django:
code
Bash
pip install django
8. Procedimiento para crear proyecto backend_Hospitalmujer sin duplicar carpeta.
Asegúrate de estar en la raíz de tu proyecto (UIII_Hospitaldelamujer_0290) y ejecuta:
code
Bash
django-admin startproject backend_Hospitalmujer .
El . al final evita que se cree una carpeta anidada con el mismo nombre.
9. Procedimiento para ejecutar servidor en el puerto 8023
Desde la raíz del proyecto, ejecuta:
code
Bash
python manage.py runserver 8023
10. Procedimiento para copiar y pegar el link en el navegador.
Una vez que el servidor esté ejecutándose, verás un mensaje como: Starting development server at http://127.0.0.1:8023/. Copia esa URL (http://127.0.0.1:8023/) y pégala en tu navegador. Deberías ver la página de bienvenida de Django.
11. Procedimiento para crear aplicación app_Hospital
Abre una nueva terminal en VS Code (o detén el servidor con Ctrl+C y luego reinícialo más tarde) y, desde la raíz del proyecto, ejecuta:
code
Bash
python manage.py startapp app_Hospital
29. Al inicio crear la estructura completa de carpetas y archivos.
Vamos a crear la estructura de carpetas y archivos ahora, aunque algunos estarán vacíos por el momento.
code
Code
UIII_Hospitaldelamujer_0290/
├── .venv/
├── backend_Hospitalmujer/
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── app_Hospital/
│   ├── migrations/
│   │   └── __init__.py
│   ├── templates/
│   │   └── beneficiaria/
│   │       ├── agregar_beneficiaria.html
│   │       ├── actualizar_beneficiaria.html
│   │       ├── borrar_beneficiaria.html
│   │       └── ver_beneficiarias.html
│   │   ├── base.html
│   │   ├── header.html
│   │   ├── navbar.html
│   │   ├── footer.html
│   │   └── inicio.html
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tests.py
│   ├── urls.py  <-- ¡Lo crearemos nosotros!
│   └── views.py
└── manage.py
Puedes crear estas carpetas y archivos manualmente en VS Code o usar comandos mkdir y touch en la terminal.
12. Aquí el modelo models.py
Abre app_Hospital/models.py y pega el siguiente código:
code
Python
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
# MODELO: Personal (Pendiente)
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
# MODELO: Consulta (Pendiente)
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
25. Procedimiento para agregar app_Hospital en settings.py de backend_Hospitalmujer
Abre backend_Hospitalmujer/settings.py y busca la lista INSTALLED_APPS. Agrega 'app_Hospital' a la lista:
code
Python
# backend_Hospitalmujer/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app_Hospital', # Agrega tu app aquí
]
12.5 Procedimiento para realizar las migraciones (makemigrations y migrate).
Asegúrate de que tu entorno virtual esté activado y que estés en la raíz del proyecto. Ejecuta:
code
Bash
python manage.py makemigrations
python manage.py migrate
27. Procedimiento para registrar los modelos en admin.py y volver a realizar las migraciones.
Abre app_Hospital/admin.py y modifica el archivo para registrar el modelo Beneficiaria:
code
Python
# app_Hospital/admin.py

from django.contrib import admin
from .models import Beneficiaria, Personal, Consulta

@admin.register(Beneficiaria)
class BeneficiariaAdmin(admin.ModelAdmin):
    list_display = ('nombre', 'apellido', 'fecha_nacimiento', 'numero_expediente', 'correo', 'telefono')
    search_fields = ('nombre', 'apellido', 'numero_expediente')
    list_filter = ('fecha_nacimiento',)

# Por ahora solo trabajamos con Beneficiaria.
# Puedes descomentar y adaptar Personal y Consulta cuando los necesites.
# @admin.register(Personal)
# class PersonalAdmin(admin.ModelAdmin):
#     list_display = ('nombre', 'apellido', 'puesto', 'especialidad', 'fecha_contratacion')
#     search_fields = ('nombre', 'apellido', 'puesto')
#     list_filter = ('puesto', 'especialidad')

# @admin.register(Consulta)
# class ConsultaAdmin(admin.ModelAdmin):
#     list_display = ('beneficiaria', 'personal', 'fecha_consulta', 'costo')
#     search_fields = ('beneficiaria__nombre', 'beneficiaria__apellido', 'personal__nombre', 'personal__apellido', 'motivo')
#     list_filter = ('fecha_consulta',)
Ahora, como hemos modificado admin.py (lo que no afecta directamente a la base de datos pero es buena práctica), y para estar seguros de que todo está en orden, vamos a crear un superusuario para acceder al panel de administración de Django:
code
Bash
python manage.py createsuperuser
Sigue las instrucciones para crear tu usuario y contraseña.
No es necesario "volver a realizar las migraciones" por un cambio en admin.py, ya que solo afecta a la interfaz de administración y no a la estructura de la base de datos. Las migraciones anteriores ya crearon las tablas.
14. En view de app_Hospital crear las funciones con sus códigos correspondientes (inicio_hospital, agregar_beneficiaria, actualizar_beneficiaria, realizar_actualizacion_beneficiaria, borrar_beneficiaria)
Abre app_Hospital/views.py y pega el siguiente código. Nota que realizar_actualizacion_beneficiaria se integrará dentro de actualizar_beneficiaria para manejar ambos métodos GET y POST.
code
Python
# app_Hospital/views.py

from django.shortcuts import render, redirect, get_object_or_404
from .models import Beneficiaria

def inicio_hospital(request):
    return render(request, 'inicio.html')

def agregar_beneficiaria(request):
    if request.method == 'POST':
        # No se usa forms.py, así que procesamos directamente los datos del POST
        nombre = request.POST.get('nombre')
        apellido = request.POST.get('apellido')
        fecha_nacimiento = request.POST.get('fecha_nacimiento')
        direccion = request.POST.get('direccion')
        telefono = request.POST.get('telefono')
        correo = request.POST.get('correo')
        numero_expediente = request.POST.get('numero_expediente')

        # Creamos y guardamos la beneficiaria
        Beneficiaria.objects.create(
            nombre=nombre,
            apellido=apellido,
            fecha_nacimiento=fecha_nacimiento,
            direccion=direccion,
            telefono=telefono,
            correo=correo,
            numero_expediente=numero_expediente
        )
        return redirect('ver_beneficiarias') # Redirige a la lista de beneficiarias
    return render(request, 'beneficiaria/agregar_beneficiaria.html')

def ver_beneficiarias(request):
    beneficiarias = Beneficiaria.objects.all().order_by('apellido', 'nombre')
    return render(request, 'beneficiaria/ver_beneficiarias.html', {'beneficiarias': beneficiarias})

def actualizar_beneficiaria(request, pk):
    beneficiaria = get_object_or_404(Beneficiaria, pk=pk)
    if request.method == 'POST':
        beneficiaria.nombre = request.POST.get('nombre')
        beneficiaria.apellido = request.POST.get('apellido')
        beneficiaria.fecha_nacimiento = request.POST.get('fecha_nacimiento')
        beneficiaria.direccion = request.POST.get('direccion')
        beneficiaria.telefono = request.POST.get('telefono')
        beneficiaria.correo = request.POST.get('correo')
        beneficiaria.numero_expediente = request.POST.get('numero_expediente')
        beneficiaria.save()
        return redirect('ver_beneficiarias')
    return render(request, 'beneficiaria/actualizar_beneficiaria.html', {'beneficiaria': beneficiaria})

def borrar_beneficiaria(request, pk):
    beneficiaria = get_object_or_404(Beneficiaria, pk=pk)
    if request.method == 'POST':
        beneficiaria.delete()
        return redirect('ver_beneficiarias')
    return render(request, 'beneficiaria/borrar_beneficiaria.html', {'beneficiaria': beneficiaria})
24. Procedimiento para crear el archivo urls.py en app_Hospital con el código correspondiente para acceder a las funciones de views.py para operaciones de crud en beneficiarias.
Crea el archivo app_Hospital/urls.py y pega el siguiente código:
code
Python
# app_Hospital/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_hospital, name='inicio_hospital'),
    path('beneficiarias/agregar/', views.agregar_beneficiaria, name='agregar_beneficiaria'),
    path('beneficiarias/', views.ver_beneficiarias, name='ver_beneficiarias'),
    path('beneficiarias/actualizar/<int:pk>/', views.actualizar_beneficiaria, name='actualizar_beneficiaria'),
    path('beneficiarias/borrar/<int:pk>/', views.borrar_beneficiaria, name='borrar_beneficiaria'),
]
26. Realizar las configuraciones correspondiente a urls.py de backend_Hospitalmujer para enlazar con app_Hospital
Abre backend_Hospitalmujer/urls.py y modifica el archivo para incluir las URLs de app_Hospital:
code
Python
# backend_Hospitalmujer/urls.py

from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_Hospital.urls')), # Incluye las URLs de tu app
]
15. Crear la carpeta “templates” dentro de “app_Hospital”.
21. Crear la subcarpeta 'beneficiaria' dentro de app_Hospital\templates.
Esto ya lo hicimos en el paso 29, así que la estructura debe ser:
app_Hospital/templates/
app_Hospital/templates/beneficiaria/
16. En la carpeta templates crear los archivos html (base.html, header.html, navbar.html, footer.html, inicio.html).
22. crear los archivos html con su codigo correspondientes de (agregar_beneficiaria.html, ver_beneficiarias.html mostrar en tabla con los botones ver, editar y borrar, actualizar_beneficiaria.html, borrar_beneficiaria.html) dentro de app_Hospital\templates\beneficiaria.
28. Utilizar colores suaves, atractivos y modernos, el código de las páginas web sencillas.
Aquí está el código para los archivos HTML, implementando Bootstrap para estilos y manteniendo la sencillez.
app_Hospital/templates/base.html
code
Html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Hospital de la Mujer{% endblock %}</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <!-- Font Awesome para iconos -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.2/css/all.min.css" integrity="sha512-SnH5WK+bZxgPHs44uWIX+LLJAJ9/2PkPKZ5QiAj6Ta86w+fsb2j+FWQo/UoJwRxoSP definizione di css -->
    <style>
        body {
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            background-color: #f8f9fa; /* Color de fondo suave */
        }
        .wrapper {
            flex: 1;
        }
        .footer {
            background-color: #e9ecef; /* Color de footer suave */
            color: #495057;
            padding: 1rem 0;
            text-align: center;
            position: sticky;
            bottom: 0;
            width: 100%;
        }
        .navbar {
            background-color: #b0e0e6 !important; /* Azul cielo suave para navbar */
        }
        .navbar-brand, .nav-link, .dropdown-item {
            color: #343a40 !important; /* Texto oscuro para contraste */
        }
        .navbar-brand:hover, .nav-link:hover, .dropdown-item:hover {
            color: #007bff !important; /* Azul brillante al pasar el ratón */
        }
        .container {
            margin-top: 20px;
            margin-bottom: 20px;
        }
    </style>
</head>
<body>
    <div class="wrapper">
        {% include 'header.html' %}
        {% include 'navbar.html' %}
        <div class="container">
            {% block content %}
            {% endblock %}
        </div>
    </div>
    {% include 'footer.html' %}

    <!-- Bootstrap JS Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
</body>
</html>
app_Hospital/templates/header.html (Este archivo no es estrictamente necesario si ya tienes el navbar, pero lo incluyo por si quieres un encabezado separado)
code
Html
<header class="py-3 bg-light border-bottom">
    <div class="container d-flex justify-content-center">
        <h1 class="h3 mb-0 text-muted">Sistema de Administración Hospital de la Mujer</h1>
    </div>
</header>
app_Hospital/templates/navbar.html
code
Html
<nav class="navbar navbar-expand-lg navbar-light">
    <div class="container-fluid">
        <a class="navbar-brand" href="{% url 'inicio_hospital' %}">
            <i class="fas fa-hospital-alt me-2"></i> Hospital de la Mujer
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item">
                    <a class="nav-link" aria-current="page" href="{% url 'inicio_hospital' %}">
                        <i class="fas fa-home me-1"></i> Inicio
                    </a>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="beneficiariasDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-user-injured me-1"></i> Beneficiarias
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="beneficiariasDropdown">
                        <li><a class="dropdown-item" href="{% url 'agregar_beneficiaria' %}">Agregar Beneficiaria</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_beneficiarias' %}">Ver Beneficiarias</a></li>
                        <!-- Opciones para actualizar y borrar se manejarán a través de la tabla de "Ver Beneficiarias" -->
                    </ul>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="personalDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-user-md me-1"></i> Personal
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="personalDropdown">
                        <li><a class="dropdown-item" href="#">Agregar Personal (Pendiente)</a></li>
                        <li><a class="dropdown-item" href="#">Ver Personal (Pendiente)</a></li>
                    </ul>
                </li>
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="consultasDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
                        <i class="fas fa-calendar-check me-1"></i> Consultas
                    </a>
                    <ul class="dropdown-menu" aria-labelledby="consultasDropdown">
                        <li><a class="dropdown-item" href="#">Agregar Consulta (Pendiente)</a></li>
                        <li><a class="dropdown-item" href="#">Ver Consultas (Pendiente)</a></li>
                    </ul>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="/admin">
                        <i class="fas fa-cogs me-1"></i> Admin
                    </a>
                </li>
            </ul>
        </div>
    </div>
</nav>
app_Hospital/templates/footer.html
code
Html
<footer class="footer mt-auto py-3 bg-light">
    <div class="container text-center">
        <span class="text-muted">© {{ 'now'|date:"Y" }} Hospital de la Mujer. Todos los derechos reservados.</span><br>
        <span class="text-muted">Creado por Ing. Eliseo Nava, Cbtis 128</span>
    </div>
</footer>
app_Hospital/templates/inicio.html
code
Html
{% extends 'base.html' %}

{% block title %}Inicio - Hospital de la Mujer{% endblock %}

{% block content %}
<div class="row">
    <div class="col-md-8 offset-md-2">
        <div class="card shadow-sm p-4">
            <h2 class="card-title text-center mb-4" style="color: #6a5acd;">Bienvenido al Sistema de Administración del Hospital de la Mujer</h2>
            <p class="card-text text-center text-muted">
                Este sistema está diseñado para facilitar la gestión eficiente de la información de beneficiarias, personal médico y consultas dentro de nuestro hospital, asegurando un servicio de calidad y una administración organizada.
            </p>
            <hr>
            <p class="card-text text-center text-secondary">
                Explore las diferentes secciones para agregar, ver, actualizar y borrar registros de forma intuitiva y segura.
            </p>
            <div class="text-center mt-4">
                <img src="https://images.unsplash.com/photo-1587854692131-41991a0a552e?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D" class="img-fluid rounded shadow-sm" alt="Hospital de la Mujer" style="max-height: 400px; object-fit: cover;">
            </div>
            <p class="text-center mt-3 text-muted">
                *Imagen cortesía de Unsplash, solo para fines ilustrativos.
            </p>
        </div>
    </div>
</div>
{% endblock %}
`
app_Hospital/templates/beneficiaria/agregar_beneficiaria.html
code
Html
{% extends 'base.html' %}

{% block title %}Agregar Beneficiaria{% endblock %}

{% block content %}
<div class="row justify-content-center">
    <div class="col-md-8">
        <div class="card shadow-sm p-4">
            <h2 class="card-title text-center mb-4" style="color: #6a5acd;">Agregar Nueva Beneficiaria</h2>
            <form method="post">
                {% csrf_token %}
                <div class="mb-3">
                    <label for="nombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="nombre" name="nombre" required>
                </div>
                <div class="mb-3">
                    <label for="apellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="apellido" name="apellido" required>
                </div>
                <div class="mb-3">
                    <label for="fecha_nacimiento" class="form-label">Fecha de Nacimiento:</label>
                    <input type="date" class="form-control" id="fecha_nacimiento" name="fecha_nacimiento" required>
                </div>
                <div class="mb-3">
                    <label for="direccion" class="form-label">Dirección:</label>
                    <input type="text" class="form-control" id="direccion" name="direccion" required>
                </div>
                <div class="mb-3">
                    <label for="telefono" class="form-label">Teléfono (opcional):</label>
                    <input type="text" class="form-control" id="telefono" name="telefono">
                </div>
                <div class="mb-3">
                    <label for="correo" class="form-label">Correo Electrónico (opcional):</label>
                    <input type="email" class="form-control" id="correo" name="correo">
                </div>
                <div class="mb-3">
                    <label for="numero_expediente" class="form-label">Número de Expediente:</label>
                    <input type="text" class="form-control" id="numero_expediente" name="numero_expediente" required>
                </div>
                <div class="d-grid gap-2 mt-4">
                    <button type="submit" class="btn btn-primary" style="background-color: #6a5acd; border-color: #6a5acd;"><i class="fas fa-save me-2"></i> Guardar Beneficiaria</button>
                    <a href="{% url 'ver_beneficiarias' %}" class="btn btn-secondary"><i class="fas fa-arrow-left me-2"></i> Cancelar</a>
                </div>
            </form>
        </div>
    </div>
</div>
{% endblock %}
app_Hospital/templates/beneficiaria/ver_beneficiarias.html
code
Html
{% extends 'base.html' %}

{% block title %}Ver Beneficiarias{% endblock %}

{% block content %}
<div class="card shadow-sm p-4">
    <h2 class="card-title text-center mb-4" style="color: #6a5acd;">Beneficiarias Registradas</h2>
    {% if beneficiarias %}
    <div class="table-responsive">
        <table class="table table-striped table-hover align-middle">
            <thead class="table-dark" style="background-color: #6a5acd;">
                <tr>
                    <th>ID</th>
                    <th>Nombre Completo</th>
                    <th>Fecha Nacimiento</th>
                    <th>Expediente</th>
                    <th>Correo</th>
                    <th>Teléfono</th>
                    <th class="text-center">Acciones</th>
                </tr>
            </thead>
            <tbody>
                {% for beneficiaria in beneficiarias %}
                <tr>
                    <td>{{ beneficiaria.id }}</td>
                    <td>{{ beneficiaria.nombre }} {{ beneficiaria.apellido }}</td>
                    <td>{{ beneficiaria.fecha_nacimiento|date:"d/m/Y" }}</td>
                    <td>{{ beneficiaria.numero_expediente }}</td>
                    <td>{{ beneficiaria.correo|default:"N/A" }}</td>
                    <td>{{ beneficiaria.telefono|default:"N/A" }}</td>
                    <td class="text-center">
                        <a href="{% url 'actualizar_beneficiaria' beneficiaria.pk %}" class="btn btn-sm btn-info me-2" title="Editar"><i class="fas fa-edit"></i></a>
                        <a href="{% url 'borrar_beneficiaria' beneficiaria.pk %}" class="btn btn-sm btn-danger" title="Borrar"><i class="fas fa-trash-alt"></i></a>
                    </td>
                </tr>
                {% endfor %}
            </tbody>
        </table>
    </div>
    {% else %}
    <div class="alert alert-info text-center" role="alert">
        No hay beneficiarias registradas aún. <a href="{% url 'agregar_beneficiaria' %}" class="alert-link">¡Agrega una ahora!</a>
    </div>
    {% endif %}
    <div class="text-center mt-4">
        <a href="{% url 'agregar_beneficiaria' %}" class="btn btn-success" style="background-color: #5cb85c; border-color: #5cb85c;"><i class="fas fa-plus-circle me-2"></i> Agregar Nueva Beneficiaria</a>
    </div>
</div>
{% endblock %}
app_Hospital/templates/beneficiaria/actualizar_beneficiaria.html
code
Html
{% extends 'base.html' %}

{% block title %}Actualizar Beneficiaria{% endblock %}

{% block content %}
<div class="row justify-content-center">
    <div class="col-md-8">
        <div class="card shadow-sm p-4">
            <h2 class="card-title text-center mb-4" style="color: #6a5acd;">Actualizar Beneficiaria: {{ beneficiaria.nombre }} {{ beneficiaria.apellido }}</h2>
            <form method="post">
                {% csrf_token %}
                <div class="mb-3">
                    <label for="nombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="nombre" name="nombre" value="{{ beneficiaria.nombre }}" required>
                </div>
                <div class="mb-3">
                    <label for="apellido" class="form-label">Apellido:</label>
                    <input type="text" class="form-control" id="apellido" name="apellido" value="{{ beneficiaria.apellido }}" required>
                </div>
                <div class="mb-3">
                    <label for="fecha_nacimiento" class="form-label">Fecha de Nacimiento:</label>
                    <input type="date" class="form-control" id="fecha_nacimiento" name="fecha_nacimiento" value="{{ beneficiaria.fecha_nacimiento|date:'Y-m-d' }}" required>
                </div>
                <div class="mb-3">
                    <label for="direccion" class="form-label">Dirección:</label>
                    <input type="text" class="form-control" id="direccion" name="direccion" value="{{ beneficiaria.direccion }}" required>
                </div>
                <div class="mb-3">
                    <label for="telefono" class="form-label">Teléfono (opcional):</label>
                    <input type="text" class="form-control" id="telefono" name="telefono" value="{{ beneficiaria.telefono|default:'' }}">
                </div>
                <div class="mb-3">
                    <label for="correo" class="form-label">Correo Electrónico (opcional):</label>
                    <input type="email" class="form-control" id="correo" name="correo" value="{{ beneficiaria.correo|default:'' }}">
                </div>
                <div class="mb-3">
                    <label for="numero_expediente" class="form-label">Número de Expediente:</label>
                    <input type="text" class="form-control" id="numero_expediente" name="numero_expediente" value="{{ beneficiaria.numero_expediente }}" required>
                </div>
                <div class="d-grid gap-2 mt-4">
                    <button type="submit" class="btn btn-primary" style="background-color: #6a5acd; border-color: #6a5acd;"><i class="fas fa-sync-alt me-2"></i> Actualizar Beneficiaria</button>
                    <a href="{% url 'ver_beneficiarias' %}" class="btn btn-secondary"><i class="fas fa-
