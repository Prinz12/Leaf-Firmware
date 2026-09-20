# Änderungen

## 1.0.0 Beta – 2026-09-20

- OTA akzeptiert ab dieser Version ausschließlich signierte Leaf-Firmware. Vollständige Prüfungen von Imageaufbau, Länge, Integrität, Ziel und Profil erfolgen vor Freigabe des Updates.
- Zurückgelesene Flashdaten werden einschließlich Lese- und Schreibfehlern geprüft. Zusätzliche Dateien, unvollständige Uploads und Abbrüche werden abgewiesen.
- Der erste Wechsel von älterer Firmware auf 1.0.0 erfolgt noch über deren bisherigen Updater. Die neuen Prüfungen greifen nach dem Start von 1.0.0.
- Alte unsignierte Dateien werden danach auch für ein Downgrade abgewiesen. Ausschließlich die signierte firmware.bin aus dem offiziellen OTA-Kanal verwenden.
- Ein Hardware-/Safe-Profilwechsel verlangt eine ausdrückliche Serviceauswahl in der Weboberfläche. Der öffentliche OTA-Kanal enthält weiterhin ausschließlich das Hardwareprofil.
- Bestehende Einstellungen und Hausplan behalten ihr Speicherformat. Der Bootloader bleibt unverändert; A/B-Rückfall und Stromausfallschutz beim Kopieren sind noch nicht enthalten.
- Geprüft: 184 Hosttests, 23 native Testprogramme, Browserregression sowie Hardware- und Safe-Build. Der physische OTA-/RAM-Test steht aus; Beta-Version ohne Stable-Freigabe. Durch diese Veröffentlichung wird kein Gerät automatisch geflasht.

Hardware-Firmware für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85. Das separate Safe-Bridge-Paket akzeptiert diese Datei nicht.

## 0.9.2 Beta – 2026-09-20

- OTA wartet nach erfolgreicher Firmwareprüfung bis zu fünf Sekunden auf die TCP-Bestätigung der Abschlussantwort. Anschließend folgt ein kontrollierter Neustart mit 1,5 Sekunden Nachlauf.
- Verzögerte Verbindungen, etwa über VPN, erhalten damit mehr Zeit für die Abschlussbestätigung. Ein nicht mehr erreichbarer Client verhindert den Neustart nicht.
- Der erste Wechsel von einer älteren Firmware auf 0.9.2 wird noch von deren bisherigem OTA-Code abgewickelt. Die Verbesserung greift bei nachfolgenden Updates.
- 178 Hosttests, 20 native Regressionen sowie Hardware- und Safe-Build erfolgreich. Keine physische VPN-/OTA-Prüfung; kein Gerät automatisch geflasht.
- Dieses öffentliche Firmwarepaket enthält ausschließlich die Hardware-Version für ESP8266 ESP-12F mit 4 MiB Flash.

## 0.9.1 Beta — 2026-09-20

- „Öffnen“ in der gemeinsamen Geräteübersicht öffnet bei Gateways die vollständige Webseite über ihre eigene IP-Adresse.
- Nur Repeater öffnen die kompakte Geräteansicht über ihr zuständiges Gateway. Das Hardware-/Safe-Profil beeinflusst die Auswahl nicht. Rollenwechsel werden bei der nächsten Statusabfrage berücksichtigt.
- Fehlende/ungültige Gateway-Adressen erzeugen keinen falschen Link; das lokale Gerät bleibt lokal.
- Gateway-Wiederherstellung, LED-Korrektur, WLAN-Bewertung und OTA-Fortschritt aus 0.9.0 bleiben enthalten. Motorsteuerung und Speicherformate unverändert.
- Geprüft: Hardware-/Safe-Builds, 178 Hosttests und simulierte Desktop-/Mobil-Browserabläufe einschließlich Linkzielen und Rollenwechsel. Kein Gerät geflasht; keine reale Gerätenavigation mit dieser Ausgabe getestet.

Hardware-Firmware für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85. Beta-Kanal. Die Veröffentlichung enthält kein Safe-/Recovery-Abbild.

## 0.9.0 Beta — 2026-09-19

- Feste Repeater erholen sich jetzt auch nach dem Ausfall einer zuvor funktionierenden Gateway-Verbindung: regelmäßige Ende-zu-Ende-Bestätigungen, nach 90–120 Sekunden ohne neue Bestätigung kontrollierter Neustart in Automatik. Die Wartezeit ist geräteabhängig verteilt; ein vorher wieder erreichbares Gateway verhindert den Neustart. Ein Ersatzgateway setzt passende WLAN-Erreichbarkeit voraus.
- Erfolgreich verbundene Repeater beenden das schnelle Verbindungsblinken der LED. Filter-, Bedien- und Servicehinweise behalten ihre Priorität.
- WLAN-Empfang mit dBm, Farbe und Textbewertung; OTA-Upload mit Prozentbalken sowie getrennten Meldungen für Firmwareprüfung und Neustart.
- Raumauswahl aus vorhandenen Gruppen oder neuen Räumen. Statusabfragen überschreiben keine laufenden Eingaben. Partnerdiagnose zeigt die Herkunft fehlender/ungültiger Sensorwerte.
- Webantworten berücksichtigen langsame VPN-Verbindungen und übertragen große Seiten in kleinen, kooperativen Schritten.
- Konfiguration und Hausplan bleiben erhalten. Bestehende Speicherprüfungen für OTA werden nicht umgangen. Die Versionsnummer bleibt auf ausdrücklichen Wunsch 0.9.0 Beta; bereits zuvor manuell installierte 0.9.0-Builds benötigen diese neue BIN für die Ergänzungen.
- Geprüft: Hardware-/Safe-Builds, 178 Hosttests, 19 native Testprogramme und simulierte Desktop-/Mobil-Browserabläufe. Gateway-Ausfall und OTA wurden mit dieser Ausgabe noch nicht physisch am Gerät getestet. Kein Gerät durch die Veröffentlichung geflasht.

