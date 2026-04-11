# What's On TV <br> Search and Notify <br> Lovelace Card

<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/297b38ed5f117f3e127bd9932c1b2c2dc41d6b9f/What's%20On%20TV.png" alt="What's On TV" width="300">

![Version](https://img.shields.io/badge/version-1.0.0-blue?style=for-the-badge)
![HA](https://img.shields.io/badge/Home%20Assistant-2024.1+-orange?style=for-the-badge&logo=home-assistant)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![IoT Class](https://img.shields.io/badge/IoT%20Class-Cloud%20Polling-lightgrey?style=for-the-badge)
[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41bdf5.svg?style=for-the-badge)](https://hacs.xyz/docs/publish/start)
![KO-FI](https://img.shields.io/badge/HACS-Custom-teal?style=for-the-badge)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow.svg?style=for-the-badge)](https://www.buymeacoffee.com/janfajessen)
[![Patreon](https://img.shields.io/badge/Patreon-Support-red.svg?style=for-the-badge)](https://www.patreon.com/janfajessen)

[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-2026.2%2B-41bdf5.svg?style=for-the-badge)](https://www.home-assistant.io/)
[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41bdf5.svg?style=for-the-badge)](https://hacs.xyz/docs/publish/start)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow.svg?style=for-the-badge)](https://www.buymeacoffee.com/janfajessen)
[![Patreon](https://img.shields.io/badge/Patreon-Support-red.svg?style=for-the-badge)](https://www.patreon.com/janfajessen)

A Lovelace card for searching your EPG and setting up automatic notifications when a programme appears in the guide. Works alongside the [What's On TV Integration](https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card) and pairs perfectly with the [EPG Card](https://github.com/janfajessen/whatsontv-epg-card).

> **Requires:** [What's On TV Integration](https://github.com/janfajessen/whatson_tv)
>
> **Pair with:** [What's On TV — EPG Card](https://github.com/janfajessen/whatsontv-epg-card) for the full experience

<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/297b38ed5f117f3e127bd9932c1b2c2dc41d6b9f/What's%20On%20TV.png" alt="What's On TV" width="300">

<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/297b38ed5f117f3e127bd9932c1b2c2dc41d6b9f/What's%20On%20TV.png" alt="What's On TV" width="300">

<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/297b38ed5f117f3e127bd9932c1b2c2dc41d6b9f/What's%20On%20TV.png" alt="What's On TV" width="300">


---

## Features

- **Search** across all your EPG channels for any programme title (current and future only — no past results)
- Send an instant notification for any result via any HA notify service
- **Saved searches (Watches)** — add a keyword + notification service + advance window; get notified automatically when the programme appears
- Watches stored in **HA Storage** via the `whatson_tv` integration — synced across all browsers and devices
- Supports **Telegram** (text + photo via `telegram_bot.send_photo`), **mobile_app** (with image), and any other HA notify service
- Configurable **default notification service** — your preferred service appears first
- **Telegram photo support** — configure `chat_id` per bot for channel artwork delivery
- Dark and light themes, accent colour, 49 languages

---

## Installation

### Via HACS (recommended)

1. Open HACS → **Frontend** → ⋮ → **Custom repositories**
2. Add `https://github.com/YOUR_GITHUB_USER/whatsontv-notify-card` — category **Lovelace**
3. Search for **What's On TV Notify Card** and install

### Manual

1. Copy `whatsontv-notify-card.js` to `config/www/`
2. Add as a resource in **Settings → Dashboards → Resources**

---

## Usage

```yaml
type: custom:whatsontv-notify-card
title: What's On TV Notify
theme: dark
accent: "#e8872a"
default_service: "notify.telegram_mybot"
```

---

## Telegram Photo Support

To send channel artwork via Telegram (in addition to the text notification), add your chat IDs to the card config:

```yaml
type: custom:whatsontv-notify-card
default_service: "notify.telegram_mybot"
telegram_chat_ids:
  telegram_mybot: 123456789
  telegram_bot2: 987654321
  telegram_bot3: 111222333
```

Get your chat ID by messaging your bot and visiting:
`https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates`

When a chat ID is configured, the card sends the text notification first, then sends the channel logo image via `telegram_bot.send_photo`.

---

## Notification Services

The card detects all available notify services automatically:

- **HA 2024+ entities** (Telegram bots, etc.): detected from `hass.states` and called via `notify.send_message` with `entity_id` target
- **Legacy services** (mobile_app, Alexa, FireTV, etc.): detected from `hass.services.notify`
- Filtered out automatically: `send_message`, `persistent_notification`, `notify`, `reload`

Set your preferred default service in the card editor — it will always appear first in the selector.

---

## Watches — Automatic Notifications

1. Go to the **Saved** tab
2. Enter a keyword (e.g. `Champions`, `Dune`, `Formula 1`)
3. Select your notification service and how far in advance to alert
4. Click **Save search**

From that point, every time HA updates the EPG data, the card checks if any future programme matches your keyword within the configured time window and sends a notification automatically.

Watches are stored in HA Storage (via `whatson_tv` integration services) — not in the browser. They appear on any device that has this card.

---

## HA Automation Equivalent

If you prefer automations over the card watches:

```yaml
alias: "EPG — Champions League alert"
trigger:
  - platform: template
    value_template: >
      {% for state in states.sensor %}
        {% if state.attributes.channel_id is defined %}
          {% for prog in state.attributes.programacion | default([]) %}
            {% set start = prog.inicio | as_datetime %}
            {% set diff_h = ((start - now()).total_seconds() / 3600) %}
            {% if "champions" in prog.titulo | lower
               and diff_h >= 0 and diff_h <= 2 %}
              true
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}
action:
  - action: notify.send_message
    target:
      entity_id: notify.telegram_mybot
    data:
      message: "Champions League found in the guide!"
```

## Services

### `whatson_tv.add_watch`

```yaml
action: whatson_tv.add_watch
data:
  keyword: "Champions"
  notify_service: "notify.telegram_mybot"
  hours_before: 2   # optional, default 24
```

### `whatson_tv.remove_watch`

```yaml
action: whatson_tv.remove_watch
data:
  watch_id: "abc12345"
```

---

## Automations — Future Programme Notifications

You can replicate the Notify Card watch behaviour directly in HA automations:

```yaml
alias: "EPG — Notify when Champions League appears"
trigger:
  - platform: template
    value_template: >
      {% set keyword = "champions" %}
      {% set hours_before = 2 %}
      {% for state in states.sensor %}
        {% if state.attributes.channel_id is defined %}
          {% for prog in state.attributes.programacion | default([]) %}
            {% set start = prog.inicio | as_datetime %}
            {% set diff_h = ((start - now()).total_seconds() / 3600) %}
            {% if keyword in prog.titulo | lower and diff_h >= 0 and diff_h <= hours_before %}
              true
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}
condition: []
action:
  - action: notify.telegram_mybot
    data:
      message: >
        {% for state in states.sensor %}
          {% if state.attributes.channel_id is defined %}
            {% for prog in state.attributes.programacion | default([]) %}
              {% set start = prog.inicio | as_datetime %}
              {% set diff_h = ((start - now()).total_seconds() / 3600) %}
              {% if "champions" in prog.titulo | lower and diff_h >= 0 and diff_h <= 2 %}
                📺 {{ state.attributes.channel_name }} — {{ prog.titulo }}
                🕐 {{ start | as_local | as_timestamp | timestamp_custom('%H:%M') }}
              {% endif %}
            {% endfor %}
          {% endif %}
        {% endfor %}
```

> **Tip:** Use the **Notify Card** for a simpler no-code experience — it handles watches automatically without writing automations.
> 

---

## Configuration Options

| Option | Type | Default | Description |
|---|---|---|---|
| `title` | string | `What's On TV Notify` | Card title |
| `theme` | `dark` / `light` | `dark` | Visual theme |
| `accent` | string | `#e8872a` | Accent colour |
| `default_service` | string | _(first available)_ | Preferred notification service |
| `telegram_chat_ids` | object | `{}` | Map of Telegram entity name → chat ID for photo support |

---

## Requirements

- Home Assistant 2024.1+
- [What's On TV Integration](https://github.com/janfajessen/whatson_tv) — required for sensors and watch storage

---

## License

MIT — see [LICENSE](LICENSE)
