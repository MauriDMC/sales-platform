# Plataforma Comercial para Vendedores

Prototipo de una capa comercial moderna sobre un sistema legado de gestión. El objetivo es simplificar el acceso del vendedor a información de clientes, cuentas por cobrar, rutas e indicadores comerciales sin obligarlo a ingresar directamente al sistema fuente ni descargar reportes manualmente.

## Problema

El sistema legado utilizado como fuente de información no está orientado a una experiencia comercial moderna. La consulta de datos puede requerir navegación poco amigable, exportaciones manuales y trabajo adicional antes de que la información sea útil para el vendedor.

La plataforma busca desacoplar la experiencia comercial del sistema fuente: el vendedor trabaja sobre una interfaz moderna y el backend se encarga de obtener, preparar y entregar los datos correspondientes.

## Arquitectura objetivo

```text
Sistema legado (Anzio)
        ↓
Extracción automatizada
        ↓
SQL Server
        ↓
Django / lógica de negocio
        ↓
Plataforma Comercial para Vendedores
```

La sincronización objetivo es aproximadamente cada 5 minutos, por lo que la información debe describirse como **casi en tiempo real (near real-time)** y no como tiempo real estricto.

Principios:

- Anzio permanece como sistema fuente en la etapa inicial.
- El vendedor no consulta directamente el servidor de origen.
- La extracción y actualización de datos se automatiza.
- SQL Server funciona como capa estructurada de datos.
- Django controla autenticación, permisos, reglas de negocio y acceso por vendedor.
- La interfaz muestra únicamente la información autorizada para la identidad/código comercial del usuario.

## Estado actual

El repositorio contiene un prototipo HTML funcional de la experiencia de usuario. Actualmente varias fuentes se cargan manualmente o se mantienen en almacenamiento local del navegador. El código ya separa conceptualmente los conectores de clientes, vendedores y cuentas para permitir reemplazar posteriormente la carga manual por integración SQL/API.

> Importante: la integración productiva con SQL Server y Django **todavía no está implementada en este repositorio**. La documentación distingue entre funcionalidades actuales y arquitectura objetivo.

## Módulos del prototipo

- Inicio y panel comercial.
- Clientes.
- Rutas de clientes.
- Estado de cuentas y facturas por cobrar.
- Base de conocimientos.
- Colas y chats de apoyo.
- Herramientas del vendedor.
- Ficha Comercial.
- Configuración de cuenta y código de vendedor.

## Objetivo funcional

La evolución del sistema busca que cada vendedor pueda consultar desde una sola interfaz:

- cartera de clientes asignados;
- facturas pendientes y vencimientos;
- saldos por cliente;
- estadísticas de ventas;
- cumplimiento de metas;
- evolución comercial;
- clientes principales;
- planificación de rutas;
- fichas y herramientas comerciales.

## Privacidad y seguridad

Este repositorio es público. Por ello:

- no deben subirse credenciales, cadenas de conexión ni secretos;
- no deben incluirse bases reales de clientes, cuentas o facturas;
- los datos demostrativos deben ser ficticios o anonimizados;
- cualquier integración productiva debe aplicar control de acceso por vendedor y principio de mínimo privilegio;
- la conexión a sistemas internos debe realizarse desde backend, nunca desde el navegador del vendedor.

## Estructura

```text
sales-platform/
├── index.html
├── README.md
├── CHANGELOG.md
├── SECURITY.md
├── .gitignore
└── docs/
    ├── arquitectura.md
    ├── funcionalidades.md
    ├── roadmap.md
    └── modelo-datos.md
```

## Ejecución del prototipo

Para una revisión simple, abrir `index.html` en un navegador moderno. Algunas funciones utilizan APIs del navegador y almacenamiento local.

El módulo de Ficha Comercial referencia `Conector_Ficha_Comercial.html`. Ese componente debe incorporarse por separado cuando su versión aprobada esté disponible.

## Versionado

Se utilizará versionado semántico durante la evolución del proyecto:

- `v0.x`: prototipo y construcción de arquitectura;
- `v1.0.0`: primera versión funcional integrada y validada.

Los cambios relevantes se registran en `CHANGELOG.md`.

## Licencia

No se ha definido todavía una licencia de distribución. Hasta que exista una decisión explícita, no debe asumirse una licencia open source.