# dennisfury.github.io
This is for personal use, I have a home assistant automation that will randomly play one of these mp3 files when my fridge is opened.  If you want the YAML example, here you go---

```
alias: Motivation Fridge Opened
description: Motivation Fridge Opened
triggers:
  - type: opened
    device_id: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
    entity_id: yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
    domain: binary_sensor
    trigger: device
conditions:
  - condition: template
    value_template: >
      {{ now() - state_attr('automation.motivation_fridge_opened', 'last_triggered')
      > timedelta(minutes=5) or
         state_attr('automation.motivation_fridge_opened', 'last_triggered') is none }}
actions:
  - variables:
      mp3_urls:
        - https://dennisfury.github.io/david_goggins-you_are_a_b.mp3
        - https://dennisfury.github.io/david_goggins-like_you_love_it.mp3
        - https://dennisfury.github.io/michael_scott-five_cameras.mp3
        - https://dennisfury.github.io/michael_scott-buffet.mp3
        - https://dennisfury.github.io/michael_scott-geez_hes_fat.mp3
        - https://dennisfury.github.io/michael_scott-swim_past_buoys.mp3
        - https://dennisfury.github.io/michael_scott-ice_cream_soup.mp3
        - https://dennisfury.github.io/michael_scott-ate_all_letters.mp3
        - https://dennisfury.github.io/will_ferrell-get_fat_out_of_ears.mp3
      random_url: "{{ mp3_urls | random }}"
  - data:
      message: <audio src='{{ random_url }}'/>
      target: media_player.kitchen_show
      data:
        type: tts
    action: notify.alexa_media
mode: single
```
