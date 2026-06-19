# Versiones compatibles

Esta página proporciona información general sobre todas las versiones compatibles y la compatibilidad de Edit in Outlook.

## Versiones de Business Central

### Compatibilidad actual

#### Business Central SaaS
| Versión BC | Versión Edit in Outlook | Estado | Fecha de lanzamiento | Fecha EOL |
|-----------|------------------------|--------|----------------------|----------|
| **BC 27** | 27.0.46066.0+ | ✅ Actual | Noviembre 2024 | Abril 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Compatible | Abril 2024 | Octubre 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Compatible | Octubre 2023 | Abril 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Heredado | Abril 2023 | Octubre 2024 |

#### Business Central instalación local
| Versión BC | Versión Edit in Outlook | Estado | Notas |
|-----------|------------------------|--------|-------|
| **BC 27** | 27.0.46066.0+ | ✅ Actual | Funcionalidad completa |
| **BC 26** | 26.0.45889.0+ | ✅ Compatible | Funcionalidad completa |
| **BC 25** | 25.0.45294.0+ | ✅ Compatible | Nuevas características limitadas |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Heredado | Solo actualizaciones de seguridad |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Ya no es compatible |

### Versiones heredadas (Repositorios independientes)
Para versiones más antiguas de Business Central, hay disponibles versiones heredadas específicas:

#### BC 16 (2020 Wave 1)
- **Repositorio**: `qt-bc-outlookedit-legacy-16`
- **Estado**: ❌ End of Life
- **Última versión**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repositorio**: `qt-bc-outlookedit-legacy-15`
- **Estado**: ❌ End of Life
- **Última versión**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repositorio**: `qt-bc-outlookedit-legacy-14`
- **Estado**: ❌ End of Life
- **Última versión**: 14.0.xxxxx.0

## Versiones de Microsoft Office

### Office 365 / Microsoft 365

#### Outlook Desktop
| Versión | Estado | Notas |
|---------|--------|-------|
| **Outlook 365 Actual** | ✅ Totalmente compatible | Plataforma recomendada |
| **Outlook 365 Semi-Annual** | ✅ Compatible | Versión empresarial estable |
| **Outlook 2021 LTSC** | ✅ Compatible | Empresa con instalación local |
| **Outlook 2019** | ⚠️ Compatibilidad limitada | Funcionalidad básica |
| **Outlook 2016** | ❌ No compatible | Demasiado antiguo para EML |

#### Outlook Web Access (OWA)
| Versión | Estado | Compatibilidad EML | Notas |
|---------|--------|-------------------|-------|
| **OWA Actual** | ✅ Compatible | Mediante descarga | Depende del navegador |
| **OWA Government** | ✅ Compatible | Mediante descarga | Aprobado para cumplimiento |

#### Outlook Mobile
| Plataforma | Estado | Funcionalidad |
|------------|--------|--------------|
| **iOS Outlook** | ✅ Compatible | Mediante uso compartido de archivos |
| **Android Outlook** | ✅ Compatible | Mediante uso compartido de archivos |
| **Windows Mobile** | ❌ No compatible | Plataforma descontinuada |

### Office instalación local
| Versión | Estado | Instalación | Notas |
|---------|--------|------------|-------|
| **Office LTSC 2021** | ✅ Compatible | MSI/Click-to-Run | Recomendado para empresas |
| **Office 2019** | ⚠️ Limitado | MSI/Click-to-Run | Compatibilidad EML básica |
| **Office 2016** | ❌ No compatible | - | EOL alcanzado |

## Compatibilidad con exploradores

### Exploradores recomendados

#### Windows
| Explorador | Versión | Estado | Rendimiento |
|-----------|---------|--------|-------------|
| **Microsoft Edge** | 118+ | ✅ Excelente | Mejor rendimiento |
| **Chrome** | 118+ | ✅ Excelente | Muy buen rendimiento |
| **Firefox** | 118+ | ✅ Bueno | Buen rendimiento |
| **Internet Explorer** | Todos | ❌ No compatible | Obsoleto |

#### macOS
| Explorador | Versión | Estado | Rendimiento |
|-----------|---------|--------|-------------|
| **Safari** | 16+ | ✅ Bueno | Integración nativa con macOS |
| **Chrome** | 118+ | ✅ Excelente | Coherencia multiplataforma |
| **Firefox** | 118+ | ✅ Bueno | Opción de código abierto |
| **Edge** | 118+ | ✅ Excelente | Ecosistema de Microsoft |

### Requisitos del Control Add-in
- **JavaScript**: Compatibilidad con ES6+
- **HTML5**: API Canvas y File
- **CSS3**: Diseños Flexbox y Grid
- **WebAssembly**: Para vista previa de PDF (opcional)

## Compatibilidad con plataformas

### Sistemas operativos

#### Windows
| Versión | Estado | Integración con Outlook | Notas |
|---------|--------|------------------------|-------|
| **Windows 11** | ✅ Totalmente compatible | Nativa | Plataforma recomendada |
| **Windows 10 (1909+)** | ✅ Compatible | Nativa | Versión mínima |
| **Windows Server 2022** | ✅ Compatible | Terminal Server | Escenario empresarial |
| **Windows Server 2019** | ✅ Compatible | Terminal Server | Empresa heredada |
| **Windows 8.1** | ❌ No compatible | - | EOL alcanzado |

#### macOS
| Versión | Estado | Integración con Outlook | Notas |
|---------|--------|------------------------|-------|
| **macOS Sonoma (14.x)** | ✅ Compatible | Mediante Outlook para Mac | Última versión |
| **macOS Ventura (13.x)** | ✅ Compatible | Mediante Outlook para Mac | Compatible |
| **macOS Monterey (12.x)** | ⚠️ Limitado | Mediante Outlook para Mac | Problemas menores de compatibilidad |
| **macOS Big Sur (11.x)** | ❌ No compatible | - | Demasiado antiguo |

#### Linux
| Distribución | Estado | Alternativa a Outlook | Notas |
|-------------|--------|----------------------|-------|
| **Ubuntu 22.04+** | ⚠️ Limitado | Web/Thunderbird | Archivos EML compatibles |
| **Red Hat Enterprise** | ⚠️ Limitado | Web/Evolution | Entorno empresarial |
| **Todas las distribuciones** | ❌ Sin compatibilidad nativa | - | Sin Outlook nativo |

## Calendario de versiones

### Ciclo de versiones

#### Versiones principales
- **Versión de abril** (Wave 1): Nuevas características principales
- **Versión de octubre** (Wave 2): Mejoras y refinamientos

#### Versiones secundarias
- **Mensual**: Correcciones de errores y mejoras menores
- **Revisiones**: Problemas críticos en 48 horas

### Compatibilidad con versiones anteriores
| Aspecto | Directiva | Período de tiempo |
|---------|----------|------------------|
| **Cambios en la API** | Aviso de 6 meses | Cambios importantes |
| **Cambios en la interfaz de usuario** | Aviso de 3 meses | Actualizaciones importantes de interfaz |
| **Configuración** | Migración automática | Actualizaciones de versión |

**Véase también:** [Editar correos electrónicos](editing-emails.md) | [Limitaciones](limitations.md)
