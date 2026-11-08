# LilyPichu Revived

## Wallpaper

Paste this into your theme file, under the `@import` line, and swap in your own picture. Animated GIF and WebP files play as the wallpaper, and the dim and blur still apply to them:

```css
:root {
  --lp-wallpaper: url("https://i.imgur.com/example.png");
  --lp-wallpaper-x: 50%;
  --lp-wallpaper-y: 35%;
  --lp-wallpaper-zoom: 1;
  --lp-wallpaper-blur: 0px;
  --lp-wallpaper-dim: 0.5;
}
```

| | |
|---|---|
| `--lp-wallpaper-x`, `--lp-wallpaper-y` | The point of the picture that stays put. `50% 35%` pins the spot halfway across and a third of the way down the picture to the same spot in the window, so put it on the face you want to keep in view. Percentages keep working when you resize the window. Pixel values don't, and a big one can drag the picture off its edge and leave a blank strip. |
| `--lp-wallpaper-zoom` | `1` fills the window. `1.5` is half again closer, and it grows around the x and y point. A tall picture on a wide window is already exactly as wide as the window, so x has nothing to move until you zoom in a little. |
| `--lp-wallpaper-blur` | Softens the picture and nothing else; the panels on top stay sharp. `0px` is off, and 1px to 3px takes the edge off a small or busy picture. |
| `--lp-wallpaper-dim` | Black laid over the picture, from `0` to `1`. Bright pictures want 0.5 or more so the text on the panels stays easy to read. `--lp-wallpaper-light` does the same in white. |
| `--lp-wallpaper-fit` | `cover`, the default, fills the window. `contain` shows the whole picture with bars around it, `100% 100%` stretches it to the window, and `auto` keeps the picture's own size. |
| `--lp-wallpaper-repeat` | `no-repeat`, the default, shows the picture once. `repeat` tiles it across the window, which suits a small pattern with `--lp-wallpaper-fit: auto`. |

### Finding the numbers by eye

Download [`tools/wallpaper-placer.html`](tools/wallpaper-placer.html) and open it in your browser. Drop your picture in, drag it until the faces sit where you want them around the panels, scroll to zoom, and press Copy. It gives you the block above with your numbers in it.

### A picture from your own computer

On Equicord you can skip uploading. Put the picture in a `wallpapers` folder inside your themes folder (Settings, Themes, Open Themes Folder) and point at it with three slashes:

```css
--lp-wallpaper: url("equicord:///themes/wallpapers/my-picture.jpg");
```

Other clients block files from your computer, so use a link there, from imgur or anywhere else that serves the image directly.
