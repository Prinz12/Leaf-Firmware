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

## Prüfstand und Grenzen

195 Hosttests, 29 native Testprogramme und die Web-Rückkehrprüfung bestanden. Hardware-/Safe-Builds für Legacy und A/B sowie der Migrationsbuild erfolgreich. Die vollständige OTA-Kette von 1.0.0 bis zu beiden A/B-Slots wurde auf der Testplatine ausgeführt. Manipulierte, falsche und abgebrochene Migrationsuploads wurden abgewiesen; Einstellungen und Hausplan blieben erhalten. Bootloader, beide Anwendungen, Bootdatensätze und Benutzerdaten wurden anschließend seriell per Prüfsumme bestätigt.

Reale Versorgungstrennungen bei A/B-Kaltstart, unbestätigtem Teststart und Upload wurden bereits geprüft. Der zusätzliche präzise Stromausfalltest innerhalb einzelner Flash-Lösch-/Schreibimpulse wurde auf Wunsch zurückgestellt und wird nicht als bestanden angegeben. Beta-Freigabe, keine vollständige elektrische Kundenabnahme. Für einen beschädigten Bootloader, zwei zerstörte Bootdatensätze oder ein nachträglich beschädigtes bestätigtes Image gibt es noch kein unabhängiges Rettungsimage.

## Updatekanal

Separater A/B-Tag **ab-v2.0.0-beta**, Artefaktzweig **ab-beta**, Layout2-Manifest mit Schema 2. Der bisherige `main`-/`v1.0.0-beta`-Kanal bleibt bestehen. Vorhandene Leaf-Local-Apps wählen dieses A/B-Release nicht automatisch aus; für die Umstellung das Servicewerkzeug oder die Gerätewebseite verwenden. Durch diese Veröffentlichung wird kein weiteres Gerät aktualisiert.

Das Paket enthält nur die signierte Hardware-Firmware, die signierte Zwischenfirmware, Versionsinformationen und diese Anleitung. Keine Safe-/Testimages, Firmwarequellen oder Gerätedaten.
