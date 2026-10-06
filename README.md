# HomeAssistant-Blueprints

Eigene Home-Assistant-Blueprints von [tojollinor](https://github.com/tojollinor).

## Enthaltene Blueprints

### Türklingel – Gong & Ansage auf Google/Nest oder Alexa

Datei: `blueprints/automation/doorbell_chime_announcement.yaml`

Funktionen:

- Klingeldruck über einen `binary_sensor` als Trigger
- mehrere Lautsprecher/Displays auswählbar
- Ausgabesystem als Dropdown:
  - **Google / Nest Hub (getestet)**
  - **Amazon Alexa (Beta, ungetestet)**
- optionaler Zweiton-Gong
- optionale Sprachausgabe
- Gong- und Ansagelautstärke getrennt einstellbar
- Wartezeiten über die Blueprint-GUI einstellbar
- ursprüngliche Lautstärke der Geräte wird nach der Ausgabe wiederhergestellt
- Google-Cast-Session kann anschließend automatisch beendet werden

### Import in Home Assistant

In Home Assistant:

**Einstellungen → Automationen & Szenen → Blaupausen → Blaupause importieren**

Dann diese URL einfügen:

`https://github.com/tojollinor/HomeAssistant-Blueprints/blob/main/blueprints/automation/doorbell_chime_announcement.yaml`

Direkter Blueprint-Link:

https://github.com/tojollinor/HomeAssistant-Blueprints/blob/main/blueprints/automation/doorbell_chime_announcement.yaml

## Hinweise zu Alexa

Die Alexa-Unterstützung verwendet **Alexa Media Player** und ist ausdrücklich als **Beta / ungetestet** markiert. Alexa Media Player verwendet eine inoffizielle Alexa-API und kann sich durch Änderungen auf Amazon-Seite verändern.

Der Alexa-Gong verwendet den Alexa-Sound-Library-Effekt `amzn_sfx_doorbell_chime_01`. Für Google/Nest wird standardmäßig `Doorbell-cheap-dingdong.ogg` von Wikimedia Commons verwendet. Die Aufnahme wurde vom Urheber in die Public Domain freigegeben; die URL kann in der Blueprint-GUI durch eine eigene Gong-Datei ersetzt werden.
