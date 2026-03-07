# Supported Versions

This page provides an overview of all supported versions and compatibility for Edit in Outlook.

## Business Central Versions

### Current Support

#### Business Central SaaS
| BC Version | Edit in Outlook Version | Status | Release Date | EOL Date |
|-----------|------------------------|--------|--------------|-----------|
| **BC 27** | 27.0.46066.0+ | ✅ Current | November 2024 | April 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Supported | April 2024 | October 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Supported | October 2023 | April 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Legacy | April 2023 | October 2024 |

#### Business Central On-Premise
| BC Version | Edit in Outlook Version | Status | Notes |
|-----------|------------------------|--------|--------|
| **BC 27** | 27.0.46066.0+ | ✅ Current | Full functionality |
| **BC 26** | 26.0.45889.0+ | ✅ Supported | Full functionality |  
| **BC 25** | 25.0.45294.0+ | ✅ Supported | Limited new features |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Legacy | Security updates only |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | No longer supported |

### Legacy Versions (Separate Repositories)
For older Business Central versions, specific legacy versions are available:

#### BC 16 (2020 Wave 1)
- **Repository**: `qt-bc-outlookedit-legacy-16`
- **Status**: ❌ End of Life
- **Last Version**: 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Repository**: `qt-bc-outlookedit-legacy-15`  
- **Status**: ❌ End of Life
- **Last Version**: 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Repository**: `qt-bc-outlookedit-legacy-14`
- **Status**: ❌ End of Life  
- **Last Version**: 14.0.xxxxx.0

## Microsoft Office Versions

### Office 365 / Microsoft 365

#### Outlook Desktop
| Version | Status | Notes |
|---------|--------|-------|
| **Outlook 365 Current** | ✅ Fully Supported | Recommended platform |
| **Outlook 365 Semi-Annual** | ✅ Supported | Stable enterprise version |
| **Outlook 2021 LTSC** | ✅ Supported | On-premise enterprise |
| **Outlook 2019** | ⚠️ Limited Support | Basic functionality |
| **Outlook 2016** | ❌ Not Supported | Too old for EML handling |

#### Outlook Web Access (OWA)
| Version | Status | EML Support | Notes |
|---------|--------|-------------|-------|
| **OWA Current** | ✅ Supported | Via download | Browser dependent |
| **OWA Government** | ✅ Supported | Via download | Compliance approved |

#### Outlook Mobile
| Platform | Status | Functionality |  
|----------|--------|---------------|
| **iOS Outlook** | ✅ Supported | Via file sharing |
| **Android Outlook** | ✅ Supported | Via file sharing |
| **Windows Mobile** | ❌ Not Supported | Platform discontinued |

### Office On-Premise
| Version | Status | Installation | Notes |
|---------|--------|-------------|-------|
| **Office LTSC 2021** | ✅ Supported | MSI/Click-to-Run | Enterprise recommended |
| **Office 2019** | ⚠️ Limited | MSI/Click-to-Run | Basic EML support |
| **Office 2016** | ❌ Not Supported | - | EOL reached |

## Browser Compatibility

### Recommended Browsers
For optimal Business Central and Control Add-in experience:

#### Windows
| Browser | Version | Status | Performance |
|---------|---------|---------|-------------|
| **Microsoft Edge** | 118+ | ✅ Excellent | Best performance |
| **Chrome** | 118+ | ✅ Excellent | Very good performance |
| **Firefox** | 118+ | ✅ Good | Good performance |
| **Internet Explorer** | All | ❌ Not Supported | Deprecated |

#### macOS
| Browser | Version | Status | Performance |
|---------|---------|---------|-------------|
| **Safari** | 16+ | ✅ Good | Native macOS integration |
| **Chrome** | 118+ | ✅ Excellent | Cross-platform consistency |
| **Firefox** | 118+ | ✅ Good | Open source option |
| **Edge** | 118+ | ✅ Excellent | Microsoft ecosystem |

### Control Add-in Requirements
- **JavaScript**: ES6+ support
- **HTML5**: Canvas and File API
- **CSS3**: Flexbox and Grid layouts
- **WebAssembly**: For PDF preview (optional)

## Platform Support

### Operating Systems

#### Windows
| Version | Status | Outlook Integration | Notes |
|---------|--------|-------------------|-------|
| **Windows 11** | ✅ Fully Supported | Native | Recommended platform |
| **Windows 10 (1909+)** | ✅ Supported | Native | Minimum version |
| **Windows Server 2022** | ✅ Supported | Terminal Server | Enterprise scenario |
| **Windows Server 2019** | ✅ Supported | Terminal Server | Legacy enterprise |
| **Windows 8.1** | ❌ Not Supported | - | EOL reached |

#### macOS
| Version | Status | Outlook Integration | Notes |
|---------|--------|-------------------|-------|
| **macOS Sonoma (14.x)** | ✅ Supported | Via Outlook for Mac | Latest version |
| **macOS Ventura (13.x)** | ✅ Supported | Via Outlook for Mac | Supported |
| **macOS Monterey (12.x)** | ⚠️ Limited | Via Outlook for Mac | Minor compatibility issues |
| **macOS Big Sur (11.x)** | ❌ Not Supported | - | Too old |

#### Linux
| Distribution | Status | Outlook Alternative | Notes |
|-------------|--------|-------------------|-------|
| **Ubuntu 22.04+** | ⚠️ Limited | Web/Thunderbird | EML files supported |
| **Red Hat Enterprise** | ⚠️ Limited | Web/Evolution | Enterprise environment |
| **All Distributions** | ❌ Native Support | - | No native Outlook |

## Release Schedule

### Release Cycle
Edit in Outlook follows Microsoft Business Central release schedule:

#### Major Releases
- **April Release** (Wave 1): Major new features  
- **October Release** (Wave 2): Improvements and refinements

#### Minor Releases
- **Monthly**: Bug fixes and minor improvements
- **Hotfixes**: Critical issues within 48 hours

### Backward Compatibility
| Aspect | Policy | Time Frame |
|--------|---------|-----------|
| **API Changes** | 6 months notice | Breaking changes |
| **UI Changes** | 3 months notice | Major UI updates |
| **Configuration** | Automatic migration | Version updates |
| **Templates** | Full compatibility | All versions |

## Upgrade Paths

### From Legacy Versions

#### BC 14/15/16 → Current
1. **Backup**: Full backup of current installation
2. **Uninstall**: Remove old version
3. **Install**: New version via AppSource/manual
4. **Migrate**: Configuration and templates
5. **Test**: Complete functionality test

#### Compatibility Notes
- **Templates**: Automatic migration
- **Configuration**: Manual review required  
- **User Rights**: Reassignment needed
- **API Changes**: Developer review required

### Update Best Practices
1. **Test Environment**: Always test in test environment first
2. **User Communication**: Communicate changes in advance  
3. **Rollback Plan**: Have procedure ready
4. **Documentation**: Update internal documentation

---

**Next steps:**
- [Limitations](limitations.md) - Known limitations
- [Installation](../installation/installation-overview.md) - Setup for your version
- [FAQ](../faq/faq.md) - Version-specific questions