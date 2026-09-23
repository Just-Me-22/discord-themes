# Circular Status

Discord marks status by biting a notch out of the corner of an avatar and putting a dot in the hole. This puts the corner back and draws the status as a ring around the whole picture instead.

**What it does**
- Ring instead of the corner dot, everywhere an avatar shows up: member list, DM list, channel header, profile popouts, your own user panel
- Sizes itself. It reads the picture's real size out of the markup, so it hugs a 16px avatar in a header and a 120px one in a popout
- Five colours, one per status, set to any hex you like. Left alone they follow Discord's own, so it matches whatever theme you already run
- One number sets the thickness, and each avatar size carries its own multiplier so a big popout avatar does not end up with a slab around it
- Typing moves onto the picture. It darkens, the dots sit in the middle of it, and it clears on its own when they stop
- Speaking in voice makes the ring breathe in the speaking colour, and it settles back when they stop
- Group DMs stop being cropped, so both faces show whole with a ring each. They slide apart on hover, and the ring shows whether the group is open, unread, muted or in a call. Hover one with someone online and the ring traces round in their status colour
- Voice channel avatars in the sidebar get a ring and a glow of their own
- Avatar decorations keep working and sit in front, uncut
- Edits apply live, no reload needed

**Import**
```css
@import url("https://raw.githubusercontent.com/Just-Me-22/discord-themes/main/circular-status.css");
```

**Raw**
```
https://raw.githubusercontent.com/Just-Me-22/discord-themes/main/circular-status.css
```

**Knobs**
`--cs-width` is the thickness. `--cs-online`, `--cs-idle`, `--cs-dnd`, `--cs-offline` and `--cs-streaming` are the colours. `--cs-typing-scrim` and `--cs-typing-dim` control the darkening while someone types, `--cs-typing-dots-lift` where the dots sit. `--cs-speaking`, `--cs-breath`, `--cs-breath-scale` and `--cs-breath-dim` are the speaking ring, `--cs-ring` and `--cs-ring-w` the resting ring on voice avatars, `--cs-group` and `--cs-group-w` the rings on group DM faces, and `--cs-group-style` picks `faces`, `split`, `capsule` or `segments`. The README lists the rest.

CSS only. No plugin.