---

title: "Discord Overlay for Linux"
date: 2020-07-27T11:16:14+05:30
draft: false

---


As a casual gamer using linux, One of the most bugging thing when it comes to using Discord is the absence of an Overlay system while in voice call.

Fear not!
As always, there is an amazing community developed solution for it.

<https://github.com/trigg/DiscordOverlayLinux>

Here are some screenshots from the project README


![Screenshot](https://user-images.githubusercontent.com/42376598/81101265-274ea100-8f0e-11ea-83dc-1a5476bffe3d.png)

![Witch It](https://user-images.githubusercontent.com/964775/81019917-99b47800-8e5f-11ea-9514-2b3cef24ebbf.png)

![Configuration](https://user-images.githubusercontent.com/535772/82892575-a2243e00-9f47-11ea-8d42-0ec08be39441.png)


## Installation

```bash
git clone https://github.com/trigg/DiscordOverlayLinux.git
cd DiscordOverlayLinux
python -m pip install . --user
```
## Setup

After a successful installation, open up discord and jump into a voice channel.
A new icon for `Discord Overlay` would appear on your application menu, click on it and launch it.

![overlay](/assets/images/overlay.png)

On clicking it, you'll be met with a screen similar to this

![overlay_2](/assets/images/overlay_2.png)

If for some reason this didn't pop up, there would probably an icon in you taskbar, right click on it and access settings.

![overlay_4](/assets/images/overlay_4.png)

On reaching here, the discord client would probably ask whether to give the overlay app permission.
Click on YES.

I use two overlays. By default, there would be only the overlay named main.
Click on Layout to change it's properties.
Be sure to open the discord client while doing this.

![overlay_3](/assets/images/overlay_3.png)

After configuring the layout, go back and head over to the position tab and adjust it to your taste.

And viola! you got yourself a neat looking Overlay for Discord!

## References

1. <https://github.com/trigg/DiscordOverlayLinux>

2. <https://www.gamingonlinux.com/articles/you-can-now-use-the-discord-overlay-on-linux-thanks-to-a-new-community-project.16573>

3. <https://www.reddit.com/r/linux_gaming/comments/gczinw/linux_discord_overlay/>
