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
- **Sprache an TTS übergeben** separat ein-/ausschaltbar
- wenn deaktiviert, wird kein `language`-Parameter an die TTS-Engine gesendet
- **Gong-Lautstärke anpassen** separat ein-/ausschaltbar
- **Ansage-Lautstärke anpassen** separat ein-/ausschaltbar
- **Wartezeit nach der Ansage** frei von 0 bis 60 Sekunden einstellbar; Standard 3 Sekunden
- Gong- und Ansagelautstärke getrennt einstellbar
- wenn eine Lautstärkeanpassung deaktiviert ist, bleibt die aktuelle Gerätelautstärke unverändert
- **Vorherige Lautstärke wiederherstellen** bleibt als eigener Schalter im Abschnitt Abschluss
- optionale Kameraausgabe auf Google/Nest Hubs mit zwei Kamera-Methoden:
  - **Home-Assistant-Kamera** über `camera.play_stream`
  - **Frigate-Kamera (Advanced Camera Card)** über `cast.show_lovelace_view`
- bei der Frigate-Methode werden Dashboard-Pfad und View-Pfad der vorbereiteten Advanced-Camera-Card-Ansicht angegeben
- Kamera-Anzeigedauer gilt gemeinsam für beide Kamera-Methoden
- ohne Kamera geht es nach der TTS-Wartezeit direkt zum Abschluss
- mit Kamera startet danach die gewählte Kamera-Methode und läuft für die eingestellte Kamera-Anzeigedauer
- Google-Cast-Wiedergabe kann anschließend per `media_player.media_stop` automatisch beendet werden
- relevante Service-Aufrufe sind fehlertolerant: ein Fehler bei Gong, TTS, Kamera, Lautstärke oder Cast-Cleanup soll den restlichen Ablauf nicht abbrechen
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

Nach dem Update sollte eine bestehende Automation einmal geöffnet, kontrolliert und gespeichert werden, insbesondere die Zielgeräte, die Lautstärke-Schalter, **Sprache an TTS übergeben**, **Wartezeit nach der Ansage**, **Kamera-Methode** und die dazugehörigen Kameraoptionen.

## Google / Nest Hub

Für Google/Nest wird standardmäßig `Doorbell-cheap-dingdong.ogg` von Wikimedia Commons verwendet. Die Aufnahme wurde vom Urheber in die Public Domain freigegeben; die URL kann in der Blueprint-GUI durch eine eigene Gong-Datei ersetzt werden.

Für die Kameraausgabe stehen zwei Methoden zur Verfügung:

- **Home-Assistant-Kamera:** Eine normale `camera.*`-Entity wird mit `camera.play_stream` auf die ausgewählten Google/Nest-Hubs übertragen.
- **Frigate-Kamera (Advanced Camera Card):** Statt die Frigate-`camera.*`-Entity direkt zu streamen, wird mit `cast.show_lovelace_view` eine vorbereitete Dashboard-View mit der Advanced Camera Card auf den Hub gecastet. Das ist besonders für Frigate/go2rtc-Setups sinnvoll, wenn die Card-Liveansicht bereits funktioniert, der direkte RTSP-Restream für Home Assistant aber absichtlich nicht erreichbar ist.

Für die Frigate-Methode werden in der Blueprint **Dashboard-Pfad** und **View-Pfad** eingetragen.


### Frigate / Advanced Camera Card einrichten

Für die Kamera-Methode **Frigate-Kamera (Advanced Camera Card)** muss vorab eine eigene Dashboard-View angelegt werden, die nur bzw. hauptsächlich die gewünschte Advanced Camera Card enthält.

Beispiel für die in diesem Projekt getestete Kamera `cam_backdoor`:

```yaml
type: custom:advanced-camera-card
cameras:
  - camera_entity: camera.cam_backdoor
    live_provider: go2rtc
    go2rtc:
      modes:
        - mse
    frigate:
      camera_name: cam_backdoor
live:
  preload: true
  controls:
    builtin: false
view:
  default: live
```

Die bestehende normale Kamera-Karte darf natürlich umfangreicher bleiben. Für den Cast ist eine möglichst schlanke View meist übersichtlicher.

Beispiel:
- Dashboard-URL: `/camera-cast/`
- View-URL: `/camera-cast/backdoor`
- Blueprint **Dashboard-Pfad**: `camera-cast`
- Blueprint **View-Pfad**: `backdoor`

Die Blueprint castet dann diese View auf jeden ausgewählten Google/Nest Hub. Die Advanced Camera Card übernimmt innerhalb der View den bereits funktionierenden Frigate/go2rtc-Livepfad.

## Amazon Alexa (Beta)

Die Alexa-Unterstützung verwendet **Alexa Media Player**. Diese Integration nutzt eine inoffizielle Alexa-API und kann sich durch Änderungen auf Amazon-Seite verändern.

Der Alexa-Gong verwendet den Alexa-Sound-Library-Effekt `amzn_sfx_doorbell_chime_01`.

## Andere Lautsprecher (Beta)

Für andere Media Player werden die allgemeinen Home-Assistant-Dienste `media_player.play_media`, `media_player.volume_set` und die gewählte TTS-Engine verwendet. Die tatsächliche Unterstützung hängt vom jeweiligen Media Player ab.