Öffentliches Hardwareprofil für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85. Kein Safe-/Recovery-Abbild. Beta-Kanal.

## 0.7.6 Beta — 2026-09-15

- Versionskennung gegenüber 0.7.5 Beta erhöht und neu gebaut, damit die App ein neues Firmwareupdate zum Download anbietet.
- Funktionen, Protokolle, Speicherformate und Geräteeinstellungen unverändert.
- Hardwareprofil für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85-Motorsteuerung. Beta-Kanal wie bisher.
- Kein Gerät geflasht; diese Ausgabe dient dem erneuten Download-/Update-Test.

## 0.7.5 Beta — 2026-09-13

- Mehr Arbeitsspeicher für den laufenden Betrieb: 174 serielle Diagnoseausgaben speichern ihre festen Texte jetzt im Flash.
- Die statische RAM-Belegung der Hardware-Firmware sinkt von 60.792 auf 51.484 Byte (74,2 % auf 62,8 %). Dadurch stehen zusätzlich 9.308 Byte, rund 9,1 KiB, als Reserve zur Verfügung.
- Diagnoseinhalte, Steuerungslogik, Netzwerkprotokolle, gespeicherte Einstellungen und bestehende Speicher-Schutzgrenzen bleiben unverändert. Der Serientest bleibt vollständig erhalten.
- Die Firmwaredatei benötigt dafür nur 224 Byte mehr Flash-Speicher und ist insgesamt 606.080 Byte groß.
- Geprüft: 171 Hosttests, 16 native Testprogramme und erfolgreiche Builds beider Firmwareprofile.
- Die Speicherersparnis ist durch den Build belegt. Diese Version wurde noch nicht auf einem Hardwaregerät installiert; der freie Laufzeit-Heap und die Fragmentierung sind damit noch nicht gemessen.

Hardware-Firmware für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85-Motorsteuerung. Beta-Version.

## 0.7.4 Beta — 2026-09-13

- Stabilere erneute WLAN-Einrichtung: unbenutzte Arbeitspuffer werden freigegeben und der verfügbare Speicher vor dem Schlüsselaustausch geprüft.
- Öffentliche Schlüsselantworten verwenden einen festen Puffer und werden kurz wiederholt, um einzelne verlorene UDP-Antworten abzufangen.
- Leaf Local ab 0.33.1 zeigt ausdrücklich gemeldeten Speichermangel verständlich an.
- Auf einem Hardwaregerät geprüft: Firmwareupdate, erneute WLAN-Einrichtung und bestätigte Raumzuordnung erfolgreich; Einstellungen und Hausplan erhalten.
- Beta-Firmware; der erfolgreiche Gerätetest ist keine Langzeitgarantie für jede Funkumgebung.

## 0.7.2 Beta — 2026-09-12

- Verbesserte OTA-Vorbereitung: nicht mehr benötigte Arbeitspuffer werden vor dem Update freigegeben.
- Bei knappem Speicher wartet die Firmware kurz auf ausstehende Netzwerkfreigaben und prüft den Speicher erneut.
- Speichergrenzen, Motorschutz und gespeicherte Einstellungen bleiben erhalten.
- Die Verbesserung wirkt bei nachfolgenden Updates, sobald 0.7.2 auf dem Gerät installiert ist. Leaf Local ab 0.32.3 kann einen ausdrücklich gemeldeten Speicher-Neustart abfangen und die Vorbereitung einmal erneut versuchen.

## 0.7.1 Beta — 2026-09-12

- Testversion für den Firmware-Updateweg in Leaf Local: Versionskennung von 0.7.0 Beta auf 0.7.1 Beta erhöht.
- Funktionen und Verhalten entsprechen 0.7.0 Beta. Bestehende Einstellungen und Speicherformat bleiben unverändert.
- Hardware-Firmware für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85-Motorsteuerung.

## 0.7.0 Beta — 2026-09-11

- Verbesserte WLAN-Einrichtung mit Leaf Local ab Version 0.31.0: Das Gerät wird nach der WLAN-Übernahme gezielt wiedergefunden und die gespeicherte Raumzuordnung bestätigt.
- mDNS startet nach erfolgreicher WLAN-Übernahme ohne pauschale Pause. Normale Raumabfragen verlängern die Lastpause nicht.
- Schutz bei hoher Abfragelast und knappem Speicher bleibt erhalten.
- Das Speicherformat für bestehende Einstellungen bleibt unverändert.

Diese Veröffentlichung enthält die Hardware-Firmware für ESP8266 ESP-12F mit 4 MiB Flash und ATtiny85-Motorsteuerung. Es handelt sich um eine Beta-Version. Die Safe-Variante ist nicht Bestandteil dieser Veröffentlichung.
