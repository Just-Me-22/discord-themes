Discord marks someone's status by biting a notch out of the corner of their avatar and
putting a coloured dot in the hole. This puts the corner back and draws the status as a ring
around the whole picture instead. It works everywhere an avatar appears, and it reads the
picture's real size out of the markup, so the ring hugs a 16px avatar in a channel header
and a 120px one in a profile popout without being told about either.

Typing moves onto the picture too. Instead of the dot stretching into a little pill in the
corner, the picture darkens and the dots sit in the middle of it, and everything goes back to
normal on its own when the person stops.

Group DMs get rings too. Discord draws those as two faces sharing one circle, and it crops
both of them to fit. That crop comes off, so each face is a whole circle with a ring, and
the back one keeps its notch where the front sits over it. There is no status on a group
entry, so that ring is a flat colour rather than green or yellow.

The two faces slide apart when you hover the row. The ring also shows the row's state: it
gets thicker on the one you have open, lighter when there are unread messages, dashed and
grey when the group is muted, and it pulses in the speaking colour while a call is going.
A group with its own picture gets a double ring instead. `--cs-group-style` swaps the two
rings for other shapes: `split` keeps only the outer half of each ring, `capsule` draws one
pill around both faces, and `segments` draws a dashed circle around both.

Speaking shows as a breathing ring. When someone talks, their ring turns the speaking
colour and slowly swells and fades, and it goes back to the status ring when they stop.
Voice channel avatars in the sidebar get a resting ring of their own so they are not bare
the rest of the time, with a small gap and a glow, and it breathes the same way when they
talk.

Avatar decorations keep working. They carry the same notch as the picture, so they get the
same treatment and sit in front, uncut.

CSS only. No plugin, nothing to install besides the one line below.

## Screenshots

**User panel**

![User panel](screenshots/user-panel.png)

**Direct message list**

![Direct messages](screenshots/direct-messages.png)

**Channel header**

![Channel header](screenshots/header.png)

**Profile popout**

![Profile popout](screenshots/popout.png)

**Member list**

![Member list](screenshots/member-list.png)

## Install

Paste this into **QuickCSS**.

```css
@import url("https://raw.githubusercontent.com/Just-Me-22/discord-themes/main/circular-status.css");
```

## Values you may want to change

| knob | does |
|---|---|
| `--cs-width` | how thick the ring is |
| `--cs-radius` | the shape. `50%` is round, `22%` is a rounded square, `0` is a sharp square |
| `--cs-glow` | how far the glow spreads, as a share of the avatar's width. `0` switches it off |
| `--cs-glow-core` | how much of the glow is solid before it starts to fade, same share. Raise it on a light background |
| `--cs-online` | the green |
| `--cs-idle` | the yellow |
| `--cs-dnd` | the red |
| `--cs-offline` | the grey |
| `--cs-streaming` | the purple |
| `--cs-typing-scrim` | the colour the picture darkens to while someone types |
| `--cs-typing-dim` | how dark that gets |
| `--cs-typing-dots-lift` | how far above centre the typing dots sit |
| `--cs-speaking` | the ring colour while someone is talking |
| `--cs-breath` | how long one breath takes |
| `--cs-breath-scale` | how far the ring swells at the top of a breath |
| `--cs-breath-dim` | how faint it gets at the top of a breath |
| `--cs-ring` | the resting ring on voice channel avatars |
| `--cs-ring-w` | how thick that resting ring is |
| `--cs-ring-gap` | the gap between a voice avatar and its ring |
| `--cs-speak-w` | how thick the voice ring is while someone talks |
| `--cs-group` | the ring on each face in a group DM avatar |
| `--cs-group-w` | how thick that one is |
| `--cs-group-style` | `faces`, `split`, `capsule` or `segments` |
| `--cs-group-front` | the front face's ring |
| `--cs-group-back` | the back face's ring |
| `--cs-group-blend` | `1` fades the two colours into each other |
| `--cs-group-radius` | the shape of the group faces, same as `--cs-radius` |
| `--cs-group-spread` | how far apart the faces sit |
| `--cs-group-spread-hover` | how far apart they slide on hover |
| `--cs-group-back-size` | how big the back face is next to the front one |
| `--cs-group-gap` | the gap the front face cuts out of the back one |
| `--cs-group-pad` | the gap between the faces and a `capsule` or `segments` ring |
| `--cs-group-segments` | how many dashes `segments` has |
| `--cs-group-icon-w` | how thick the double ring on a group picture is |
| `--cs-group-selected` | the ring on the group you have open |
| `--cs-group-selected-w` | how thick that is |
| `--cs-group-unread` | the ring when there are unread messages |
| `--cs-group-muted` | the ring on a muted group |
| `--cs-group-call` | the ring during a call |
| `--cs-group-call-w` | how thick that is |

The five colours default to Discord's own, so leaving them alone follows your theme. Set
`--cs-typing-dim` to `0` if you want the dots without the picture darkening.

The thickness is a share of the picture rather than a pixel value, and each avatar size
carries its own multiplier on top, so one number holds from a 16px avatar to a 120px one
without the big ones turning into slabs.

The ring only breathes while someone is actually speaking, so nothing runs when a channel
is quiet. In the DM list and user panel it moves with `transform` and `opacity`. In the voice
list it swells by redrawing a small gradient instead, because a scaled ring there drifts
half a pixel off the picture; that costs one repaint of a 36px circle per frame, and only
for whoever is talking.

Changes apply live. You can edit a knob with Discord open and watch the ring change, no
reload needed.

## About the glow

The glow is a `box-shadow` on the avatar's wrapper, not a filter on the ring. It has to be.
A CSS filter on an SVG element is clipped to that element's bounding box plus ten percent,
and inside that ceiling there is no room for a falloff you can see. Widening the blur only
makes it fainter, because a blur spreads a fixed amount of colour rather than adding any.
Adding colour at that width saturates the pixels beside the ring instead, so the ring just
looks thicker. A box-shadow on an HTML element has no filter region, so it can be as soft
as it likes.

The glow only draws in the user panel, the DM list, profile popouts and the voice list in
the server sidebar. Those are the places with a handful of avatars, and the member list,
where there can be hundreds, stays free of it.

`--cs-glow` is a share of the avatar's width, measured with `cqw` off the wrapper, so one
number holds its proportions from a 20px DM row up to a 120px profile. At the default `0.1`
that is 3.2px in the member list and 12px on a profile. The wrapper gets
`container-type: inline-size` purely to give `cqw` something to measure.

Keep it near the ring's own thickness. A halo much wider than the ring has no bright core
to read against and goes diffuse, which is how the filter version failed.

`--cs-glow-core` is the part that stays solid before the fade begins. Widening `--cs-glow`
on its own never makes the glow stronger, only larger and fainter, because a blur spreads a
fixed amount of colour rather than adding any. The core is the knob that makes it brighter.
Raise it on a light background, where the same colour reads far softer than it does on
Discord's dark one, and keep it under about `0.06` or it stops looking like light and starts
looking like a second ring.

A box-shadow draws into a layer that already exists, so unlike the drop-shadow it replaced,
it does not promote every avatar on screen to its own compositing layer. `--cs-glow: 0`
leaves an invisible shadow still being drawn, so to get the cost back, switch it off:

```css
:is(section[class*="panels_"], nav[class*="privateChannels_"], .user-profile-popout) [class*="wrapper_"]::before {
  display: none;
}
```
