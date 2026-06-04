# Datenbank-Honeypot

Ein Honeypot, der einen Datenbank-Dienst (MySQL) vortaeuscht, um echte Angreifer aus dem Internet anzulocken und ihre Eindringversuche aufzuzeichnen und auszuwerten.

## Worum geht es

Dieses Projekt taeuscht nach aussen einen verwundbar wirkenden Datenbank-Dienst vor. Echte Angreifer aus dem offenen Internet finden diesen Dienst, halten ihn fuer ein lohnendes Ziel und starten Eindringversuche. Der Honeypot nimmt diese Versuche entgegen, schneidet sie mit und speichert sie strukturiert in einer Datenbank. Aus den gesammelten Daten lassen sich anschliessend Angriffsmuster erkennen und Erkenntnisse darueber gewinnen, wie Angreifer vorgehen.

Der Beobachtungsschwerpunkt liegt bewusst darauf, **wie Angreifer versuchen hineinzukommen** (verwendete Zugangsdaten, Verbindungs- und Eindringversuche, Methoden) und nicht darauf, was sie nach einem erfolgreichen Einbruch tun.

## Ausbildungskontext

Dieses Projekt entsteht im Rahmen der Ausbildung in der Fachrichtung **Plattformentwicklung**. Der Schwerpunkt der eigenen Arbeit liegt deshalb nicht im Erfinden eines Honeypots, sondern im sicheren und durchdachten **Betreiben eines Dienstes auf einer Plattform** sowie im Auswerten der Ergebnisse: konfigurieren, containerisieren, haerten, isolieren, den Live-Betrieb aufsetzen, eine Datenbank entwerfen und die Daten auswerten.

## Eingesetzte Bereiche und Technologien

- **Security** – Honeypot, Angriffsbeobachtung und Auswertung
- **Cloud / Plattform** – Betrieb auf einer aus dem Internet erreichbaren, isolierten Umgebung
- **Datenbanken** – als vorgetaeuschter Koeder und als echte Datenbank im Hintergrund zur Speicherung der Erkenntnisse
- **Container** – der Honeypot wird containerisiert betrieben
- **Orchestrierung** – Kubernetes / OpenShift fuer den Betrieb und die Absicherung im Live-Betrieb

> Hinweis: Es gibt in diesem Projekt zwei verschiedene Datenbanken, die nicht verwechselt werden duerfen:
> 1. die **vorgetaeuschte Koeder-Datenbank** (nur eine Attrappe, ohne echte Funktion), und
> 2. die **echte Datenbank im Hintergrund**, in der die gesammelten Angriffsdaten gespeichert werden.

## Wichtige Entscheidungen mit Begruendung

- **Nur den Dienst vortaeuschen, keine echte Koeder-Datenbank**, da der Fokus auf dem Hineinkommen liegt. Das senkt Aufwand und Risiko (niedrig-interaktiver Honeypot).
- **Betrieb im offenen Internet statt im internen Netz**, da gezielt anonyme Angreifer aus dem Internet beobachtet werden sollen. Der Honeypot muss daher oeffentlich erreichbar und zugleich sicher vom eigenen Netz getrennt sein.
- **Risiko-Beherrschung** durch Haerten des Containers, Sperren des ausgehenden Verkehrs (gegen Missbrauch als Sprungbrett) und Einholen der Freigabe des Ausbildungsbetriebs. Ein absolutes Null-Risiko gibt es nicht.
- **Laufzeit nach Datenlage**: mehrere Tage mit Ueberwachung und der Moeglichkeit, jederzeit abzuschalten. Abschaltung, sobald genug Daten fuer erkennbare Muster vorliegen.

## Meilensteine

### Meilenstein 1 – Vorgetaeuschter Dienst laeuft lokal
Der Honeypot taeuscht lokal einen Datenbank-Dienst ueberzeugend vor, nimmt eingehende Verbindungen an und verleitet zu Login-Versuchen. Selbst getestet und stabil lokal lauffaehig.

### Meilenstein 2 – Mitschneiden und Festhalten
Die Versuche werden zuverlaessig protokolliert (Zugangsdaten, Verbindungsdetails) und strukturiert in einer Datenbank gespeichert, sodass sie spaeter ausgewertet werden koennen.

### Meilenstein 3 – Sicherer Live-Betrieb und Auswertung
Den Honeypot containerisieren, haerten und isolieren, den ausgehenden Verkehr einschraenken und ueber Kubernetes / OpenShift live ins Internet stellen. Anschliessend die echten Angriffsdaten auswerten und die Erkenntnisse ueber die beobachteten Angriffstaktiken in einem Fazit festhalten.

## Aufbau (geplant)

1. **Lokale Entwicklung und Test** auf dem Arbeitslaptop (Meilenstein 1 und 2).
2. **Live-Betrieb** auf einer aus dem Internet erreichbaren Maschine, auf der Kubernetes / OpenShift den containerisierten Honeypot betreibt (Meilenstein 3).

## Offene Punkte

- Klaerung mit dem Ausbildungsbetrieb, **wo** Kubernetes / OpenShift betrieben wird (eigener Server oder fertiger Dienst eines Anbieters).
- **Freigabe** fuer den Live-Betrieb eines bewusst Angreifer-anlockenden Honeypots einholen.
- **Kostenfrage** fuer die Betriebsumgebung klaeren.

## Sicherheitshinweis

Dieses Projekt betreibt bewusst einen verwundbar wirkenden Dienst, um Angreifer anzulocken. Der Betrieb erfolgt ausschliesslich in einer isolierten, vom Produktiv- und Privatnetz getrennten Umgebung, mit gesperrtem ausgehendem Verkehr und nach vorheriger Freigabe. Mitgeschnittene Daten (z. B. IP-Adressen) werden sorgsam behandelt und nicht veroeffentlicht.
