# Despliegue de Mixpost en EasyPanel

Esta carpeta contiene una configuración lista para desplegar **Mixpost Lite** con Docker Compose en EasyPanel, usando la imagen oficial `inovector/mixpost`.

## 1) Crear servicio en EasyPanel

- Crea un nuevo servicio de tipo **Compose**.
- Sube el archivo `docker-compose.yml` de esta carpeta.
- Define variables en EasyPanel (recomendado) usando `.env.example` como referencia.
- Opcional: si ejecutas localmente con Docker Compose, crea `.env` a partir de `.env.example`.

Alternativa en EasyPanel (modo **Application**):

- Este repositorio ya incluye `Dockerfile` en la raíz para que EasyPanel pueda construir sin error `open Dockerfile: no such file or directory`.

## 2) Variables mínimas obligatorias

- `APP_KEY` (générala desde https://mixpost.app/tools/encryption-key-generator)
- `APP_DOMAIN`
- `DB_DATABASE`
- `DB_USERNAME`
- `DB_PASSWORD`
- `DB_ROOT_PASSWORD`

## 3) Dominio y puerto

- El contenedor expone `80` internamente y se publica como `8080:80`.
- En EasyPanel, apunta tu dominio al servicio `mixpost` (puerto `8080`) o ajusta el mapeo según tu configuración.

## 4) Primer inicio

- Despliega el stack.
- Espera a que `mysql` y `redis` estén en estado healthy.
- Abre `https://<APP_DOMAIN>`.

Credenciales por defecto de Mixpost (según documentación oficial):

- Usuario: `admin@example.com`
- Contraseña: `changeme`

Cámbiala inmediatamente después del primer acceso.

## 5) Persistencia

Se definen volúmenes para no perder datos:

- `mysql` → datos de base de datos
- `redis` → persistencia de Redis
- `storage` y `logs` → archivos y logs de Mixpost

## 6) Recomendaciones para producción

- Usa contraseñas fuertes.
- Configura SMTP real para recuperación de contraseña.
- Mantén `APP_DEBUG=false`.
- Habilita HTTPS en EasyPanel (o proxy frontal) y usa `APP_URL` con `https`.
