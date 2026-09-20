# Leaf Basic 2.0.0 Beta Safe – A/B und OTA-Migration

Veröffentlicht am 21.09.2026 für ESP8266 ESP-12F mit 4 MiB Flash und Safe-Profil.

## Safe-Migration ergänzt

Das bisherige Migrationspaket 0.1.0 ist für das Hardwareprofil signiert. Safe-Geräte lehnen es mit „Firmwareprofil passt nicht“ ab. Für Safe 1.0.0 ist jetzt die separate, signierte Zwischenfirmware 0.2.0 verfügbar. Profilprüfung und Signaturprüfung bleiben aktiv. Das Safe-Profil und die deaktivierten Hardwareausgänge bleiben bei allen drei OTA-Schritten erhalten.

Die endgültige Safe-Firmware 2.0.0 verwendet zwei Anwendungsslots. Normale spätere A/B-Updates schreiben in den inaktiven Slot. Eine neue Anwendung muss ihren Start nach mindestens 30 Sekunden gesunder Laufzeit und lokalem Statusabruf bestätigen. Bei fehlender Bestätigung erfolgt nach spätestens 120 Sekunden ein Neustart mit Rückfall auf den zuvor bestätigten Stand.

## Safe 1.0.0 per OTA umstellen

Dieser Weg ist für die eigenen, noch nicht bei Kunden installierten Platinen freigegeben. Voraussetzung ist **Leaf 1.0.0 Beta im Safe-Profil** mit direkter HTTP-Erreichbarkeit.

Stabile Stromversorgung und serielle Reparaturmöglichkeit für den Fehlerfall bereithalten. Der erste Legacy-OTA-Kopiervorgang und der einmalige Bootloaderwechsel sind nicht stromausfallfest. Ein Versorgungsausfall während des Bootloaderwechsels kann serielle Wiederherstellung erfordern.

1. Unter `http://<IP>/update` **migration-safe-from-1.0.0.bin** installieren. Auf **Leaf A/B OTA Migration 0.2.0 Beta** warten.
2. Auf derselben Update-Seite **firmware-safe.bin** installieren. Die Zwischenfirmware akzeptiert ausschließlich die hier veröffentlichte signierte Safe-2.0.0-Datei. Sie prüft diese vollständig, bereitet Slot B und beide Bootdatensätze vor und ersetzt den Bootloader zuletzt. Danach startet **2.0.0 Beta** aus B.
3. Nach diesem Start erneut **firmware-safe.bin** installieren und die Startbestätigung abwarten. Damit ist auch Slot A mit Safe bestückt und dauerhaft bestätigt.

WLAN, Einstellungen und Hausplan bleiben erhalten. Das interne Servicewerkzeug verwendet `--profile safe` und gleicht Gerätekennung, Profil, Imagehash, Einstellungen und Hausplan ab. Unklare Uploads werden nicht automatisch wiederholt. Profilwechsel sind während der Migration gesperrt.

Bereits vollständig umgestellte Safe-A/B-Geräte verwenden für künftige Updates nur die passende **firmware-safe.bin**. Die Zwischenfirmware wird dort nicht mehr benötigt. Eine direkte Rückkehr zu 1.0.0 per normalem A/B-OTA ist nicht vorgesehen.

## Prüfstand und Grenzen

198 Hosttests, 29 native Testprogramme und die Web-Rückkehrprüfung bestanden. Legacy-Hardware, Legacy-Safe und beide Migrationsprofile erfolgreich gebaut. Die vollständige Safe-OTA-Kette von 1.0.0 über Migration 0.2.0 bis zu beiden Safe-A/B-Slots wurde auf der freigegebenen Testplatine ausgeführt. Hardwarepakete und eine manipulierte Safe-Datei wurden abgewiesen; die Ausgänge blieben deaktiviert. Einstellungen und Hausplan blieben erhalten.

Bootloader, beide Safe-Anwendungen, Bootdatensätze und unveränderte Benutzerdaten wurden anschließend seriell per Prüfsumme bestätigt. Ein Neustart mit gelöschten RTC-Bootinformationen bestätigte den dauerhaft gespeicherten Safe-Start.

Der zusätzliche präzise Stromausfalltest innerhalb einzelner Flash-Lösch-/Schreibimpulse wurde auf Wunsch zurückgestellt und wird nicht als bestanden angegeben. Beta-Freigabe, keine vollständige elektrische Kundenabnahme. Für einen beschädigten Bootloader, zwei zerstörte Bootdatensätze oder ein nachträglich beschädigtes bestätigtes Image gibt es noch kein unabhängiges Rettungsimage.

## Updatekanal

Separater Safe-A/B-Tag **ab-safe-v2.0.0-beta**, Artefaktzweig **ab-safe-beta**, Layout2-Manifest mit Schema 2. Der Hardware-A/B-Kanal `ab-v2.0.0-beta` und der bisherige `main`-/`v1.0.0-beta`-Kanal bleiben bestehen. Vorhandene Leaf-Local-Apps wählen dieses A/B-Release nicht automatisch aus; für die Umstellung das Servicewerkzeug oder die Gerätewebseite verwenden. Durch diese Veröffentlichung wird kein weiteres Gerät aktualisiert.

Das Paket enthält nur die signierte Safe-Firmware, die signierte Safe-Zwischenfirmware, Versionsinformationen und diese Anleitung. Keine Testimages, Firmwarequellen oder Gerätedaten.
