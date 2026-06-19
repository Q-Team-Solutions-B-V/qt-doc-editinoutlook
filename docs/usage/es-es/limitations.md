# Limitaciones

Esta página describe las limitaciones, restricciones y consideraciones conocidas al usar Edit in Outlook.

## Limitaciones técnicas

### Limitaciones del navegador y la descarga

#### Límites de tamaño de archivo
| Componente | Tamaño máximo | Motivo | Solución alternativa |
|------------|--------------|--------|---------------------|
| **Archivo EML** | 25 MB | Límite de descarga del navegador | Dividir archivos adjuntos grandes |
| **Archivos adjuntos PDF** | 20 MB | Límites del cliente de correo | Comprimir el PDF |
| **Correo electrónico total** | 30 MB | Límite de Outlook/Exchange | Usar vínculos de SharePoint |
| **Control Add-in** | 100 MB de memoria | Rendimiento del navegador | Actualizar la página |

#### Problemas específicos del navegador
- **Chrome**: El bloqueador de elementos emergentes puede bloquear las descargas
- **Firefox**: Problemas de codificación con caracteres no ASCII
- **Edge**: Tiempo de espera ocasional con archivos grandes
- **Safari**: Compatibilidad limitada con la vista previa de PDF

### Limitaciones de la plataforma Business Central

#### SaaS frente a instalación local
| Funcionalidad | SaaS | Instalación local | Nota |
|---------------|------|-------------------|------|
| **Actualizaciones automáticas** | ✅ | ❌ | SaaS automático, local manual |
| **Extensiones personalizadas** | ⚠️ Limitado | ✅ Completo | Restricciones de espacio aislado SaaS |
| **Modo de depuración** | ❌ | ✅ | Directiva de seguridad SaaS |
| **Acceso a registros** | ⚠️ Application Insights | ✅ Directo | Distintos enfoques de registro |

#### Límites de la API
- **Solicitudes por minuto**: 100 (SaaS), Ilimitado (local)
- **Tiempo de espera de sesión**: 30 minutos de forma predeterminada
- **Usuarios simultáneos**: Según el modelo de licencia

## Limitaciones de Outlook y Office

### Outlook Desktop frente a la versión web

#### Comparación de características
| Característica | Desktop | Web | Móvil |
|----------------|---------|-----|-------|
| **Apertura EML** | ✅ Nativa | ⚠️ Mediante navegador | ❌ Limitada |
| **Formato enriquecido** | ✅ Completo | ✅ Completo | ⚠️ Básico |
| **Administración de archivos adjuntos** | ✅ Completa | ✅ Completa | ⚠️ Solo carga |
| **Acceso sin conexión** | ✅ Completo | ❌ Ninguno | ⚠️ Limitado |

#### Dependencias de versión
- **Outlook 2016/2019**: Compatibilidad EML limitada
- **OWA Legacy**: Sin apertura directa de EML
- **Aplicaciones móviles**: Requiere un paso de preparación en el equipo de escritorio

### Límites de Exchange y O365

#### Límites de tamaño de correo electrónico
| Plataforma | Tamaño máximo de mensaje | Máx. archivos adjuntos | Máx. destinatarios |
|------------|-------------------------|----------------------|-------------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (predeterminado) | Ilimitado | 5000 |
| **Exchange 2016** | 25 MB (predeterminado) | Ilimitado | 5000 |

> **Nota**: La configuración de la organización puede restringir aún más estos límites

## Limitaciones por tipo de documento

### Compatible frente a no compatible

#### Totalmente compatible
- ✅ Ofertas, pedidos, facturas de venta
- ✅ Pedidos, facturas de compra
- ✅ Documentos registrados
- ✅ Abonos
- ✅ Envíos de almacén

#### Compatibilidad limitada
- ⚠️ **Documentos de servicio**: Compatibilidad básica con plantillas
- ⚠️ **Documentos de proyecto**: Personalización mínima
- ⚠️ **Pedidos de ensamblado**: Sin plantillas específicas

#### No compatible
- ❌ **Objetos de informe personalizados**: Sin generación de EML
- ❌ **Integración con Dataverse**: Solo BC nativo
- ❌ **Documentos externos**: Sin compatibilidad de terceros

### Limitaciones de plantillas

#### Problemas de plantillas HTML

```html
/* CSS problemático */
.no-compatible {
    position: absolute;  /* No ampliamente compatible */
    transform: rotate(); /* Problemas con los clientes de correo */
    /* @media queries — Compatibilidad limitada */
}
```

#### Subconjunto HTML compatible
- ✅ Etiquetas HTML básicas (p, div, table, br)
- ✅ Estilos CSS (se prefieren en línea)
- ✅ Imágenes (incrustadas o vinculadas)
- ❌ JavaScript (bloqueado por seguridad)
- ❌ Diseños CSS complejos (flexbox, grid)
- ❌ Carga de fuentes externas

## Limitaciones de usuario y derechos

### Dependencias de permisos

#### Derechos mínimos necesarios
Un usuario necesita como mínimo:
- **Lectura de documentos**: Para acceder a los documentos
- **Lectura de plantillas de correo**: Para acceder a las plantillas
- **Descarga de archivos**: Para los archivos EML
- **Ejecución del Control Add-in**: Para la funcionalidad del navegador

**Véase también:** [Editar correos electrónicos](editing-emails.md) | [Versiones compatibles](supported-versions.md)
