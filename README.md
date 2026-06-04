# Datenbank-Honeypot

Ein Honeypot, der einen Datenbank-Dienst (MySQL) vortaeuscht, um echte Angreifer aus dem Internet anzulocken und ihre Eindringversuche aufzuzeichnen und auszuwerten.

## Worum es geht 

Dieses Projekt täuscht nach aussen einen verwundbar wirkenden Datenbank-Dienst vor. Echte Angreifer aus dem offenen Internet finden diesen Dienst, halten ihn für ein lohnendes Ziel und starten Eindringversuche. Der Honeypot nimmt diese Versuche entgegen, schneidet sie mit und speichert sie strukturiert in einer Datenbank. Aus den gesammelten Daten lassen sich anschliessend Angriffsmuster erkennen und Erkenntnisse darüber gewinnen, wie Angreifer vorgehen.

Der Beobachtungsschwerpunkt liegt bewusst darauf, **wie Angreifer versuchen hineinzukommen** (verwendete Zugangsdaten, Verbindungs- und Eindringversuche, Methoden) und nicht darauf, was sie nach einem erfolgreichen Einbruch tun.

## Ausbildungskontext

Dieses Projekt entsteht im Rahmen der Ausbildung in der Fachrichtung **Plattformentwicklung**. Der Schwerpunkt der eigenen Arbeit liegt deshalb nicht im Erfinden eines Honeypots, sondern im sicheren und durchdachten **Betreiben eines Dienstes auf einer Plattform** sowie im Auswerten der Ergebnisse: konfigurieren, containerisieren, härten, isolieren, den Live-Betrieb aufsetzen, eine Datenbank entwerfen und die Daten auswerten.

## Eingesetzte Bereiche und Technologien

- **Security** – Honeypot, Angriffsbeobachtung und Auswertung
- **Cloud / Plattform** – Betrieb auf einer aus dem Internet erreichbaren, isolierten Umgebung
- **Datenbanken** – als vorgetäuschter Köder und als echte Datenbank im Hintergrund zur Speicherung der Erkenntnisse
- **Container** – der Honeypot wird containerisiert betrieben
- **Orchestrierung** – Kubernetes / OpenShift für den Betrieb und die Absicherung im Live-Betrieb

> Hinweis: Es gibt in diesem Projekt zwei verschiedene Datenbanken, die nicht verwechselt werden dürfen:
> 1. die **vorgetäuschte Köder-Datenbank** (nur eine Attrappe, ohne echte Funktion), und
> 2. die **echte Datenbank im Hintergrund**, in der die gesammelten Angriffsdaten gespeichert werden.

## Wichtige Entscheidungen mit Begründung

- **Nur den Dienst vortäuschen, keine echte Köder-Datenbank**, da der Fokus auf dem Hineinkommen liegt. Das senkt Aufwand und Risiko (niedrig-interaktiver Honeypot).
- **Betrieb im offenen Internet statt im internen Netz**, da gezielt anonyme Angreifer aus dem Internet beobachtet werden sollen. Der Honeypot muss daher öffentlich erreichbar und zugleich sicher vom eigenen Netz getrennt sein.
- **Risiko-Beherrschung** durch Härten des Containers, Sperren des ausgehenden Verkehrs (gegen Missbrauch als Sprungbrett) und Einholen der Freigabe des Ausbildungsbetriebs. Ein absolutes Null-Risiko gibt es nicht.
- **Laufzeit nach Datenlage**: mehrere Tage mit überwachung und der Möglichkeit, jederzeit abzuschalten. Abschaltung, sobald genug Daten für erkennbare Muster vorliegen.

## Meilensteine

### Meilenstein 1 – Vorgetäuschter Dienst läuft lokal
Der Honeypot täuscht lokal einen Datenbank-Dienst überzeugend vor, nimmt eingehende Verbindungen an und verleitet zu Login-Versuchen. Selbst getestet und stabil lokal lauffähig.

### Meilenstein 2 – Mitschneiden und Festhalten
Die Versuche werden zuverlässig protokolliert (Zugangsdaten, Verbindungsdetails) und strukturiert in einer Datenbank gespeichert, sodass sie später ausgewertet werden können.

### Meilenstein 3 – Sicherer Live-Betrieb und Auswertung
Den Honeypot containerisieren, härten und isolieren, den ausgehenden Verkehr einschränken und über Kubernetes / OpenShift live ins Internet stellen. Anschliessend die echten Angriffsdaten auswerten und die Erkenntnisse über die beobachteten Angriffstaktiken in einem Fazit festhalten.

## Aufbau (geplant)

1. **Lokale Entwicklung und Test** auf dem Arbeitslaptop (Meilenstein 1 und 2).
2. **Live-Betrieb** auf einer aus dem Internet erreichbaren Maschine, auf der Kubernetes / OpenShift den containerisierten Honeypot betreibt (Meilenstein 3).

## Offene Punkte

- Klärung mit dem Ausbildungsbetrieb, **wo** Kubernetes / OpenShift betrieben wird (eigener Server oder fertiger Dienst eines Anbieters).
- **Freigabe** für den Live-Betrieb eines bewusst Angreifer-anlockenden Honeypots einholen.
- **Kostenfrage** für die Betriebsumgebung klären.

## Sicherheitshinweis

Dieses Projekt betreibt bewusst einen verwundbar wirkenden Dienst, um Angreifer anzulocken. Der Betrieb erfolgt ausschliesslich in einer isolierten, vom Produktiv- und Privatnetz getrennten Umgebung, mit gesperrtem ausgehendem Verkehr und nach vorheriger Freigabe. Mitgeschnittene Daten (z. B. IP-Adressen) werden sorgsam behandelt und nicht veröffentlicht.
