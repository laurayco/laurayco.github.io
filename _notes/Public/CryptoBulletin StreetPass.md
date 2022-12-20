---
title: CryptoBulletin "StreetPass"
feed: show
date: 2022-12-19
tags: p2p
---

# Problem

The main struggle with [[P2P Cryptographic Bulletin Board Over Constrained Networks]] is the particularly low bandwidth in the suggested QR Code / NFC Tag beacons. I would propose an additional kind of Beacon, which would require specialized hardware, and use loRa radio communications.

# Inspiration

If you're unfamiliar, [StreetPass](https://en.wikipedia.org/wiki/SpotPass_and_StreetPass#StreetPass) was a feature of the Nintendo 3DS which allowed users to passively share (gameplay) data with each other by having their consoles in close proximity to each other. I'm not as into the "nintendo console hacking" scene as I was when this was new, so I'm having a bit of trouble identifying the specific details on the communication protocols involved in StreetPass specifically.

# Proposal

Low energy device which utilizes loRA and a microSD card, with a usb-c port for charging and exposing the microSD card as bulk storage. While connected to a host, the device simply behaves as a bulk storage device. Files in the microSD card are envelopes for each bulletin board they're a member of. When not connected to a host, the device will cycle through an "outbox" directory, and broadcast any files found, and conversely it will also monitor for any transmissions it might receive, which can then be stored in an "inbox" directory. An optional config file can provide a block / allow list to discard irrelevant transmissions for which a user might not have a key. I would be curious to see if this device could fit in a comparable form factor to say, a [Tile.](https://www.tile.com/product/black-mate-premium?categorySlug=tile-mate)

Alternatively...the Nintendo 3DS is [Notoriously Easy to hack](https://3ds.hacks.guide/) these days, and is an aging console. A homebrew app running on actual 3DS hardware could provide a relatively low entry barrier method of leveraging the literal OG StreetPass technology. The 3DS also has other features, like "[SpotPass](https://en.wikipedia.org/wiki/SpotPass_and_StreetPass#SpotPass)" and WiFi connectivity, potentially opening further use-cases for the hardware.