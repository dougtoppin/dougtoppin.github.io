---
title: "Another impressive experience with ChatGPT"
date: 2025-07-25
---

I run HomeAssistant OS on a Raspberry Pi 4b initially with the micro-sd card. I wanted to switch that to an nvme/ssd instead for more storage and reliability.

I had several conversations with ChatGPT on how to do it, and the suggestions were very helpful.

After that was working, the temperature of the Pi was a little higher than I wanted it to be, so I added a fan because I had several two-wire fans available. The ssd is mounted under the Pi with an nvme HAT using the underside of 3 of the header pins for power. Because of that, I did not have a case that the Pi would fit, so it just sits on the top of my desk.

I found a fan mount on MakerWorld, I have a BambuLab X1C/AMS, which was exactly what I needed. I printed it in PLA, but the posts were a little tight, and 2 of them shattered while trying to screw them in. I switched to PET-G, and it printed perfectly. The fan works now, with an almost 50-degree drop in temperature.

The neat ChatGPT aspect of this is I wanted to have a log file in HomeAssistant for my configuration change notes. I could not find any specific add-ons for that, and neither could ChatGPT. It suggested that I just keep a /config/notes.md file in HA and asked if I wanted a starting template for it, to which I said yes. I started up Studio Code Server and created the file with the suggested content.

What was interesting is that the initial content was notes from the conversations that I had with ChatGPT on adding the ssd and fan. It turned out to be exactly what I wanted.

This is another example of the value of AI and, in particular, the history of conversations with it.

I continue to be impressed with ChatGPT and GitHub Copilot and am excited about what can be done with AI and am excited about the continued improvements in both.