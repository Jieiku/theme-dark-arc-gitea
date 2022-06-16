# Dark Arc
A dark theme for gitea with high contrast.

This theme was created by making a copy of theme-arc-green.css and making things darker for better contrast.

If you make improvements/tweaks to this theme please send a pull request, or dump your changes in an issue report.

![dark-arc-dashboard](screenshot.png)

![dark-arc-repository](screenshot2.png)

## Before install, first you need to identify 3 things:

- Location of $GITEA_CUSTOM
- Location of app.ini ([Example app.ini](https://raw.githubusercontent.com/go-gitea/gitea/main/custom/conf/app.example.ini))
- User the gitea service runs as

Here is a screenshot of my environment and where to find this info:

![gitea-config](install.png)

## Create a public/css directory under your gitea/custom path and download the theme.

Create `/public/css` below your $GITEA_CUSTOM path, MY custom path is `/var/lib/gitea/custom`, as seen in the [install screenshot](install.png).

    sudo mkdir -p /var/lib/gitea/custom/public/css
    cd /var/lib/gitea/custom/public/css
    wget https://raw.githubusercontent.com/Jieiku/theme-dark-arc-gitea/main/theme-dark-arc.css

## Make sure ownership is correct:

Set ownership of your $GITEA_CUSTOM directory and files, I set ownership to git because gitea runs as user git, as seen in the [install screenshot](install.png).

    sudo chown -R git:git /var/lib/gitea/custom

## Edit the app.ini config file to include dark-arc theme:

The app.ini file location may differ depending on environment, this matches the location of my file, as seen in the [install screenshot](install.png).

`sudo nano /var/lib/gitea/custom/conf/app.ini`

    [ui]
    DEFAULT_THEME = dark-arc
    THEMES = gitea,dark-arc

## Restart gitea service

    sudo systemctl restart gitea

    *or*

    sudo reboot

The theme may automatically be active now, but if not click your avatar in top right, click settings, click appearance tab, select the theme and click update theme button.


## Notes

### assets:

`/assets` is simply a POINTER to `$GITEA_CUSTOM/public` you should NOT actually create an assets directory.

So for me my directory structure is:

`/var/lib/gitea/custom/public/css/theme-dark-arc.css`

but if you view the page source in a web browser you will see:

`/assets/css/index.css?v=1b37ebcaa3151193e91d19ed55808a12`

They are one and the same file.

### You can set `config` and `custom-path` values when running gitea as a service:

```shell
sudo nano /etc/systemd/system/gitea.service

ExecStart=/usr/local/bin/gitea web --custom-path /var/lib/gitea/custom --config /var/lib/gitea/custom/conf/app.ini
```

### Organizations:

I created a feature request for a way to disable organizations because I don't use them.

I was promptly told to use css and my request was closed: https://github.com/go-gitea/gitea/issues/19391

This theme hides Organizations using CSS, you can find it at the bottom of the theme:

```css
#dashboard-repo-list > div > div:first-child {
  display: none !important;
}
```
