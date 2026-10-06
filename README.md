# HomeAssistant-Blueprints

Eigene Home-Assistant-Blueprints von [tojollinor](https://github.com/tojollinor).

## Enthaltene Blueprints

### Türklingel – Gong, Ansage & Kamera

Datei: `blueprints/automation/doorbell_chime_announcement.yaml`

Funktionen:

- Klingeldruck über einen `binary_sensor` als Trigger
- Ausgabesystem per Dropdown:
  - **Google / Nest Hub**
  - **Amazon Alexa (Beta)**
  - **Andere Lautsprecher (Beta)**
- Google-Geräteauswahl auf `media_player` der Integration `cast` gefiltert
- Alexa-Geräteauswahl auf `media_player` der Integration `alexa_media` gefiltert
- beliebig mehrere Zielgeräte auswählbar
- optionaler Zweiton-Gong
- optionale Sprachausgabe
- Gong- und Ansagelautstärke getrennt einstellbar
- ursprüngliche Lautstärke der Geräte wird nach der Ausgabe wiederhergestellt
- optionaler Live-Kamerastream auf Google/Nest Hubs über `camera.play_stream`
- Kamera und Kamera-Anzeigedauer frei auswählbar
- Google-Cast-Session kann anschließend automatisch beendet werden
- Wartezeiten und Lautstärken über die Blueprint-GUI einstellbar

### Import in Home Assistant

In Home Assistant:

**Einstellungen → Automationen & Szenen → Blaupausen → Blaupause importieren**

Dann diese URL einfügen:

`https://github.com/tojollinor/HomeAssistant-Blueprints/blob/main/blueprints/automation/doorbell_chime_announcement.yaml`

Direkter Blueprint-Link:

https://github.com/tojollinor/HomeAssistant-Blueprints/blob/main/blueprints/automation/doorbell_chime_announcement.yaml

### Aktualisieren

Wenn der Blueprint bereits importiert ist, in Home Assistant unter **Einstellungen → Automationen & Szenen → Blaupausen** den Blueprint öffnen und die Aktualisierung/erneuten Import über die ursprüngliche Quell-URL durchführen. Bestehende Automationen sollten danach auf den aktualisierten Blueprint zeigen; neue Eingaben wie Kamera oder getrennte Gerätefelder müssen gegebenenfalls einmal in der Automation konfiguriert werden.

## Google / Nest Hub

Für Google/Nest wird standardmäßig `Doorbell-cheap-dingdong.ogg` von Wikimedia Commons verwendet. Die Aufnahme wurde vom Urheber in die Public Domain freigegeben; die URL kann in der Blueprint-GUI durch eine eigene Gong-Datei ersetzt werden.

Der optionale Kamerastream wird mit dem offiziellen Home-Assistant-Dienst `camera.play_stream` auf die ausgewählten Google/Nest-Hubs übertragen.

## Amazon Alexa (Beta)

Die Alexa-Unterstützung verwendet **Alexa Media Player**. Diese Integration nutzt eine inoffizielle Alexa-API und kann sich durch Änderungen auf Amazon-Seite verändern.

Der Alexa-Gong verwendet den Alexa-Sound-Library-Effekt `amzn_sfx_doorbell_chime_01`.

## Andere Lautsprecher (Beta)

Für andere Media Player werden die allgemeinen Home-Assistant-Dienste `media_player.play_media`, `media_player.volume_set` und die gewählte TTS-Engine verwendet. Die tatsächliche Unterstützung hängt vom jeweiligen Media Player ab.
