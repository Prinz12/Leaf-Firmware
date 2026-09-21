# Leaf Basic 2.0.0 Beta – A/B und OTA-Migration

Veröffentlicht am 21.09.2026 für ESP8266 ESP-12F mit 4 MiB Flash und Hardwareprofil.

## Verbesserungen

- Signierte Updates schreiben nur den inaktiven Anwendungsslot. Der bestätigte bisherige Stand bleibt während des Uploads erhalten.
- Die neue Anwendung muss ihren Start nach mindestens 30 Sekunden gesunder Laufzeit und lokalem Statusabruf bestätigen. Bei fehlender Bestätigung erfolgt nach spätestens 120 Sekunden der Neustart mit Rückfall.
- Doppelte Bootdatensätze, Rückleseprüfung und Prüfung von Image, Hash und Signatur schützen vor unvollständigen und falschen Updates.
- Während des Teststarts bleiben Motorbefehle neutral und das Einstellungsjournal schreibgeschützt. Die Webseite wartet auf die Bestätigung des tatsächlich übertragenen Images.

## Bestehende 1.0.0-Geräte per OTA umstellen

Die Datei **firmware.bin ist ausschließlich für das A/B-Layout**. Für 1.0.0 ist einmalig die mitgelieferte, signierte Zwischenfirmware erforderlich. Dieser Weg ist für die eigenen, noch nicht bei Kunden installierten Platinen freigegeben.

Stabile Stromversorgung und serielle Reparaturmöglichkeit für den Fehlerfall bereithalten. Der erste Legacy-OTA-Kopiervorgang und der einmalige Bootloaderwechsel sind nicht stromausfallfest. Ein Versorgungsausfall während des Bootloaderwechsels kann serielle Wiederherstellung erfordern.

1. Auf dem direkt erreichbaren 1.0.0-Gerät `http://<IP>/update` öffnen und **migration-from-1.0.0.bin** hochladen. Auf den Start von **Leaf A/B OTA Migration 0.1.0 Beta** warten.
2. Dieselbe Update-Seite erneut öffnen und **firmware.bin** hochladen. Die Zwischenfirmware akzeptiert ausschließlich die hier veröffentlichte signierte 2.0.0-Hardwaredatei. Sie prüft diese vollständig, bereitet Slot B und beide Bootdatensätze vor und ersetzt den Bootloader zuletzt. Danach startet **2.0.0 Beta** aus B.
3. In der jetzt laufenden 2.0.0 erneut **firmware.bin** über die Update-Seite installieren und deren Startbestätigung abwarten. Damit ist auch A bestückt und dauerhaft bestätigt.

WLAN, Einstellungen und Hausplan bleiben erhalten. Der interne Service kann die drei Schritte mit dem geprüften Migrationswerkzeug automatisieren; es gleicht Gerätekennung, Firmware, Imagehash, Einstellungen und Hausplan ab und wiederholt unklare Uploads nicht automatisch.

Bereits vollständig umgestellte A/B-Geräte verwenden für künftige Updates ausschließlich **firmware.bin**. Die Zwischenfirmware wird dort nicht mehr benötigt. Eine direkte Rückkehr zu 1.0.0 per normalem A/B-OTA ist nicht vorgesehen.

## Umstellung mit Leaf Local ab 0.37.0

Zuerst unter **Einstellungen → App-Update** die App auf [0.37.0 oder neuer](https://github.com/Prinz12/Leaf-Firmware/releases/tag/app-v0.37.0) aktualisieren. Danach **Firmware-Updates** öffnen, **Beta-Versionen anzeigen** aktivieren, **VERSION PRÜFEN**, **FIRMWARE HERUNTERLADEN** und **GERÄTE PRÜFEN** ausführen. Die gewünschten Geräte auswählen und **AUSWAHL AKTUALISIEREN** bestätigen.

Die App wählt das passende Profil selbst und führt die drei OTA-Schritte nacheinander aus. Vor einer Bootloaderänderung verlangt ein zusätzliches Warnfenster ausdrücklich **VERSTANDEN – UPDATE STARTEN**:

> Während der gesamten Umstellung auf keinen Fall die Spannungsversorgung unterbrechen!

Abbrechen startet keinen Upload. Die App prüft Signatur, Gerätekennung, Profil, Imagehash, bestätigten Start, Einstellungen und Hausplan. Safe bleibt Safe. Ein Fehler stoppt die Updatefolge; ein angeforderter Stopp beendet zuerst den vollständigen Vorgang am aktuellen Gerät. Nach einem App-Abbruch muss der Nutzer erneut prüfen und bestätigen; unklare Uploads werden nicht automatisch wiederholt.

Die Beschränkung auf eigene Testgeräte mit serieller Reparaturmöglichkeit bleibt bestehen. Normale spätere A/B-Updates ändern den Bootloader nicht.

## Prüfstand und Grenzen

195 Hosttests, 29 native Testprogramme und die Web-Rückkehrprüfung bestanden. Hardware-/Safe-Builds für Legacy und A/B sowie der Migrationsbuild erfolgreich. Die vollständige OTA-Kette von 1.0.0 bis zu beiden A/B-Slots wurde auf der Testplatine ausgeführt. Manipulierte, falsche und abgebrochene Migrationsuploads wurden abgewiesen; Einstellungen und Hausplan blieben erhalten. Bootloader, beide Anwendungen, Bootdatensätze und Benutzerdaten wurden anschließend seriell per Prüfsumme bestätigt.

Reale Versorgungstrennungen bei A/B-Kaltstart, unbestätigtem Teststart und Upload wurden bereits geprüft. Der zusätzliche präzise Stromausfalltest innerhalb einzelner Flash-Lösch-/Schreibimpulse wurde auf Wunsch zurückgestellt und wird nicht als bestanden angegeben. Beta-Freigabe, keine vollständige elektrische Kundenabnahme. Für einen beschädigten Bootloader, zwei zerstörte Bootdatensätze oder ein nachträglich beschädigtes bestätigtes Image gibt es noch kein unabhängiges Rettungsimage.

## Updatekanal

Separater A/B-Tag **ab-v2.0.0-beta**, Artefaktzweig **ab-beta**, Layout2-Manifest mit Schema 2. Der bisherige `main`-/`v1.0.0-beta`-Kanal bleibt bestehen. Leaf Local ab 0.37.0 unterstützt diesen Kanal nach Aktivierung von **Beta-Versionen anzeigen** und ausdrücklichem Start durch den Nutzer. Ältere Apps benötigen zuerst das App-Update. Es erfolgt keine selbstständige Migration im Hintergrund. Durch diese Veröffentlichung wird kein weiteres Gerät aktualisiert.

Das Paket enthält nur die signierte Hardware-Firmware, die signierte Zwischenfirmware, Versionsinformationen und diese Anleitung. Keine Safe-/Testimages, Firmwarequellen oder Gerätedaten.
