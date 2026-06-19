# Einschränkungen

Auf dieser Seite werden die bekannten Einschränkungen, Beschränkungen und Überlegungen bei der Verwendung von Edit in Outlook beschrieben.

## Technische Einschränkungen

### Browser- und Download-Einschränkungen

#### Dateigrößenbeschränkungen
| Komponente | Maximale Größe | Grund | Abhilfemaßnahme |
|------------|---------------|-------|-----------------|
| **EML-Datei** | 25 MB | Browser-Download-Limit | Große Anhänge aufteilen |
| **PDF-Anhänge** | 20 MB | E-Mail-Client-Limits | PDF komprimieren |
| **Gesamt-E-Mail** | 30 MB | Outlook/Exchange-Limit | SharePoint-Links verwenden |
| **Control Add-in** | 100 MB Arbeitsspeicher | Browser-Performance | Seite neu laden |

#### Browserspezifische Probleme
- **Chrome**: Popup-Blocker kann Downloads blockieren
- **Firefox**: Codierungsprobleme mit Nicht-ASCII-Zeichen
- **Edge**: Gelegentliche Zeitüberschreitung bei großen Dateien
- **Safari**: Eingeschränkte PDF-Vorschau-Unterstützung

### Business Central-Plattformeinschränkungen

#### SaaS vs. On-Premises
| Funktionalität | SaaS | On-Premises | Hinweis |
|----------------|------|-------------|---------|
| **Automatische Updates** | ✅ | ❌ | SaaS automatisch, On-Premises manuell |
| **Benutzerdefinierte Erweiterungen** | ⚠️ Begrenzt | ✅ Vollständig | SaaS-Sandbox-Einschränkungen |
| **Debug-Modus** | ❌ | ✅ | SaaS-Sicherheitsrichtlinie |
| **Protokollzugriff** | ⚠️ Application Insights | ✅ Direkt | Verschiedene Protokollierungsansätze |

#### API-Limits
- **Anfragen pro Minute**: 100 (SaaS), Unbegrenzt (On-Premises)
- **Sitzungs-Timeout**: Standardmäßig 30 Minuten
- **Gleichzeitige Benutzer**: Abhängig vom Lizenzmodell

## Outlook- und Office-Einschränkungen

### Outlook Desktop vs. Web

#### Funktionsvergleich
| Funktion | Desktop | Web | Mobil |
|----------|---------|-----|-------|
| **EML öffnen** | ✅ Nativ | ⚠️ Über Browser | ❌ Begrenzt |
| **Umfangreiche Formatierung** | ✅ Vollständig | ✅ Vollständig | ⚠️ Einfach |
| **Anlagenverwaltung** | ✅ Vollständig | ✅ Vollständig | ⚠️ Nur hochladen |
| **Offline-Zugriff** | ✅ Vollständig | ❌ Keine | ⚠️ Begrenzt |

#### Versionsabhängigkeiten
- **Outlook 2016/2019**: Eingeschränkte EML-Unterstützung
- **OWA Legacy**: Kein direktes Öffnen von EML
- **Mobile Apps**: Erfordert Vorbereitungsschritt auf dem Desktop

### Exchange- und O365-Limits

#### E-Mail-Größenbeschränkungen
| Plattform | Max. Nachrichtengröße | Max. Anhänge | Max. Empfänger |
|-----------|----------------------|-------------|----------------|
| **Exchange Online** | 150 MB | 100 | 500 |
| **Exchange 2019** | 35 MB (Standard) | Unbegrenzt | 5000 |
| **Exchange 2016** | 25 MB (Standard) | Unbegrenzt | 5000 |

> **Hinweis**: Organisationseinstellungen können diese Limits weiter einschränken

## Dokumenttyp-Einschränkungen

### Unterstützt vs. nicht unterstützt

#### Vollständig unterstützt
- ✅ Verkaufsangebote, -aufträge, -rechnungen
- ✅ Einkaufsbestellungen, -rechnungen
- ✅ Gebuchte Dokumente
- ✅ Gutschriften
- ✅ Lagerlieferungen

#### Eingeschränkte Unterstützung
- ⚠️ **Servicedokumente**: Einfache Vorlagenunterstützung
- ⚠️ **Projektdokumente**: Minimale Personalisierung
- ⚠️ **Montageaufträge**: Keine spezifischen Vorlagen

#### Nicht unterstützt
- ❌ **Benutzerdefinierte Berichtsobjekte**: Keine EML-Generierung
- ❌ **Dataverse-Integration**: Nur BC-nativ
- ❌ **Externe Dokumente**: Keine Drittanbieter-Unterstützung

### Vorlageneinschränkungen

#### HTML-Vorlagenprobleme

```html
/* Problematisches CSS */
.nicht-unterstuetzt {
    position: absolute;  /* Nicht weit verbreitet unterstützt */
    transform: rotate(); /* E-Mail-Client-Probleme */
    /* @media queries — Eingeschränkte Unterstützung */
}
```

#### Unterstützte HTML-Teilmenge
- ✅ Grundlegende HTML-Tags (p, div, table, br)
- ✅ CSS-Formatierung (Inline bevorzugt)
- ✅ Bilder (eingebettet oder verknüpft)
- ❌ JavaScript (Sicherheitsblockierung)
- ❌ Komplexe CSS-Layouts (Flexbox, Grid)
- ❌ Externes Schriftladen

## Benutzer- und Rechtseinschränkungen

### Berechtigungsabhängigkeiten

#### Mindesterforderliche Rechte
Ein Benutzer benötigt mindestens:
- **Dokument lesen**: Für Dokumentzugriff
- **E-Mail-Vorlage lesen**: Für Vorlagenzugriff
- **Datei herunterladen**: Für EML-Dateien
- **Control Add-in ausführen**: Für Browser-Funktionalität

**Siehe auch:** [E-Mails bearbeiten](editing-emails.md) | [Unterstützte Versionen](supported-versions.md)
