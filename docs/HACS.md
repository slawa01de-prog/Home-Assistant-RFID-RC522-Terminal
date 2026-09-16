# HACS / Dashboard-Abhängigkeiten

## Erforderlich

### Button Card

Die animierten Karten verwenden:

```yaml
type: custom:button-card
```

Daher muss **Button Card** über HACS installiert sein.

Nach der Installation Home Assistant bzw. das Frontend vollständig neu laden.

## Optional

### card-mod

`card-mod` ist für die aktuell enthaltenen drei Karten nicht zwingend erforderlich, kann aber für weitere Layout- und Designanpassungen genutzt werden.

## Fehler: Custom element doesn't exist

Wenn Home Assistant meldet:

```text
Custom element doesn't exist: button-card
```

prüfen:

1. Button Card in HACS installiert?
2. Home Assistant vollständig neu geladen?
3. Browser-Cache mit Strg+F5 aktualisiert?
4. HACS-Ressource korrekt geladen?
