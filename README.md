# Signature Status

Repo base para el ejercicio práctico. El enunciado está en [EXERCISE.md](EXERCISE.md).

## Prerrequisitos

- .NET 8 SDK
- Node.js 20+
- Tu herramienta de IA instalada y funcionando

## Estructura

```
backend/
  src/SignatureStatus.Api        # ASP.NET Core Web API (.NET 8)
  tests/SignatureStatus.Tests    # xUnit
frontend/                        # React + TypeScript (Vite), Vitest + React Testing Library
SignatureStatus.sln
```

## Antes de la entrevista

Haz fork del repo a tu cuenta, clona tu fork y verifica que todo compila y que los tests pasan:

```bash
# Backend
dotnet test

# Frontend
cd frontend
npm install
npm test
```

## Correr en local

```bash
# API en http://localhost:5080 (Swagger en /swagger)
dotnet run --project backend/src/SignatureStatus.Api --launch-profile http

# Frontend en http://localhost:5173, con /api redirigido al backend
cd frontend && npm run dev
```
