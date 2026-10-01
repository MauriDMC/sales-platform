# Arquitectura

## 1. Propósito

La Plataforma Comercial para Vendedores funciona como una capa de experiencia y análisis sobre un sistema legado. Su objetivo es evitar que el usuario comercial tenga que navegar directamente por el sistema fuente, descargar reportes y preparar manualmente información antes de utilizarla.

## 2. Arquitectura objetivo

```text
┌──────────────────────────────┐
│ Sistema legado / Anzio       │
│ Fuente operacional           │
└──────────────┬───────────────┘
               │
               │ extracción controlada
               ▼
┌──────────────────────────────┐
│ Proceso de sincronización    │
│ frecuencia objetivo ~5 min   │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ SQL Server                   │
│ datos estructurados          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Django                       │
│ autenticación                │
│ autorización                 │
│ lógica de negocio            │
│ API interna                  │
└──────────────┬───────────────┘
               │ HTTPS
               ▼
┌──────────────────────────────┐
│ Plataforma del vendedor      │
│ clientes / cuentas / ventas  │
│ rutas / indicadores          │
└──────────────────────────────┘
```

## 3. Near real-time

El objetivo de actualización es aproximadamente cada cinco minutos. Esto corresponde a una arquitectura **near real-time**, no a tiempo real estricto.

La frecuencia definitiva debe validarse según:

- capacidad del sistema fuente;
- volumen de registros;
- ventana operacional;
- impacto de consultas;
- requerimientos de TI;
- consistencia requerida por cada indicador.

## 4. Responsabilidades por capa

### Sistema fuente

- Mantiene el dato operacional original.
- Continúa siendo la referencia inicial para los procesos existentes.
- No es accedido directamente por el navegador del vendedor.

### Sincronización

- Extrae únicamente los datos necesarios.
- Debe soportar ejecución incremental cuando sea técnicamente posible.
- Registra fecha/hora de última ejecución, cantidad de filas y errores.
- Evita procesos de extracción innecesariamente pesados.

### SQL Server

- Estructura clientes, vendedores, documentos, cuentas, ventas y relaciones.
- Permite consultas controladas y optimizadas.
- Separa el consumo analítico/comercial del sistema legado.

### Django

- Autentica usuarios.
- Relaciona usuario con vendedor/código comercial.
- Aplica autorización a nivel de registro.
- Ejecuta reglas de negocio.
- Expone endpoints para la interfaz.
- Impide que credenciales de base de datos lleguen al navegador.

### Frontend

- Presenta la información de manera comercial.
- No contiene credenciales de sistemas internos.
- No consulta directamente SQL Server ni el sistema legado.
- Solicita al backend únicamente la información autorizada.

## 5. Flujo por vendedor

1. El usuario inicia sesión.
2. Django identifica su identidad y código de vendedor.
3. Cada consulta se filtra por las relaciones autorizadas.
4. El vendedor visualiza únicamente clientes, cuentas, ventas e indicadores permitidos.
5. Las acciones relevantes quedan disponibles para auditoría cuando se implemente el backend.

## 6. Estado del prototipo

La versión actual es frontend/prototipo. Utiliza almacenamiento local y mecanismos de carga manual para simular fuentes de datos. La integración automática con SQL Server y Django está documentada como evolución futura.

## 7. Dependencia de Ficha Comercial

El prototipo referencia `Conector_Ficha_Comercial.html`. La integración definitiva debe decidir si este componente:

- se incorpora como módulo del mismo frontend;
- se sirve desde Django;
- o se mantiene desacoplado mediante una ruta propia.

No se incluye una implementación inventada mientras no exista una versión aprobada del conector.