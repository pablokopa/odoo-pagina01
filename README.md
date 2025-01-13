# ODOO_SXE01 🌐
---
### Creación y configuración del archivo.

<details>
<summary> <b> 1. Para crear y abrir un archivo de configuración: </b></summary>
<br>

```bash
# Crea y abre el archivo
nano docker-compose.yaml
```
</details>

<details>
<summary> <b> 2. Configuración del archivo: </b></summary>
<br>

```yaml
services:
  web:
    image: odoo:17.0
    depends_on:
      - db
    ports:
      - "8069:8069"
    volumes:
      - ./addons:/mnt/extra-addons # Permite que los módulos personalizados se almacenen en la carpeta addons del host
      - ./etc:/etc/odoo # Monta una carpeta local para configurar los archivos de Odoo
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    volumes:
        - ./postgresql:/var/lib/postgresql/data # Monta un volumen local para persistir los datos de PostgreSQL.
  pgadmin:
    container_name: pgadmin_container
    image: dpage/pgadmin4
    environment:
      - PGADMIN_DEFAULT_EMAIL=pgadmin4@pgadmin.org
      - PGADMIN_DEFAULT_PASSWORD=admin
    depends_on:
      - db
    ports:
      - "5050:80"
    restart: unless-stopped
```
Una vez terminado el archivo de configuración, lo lanzamos utilizando:
```bash
sudo docker compose up -d
```
**Importante hacerlo desde el directorio en el que se encuentra el archivo de configuración ⚠️**

![imagen](https://github.com/user-attachments/assets/5d2a2d54-7eb7-41af-9a8f-7aecc8f15e49)

</details>

<details>
<summary> <b> 3. Pruebas y configuración (Odoo): </b></summary>
<br>

```bash
# Utilizo en el navegador la ip de mi ordenador con el puerto seleccionado
10.0.9.108:8069 # Odoo
```
Una vez comprobado que todo funciona correctamente, me pongo a configurar todo desde el navegador ✅

**1. Asistente de instalación:**

  ![imagen](https://github.com/user-attachments/assets/8b7c1186-b7bc-4407-95ca-193855ea5ea9)

  Hay que crear la base de datos con otro nombre ya que 'postgres' ya existe porque la hemos creado antes.

**2. Iniciar sesión:**

  ![imagen](https://github.com/user-attachments/assets/94ac4bd9-28fd-4dbc-8ddd-b584c6d8ed1b)

**3. Página funcional:**

  ![imagen](https://github.com/user-attachments/assets/4e47970d-57d6-4479-933d-126c89353883)

</details>

<details>
<summary> <b> 3. Pruebas y configuración (pgAdmin): </b></summary>
<br>

```bash
# Utilizo en el navegador la ip de mi ordenador con el puerto seleccionado
10.0.9.108:5050 # pgAdmin
```

**1. Inicio de sesión:**

  ![imagen](https://github.com/user-attachments/assets/afd9f772-4e5b-4b1c-af9c-25c8aeb0deec)

Para ello utilizo los siguientes datos indicados en el compose:
- email: pgadmin4@pgadmin.org
- password: admin

**2. Página funcional:**

![imagen](https://github.com/user-attachments/assets/337f436d-a633-4077-bdc7-9dbb3263d601)

Como se puede comprobar, todo funciona correctamente... ✌🏼
