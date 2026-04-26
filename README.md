<div align="center">

# What's On TV — <br> Search & Notify Card <br> Home Assistant Lovelace Card

<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card---Home-Assistant/blob/b0bfdedda91bcb91d8f40e5f2a4862313d183947/brand/logo%402x.png" alt="What's On TV" width="450">

![Version](https://img.shields.io/badge/version-3.26.3-blue?style=for-the-badge)
![HA](https://img.shields.io/badge/Home%20Assistant-2024.1+-orange?style=for-the-badge&logo=home-assistant)
![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)
![Languages](https://img.shields.io/badge/Languages-49-brightgreen?style=for-the-badge)
![HACS](https://img.shields.io/badge/HACS-Compatible-41BDF5?style=for-the-badge&logo=homeassistantcommunitystore&logoColor=white)<br>
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow?style=for-the-badge&logo=buymeacoffee)
](https://www.buymeacoffee.com/janfajessen) 
[![Patreon](https://img.shields.io/badge/Patreon-Support-red?style=for-the-badge&logo=patreon)](https://www.patreon.com/janfajessen)
<!--[![Ko-Fi](https://img.shields.io/badge/Ko--Fi-Support-teal?style=for-the-badge&logo=ko-fi)](https://ko-fi.com/janfajessen)
[![GitHub Sponsors](https://img.shields.io/badge/GitHub%20Sponsors-Support-pink?style=for-the-badge&logo=githubsponsors)](https://github.com/sponsors/janfajessen)
[![PayPal](https://img.shields.io/badge/PayPal-Donate-blue?style=for-the-badge&logo=paypal)](https://paypal.me/janfajessen)
-->
</div>

## 🔍 Never miss what you want to watch

The keyword watch system lets you search across all configured EPG sources simultaneously. Some ideas:

- ⚽ **Lost the match live and want to see?** Set a watch for `"LaLiga"`,`"Champions"`,`"Libertadores"`, or `"Premier League"` — you'll get notified before the replay airs, without any spoilers in the notification
- 🎬 **Looking for a classic you can never find?** Try `Funny games`, `"The Apartment"`,`Rope`, `"Casablanca"`, `"Blade Runner"`, `"The Godfather"` or `"2001"` — old films rotate on cable channels more often than you'd think
- 📺 **Never miss your favourite show:** Set `"Jeopardy"`, `"MasterChef"`, `"Survivor"` or `"Who Wants to Be a Millionaire"` and get alerted before it starts
- 🎤 **Music fan?** Search `Eminem`,`"Glastonbury"`, `"Eurovision"` or your favourite artist's name
- 🌍 **Documentary hunter?** Try `"Planet Earth"`, `"Cosmos"` or `"Ken Burns"` — they rerun constantly on documentary channels
- 🏎️ **Sports in general:** `ATP1000`,`"Formula 1"`, `"La vuelta"`, `"NBA"` — works across all your configured countries simultaneously
- 🦈 The ultimate channel surfing trap: Set `"Jaws"` — it's been airing every summer weekend since 1975 and somehow always catches you off guard
- 🎄 Tired of missing the annual TV tradition? Set a watch for `"Home Alone"` — because it airs every Christmas on at least 12 channels simultaneously, and somehow you always miss it.

> The **Word** match mode finds `"Friends"` but not `"Girlfriends"` or `"Unfriendly"`. The **Contains** mode is broader. Use **Exact** only for very specific titles.

A worldwide EPG (Electronic Programme Guide) integration for Home Assistant. Turns any XMLTV-compatible TV guide source into HA sensors — one sensor per channel, updated automatically.

> **Highly recommended companions:**
> - 📺 [What's On TV — EPG Card](https://github.com/janfajessen/What-s-On-TV---EPG-TV-Guide---Home-Assistant) — visual TV guide card for Lovelace


<!-- > **🔒 This card is available exclusively to supporters.** > After contributing via Ko-Fi, Buy Me a Coffee or Patreon, open an issue or contact via GitHub with your username and the platform used — access to the private repository will be granted manually -->


A Lovelace card for searching your EPG and setting up automatic notifications when a programme appears in the guide. Works alongside the [What's On TV Integration](https://github.com/janfajessen/What-s-On-TV---EPG-TV-Guide---Home-Assistant) and pairs perfectly with the [EPG Card](https://github.com/janfajessen/What-s-On-TV-EPG-TV-Guide-Card).

> **Requires:** [What's On TV Integration](https://github.com/janfajessen/What-s-On-TV---EPG-TV-Guide---Home-Assistant)
>
> **Pair with:** [What's On TV — EPG Card](https://github.com/janfajessen/What-s-On-TV-EPG-TV-Guide-Card) for the full experience
> 
<div align="center">
<img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/939e5c8081f6e22ade78361b7499cdf47b38e6f2/whatsontv_search_and_notify_card.png" alt="What's On TV Search" width="35%">  <img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/939e5c8081f6e22ade78361b7499cdf47b38e6f2/whatsontv_search_and_notify_card_saved_watches.png" alt="What's On TV Saved Watches" width="35%">
</div>

---

## Features

- **Search** across all your EPG channels for any programme title (current and future — no past results)
- Send an instant notification for any result via any HA notify service
- **Saved searches (Watches)** — add a keyword + notification service + advance window; get notified automatically when the programme appears
- Watches stored in **HA Storage** via the `whatson_tv` integration — synced across all browsers and devices
- Supports **Telegram** (text + photo via `telegram_bot.send_photo` with `entity_id`), **mobile_app** (with image), and any other HA notify service
- Configurable **default notification service** — your preferred service appears first
- Dark and light themes, accent colour, 49 languages

---

## Installation

This card is distributed as a private repository. Once you have been granted access:

### Via HACS

1. Open HACS → **Frontend** → ⋮ → **Custom repositories**
2. Add the private repository URL — category **Dashboard**
3. Search for **What's On TV Search & Notify Card** and install

### Manual

1. Copy `whatsontv-notify-card.js` to `config/www/`
2. In Home Assistant go to **Settings → Dashboards** → ⋮ → **Resources** → **+ Add Resource**
3. Set URL to `/local/whatsontv-notify-card.js` and type to **JavaScript module**

> **Tip:** Add `?v=1.0.0` to the URL to force browsers to reload after updates — e.g. `/local/whatsontv-notify-card.js?v=3.24.1`

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

## Telegram Support

The card sends channel artwork via `telegram_bot.send_photo` using `entity_id` — no chat ID configuration needed. Simply select your Telegram notify entity as the default service and photos will be sent automatically when available.

```yaml
type: custom:whatsontv-notify-card
default_service: "notify.telegram_myname"
```

---

## Notification Services

The card detects all available notify services automatically:

- **HA 2024+ entities** (Telegram bots, etc.) — called via `notify.send_message` with `entity_id` target
- **Legacy services** (mobile_app, etc.) — called directly
- Filtered out automatically: `send_message`, `persistent_notification`, `notify`, `reload`

---

## Watches — Automatic Notifications

1. Go to the **Saved** tab
2. Enter a keyword (e.g. `Champions`, `Dune`, `Formula 1`)
3. Select match mode: **Word** (recommended), **Contains** or **Exact**
4. Select your notification service and how far in advance to alert (30 min to 48 h)
5. Click **Save search**

Watches are stored in HA Storage via the `whatson_tv` integration — not in the browser. They appear on any device and work even when the card is not open.

---

## HA Automation Equivalent

```yaml
alias: "EPG — Champions League alert"
trigger:
  - platform: time_pattern
    minutes: "/5"
condition:
  - condition: template
    value_template: >
      {% set keyword = "champions" %}
      {% set hours_before = 2 %}
      {% set found = namespace(value=false) %}
      {% for state in states.sensor %}
        {% if state.attributes.channel_id is defined %}
          {% for prog in state.attributes.schedule | default([]) %}
            {% set start = prog.start | as_datetime %}
            {% set diff_h = ((start - now()).total_seconds() / 3600) %}
            {% if keyword in prog.title | lower and diff_h >= 0 and diff_h <= hours_before %}
              {% set found.value = true %}
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}
      {{ found.value }}
action:
  - action: notify.send_message
    target:
      entity_id: notify.telegram_mybot
    data:
      message: "📺 Champions League found in the guide!"
```

---

## Configuration Options

| Option | Type | Default | Description |
|---|---|---|---|
| `title` | string | `What's On TV Notify` | Card title |
| `theme` | `dark` / `light` | `dark` | Visual theme |
| `accent` | string | `#e8872a` | Accent colour |
| `default_service` | string | _(first available)_ | Preferred notification service |

---

## Requirements
<div align="center">
<a href="https://www.home-assistant.io/"><img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/b3645cf0af684bdde893675cb4c80660424873ba/home_assistant_logo.png" alt="Home Assistant" width="60">
</div>

<a href="https://www.home-assistant.io/">Home Assistant 2024.1+</a>
<div align="center">
<a href="https://github.com/janfajessen/What-s-On-TV---EPG-TV-Guide"><img src="https://github.com/janfajessen/What-s-On-TV-Search-and-Notify-Card/blob/297b38ed5f117f3e127bd9932c1b2c2dc41d6b9f/What's%20On%20TV.png" alt="What's On TV" width="100">
</div>
<a href="https://github.com/janfajessen/What-s-On-TV---EPG-TV-Guide">What's On TV Integration></a>— required for sensors and watch storage

---


*If this integration is useful to you, consider giving it a ⭐ on GitHub.*
Or consider supporting development!

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-Donate-yellow?style=for-the-badge&logo=buymeacoffee)
](https://www.buymeacoffee.com/janfajessen) 
[![Patreon](https://img.shields.io/badge/Patreon-Support-red?style=for-the-badge&logo=patreon)](https://www.patreon.com/janfajessen)
</div>


## License

Proprietary — maybe access granted to supporters only. Redistribution or public sharing of this code is not permitted.

© [@janfajessen](https://github.com/janfajessen)
