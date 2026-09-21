# Leaf Basic 2.0.2 Beta – schnellere Startbestätigung

Veröffentlicht am 21.09.2026.

Die neue Firmware bestätigt ihren Start nach **zehn statt 30 Sekunden kontinuierlich gesunder Laufzeit**. Initialisierung, gültige Bootdaten, lokaler Statusabruf und dauerhafte Flash-Bestätigung bleiben erforderlich. Eine Hauptschleifenstörung setzt die Stabilitätsfrist zurück. Ohne Bestätigung bleibt der Rückfallneustart nach 120 Sekunden erhalten.

Die zehn Sekunden beginnen in der neuen Firmware. Upload, WLAN-Verbindung und gesamter Neustart können zusätzlich Zeit benötigen. Bloße Erreichbarkeit gilt weiterhin nicht als erfolgreiche Startbestätigung.

## Update mit der App

Zuerst Leaf Local auf **0.37.2 oder neuer** aktualisieren. Unter Firmware-Updates **Beta-Versionen anzeigen**, **VERSION PRÜFEN**, **FIRMWARE HERUNTERLADEN** und **GERÄTE PRÜFEN** ausführen. Bereits vollständig umgestellte A/B-Geräte erhalten ein normales Update in den inaktiven Anwendungsslot; der Bootloader wird dabei nicht geändert.

Bestehende 1.0.0-/1.0.1-Geräte müssen zuerst die vollständige Migration auf **2.0.0** abschließen. Dafür bleibt das separate Paket **ab-v2.0.0-beta** unverändert verfügbar. Danach erneut prüfen und normal auf **2.0.2** aktualisieren. Die Migrationsbrücke akzeptiert ausschließlich ihre fest gebundene 2.0.0-Datei. Dort gelten weiterhin 30 Sekunden Startbestätigung.

Vor der einmaligen Bootloaderänderung ist die Stromversorgungswarnung ausdrücklich zu bestätigen. Während der Migration darf die Spannungsversorgung auf keinen Fall unterbrochen werden. Die Migration bleibt für eigene Testgeräte mit serieller Reparaturmöglichkeit bestimmt.

App 0.37.2 erkennt einen nachweislich wiederhergestellten Ausgangszustand früher und erklärt gespeicherte Updateversuche genauer. **FEHLVERSUCH PRÜFEN** bleibt eine lesende Prüfung; ein neuer Upload benötigt eine ausdrückliche Bestätigung. Unklare oder nicht erreichbare Geräte behalten ein begrenztes Prüfzeitfenster.

## Profil und Prüfung

Hardwareprofil für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85. Ausschließlich firmware.bin für bereits umgestellte Hardwaregeräte verwenden.

Signatur-, Profil- und Integritätsprüfungen sowie Einstellungen, Hausplan und Bootdatenformat bleiben erhalten. Kein neuer Bootloader und keine neue Migrationsbrücke.

198 Hosttests, 29 native Regressionen und alle vier Hardware-/Safe-Builds erfolgreich. Die Zehn-Sekunden-Grenze, Schleifenstörungen, Statuspflicht, Flash-Commit-Fehler und Rückfallfrist wurden geprüft. Kein physisches Gerät mit dieser Ausgabe geflasht. Der zuvor zurückgestellte präzise Stromausfalltest innerhalb eines Flash-Schreibimpulses bleibt offen; Beta-Freigabe.
