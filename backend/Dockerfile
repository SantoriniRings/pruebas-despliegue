# Usa una imagen base de Python
FROM python:3.10-slim

# Establece el directorio de trabajo en /app-backend
WORKDIR /app-backend

# Copia los archivos de requisitos
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copia el resto del código del back-end
COPY . .

# Copia los archivos estáticos de React
COPY ./frontend/client/dist ./static

# Establece variables de entorno necesarias
ENV PYTHONUNBUFFERED=1

# Ejecuta las migraciones y recolecta los archivos estáticos
RUN python manage.py migrate && python manage.py collectstatic --noinput

# Expone el puerto de Gunicorn
EXPOSE 8000

# Comando para ejecutar la aplicación
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "django_crud_api.wsgi"]
