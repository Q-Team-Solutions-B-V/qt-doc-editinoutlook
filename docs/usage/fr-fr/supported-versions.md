# Versions prises en charge

Cette page fournit une vue d'ensemble de toutes les versions prises en charge et de la compatibilité pour Edit in Outlook.

## Versions Business Central

### Support actuel

#### Business Central SaaS
| Version BC | Version Edit in Outlook | Statut | Date de sortie | Date EOL |
|-----------|------------------------|--------|----------------|---------|
| **BC 27** | 27.0.46066.0+ | ✅ Actuel | Novembre 2024 | Avril 2026 |
| **BC 26** | 26.0.45889.0+ | ✅ Pris en charge | Avril 2024 | Octobre 2025 |
| **BC 25** | 25.0.45294.0+ | ✅ Pris en charge | Octobre 2023 | Avril 2025 |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Héritage | Avril 2023 | Octobre 2024 |

#### Business Central On-Premise
| Version BC | Version Edit in Outlook | Statut | Remarques |
|-----------|------------------------|--------|----------|
| **BC 27** | 27.0.46066.0+ | ✅ Actuel | Fonctionnalité complète |
| **BC 26** | 26.0.45889.0+ | ✅ Pris en charge | Fonctionnalité complète |
| **BC 25** | 25.0.45294.0+ | ✅ Pris en charge | Nouvelles fonctionnalités limitées |
| **BC 24** | 24.0.44xxx.0+ | ⚠️ Héritage | Mises à jour de sécurité uniquement |
| **BC 23** | 23.0.43xxx.0+ | ❌ End of Life | Plus pris en charge |

### Versions legacy (Référentiels séparés)
Pour les versions plus anciennes de Business Central, des versions legacy spécifiques sont disponibles :

#### BC 16 (2020 Wave 1)
- **Référentiel** : `qt-bc-outlookedit-legacy-16`
- **Statut** : ❌ End of Life
- **Dernière version** : 16.0.xxxxx.0

#### BC 15 (2019 Wave 2)
- **Référentiel** : `qt-bc-outlookedit-legacy-15`
- **Statut** : ❌ End of Life
- **Dernière version** : 15.0.xxxxx.0

#### BC 14 (Spring 2019)
- **Référentiel** : `qt-bc-outlookedit-legacy-14`
- **Statut** : ❌ End of Life
- **Dernière version** : 14.0.xxxxx.0

## Versions Microsoft Office

### Office 365 / Microsoft 365

#### Outlook Desktop
| Version | Statut | Remarques |
|---------|--------|----------|
| **Outlook 365 Actuel** | ✅ Entièrement pris en charge | Plateforme recommandée |
| **Outlook 365 Semi-Annual** | ✅ Pris en charge | Version entreprise stable |
| **Outlook 2021 LTSC** | ✅ Pris en charge | Entreprise On-Premise |
| **Outlook 2019** | ⚠️ Prise en charge limitée | Fonctionnalité de base |
| **Outlook 2016** | ❌ Non pris en charge | Trop ancien pour EML |

#### Outlook Web Access (OWA)
| Version | Statut | Support EML | Remarques |
|---------|--------|-------------|----------|
| **OWA Actuel** | ✅ Pris en charge | Via téléchargement | Dépend du navigateur |
| **OWA Government** | ✅ Pris en charge | Via téléchargement | Approuvé conformité |

#### Outlook Mobile
| Plateforme | Statut | Fonctionnalité |
|------------|--------|---------------|
| **iOS Outlook** | ✅ Pris en charge | Via partage de fichiers |
| **Android Outlook** | ✅ Pris en charge | Via partage de fichiers |
| **Windows Mobile** | ❌ Non pris en charge | Plateforme abandonnée |

