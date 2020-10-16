No Hassle AV HDMI Matrix
============
The nohassle_hdmi_matrix platform allows you to control [No Hassle AV 8x8 HDMI Matrix Switch](https://www.amazon.com/HDMI-Matrix-Switcher-18GBPS-Ultra/dp/B01GKFQNG8) by polling its webui. My matrix didn't play nicely with UDP packages in the beginning so that's why I went with this method. I may rewrite this to use UDP in a later revision if I see any benefit of doing so, but for the moment I see this as the best solution as the integration can read the current status of the matrix as well as change inputs.

## Installation using HACS (Recommended)
1. Navigate to HACS and add a custom repository  
    **URL:** https://github.com/IDmedia/hass-nohassle_hdmi_matrix  
    **Category:** Integration
2. Install module as usual
3. Restart Home Assistant

## Configuration
| Key | Default | Required | Description
| --- | --- | --- | ---
| host | 127.0.0.1 | no | The ip of your hdmi matrix.
| zones |   | yes | This is the list of zones available. Valid zones are 1, 2, 3, 4, 5, 6, 7, 8. Each zone must have a name assigned to it.
| sources |   | yes | The list of sources available. Valid source numbers are 1, 2, 3, 4, 5, 6, 7, 8. Each source number corresponds to the input number on the Blackbird matrix switch. Similar to zones, each source must have a name assigned to it.

## Example
Add the following to your `configuration.yaml`:
```
media_player:
  - platform: nohassle_hdmi_matrix
    host: 192.168.1.168
    zones:
      1:
        name: Main TV Source
      2:
        name: Second TV Source
      3:
        name: Third TV Source
    sources:
      1:
        name: PC A
      2:
        name: PC B
      3:
        name: PlayStation 4
      4:
        name: Xbox 360
      5:
        name: Nintendo Switch
      6:
        name: Wii U
      7:
        name: Nintendo 64
      8:
        name: Nintendo Gamecube
```

## Usage
Change input by using `hdmi_matrix_set_zone`:
```
media_player.hdmi_matrix_set_zone
entity_id: media_player.second_tv_source
source: Kodi
```