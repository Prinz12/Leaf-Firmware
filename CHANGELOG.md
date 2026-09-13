# Änderungen

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
