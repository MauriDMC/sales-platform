# Modelo de datos inicial

Este documento define un modelo conceptual de partida. No representa todavía un esquema SQL implementado.

## Entidades principales

### Usuario

Representa la identidad autenticada en la plataforma.

Campos conceptuales:

- `id`
- `username`
- `email`
- `is_active`
- `last_login`

### Vendedor

Representa la identidad comercial utilizada para filtrar la información.

Campos conceptuales:

- `id`
- `codigo_vendedor`
- `codigo_anzio`
- `nombre`
- `activo`

Relación esperada:

```text
Usuario 1 ── 1/N Vendedor
```

La cardinalidad definitiva debe validarse con el modelo de acceso real.

### Cliente

Campos conceptuales:

- `id`
- `codigo_anzio`
- `rut`
- `razon_social`
- `giro`
- `ciudad`
- `comuna`
- `direccion`
- `telefono`
- `email`
- `contacto`
- `estado`
- `fecha_creacion`

### AsignacionClienteVendedor

Evita asumir que la relación cliente-vendedor siempre será fija.

- `id`
- `cliente_id`
- `vendedor_id`
- `fecha_desde`
- `fecha_hasta`
- `activa`

### DocumentoCobro / Factura

- `id`
- `numero_documento`
- `cliente_id`
- `vendedor_id`
- `fecha_emision`
- `fecha_vencimiento`
- `monto_original`
- `saldo_pendiente`
- `estado`
- `fecha_actualizacion_origen`

### Venta

El nivel de detalle dependerá de la información disponible en el sistema fuente.

- `id`
- `cliente_id`
- `vendedor_id`
- `fecha`
- `documento`
- `monto_neto`
- `monto_total`
- `producto_id` cuando exista detalle por SKU
- `cantidad` cuando corresponda

### Producto

- `id`
- `sku`
- `descripcion`
- `familia`
- `unidad`
- `activo`

### MetaComercial

- `id`
- `vendedor_id`
- `periodo`
- `tipo_meta`
- `valor_objetivo`
- `unidad`

### Sincronizacion

Tabla de control operacional del proceso de extracción.

- `id`
- `fuente`
- `inicio`
- `fin`
- `estado`
- `filas_leidas`
- `filas_insertadas`
- `filas_actualizadas`
- `mensaje_error`
- `watermark_origen`

## Relaciones conceptuales

```text
Usuario
   │
   ▼
Vendedor ──────< AsignacionClienteVendedor >────── Cliente
   │                                                   │
   ├──────────────< Factura / DocumentoCobro >────────┤
   │                                                   │
   └──────────────────< Venta >────────────────────────┘
                              │
                              ▼
                           Producto

Vendedor ──────< MetaComercial

Sistema fuente ──────< Sincronizacion
```

## Reglas importantes

### Identificadores

Los códigos provenientes del sistema legado no deben asumirse automáticamente como claves primarias internas. Es preferible mantener claves internas y almacenar los códigos externos con restricciones de unicidad cuando corresponda.

### Historial de asignación

Si los clientes pueden cambiar de vendedor, se debe conservar historial para evitar alterar retrospectivamente métricas o responsabilidades.

### Saldos

Debe diferenciarse entre monto original del documento y saldo pendiente. El dashboard de cobranza debe basarse en el saldo vigente validado.

### Fechas de origen

Los registros sincronizados deben conservar una marca temporal del dato fuente y otra de la sincronización local para medir frescura.

### Calidad

Antes de implementar indicadores deben definirse reglas para:

- duplicados;
- RUT inválidos o ausentes;
- códigos de vendedor inexistentes;
- clientes sin asignación;
- fechas inconsistentes;
- montos negativos o nulos según contexto;
- documentos duplicados;
- registros eliminados o anulados en origen.

## Seguridad de datos

La autorización debe ejecutarse en Django/SQL y no depender únicamente del filtro visual del navegador. Toda consulta de clientes, ventas o cobranza debe respetar el vendedor autorizado para la sesión.