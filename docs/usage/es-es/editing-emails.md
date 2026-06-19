# Editar correos electrónicos

Esta página describe cómo usar Edit in Outlook para editar y enviar correos electrónicos de documentos de Business Central a través de Microsoft Outlook.

## Flujo de trabajo básico

### Proceso paso a paso

#### 1. Selección del documento
1. **Abra un documento de Business Central** (p. ej. oferta de venta, factura, pedido)
2. **Haga clic en «Enviar correo electrónico»** en la cinta de opciones
3. **Se abre el cuadro de diálogo de correo electrónico**

#### 2. Activar Edit in Outlook
1. **En el cuadro de diálogo de correo electrónico**:
   - Seleccione los destinatarios
   - Elija una plantilla de correo electrónico (opcional)
   - **Haga clic en «Editar en Outlook»**
2. **El navegador inicia la descarga** del archivo .eml
3. **Espere a que se complete la descarga**

#### 3. Edición en Outlook
1. **Abra el archivo .eml descargado** (doble clic)
2. **Outlook se abre** con un correo electrónico precargado:
   - Documento como archivo adjunto PDF
   - Contenido de la plantilla en el cuerpo del correo
   - Información sobre los destinatarios rellenada
3. **Edite el correo electrónico** según sea necesario:
   - Ajuste el asunto
   - Añada texto personal
   - Añada archivos adjuntos adicionales
   - Ajuste el formato

#### 4. Envío
1. **Revise su correo electrónico**
2. **Haga clic en «Enviar»** en Outlook
3. **El correo electrónico se envía** a través de su cuenta personal de Outlook
4. **El correo aparece** en la carpeta «Elementos enviados» de Outlook

## Documentos compatibles

### Documentos de ventas
| Tipo de documento | Página de Business Central | Acciones disponibles |
|-------------------|---------------------------|---------------------|
| **Ofertas de venta** | Oferta de venta (41, 42, 43) | Enviar correo → Editar en Outlook |
| **Pedidos de venta** | Pedido de venta (44, 45, 46) | Enviar correo → Editar en Outlook |
| **Facturas de venta** | Factura de venta (132, 133, 134) | Enviar correo → Editar en Outlook |
| **Facturas de venta registradas** | Factura de venta registrada (132) | Enviar correo → Editar en Outlook |
| **Abonos de venta** | Abono de venta (114, 115) | Enviar correo → Editar en Outlook |

### Documentos de compra
| Tipo de documento | Página de Business Central | Acciones disponibles |
|-------------------|---------------------------|---------------------|
| **Ofertas de compra** | Oferta de compra (49, 50, 51) | Enviar correo → Editar en Outlook |
| **Pedidos de compra** | Pedido de compra (52, 53, 54) | Enviar correo → Editar en Outlook |
| **Facturas de compra** | Factura de compra (122, 123, 124) | Enviar correo → Editar en Outlook |
| **Abonos de compra** | Abono de compra (124, 125) | Enviar correo → Editar en Outlook |

### Documentos de almacén
| Tipo de documento | Página de Business Central | Acciones disponibles |
|-------------------|---------------------------|---------------------|
| **Envíos de almacén** | Envío de almacén (7337) | Enviar correo → Editar en Outlook |
| **Envíos de almacén registrados** | Envío de almacén registrado (7348) | Enviar correo → Editar en Outlook |

## Interfaz de usuario

### Cuadro de diálogo de correo electrónico de Business Central
Cuando selecciona «Enviar correo electrónico», verá:

```
┌─ Mensaje de correo ─────────────────────────┐
│ Para: cliente@ejemplo.es                    │
│ CC:                                         │
│ CCO:                                        │
│ Asunto: Oferta de venta OV001               │
│                                             │
│ Plantilla: [Seleccionar plantilla ▼]       │
│ Archivo adjunto: Oferta de venta OV001.pdf ☑│
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ [Editar en Outlook] [Enviar directam.]  │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ [Aceptar] [Cancelar]                        │
└─────────────────────────────────────────────┘
```

### Mensaje de descarga de Edit in Outlook
Después de hacer clic en «Editar en Outlook»:

```
┌─ Descarga del navegador ────────────────────┐
│ ⬇ Descargando: OfertaVenta_OV001.eml      │
│                                             │
│ ✓ Descarga completada                      │
│                                             │
│ [ Abrir con Outlook ]  [ Mostrar en carpeta]│
└─────────────────────────────────────────────┘
```

### Ventana de redacción de Outlook
El archivo .eml se abre en Outlook con:

```
┌─ Nuevo mensaje - Outlook ───────────────────┐
│ De: su-correo@empresa.es                    │
│ Para: cliente@ejemplo.es                    │
│ Asunto: Oferta de venta OV001               │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Estimado/a cliente,                     │ │
│ │                                         │ │
│ │ Adjunto encontrará nuestra oferta OV001.│ │
│ │                                         │ │
│ │ Atentamente,                            │ │
│ │ [Su nombre]                             │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Archivos adjuntos: 📎 OfertaVenta_OV001.pdf│
│                                             │
│ [Enviar] [Guardar borrador] [Descartar]    │
└─────────────────────────────────────────────┘
```

## Funciones de edición de correos electrónicos

### Ajustes de texto
En Outlook puede:
- **Cambiar el asunto**
- **Ajustar el cuerpo del mensaje**:
  - Añadir una nota personal
  - Modificar el texto de la plantilla
  - Ajustar el formato (negrita, cursiva, colores)
  - Añadir listas
  - Insertar vínculos

### Gestión de archivos adjuntos
- **Ver archivos adjuntos existentes** (documento PDF)
- **Añadir archivos adjuntos adicionales**:
  - Documentos adicionales
  - Imágenes
  - Especificaciones
  - Contratos
- **Eliminar archivos adjuntos** (si es necesario)
- **Cambiar el nombre de los archivos adjuntos**

### Ajuste de destinatarios
- **Ampliar el campo Para** con destinatarios adicionales
- **Añadir destinatarios en CC**
- **CCO para copias ocultas**
- **Validar direcciones** a través de la libreta de direcciones de Outlook

### Firma y formato
- **Firma personal** añadida automáticamente
- **Identidad corporativa** conservada desde la plantilla
- **Formato HTML** completamente disponible
- **Edición de texto enriquecido** con el editor de Outlook

## Funciones avanzadas

### Personalización de plantillas
Personalice las plantillas según la situación:

```html
<!-- Antes de enviar -->
<p>Estimado/a %CUSTOMER_NAME%,</p>
<p>Adjunto encontrará %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Después de editar en Outlook -->
<p>Estimado Sr. García,</p>
<p>En relación con nuestra conversación de hoy, adjunto encontrará
nuestra oferta de venta revisada OV001 con los precios actualizados.</p>
```

### Edición masiva de correos electrónicos
Para varios documentos:
1. **Use Edit in Outlook** para el primer documento
2. **Guarde como plantilla** en Outlook
3. **Aplique la plantilla** a los documentos siguientes
4. **Personalice** cada mensaje

**Véase también:** [Versiones compatibles](supported-versions.md) | [Limitaciones](limitations.md)
