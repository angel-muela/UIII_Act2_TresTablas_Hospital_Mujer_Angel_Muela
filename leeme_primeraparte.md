# Proyecto: Hospital de la Mujer  
**Lenguaje:** Python  
**Framework:** Django  
**Editor:** VS Code  

## **1. Procedimiento para crear carpeta del Proyecto:**

- Crea la carpeta con el nombre: `UIII_Hospitaldelamujer_0290`.

## **2. Procedimiento para abrir VS Code sobre la carpeta `UIII_Hospitaldelamujer_0290`:**

- Abre VS Code y selecciona la carpeta previamente creada.

## **3. Procedimiento para abrir terminal en VS Code:**

- Abre la terminal desde el menú **Terminal > New Terminal**.

## **4. Procedimiento para crear carpeta entorno virtual “.venv” desde terminal de VS Code:**

- En la terminal, ejecuta el siguiente comando para crear el entorno virtual:

  ```bash
  python -m venv .venv
5. Procedimiento para activar el entorno virtual:
Para activar el entorno virtual, ejecuta:

En Windows:

bash
Copiar código
.venv\Scripts\activate
En macOS/Linux:

bash
Copiar código
source .venv/bin/activate
6. Procedimiento para activar el intérprete de Python:
Asegúrate de que VS Code está usando el intérprete de Python del entorno virtual creado. Esto se puede hacer desde la barra inferior de VS Code, seleccionando el intérprete correspondiente.

7. Procedimiento para instalar Django:
Ejecuta el siguiente comando en la terminal para instalar Django:

bash
Copiar código
pip install django
8. Procedimiento para crear proyecto backend_Hospitalmujer sin duplicar carpeta:
Para crear el proyecto, ejecuta:

bash
Copiar código
django-admin startproject backend_Hospitalmujer .
9. Procedimiento para ejecutar servidor en el puerto 8023:
Ejecuta el siguiente comando para iniciar el servidor en el puerto 8023:

bash
Copiar código
python manage.py runserver 8023
10. Procedimiento para copiar y pegar el link en el navegador:
Una vez el servidor esté corriendo, abre el navegador y accede a http://127.0.0.1:8023.

11. Procedimiento para crear aplicación app_Hospital:
Para crear la aplicación, ejecuta:

bash
Copiar código
python manage.py startapp app_Hospital
12. Aquí el modelo models.py:
python
Copiar código
from django.db import models

# MODELO: Beneficiaria
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

# MODELO: Personal
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

# MODELO: Consulta
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
12.5 Procedimiento para realizar las migraciones (makemigrations y migrate):
Para aplicar las migraciones, ejecuta los siguientes comandos:

bash
Copiar código
python manage.py makemigrations
python manage.py migrate
13. Primero trabajamos con el MODELO: BENEFICIARIA
Se trabajará inicialmente solo con el modelo Beneficiaria.

14. En la vista de app_Hospital crear las funciones con sus códigos correspondientes:
inicio_hospital

agregar_beneficiaria

actualizar_beneficiaria

realizar_actualizacion_beneficiaria

borrar_beneficiaria

15. Crear la carpeta “templates” dentro de app_Hospital:
Dentro de la carpeta app_Hospital, crea la carpeta templates.

16. En la carpeta templates crear los archivos HTML:
Crea los siguientes archivos dentro de app_Hospital/templates:

base.html

header.html

navbar.html

footer.html

inicio.html

17. En el archivo base.html agregar Bootstrap para CSS y JS:
Incluye el CDN de Bootstrap en el archivo base.html para utilizar estilos y funcionalidades de Bootstrap.

18. En el archivo navbar.html incluir las opciones:
Las opciones en el menú deben ser:

“Sistema de Administración Hospital de la Mujer”

“Inicio”

“Beneficiarias” con submenú:

Agregar Beneficiaria

Ver Beneficiarias

Actualizar Beneficiaria

Borrar Beneficiaria

“Personal” con submenú:

Agregar Personal

Ver Personal

Actualizar Personal

Borrar Personal

“Consultas” con submenú:

Agregar Consulta

Ver Consultas

Actualizar Consulta

Borrar Consulta

Añadir iconos a las opciones principales (no en los submenú).

19. En el archivo footer.html incluir los derechos de autor:
Agrega el siguiente texto al pie de página:

“Derechos de autor, fecha del sistema y Creado por Ing. Eliseo Nava, Cbtis 128”.

Mantener el footer fijo al final de la página.

20. En el archivo inicio.html se debe colocar información del sistema más una imagen tomada desde la red sobre un hospital de la mujer.
21. Crear la subcarpeta beneficiaria dentro de app_Hospital/templates:
Dentro de app_Hospital/templates, crea la subcarpeta beneficiaria.

22. Crear los archivos HTML con su código correspondiente en beneficiaria:
Crea los siguientes archivos dentro de app_Hospital/templates/beneficiaria:

agregar_beneficiaria.html

ver_beneficiarias.html (mostrar en tabla con botones para ver, editar y borrar)

actualizar_beneficiaria.html

borrar_beneficiaria.html

23. No utilizar forms.py:
Para la creación y manejo de formularios, no utilices forms.py. Realiza los formularios manualmente en los archivos .html.

24. Procedimiento para crear el archivo urls.py en app_Hospital:
Crea el archivo urls.py en la carpeta app_Hospital y agrega el código necesario para acceder a las funciones de views.py para operaciones CRUD de beneficiarias.

25. Procedimiento para agregar app_Hospital en settings.py de backend_Hospitalmujer:
En el archivo settings.py de backend_Hospitalmujer, agrega la aplicación app_Hospital en la lista de INSTALLED_APPS.

26. Realizar las configuraciones correspondientes a urls.py de backend_Hospitalmujer para enlazar con app_Hospital:
Configura las URL en urls.py de backend_Hospitalmujer para que apunten a las vistas de app_Hospital.

27. Procedimiento para registrar los modelos en admin.py y realizar las migraciones:
Registra el modelo Beneficiaria en admin.py de app_Hospital.

Realiza nuevamente las migraciones:

bash
Copiar código
python manage.py makemigrations
python manage.py migrate
28. Solo trabajar por el momento con el modelo Beneficiaria, dejando pendiente el modelo Personal y Consulta.
29. Utilizar colores suaves, atractivos y modernos para las páginas web.
Asegúrate de que el diseño sea moderno, atractivo y sencillo utilizando colores suaves.

30. No validar entrada de datos en este momento.
31. Crear la estructura completa de carpetas y archivos al inicio del proyecto.
Organiza correctamente todas las carpetas y archivos desde el inicio.

32. Proyecto totalmente funcional.
Asegúrate de que el proyecto funcione correctamente.

33. Finalmente ejecutar servidor en el puerto 8036:
Ejecuta el servidor en el puerto 8036:

bash
Copiar código
python manage.py runserver 8036
