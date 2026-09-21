# Leaf Basic 1.0.1 Beta Safe – VPN-Upload

Veröffentlicht am 21.09.2026.

- Firmwareuploads erlauben bis zu 15 Sekunden ohne neue empfangene Bytes und insgesamt fünf Minuten. Die Gerätewebseite wartet höchstens sechs Minuten.
- Die längeren Empfangsgrenzen gelten erst nach Installation; der erste Upload wird noch durch die bisherige Firmware begrenzt.
- Signatur-, Profil-, Größen- und Integritätsprüfungen bleiben erhalten. Einstellungen und Hausplan behalten ihr Speicherformat.
- 198 Hosttests, 29 native Regressionen und alle vier Hardware-/Safe-Builds erfolgreich. Kein echter Mobilfunk-/VPN-Upload mit dieser Ausgabe nachgestellt; Beta-Freigabe.

## Installation

Signiertes normales Update für das bisherige **Legacy-Layout 1**. Es verändert den Bootloader nicht und rüstet keinen A/B-Rückfall nach. Auf der Gerätewebseite unter **Firmwareupdate** die zum vorhandenen Profil passende Datei installieren. Keine Profilumstellung erforderlich.

**Safe:** firmware-safe.bin; Motor-/ATtiny-Ausgabe bleibt deaktiviert. Dies ist ein separater manueller Safe-Kanal. Die App bietet für Legacy-Safe-Geräte die geprüfte Migration auf A/B an, nicht dieses manuelle Legacy-Paket.

Leaf Local **0.37.1 oder neuer** erkennt 1.0.1 als kompatiblen Ausgangsstand für die vorhandene Migration. Diese führt weiterhin zuerst vollständig auf A/B 2.0.0 und anschließend per normalem A/B-Update auf 2.0.1. Vor einer Migration ist die separate Stromversorgungswarnung zu bestätigen. Der erste Upload auf einem 1.0.0-Gerät unterliegt weiterhin dessen bisherigen Zeitgrenzen.

Keine reale Platine durch diese Veröffentlichung aktualisiert. Der Legacy-Kopiervorgang ist weiterhin nicht stromausfallfest.
