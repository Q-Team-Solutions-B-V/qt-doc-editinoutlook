# Limitations

Cette page décrit les limitations, restrictions et considérations connues lors de l'utilisation d'Edit in Outlook.

## Limitations techniques

### Limitations du navigateur et du téléchargement

#### Limites de taille de fichier
| Composant | Taille maximale | Raison | Solution de contournement |
|-----------|----------------|--------|--------------------------|
| **Fichier EML** | 25 Mo | Limite de téléchargement du navigateur | Diviser les grandes pièces jointes |
| **Pièces jointes PDF** | 20 Mo | Limites du client de messagerie | Compresser le PDF |
| **E-mail total** | 30 Mo | Limite Outlook/Exchange | Utiliser des liens SharePoint |
| **Control Add-in** | 100 Mo de mémoire | Performances du navigateur | Actualiser la page |

#### Problèmes spécifiques au navigateur
- **Chrome** : Le bloqueur de fenêtres contextuelles peut bloquer les téléchargements
- **Firefox** : Problèmes d'encodage avec les caractères non-ASCII
- **Edge** : Délai d'attente occasionnel avec les grands fichiers
- **Safari** : Prise en charge limitée de l'aperçu PDF

### Limitations de la plateforme Business Central

#### SaaS vs. On-Premise
| Fonctionnalité | SaaS | On-Premise | Remarque |
|----------------|------|------------|---------|
| **Mises à jour automatiques** | ✅ | ❌ | SaaS automatique, On-Premise manuel |
| **Extensions personnalisées** | ⚠️ Limité | ✅ Complet | Restrictions sandbox SaaS |
| **Mode débogage** | ❌ | ✅ | Politique de sécurité SaaS |
| **Accès aux journaux** | ⚠️ Application Insights | ✅ Direct | Approches de journalisation différentes |

#### Limites de l'API
- **Requêtes par minute** : 100 (SaaS), Illimité (On-Premise)
- **Délai d'expiration de session** : 30 minutes par défaut
- **Utilisateurs simultanés** : Selon le modèle de licence

## Limitations Outlook et Office

### Outlook Desktop vs. Web

#### Comparaison des fonctionnalités
| Fonctionnalité | Desktop | Web | Mobile |
|----------------|---------|-----|--------|
| **Ouverture EML** | ✅ Natif | ⚠️ Via navigateur | ❌ Limité |
| **Mise en forme enrichie** | ✅ Complète | ✅ Complète | ⚠️ Basique |
| **Gestion des pièces jointes** | ✅ Complète | ✅ Complète | ⚠️ Envoi seul |
| **Accès hors ligne** | ✅ Complet | ❌ Aucun | ⚠️ Limité |

#### Dépendances de version
- **Outlook 2016/2019** : Prise en charge EML limitée
- **OWA Legacy** : Pas d'ouverture directe EML
- **Applications mobiles** : Nécessite une étape de préparation sur le bureau

### Limites Exchange et O365

#### Limites de taille des e-mails
| Plateforme | Taille max. des messages | Max. pièces jointes | Max. destinataires |
|------------|-------------------------|--------------------|--------------------|
| **Exchange Online** | 150 Mo | 100 | 500 |
| **Exchange 2019** | 35 Mo (défaut) | Illimité | 5000 |
| **Exchange 2016** | 25 Mo (défaut) | Illimité | 5000 |

> **Remarque** : Les paramètres de l'organisation peuvent restreindre davantage ces limites

## Limitations par type de document

### Pris en charge vs. non pris en charge

#### Entièrement pris en charge
- ✅ Devis, commandes, factures de vente
- ✅ Commandes, factures d'achat
- ✅ Documents validés
- ✅ Avoirs
- ✅ Expéditions entrepôt

#### Prise en charge limitée
- ⚠️ **Documents de service** : Prise en charge basique des modèles
- ⚠️ **Documents de projet** : Personnalisation minimale
- ⚠️ **Ordres d'assemblage** : Pas de modèles spécifiques

#### Non pris en charge
- ❌ **Objets de rapport personnalisés** : Pas de génération EML
- ❌ **Intégration Dataverse** : Uniquement BC natif
- ❌ **Documents externes** : Pas de prise en charge tierce

### Limitations des modèles

#### Problèmes de modèles HTML

```html
/* CSS problématique */
.non-supporte {
    position: absolute;  /* Pas largement pris en charge */
    transform: rotate(); /* Problèmes avec les clients de messagerie */
    /* @media queries — Prise en charge limitée */
}
```

#### Sous-ensemble HTML pris en charge
- ✅ Balises HTML de base (p, div, table, br)
- ✅ Style CSS (en ligne de préférence)
- ✅ Images (intégrées ou liées)
- ❌ JavaScript (bloqué pour des raisons de sécurité)
- ❌ Mises en page CSS complexes (flexbox, grid)
- ❌ Chargement de polices externes

## Limitations utilisateur et droits

### Dépendances d'autorisations

#### Droits minimaux requis
Un utilisateur doit disposer au minimum de :
- **Lecture des documents** : Pour l'accès aux documents
- **Lecture des modèles d'e-mail** : Pour l'accès aux modèles
- **Téléchargement de fichiers** : Pour les fichiers EML
- **Exécution du Control Add-in** : Pour les fonctionnalités du navigateur

**Voir aussi :** [Modification des e-mails](editing-emails.md) | [Versions prises en charge](supported-versions.md)
