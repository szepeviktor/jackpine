# Jackpine

Jackpine is a WordPress starter theme based on Timber with modern developer tooling.

We love WordPress. It's how many of us got our start. But it's an old content management system, and efforts to keep things backwards-compatible have meant that developers had to put up with a subpar experience. Recently, theme frameworks like Gantry, Genesis, and Timber have breathed new life into the theme development space. We think Jackpine is the next step.

When you develop a theme based on Jackpine, you get the following setup out-of-the-box:

- **Timber**, a library that lets you create WordPress templates using the Twig templating engine

- **Tailwind CSS** for rapidly building beautiful designs

- **Alpine.js** for adding reactivity to your frontend

- **wpack.io**, an awesome tool for asset bundling with Webpack and live reloading with Browsersync (designed specifically for WordPress)

- **Composer** and **Yarn** for modern dependency management

Because Jackpine is based on Timber, you have access to all of their helper classes. As an added bonus, Timber plays nice with Advanced Custom Fields, allowing you to build themes for complex use cases.

Jackpine is also designed to anticipate common WordPress plugins that have their own CSS classes and allow for custom styling, so that you an achieve a bespoke look in any theme you build.

Jackpine is a great starting point for any WordPress developer or team who is looking to create themes quicker and easier using a modern workflow. It's deliberately opinionated when it comes to tooling, with deliberately unopinionated base styling (so you can build whatever you want on top of it).

**Jackpine is 100% free and open source and released under the MIT license.**

## Timber

[Timber](https://timber.github.io/docs/) is a WordPress theme framework (originally developed and maintained by [Upstatement](https://www.upstatement.com/timber/)) that helps developers separate their themes' business logic and styling. With Timber, your HTML is generated from [Twig Template Engine](https://twig.symfony.com/) files.

An additional benefit to Timber is that it includes integrations for two of the most common WordPress plugins—[Advanced Custom Fields](https://www.advancedcustomfields.com/) and [WooCommerce](https://woocommerce.com/)—right out of the box.

!>**Timber doesn't utilize the conventional WordPress loop**. This can lead to incompatability with some plugins, especially page builders. Before using Jackpine in a project, make sure you check to see if any of your plugins have reported incompatibilities with Timber.

## Tailwind CSS

[Tailwind CSS](https://tailwindcss.com/) is a CSS framework that helps you rapidly build custom designs. It works by giving you **helper classes** that you can directly add to your HTML elements.

Jackpine ships with the [Tailwind CSS Typography Plugin](https://github.com/tailwindlabs/tailwindcss-typography) enabled by default. This powerful plugin applies elegant default styles to HTML text elements, with readable font sizes, spacing, and margins. It's specifically designed for situations where a user generates HTML that you don't have control over—like when someone creates a post or a page in WordPress.

In Jackpine, we've implemented Tailwind with Sass. This lets you use our included SCSS stubs (for styling default Gutenberg blocks) and makes it easier to [extract Tailwind styles into components](https://tailwindcss.com/docs/extracting-components/#extracting-css-components-with-apply), a topic we'll discuss in its own section.

## Alpine.js

[Alpine.js](https://github.com/alpinejs/alpine) is a simple, declarative Javascript framework that helps you build a reactive frontend. It's **perfect for common tasks** like toggling a modal or animating a modal, where most of what you need to do involves adding or removing CSS classes.

Alpine was chosen for Jackpine because it offers a good substitute for jQuery in many of the situations WordPress developers typically use it in, and because it's much lighter than its main competitors, Vue and React.

## wpack.io

[wpack.io](https://wpack.io/) is a command line webpack / browser-sync tool that makes local theme development a breeze. With wpack.io, you get a development server with live reloading, webpack asset bundling, and a theme compiler that will create a zip file that can be uploaded and activated in WordPress.

We chose to include wpack.io because it's incredibly easy to use, well maintained, and performs a number of essential tasks.
