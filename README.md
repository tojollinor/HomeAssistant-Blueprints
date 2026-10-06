# HomeAssistant-Blueprints

Eigene Home-Assistant-Blueprints von [tojollinor](https://github.com/tojollinor).

## Enthaltene Blueprints

### Türklingel – Gong, Ansage & Kamera

Datei: `blueprints/automation/doorbell_chime_announcement.yaml`

Funktionen:

- Klingeldruck über einen `binary_sensor` als Trigger
- drei unabhängig nutzbare Zielgruppen:
  - **Google / Nest Hub**
  - **Amazon Alexa (Beta)**
  - **Andere Lautsprecher (Beta)**
- mehrere Zielgruppen können gleichzeitig verwendet werden
- leere Zielgruppen werden automatisch übersprungen
- Google-Geräteauswahl auf `media_player` der Integration `cast` gefiltert
- Alexa-Geräteauswahl auf `media_player` der Integration `alexa_media` gefiltert
- doppelt gewählte Geräte werden nicht doppelt angesteuert
- optionaler Zweiton-Gong
- optionale Sprachausgabe
- **Gong-Lautstärke anpassen** separat ein-/ausschaltbar
- **Ansage-Lautstärke anpassen** separat ein-/ausschaltbar
- Gong- und Ansagelautstärke getrennt einstellbar
- wenn eine Lautstärkeanpassung deaktiviert ist, bleibt die aktuelle Gerätelautstärke unverändert
- **Vorherige Lautstärke wiederherstellen** bleibt als eigener Schalter im Abschnitt Abschluss
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

Wenn der Blueprint bereits importiert ist, aktualisiere bzw. importiere ihn erneut über dieselbe Quell-URL.

Die frühere Auswahl **Ausgabesystem** existiert nicht mehr. Welche Systeme verwendet werden, ergibt sich ausschließlich daraus, welche Geräte in den drei Zielgruppen ausgewählt sind. Dadurch können Google/Nest, Alexa und andere Lautsprecher auch gleichzeitig angesprochen werden.

Nach dem Update sollte eine bestehende Automation einmal geöffnet, kontrolliert und gespeichert werden, insbesondere die Zielgeräte, die beiden neuen Lautstärke-Schalter und die Kameraoptionen.

## Google / Nest Hub

Für Google/Nest wird standardmäßig `Doorbell-cheap-dingdong.ogg` von Wikimedia Commons verwendet. Die Aufnahme wurde vom Urheber in die Public Domain freigegeben; die URL kann in der Blueprint-GUI durch eine eigene Gong-Datei ersetzt werden.

Der optionale Kamerastream wird mit dem Home-Assistant-Dienst `camera.play_stream` auf die ausgewählten Google/Nest-Hubs übertragen.

## Amazon Alexa (Beta)

Die Alexa-Unterstützung verwendet **Alexa Media Player**. Diese Integration nutzt eine inoffizielle Alexa-API und kann sich durch Änderungen auf Amazon-Seite verändern.

Der Alexa-Gong verwendet den Alexa-Sound-Library-Effekt `amzn_sfx_doorbell_chime_01`.

## Andere Lautsprecher (Beta)

Für andere Media Player werden die allgemeinen Home-Assistant-Dienste `media_player.play_media`, `media_player.volume_set` und die gewählte TTS-Engine verwendet. Die tatsächliche Unterstützung hängt vom jeweiligen Media Player ab.
