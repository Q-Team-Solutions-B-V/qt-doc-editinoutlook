# Modification des e-mails

Cette page décrit comment utiliser Edit in Outlook pour modifier et envoyer des e-mails de documents Business Central via Microsoft Outlook.

## Flux de travail de base

### Processus étape par étape

#### 1. Sélection du document
1. **Ouvrez un document Business Central** (par ex. devis de vente, facture, commande)
2. **Cliquez sur « Envoyer un e-mail »** dans le ruban
3. **La boîte de dialogue d'e-mail s'ouvre**

#### 2. Activer Edit in Outlook
1. **Dans la boîte de dialogue d'e-mail** :
   - Sélectionner les destinataires
   - Choisir un modèle d'e-mail (facultatif)
   - **Cliquer sur « Modifier dans Outlook »**
2. **Le navigateur lance le téléchargement** du fichier .eml
3. **Attendez la fin du téléchargement**

#### 3. Modification dans Outlook
1. **Ouvrez le fichier .eml téléchargé** (double-clic)
2. **Outlook s'ouvre** avec un e-mail pré-rempli :
   - Document en pièce jointe PDF
   - Contenu du modèle dans le corps de l'e-mail
   - Informations sur les destinataires renseignées
3. **Modifiez l'e-mail** selon vos besoins :
   - Ajuster l'objet
   - Ajouter un texte personnel
   - Ajouter des pièces jointes supplémentaires
   - Ajuster la mise en forme

#### 4. Envoi
1. **Vérifiez votre e-mail**
2. **Cliquez sur « Envoyer »** dans Outlook
3. **L'e-mail est envoyé** via votre compte Outlook personnel
4. **L'e-mail apparaît** dans votre dossier Outlook « Éléments envoyés »

## Documents pris en charge

### Documents de vente
| Type de document | Page Business Central | Actions disponibles |
|------------------|----------------------|---------------------|
| **Devis de vente** | Devis de vente (41, 42, 43) | Envoyer e-mail → Modifier dans Outlook |
| **Commandes de vente** | Commande de vente (44, 45, 46) | Envoyer e-mail → Modifier dans Outlook |
| **Factures de vente** | Facture de vente (132, 133, 134) | Envoyer e-mail → Modifier dans Outlook |
| **Factures de vente validées** | Facture de vente validée (132) | Envoyer e-mail → Modifier dans Outlook |
| **Avoirs de vente** | Avoir de vente (114, 115) | Envoyer e-mail → Modifier dans Outlook |

### Documents d'achat
| Type de document | Page Business Central | Actions disponibles |
|------------------|----------------------|---------------------|
| **Devis d'achat** | Devis d'achat (49, 50, 51) | Envoyer e-mail → Modifier dans Outlook |
| **Commandes d'achat** | Commande d'achat (52, 53, 54) | Envoyer e-mail → Modifier dans Outlook |
| **Factures d'achat** | Facture d'achat (122, 123, 124) | Envoyer e-mail → Modifier dans Outlook |
| **Avoirs d'achat** | Avoir d'achat (124, 125) | Envoyer e-mail → Modifier dans Outlook |

### Documents d'entrepôt
| Type de document | Page Business Central | Actions disponibles |
|------------------|----------------------|---------------------|
| **Expéditions entrepôt** | Expédition entrepôt (7337) | Envoyer e-mail → Modifier dans Outlook |
| **Expéditions entrepôt validées** | Expédition entrepôt validée (7348) | Envoyer e-mail → Modifier dans Outlook |

## Interface utilisateur

### Boîte de dialogue d'e-mail Business Central
Lorsque vous sélectionnez « Envoyer un e-mail », vous voyez :

![Boîte de dialogue Envoyer un e-mail dans Business Central](../../../assets/Send%20Email.png)

### Invite de téléchargement Edit in Outlook
Après avoir cliqué sur « Modifier dans Outlook » :

```
┌─ Téléchargement navigateur ─────────────────┐
│ ⬇ Téléchargement : DevisVente_DV001.eml    │
│                                             │
│ ✓ Téléchargement terminé                   │
│                                             │
│ [ Ouvrir avec Outlook ]  [ Afficher dossier]│
└─────────────────────────────────────────────┘
```

### Fenêtre de rédaction Outlook
Le fichier .eml s'ouvre dans Outlook avec :

```
┌─ Nouveau message - Outlook ─────────────────┐
│ De : votre-email@entreprise.fr              │
│ À : client@exemple.fr                       │
│ Objet : Devis de vente DV001                │
│                                             │
│ ┌─────────────────────────────────────────┐ │
│ │ Madame, Monsieur,                       │ │
│ │                                         │ │
│ │ Veuillez trouver ci-joint notre        │ │
│ │ devis DV001.                            │ │
│ │                                         │ │
│ │ Cordialement,                           │ │
│ │ [Votre nom]                             │ │
│ └─────────────────────────────────────────┘ │
│                                             │
│ Pièces jointes : 📎 DevisVente_DV001.pdf  │
│                                             │
│ [Envoyer] [Enreg. brouillon] [Ignorer]    │
└─────────────────────────────────────────────┘
```

## Fonctionnalités d'édition des e-mails

### Ajustements du texte
Dans Outlook, vous pouvez :
- **Modifier l'objet**
- **Ajuster le corps du texte** :
  - Ajouter une note personnelle
  - Modifier le texte du modèle
  - Ajuster la mise en forme (gras, italique, couleurs)
  - Ajouter des listes
  - Insérer des liens

### Gestion des pièces jointes
- **Afficher les pièces jointes existantes** (document PDF)
- **Ajouter des pièces jointes supplémentaires** :
  - Documents additionnels
  - Images
  - Spécifications
  - Contrats
- **Supprimer des pièces jointes** (si nécessaire)
- **Renommer des pièces jointes**

### Ajustement des destinataires
- **Développer le champ À** avec des destinataires supplémentaires
- **Ajouter des destinataires en Cc**
- **Cci pour les copies masquées**
- **Valider les adresses** via le carnet d'adresses Outlook

### Signature et mise en forme
- **Signature personnelle** ajoutée automatiquement
- **Image de marque de l'entreprise** conservée depuis le modèle
- **Mise en forme HTML** entièrement disponible
- **Édition de texte enrichi** avec l'éditeur Outlook

## Fonctionnalités avancées

### Personnalisation du modèle
Personnaliser les modèles selon la situation :

```html
<!-- Avant l'envoi -->
<p>Madame, Monsieur %CUSTOMER_NAME%,</p>
<p>Veuillez trouver ci-joint %DOCUMENT_TYPE% %DOCUMENT_NO%.</p>

<!-- Après modification dans Outlook -->
<p>Monsieur Dupont,</p>
<p>Suite à notre conversation d'aujourd'hui, veuillez trouver ci-joint
notre devis de vente révisé DV001 avec les tarifs mis à jour.</p>
```

### Édition d'e-mails en masse
Pour plusieurs documents :
1. **Utiliser Edit in Outlook** pour le premier document
2. **Enregistrer comme modèle** dans Outlook
3. **Appliquer le modèle** aux documents suivants
4. **Personnaliser** chaque message

**Voir aussi :** [Versions prises en charge](supported-versions.md) | [Limitations](limitations.md)
