# Dark Arc
A dark theme for gitea with high contrast.

This theme was created by making a copy of theme-arc-green.css and making things darker for better contrast.

If you make improvements/tweaks to this theme please send a pull request, or dump your changes in an issue report.

![dark-arc-dashboard](screenshot.png)

![dark-arc-repository](screenshot2.png)

I created a feature request for a way to disable organizations because I don't use them.

I was promptly told to use css and my request was closed: https://github.com/go-gitea/gitea/issues/19391

This theme hides Organizations using CSS, you can find it at the bottom of the theme:

    #dashboard-repo-list > div > div:first-child {
      display: none !important;
    }
