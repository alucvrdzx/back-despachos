# Backend Despachos - Spring Boot

## Descripción

Este proyecto es el backend de Despachos para la aplicación. Expone la API REST en `http://localhost:8081/api/v1/despachos`.

## Cómo correr con Docker localmente

Desde la carpeta `back-Despachos_SpringBoot/Springboot-API-REST-DESPACHO`:

```bash
docker build -t juanvillagra/back-despachos:latest .
docker run -d --name back-despachos -p 8081:8081 --env-file .env juanvillagra/back-despachos:latest
```

## Variables de entorno requeridas

Renombra `.env.example` a `.env` y completa los valores:

```env
DB_ENDPOINT=mysql
DB_PORT=3306
DB_NAME=despachos_db
DB_USERNAME=root
DB_PASSWORD=root123
```

## Cómo funciona el pipeline CI/CD

- `build-push-despachos.yml`: se ejecuta al hacer push a la rama `deploy`, construye la imagen Docker y la sube a Docker Hub como `juanvillagra/back-despachos:latest`.
- `deploy-despachos.yml`: despliega al host EC2 `i-09e5f983fe1c13e0d` mediante AWS SSM.

Secrets requeridos:
- `DOCKERHUB_USERNAME`
- `DOCKERHUB_TOKEN`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_SESSION_TOKEN`

## Arquitectura del sistema

- `ec2_web`: frontend React Vite en `44.203.209.74`.
- `ec2_app`: backend Ventas en `10.0.8.79`, puerto `8080`.
- `ec2_datos`: backend Despachos en `10.0.8.139`, puerto `8081`, y MySQL.