### Office On-Premise
| Version | Statut | Installation | Remarques |
|---------|--------|-------------|----------|
| **Office LTSC 2021** | ✅ Pris en charge | MSI/Click-to-Run | Recommandé entreprise |
| **Office 2019** | ⚠️ Limité | MSI/Click-to-Run | Support EML basique |
| **Office 2016** | ❌ Non pris en charge | - | EOL atteint |

## Compatibilité des navigateurs

### Navigateurs recommandés

#### Windows
| Navigateur | Version | Statut | Performances |
|-----------|---------|--------|-------------|
| **Microsoft Edge** | 118+ | ✅ Excellent | Meilleures performances |
| **Chrome** | 118+ | ✅ Excellent | Très bonnes performances |
| **Firefox** | 118+ | ✅ Bon | Bonnes performances |
| **Internet Explorer** | Tous | ❌ Non pris en charge | Obsolète |

#### macOS
| Navigateur | Version | Statut | Performances |
|-----------|---------|--------|-------------|
| **Safari** | 16+ | ✅ Bon | Intégration macOS native |
| **Chrome** | 118+ | ✅ Excellent | Cohérence multiplateforme |
| **Firefox** | 118+ | ✅ Bon | Option open source |
| **Edge** | 118+ | ✅ Excellent | Écosystème Microsoft |

### Exigences du Control Add-in
- **JavaScript** : Support ES6+
- **HTML5** : Canvas et File API
- **CSS3** : Mises en page Flexbox et Grid
- **WebAssembly** : Pour l'aperçu PDF (optionnel)

## Support des plateformes

### Systèmes d'exploitation

#### Windows
| Version | Statut | Intégration Outlook | Remarques |
|---------|--------|---------------------|----------|
| **Windows 11** | ✅ Entièrement pris en charge | Natif | Plateforme recommandée |
| **Windows 10 (1909+)** | ✅ Pris en charge | Natif | Version minimale |
| **Windows Server 2022** | ✅ Pris en charge | Terminal Server | Scénario entreprise |
| **Windows Server 2019** | ✅ Pris en charge | Terminal Server | Entreprise legacy |
| **Windows 8.1** | ❌ Non pris en charge | - | EOL atteint |

#### macOS
| Version | Statut | Intégration Outlook | Remarques |
|---------|--------|---------------------|----------|
| **macOS Sonoma (14.x)** | ✅ Pris en charge | Via Outlook pour Mac | Dernière version |
| **macOS Ventura (13.x)** | ✅ Pris en charge | Via Outlook pour Mac | Pris en charge |
| **macOS Monterey (12.x)** | ⚠️ Limité | Via Outlook pour Mac | Problèmes de compatibilité mineurs |
| **macOS Big Sur (11.x)** | ❌ Non pris en charge | - | Trop ancien |

#### Linux
| Distribution | Statut | Alternative Outlook | Remarques |
|-------------|--------|---------------------|----------|
| **Ubuntu 22.04+** | ⚠️ Limité | Web/Thunderbird | Fichiers EML pris en charge |
| **Red Hat Enterprise** | ⚠️ Limité | Web/Evolution | Environnement entreprise |
| **Toutes distributions** | ❌ Pas de support natif | - | Pas d'Outlook natif |

## Calendrier des versions

### Cycle de publication

#### Versions majeures
- **Version d'avril** (Wave 1) : Nouvelles fonctionnalités majeures
- **Version d'octobre** (Wave 2) : Améliorations et ajustements

#### Versions mineures
- **Mensuel** : Corrections de bogues et améliorations mineures
- **Correctifs** : Problèmes critiques dans les 48 heures

### Compatibilité ascendante
| Aspect | Politique | Délai |
|--------|----------|-------|
| **Modifications API** | Préavis de 6 mois | Changements incompatibles |
| **Modifications UI** | Préavis de 3 mois | Mises à jour majeures de l'UI |
| **Configuration** | Migration automatique | Mises à jour de version |

**Voir aussi :** [Modification des e-mails](editing-emails.md) | [Limitations](limitations.md)
