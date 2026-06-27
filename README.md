# Cómo instalar Dockge en Docker - Gestor Docker Compose en Docker

## Dockge en Docker: Gestor moderno y reactivo de Docker Compose

Interfaz web moderna, fácil de usar y reactiva para gestionar tus stacks Docker Compose. Creado por el autor de Uptime Kuma, con UI/UX pulida y enfoque en archivos compose.yaml.

## ¿Qué es Dockge?

Dockge es un gestor auto-hospedado de stacks Docker Compose con una interfaz web moderna, reactiva y fácil de usar. Diseñado específicamente para trabajar con archivos compose.yaml, permite crear, editar, iniciar, detener, reiniciar y eliminar stacks de manera visual e intuitiva.

En Docker: Dockge se despliega como un contenedor Docker que gestiona otros contenedores Docker. Se conecta al daemon de Docker mediante el socket y te permite gestionar múltiples stacks desde una interfaz web elegante y responsive, similar a Uptime Kuma.

Ventaja principal: A diferencia de Portainer, Dockge se enfoca exclusivamente en Docker Compose y mantiene tus archivos compose.yaml en el sistema de archivos tradicional. Puedes editarlos con cualquier editor y Dockge los detectará automáticamente.

## Características principales

### Gestión de compose.yaml
Crear, editar, iniciar, detener, reiniciar y eliminar stacks.

### Editor interactivo
Editor web interactivo para archivos compose.yaml con sintaxis.

### Terminal web
Terminal web interactiva para acceso directo a los contenedores.

### Múltiples agentes
Gestionar múltiples stacks desde diferentes hosts Docker.

### Conversor docker run
Convertir comandos docker run a archivos compose.yaml.

### Estructura basada en archivos
Tus archivos compose.yaml permanecen en el sistema de archivos.

### Interfaz reactiva
Todo es responsive con progreso en tiempo real.

### UI/UX pulida
Interfaz moderna y elegante, creada por el autor de Uptime Kuma.

### Actualización de imágenes
Actualizar imágenes Docker directamente desde la interfaz.

### Multi-host
Gestionar múltiples hosts Docker en una sola interfaz.

### Open Source
MIT License. Código abierto y comunidad activa.

### Comunidad activa
23k+ estrellas en GitHub y desarrollo continuo.

## Requisitos del sistema

- Docker 20+ o Podman instalado
- 512 MB de RAM (1 GB recomendado)
- 1 GB de disco para datos y stacks
- Puerto 5001 disponible (configurable)
- Acceso al socket Docker (/var/run/docker.sock)
- Sistema Linux (Ubuntu, Debian, Fedora, CentOS, Arch)

Nota importante: Dockge requiere acceso al socket Docker para gestionar contenedores. Asegúrate de que el usuario que ejecuta Dockge tenga permisos para acceder a /var/run/docker.sock o usa el montaje de volumen correspondiente.

## Instalación rápida con Docker Compose

### Paso 1: Crear directorios

```bash
mkdir -p /opt/stacks /opt/dockge
cd /opt/dockge
```

### Paso 2: Descargar compose.yaml

```bash
curl https://raw.githubusercontent.com/louislam/dockge/master/compose.yaml --output compose.yaml
```

### Paso 3: Iniciar Dockge

```bash
docker compose up -d
```

### Paso 4: Acceder a la interfaz

Abre en tu navegador: http://localhost:5001

¡Listo! Ya puedes gestionar tus stacks Docker Compose.

Tip: Para personalizar el puerto o la ruta de los stacks, visita [dockge.kuma.pet](https://dockge.kuma.pet) para generar un compose.yaml personalizado.

## Configuración avanzada

### Generador interactivo de compose.yaml

Visita [https://dockge.kuma.pet](https://dockge.kuma.pet) para generar tu compose.yaml con opciones personalizadas:

```bash
curl "https://dockge.kuma.pet/compose.yaml?port=5001&stacksPath=/opt/stacks" --output compose.yaml
```

### Variables de entorno personalizadas

```yaml
services:
  dockge:
    image: louislam/dockge:1
    restart: unless-stopped
    ports:
      - "5001:5001"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./data:/app/data
      - /opt/stacks:/opt/stacks
    environment:
      - DOCKGE_STACKS_DIR=/opt/stacks
      - PUID=1000
      - PGID=1000
```

### Parámetros PUID/PGID

```yaml
environment:
  - PUID=1000 # Usuario propietario de los stacks
  - PGID=1000 # Grupo propietario de los stacks
```

Esto asegura que los archivos creados por Dockge tengan el propietario correcto.

### Despliegue con Caddy (SSL automático)

```
dockge.tudominio.com {
  reverse_proxy localhost:5001
}
```

## Gestión de stacks existentes

### Migrar stacks existentes a Dockge

- Detén tu stack actual: `docker compose down`
- Mueve tu archivo compose a: `/opt/stacks/nombre-stack/compose.yaml`
- En Dockge, haz clic en Scan Stacks Folder
- Tu stack aparecerá en la lista y podrás gestionarlo desde Dockge

### Convertir docker run a compose.yaml

Usa la función de conversión de Dockge para transformar comandos docker run en archivos compose.yaml listos para usar.

### Terminal web interactiva

Accede directamente a la terminal de cualquier contenedor desde la interfaz web sin necesidad de usar la CLI.

## Actualización y mantenimiento

### Actualizar a la última versión

```bash
cd /opt/dockge
docker compose pull
docker compose up -d
```

### Ver logs

```bash
docker compose logs -f dockge
```

### Reiniciar Dockge

```bash
docker compose restart dockge
```

### Detener Dockge

```bash
docker compose down
```

Importante: Al actualizar, tus stacks en /opt/stacks permanecen intactos. Solo se actualiza el contenedor de Dockge.

## Dockge vs Portainer

- Dockge: Enfoque exclusivo en Docker Compose, UI moderna y reactiva, archivos compose.yaml tradicionales, ligero y rápido
- Portainer: Características completas de Docker (redes, volúmenes, imágenes, etc.), más complejo, mayor consumo de recursos

Si solo necesitas gestionar stacks con Docker Compose, Dockge es la opción ideal. Si necesitas gestión completa de Docker, usa Portainer.

## Casos de uso

- Homelab: Gestiona todos tus stacks Docker Compose desde una interfaz unificada
- Pequeñas empresas: Administración simplificada de contenedores sin complejidad
- Desarrolladores: Prueba rápida de stacks sin escribir comandos largos
- Admins de sistema: Gestión centralizada de múltiples servidores Docker
- Fabricación: Control de stacks de producción con visibilidad en tiempo real
- Educación: Enseñar Docker Compose con interfaz visual e intuitiva

## Redes

- 📼 Youtube: [https://www.youtube.com/@genbyte](https://www.youtube.com/@genbyte)
- ⛓ Github: [https://github.com/JLalib](https://github.com/JLalib)
- 💻 Blog: [https://genbyte.blogspot.com/](https://genbyte.blogspot.com/)
- 🐦 X (Twitter): [https://twitter.com/gen_byte](https://twitter.com/gen_byte)
