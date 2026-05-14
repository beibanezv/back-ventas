# Back Ventas

Backend que guarda y entrega las órdenes de compra.

## Qué hace

- Crea ventas.
- Lista ventas.
- Actualiza y elimina ventas.

## Cómo funciona con EC2

- Este backend corre en su EC2 con Docker.
- Se expone por el puerto `8080`.
- Usa MySQL en contenedor y guarda datos con volumen Docker.

URL principal:

- `http://<IP_EC2_BACK_VENTAS>:8080/api/v1/ventas`

## Persistencia (datos no se pierden)

- Se usa el volumen `mysql_ventas_data`.
- Aunque reinicies contenedores, los datos quedan guardados.

## Despliegue automático (CI/CD)

Con push a rama `deploy`:

1. Se construye imagen Docker.
2. Se publica en Docker Hub.
3. Se copia `docker-compose.yml` a EC2.
4. Se levanta versión nueva con `docker compose up -d`.

Workflow: `.github/workflows/deploy.yml`

## Prueba rápida

Crear venta:

```bash
curl -X POST "http://<IP_EC2_BACK_VENTAS>:8080/api/v1/ventas" -H "Content-Type: application/json" -d "{\"fechaCompra\":\"2026-05-14\",\"direccionCompra\":\"Calle Falsa 123\",\"valorCompra\":12345,\"despachoGenerado\":false}"
```

Listar ventas:

```bash
curl "http://<IP_EC2_BACK_VENTAS>:8080/api/v1/ventas"
```
