# Ejercicio práctico: Estado de firma de documentos

**Duración:** 35 minutos · **Herramienta de IA:** la que prefieras · Comparte pantalla y piensa en voz alta.

## Contexto

Un proveedor de firma electrónica nos notifica por webhook los cambios de estado de un documento: `sent`, `viewed`, `signed` y `declined`. Necesitamos procesar esos eventos de forma confiable y mostrarle el estado al usuario.

## Qué construir

- **Webhook (.NET 8):** `POST /webhooks/signature`. Valida la firma HMAC-SHA256 del payload (header `X-Signature`, secreto configurable) y publica el evento a una cola. La cola puede ser en memoria o SQS con LocalStack.
- **Consumidor:** procesa los eventos de la cola y actualiza el estado del documento.
- **Persistencia:** EF Core con InMemory o SQLite. Guarda el estado actual y el historial de eventos.
- **Endpoint de consulta:** `GET /documents/{id}` devuelve el estado y su historial.
- **Frontend (React + TypeScript):** componente `DocumentStatus` con un hook propio que haga polling y muestre el estado y su historial.
- **Tests:** xUnit para la lógica de negocio y React Testing Library para el componente.

### Ejemplo de payload

```json
{
  "eventId": "evt_01HZX3K9QW",
  "documentId": "doc_123",
  "type": "signed",
  "occurredAt": "2026-11-09T18:30:00Z"
}
```

## Reglas de negocio

- Cada evento trae un `eventId` único. El proveedor puede reenviar el mismo evento más de una vez.
- Los eventos pueden llegar fuera de orden.
- `signed` y `declined` son estados finales.
- Si la firma HMAC es inválida, el evento se rechaza.

## Cómo trabajar

Usa tu herramienta de IA como lo harías en tu día a día en un equipo que entrega diario. Nos interesa ver tu flujo de trabajo con IA tanto como el resultado, así que piensa en voz alta.

## Entrega

1. Haz **fork** de este repositorio a tu cuenta de GitHub y clona tu fork.
2. Haz tus cambios en un **git worktree separado** con su propia rama creada a partir de `main`. No trabajes directamente en el checkout principal.
3. Al terminar, sube la rama a tu fork y abre un **Pull Request hacia `main` del repositorio original**.

## Notas

- No esperamos que termines todo. Si te quedas sin tiempo, prioriza el flujo backend y sus tests.
- Puedes buscar documentación y hacer preguntas sobre el enunciado en cualquier momento.
- Al final platicaremos 5 minutos sobre las decisiones que tomaste.
