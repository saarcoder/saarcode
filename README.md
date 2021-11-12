# Urban

Template für SvelteKit-Codebase mit Agentur-Stil. [Live-Demo](https://dry-duck.cloudvent.net) hier.
Verbessern Sie Ihre Web-Präsenz mit diesem konfigurierbaren Theme.

![Urban template screenshot](/static/images/saarcode_1024x875.png)

Urban wurde von [CloudCannon](https://cloudcannon.com/) erstellt, einer Jamstack-Plattform für Teams.

Weitere Templates, Themes und Tutorials finden Sie in der [CloudCannon Academy](https://learn.cloudcannon.com/).

## Features

- FrontMatter Live-Editing
- Kontakt-Formular
- Vorgefertigte Beispielseiten
- Vorgestylte Komponenten
- Team und Autoren-System
- Konfigurierbarer Footer
- Optimiert für Editing mit [CloudCannon](https://cloudcannon.com/)
- RSS/Atom-Feed
- SEO TagsSetup
- Google Analytics

## Einrichtung

1. Fügen Sie Ihre Domain und Autorendetails in `data/seo.json` hinzu.
2. Ergänzen Sie Ihren Google Analytics-Schlüssel in `data/site.json`.
3. Lernen Sie den Workflow kennen und sehen Sie Ihren Seiten-Output (direkt in [CloudCannon](https://app.cloudcannon.com/) oder lokal in Ihrer SvelteKit-Instanz).

## Entwickeln

Urban wurde mit [SvelteKit](https://kit.svelte.dev/) erstellt. Installieren Sie Abhängigkeiten und starten Sie eine Entwicklungsinstanz:

```bash
$ npm install
$ npm run dev
```

## Editieren

Urban ist bereits für das Ergänzen, Updaten und Entfernen von Seiten, Mitgliedern, Beiträgen und Unternehmensdetails sowie Footer-Elementen in [CloudCannon](https://app.cloudcannon.com/) optimiert.

### Beiträge

- Ergänzen, updaten oder entfernen Sie Beiträge in der _Posts_ collection.
- Das Feld **Staff Author** verlinkt zu Mitgliedern in der **Staff** collection.
- Ändern Sie die Standardeinträge in `content/posts/_defaults.md`, wenn Sie neue Beiträge verfassen.

### Kontakt-Formular

- Vorkonfiguriert für [CloudCannon](https://app.cloudcannon.com/), jedoch mit wenigen Änderungen auch mit anderen Providern nutzbar (z.B. [FormSpree](https://formspree.io/)).
- Versendet E-mails an die in company details angegebene E-Mail-Adresse.

### Teammitglieder

- Werden an mehreren Stellen auf der Seite eingefügt, um Doppel-Editieren zu vermeiden.

### Footer

- Inhalte als Daten-Datei zur Verfügung gestellt, um Kunden leichteren Zugang zu verschaffen.
- Eingerichtet unter _Data_ / _Footer_.

### Firmen-Details

- An mehreren Stellen auf der Seite eingefügt, um Doppel-Editieren zu vermeiden.
- Eingerichtet unter _Data_ / _Company_.

app access test
