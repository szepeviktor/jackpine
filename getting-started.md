# Getting Started

## Installation

To create a new theme using Jackpine, clone or unzip the repository to a new folder:

*[(Download a release package)](https://github.com/45-North-Ventures-LLC/jackpine/releases)*

**or**

```
git clone https://github.com/45-North-Ventures-LLC/jackpine.git MyNewProject
```

Then enter your new directory and install the dependencies by running `composer install` and ```yarn install```.

Next, configure the wpack.io server by running `yarn run bootstrap` and following the prompts.

***Optional***  
Whitelabel your Jackpine project by running `yarn run plop` and answering the questions. This will update the theme name and your contact information in the style.css file and several template files. In a client project, you may also want to replace `screenshot.png` in your theme's directory with your own image.

Finally, head over to **Appearance > Themes** in your WordPress installation and activate your theme.

## Development Server

[(Read the wpack.io docs on the development server here)](https://wpack.io/guides/start-development-server/)

Wpack.io includes a development server with live reloading capability via Browsersync. Once you've followed the installation instructions above, you can start the development server at any time by running `yarn run start` in the root directory of your theme.

While wpack.io works very well right out of the box, you may need to manually configure your server configuration. The settings are contained in your `wpackio.server.js` file.

- `proxy` needs to point to an active WordPress installation on your local machine. This could be an IP address or a host name (e.g., http://example.test/) specified in your system's hosts file that points to an IP.

- `port` is typically okay with the default setting (port 3000), but you can tweak it if you have something else listening on this port.

- `distPublicPath` is the relative path of your theme's `dist` directory, where your compiled site assets are stored. Wpack.io usually gets this right automatically, but if you are running into errors, try manually configuring this setting. In this case, set it to something like: `/wp-content/themes/my-theme/dist/`
