# Leaf Basic 2.0.1 Beta Safe – VPN-Upload

Veröffentlicht am 21.09.2026.

- Firmwareuploads erlauben bis zu 15 Sekunden ohne neue empfangene Bytes und insgesamt fünf Minuten. Die Gerätewebseite wartet höchstens sechs Minuten.
- Die längeren Empfangsgrenzen gelten erst nach Installation; der erste Upload wird noch durch die bisherige Firmware begrenzt.
- Signatur-, Profil-, Größen- und Integritätsprüfungen bleiben erhalten. Einstellungen und Hausplan behalten ihr Speicherformat.
- 198 Hosttests, 29 native Regressionen und alle vier Hardware-/Safe-Builds erfolgreich. Kein echter Mobilfunk-/VPN-Upload mit dieser Ausgabe nachgestellt; Beta-Freigabe.

## Update mit der App

Zuerst Leaf Local auf **0.37.1 oder neuer** aktualisieren. Unter Firmware-Updates **Beta-Versionen anzeigen**, **VERSION PRÜFEN**, **FIRMWARE HERUNTERLADEN** und **GERÄTE PRÜFEN** ausführen. Bereits vollständig umgestellte A/B-Geräte erhalten dieses normale Update; der Bootloader wird dabei nicht geändert.

Bestehende 1.0.0-/1.0.1-Geräte müssen zuerst die vollständige Migration auf **2.0.0** abschließen. Die App verwendet dafür weiterhin das separate Paket **ab-safe-v2.0.0-beta**. Danach erneut prüfen und 2.0.1 als normales A/B-Update installieren. Die Migrationsbrücke akzeptiert ausschließlich ihre fest gebundene 2.0.0-Datei; diese 2.0.1-Datei darf dort nicht verwendet werden.

Vor der einmaligen Bootloaderänderung muss die Stromversorgungswarnung ausdrücklich bestätigt werden. Während der gesamten Migration darf die Spannungsversorgung auf keinen Fall unterbrochen werden. Die Migration bleibt für eigene Testgeräte mit serieller Reparaturmöglichkeit bestimmt.

Bei unbestätigtem Upload erlaubt **FEHLVERSUCH PRÜFEN** eine lesende Prüfung. Erst ein nachweislich unveränderter, wiederhergestellter Ausgangszustand und eine neue ausdrückliche Bestätigung erlauben einen weiteren Versuch. Es gibt keine automatische Wiederholung.

## Profil und Grenzen

Safe-Profil ohne Motor-/ATtiny-Ausgabe. Ausschließlich firmware-safe.bin für bereits umgestellte Safe-Geräte verwenden.

Signierte Updates schreiben weiterhin nur den inaktiven Anwendungsslot. Bootdatenformat, Startbestätigung und Rückfalllogik bleiben unverändert. Dieses Release wurde automatisiert geprüft; es wurde kein Gerät damit geflasht. Der zuvor zurückgestellte präzise Stromausfalltest innerhalb eines Flash-Schreibimpulses bleibt offen.
