# Datenbank-Honeypot

Hiermit dokumentiere ich das erworbene Wissen und Vorgehen des Abschlussprojekts.


## Inhaltsverzeichnis📖

1. [Worum es geht](#worum-es-geht)
2. [Meilensteine](#meilensteine)
3. [Wichtige Entscheidungen](#wichtige-entscheidungen)
4. [Aufbau (geplant)](#aufbau-geplant)


## Worum es geht
Dieses Projekt täuscht nach aussen einen verwundbar wirkenden Datenbank-Dienst vor. Echte Angreifer aus dem offenen Internet finden diesen Dienst, halten ihn für ein wertvolles Ziel und starten Eindringversuche. Der Honeypot nimmt diese Versuche entgegen, schneidet sie mit. Diese Logdaten werden dann an einen Syslog-Server weitergeleitet und gespeichert. Aus den gesammelten Daten lassen sich anschliessend Angriffsmuster erkennen und Erkenntnisse darüber gewinnen, wie Angreifer vorgehen.

Der Beobachtungsschwerpunkt liegt bewusst darauf, wie Angreifer versuchen hineinzukommen (verwendete Zugangsdaten, Verbindungs- und Eindringversuche, Methoden) und nicht darauf, was sie nach einem erfolgreichen Einbruch tun.

## Meilensteine

### Erster Meilenstein: Vorgetäuschter Dienst läuft lokal

Honeypot täuscht lokal einen Datenbank-Dienst überzeugend vor, nimmt Verbindungen an, verleitet zu Login-Versuchen. Selbst getestet, stabil lokal lauffähig.

### Zweiter Meilenstein: Mitschneiden und Festhalten

Versuche werden zuverlässig protokolliert (Zugangsdaten, Verbindungsdetails) und an einen Syslog-Server geschickt, der sie zentral sammelt, sodass sie später ausgewertet werden können.

### Dritter Meilenstein: Sicherer Live-Betrieb und Auswertung
Containerisieren, härten, isolieren, ausgehenden Verkehr einschränken, auf gewählten Cloud-Anbieter live stellen. Anschliessend die echten Angriffsdaten auswerten und Erkenntnisse über Angriffstaktiken in einem Fazit festhalten.
---

## Wichtige Entscheidungen

- Nur den Dienst vortäuschen, keine echte Köder-Datenbank, da der Fokus auf dem Hineinkommen liegt. Das senkt Aufwand und Risiko (niedrig-interaktiver Honeypot).
- Betrieb im offenen Internet statt im internen Netz, da gezielt anonyme Angreifer aus dem Internet beobachtet werden sollen. Der Honeypot muss daher öffentlich erreichbar und zugleich sicher vom eigenen Netz getrennt sein.
- Risiko-Beherrschung durch Härten des Containers, Sperren des ausgehenden Verkehrs (gegen Missbrauch als Sprungbrett) und Einholen der Freigabe des Ausbildungsbetriebs. Ein absolutes Null-Risiko gibt es nicht.
- Laufzeit nach Datenlage: mehrere Tage mit Überwachung und der Möglichkeit, jederzeit abzuschalten. Abschaltung, sobald genug Daten für erkennbare Muster vorliegen.
---

## Aufbau (geplant)

1. **Lokale Entwicklung und Test** auf dem Arbeitslaptop (Meilenstein 1 und 2).
2. **Live-Betrieb** auf einer aus dem Internet erreichbaren Maschine, auf der Kubernetes / OpenShift den containerisierten Honeypot betreibt (Meilenstein 3).

---

[Zurück zum Anfang](#datenbank-honeypot)