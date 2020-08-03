# Building a Theme

## Asset Packaging
Wpack.io can include any assets you want in the final .zip file that gets generated for WordPress. In order to include a directory and its contents, first create it and then add the path to the `packageFiles` section of your `wpackio.project.js` file with a wildcard selector, like this:

```javascript
packageFiles: [
    ...
    "assets/**",
    ...
]
```

## CSS Components
[(Read the Tailwind CSS docs on extracting components here)](https://tailwindcss.com/docs/extracting-components)

You can make a perfectly functional theme with Tailwind CSS by just applying helper classes to the HTML elements in your Twig files. For sections of your site where the styling isn't going to be repeated elsewhere, this is probably the easiest and best way.

But as your theme grows larger and you find that you're repeating yourself more and more, it can be useful to extract **components** from your code. Components are reusable classes, often used for things like buttons and icons, which will have a mostly consistent look throughout your site.

Extracting components with Jackpine and Tailwind CSS is easy. First, create an .scss file in the `styles` directory where you'll be defining the styles for your component. Then, go into your `main.scss` file and import it _before_ the Tailwind CSS core files are imported.

Assuming you created a file called `buttons.scss` in a `components` subdirectory, here is what you would do in `styles\main.scss`:

```scss
...

// Import components
@import 'components/buttons';

...

// Import Tailwind.css core

@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';
```

Now, in your `buttons.scss` file, you would use Tailwind CSS's special `@apply` directive to apply a series of Tailwind helper classes to your custom class:

```scss
.button {
    @apply mx-4 my-3 bg-blue-400 rounded-lg flex justify-center items-center;
}
```
!>There are a few complex Tailwind CSS helper classes that can't be applied to a component via `@apply`, like `.container`. Component extraction isn't intended for high-level layout work like this. If you find yourself needing to use `.container` in an extracted component, consider if there's a way to simplify your design or break it into more granular components. 

When your SCSS is compiled, the styling associated with the Tailwind CSS helper classes you applied will be added to your custom class. Now instead of writing out all of these Tailwind CSS helper functions every time you create a new button, you would just give it a class of `button`.

Bear in mind that you can always add in your own CSS or SCSS, too—very useful for things like background images.


## Custom Page Templates
[(Read the Timber docs on custom page templates here)](https://timber.github.io/docs/guides/custom-page-templates/)

One of the most common tasks a theme creator needs to perform is creating custom templates for individual pages of a site. Jackpine makes this easy thanks to the inclusion of Timber.

All you need to do is create a Twig template file in your `templates` directory with the name of the page you're creating the template for in [kebab case](https://medium.com/better-programming/string-case-styles-camel-pascal-snake-and-kebab-case-981407998841), prefixed by `page-`. Jackpine ships with a `page-home.twig` template file you can use as an example.

If all you want to do is create a custom design for a page, that's it! Timber will detect the template file and render your page with it automatically—no need to enable anything in the WordPress dashboard.

**Twig files contain styling. Your PHP files fetch the data that they use.**

If you need to perform any custom queries or fetch things that aren't available in the default `page.php` or `single.php` files, you can create a custom PHP file for your template. Follow the same naming convention as with the Twig files—the name of your page in kebab case prefixed by `page-`—and place it in your theme's root directory.

## Path Helpers
When referencing paths to assets in your Twig template files, like images, you can (and probably should) use Timber's built-in helpers:

- `{{ theme.link }}` : returns the absolute path to the theme (e.g., `https://example.org/wp-content/themes/my-theme`)

- `{{ theme.path }}` : returns the relative path to the theme (e.g., `/wp-content/themes/my-theme`)

## Responsive Design
[(Read the Tailwind CSS docs on responsive design here)](https://tailwindcss.com/docs/responsive-design/)

When you're building a custom theme, you will almost always need to configure your design for multiple screen sizes. Multi-column layouts that look great on large desktop monitors will need to collapse into single-column layouts for smartphones. Some things will need to be shown on one screen size and hidden on another.

Tailwind CSS makes it easy to create responsive designs because every helper class has prefixes for common screen sizes:

- **Small** (sm): Feature phones, low-end smartphones
- **Medium** (md): Smartphones
- **Large** (lg): Tablets, newer smartphones
- **Extra Large** (xl): Desktops and modern laptops

Each prefix corresponds to a standard CSS media query:

```scss
/* Small (sm) */
@media (min-width: 640px) { /* ... */ }

/* Medium (md) */
@media (min-width: 768px) { /* ... */ }

/* Large (lg) */
@media (min-width: 1024px) { /* ... */ }

/* Extra Large (xl) */
@media (min-width: 1280px) { /* ... */ }
```

**Many first-timers to Tailwind make the mistake of designing for the (larger) screen they're working on first and worrying about smaller screens later.** Tailwind CSS is designed to work by starting with the smallest possible screen size and using prefixes for successively larger screen sizes.

The following example illustrates this:

```html
<p class="text-sm md:text-base lg:text-lg xl:text-xl">The text gets larger as the screen gets larger.</p>
```

**Whenever practical, start small and work up.**

### SCSS Stubs
Jackpine ships with **SCSS stubs**, located in the ```\styles``` directory. These are designed to help you apply styling to Gutenberg blocks, form elements, and WooCommerce-specific classes. These are best used by extracting components from Tailwind CSS classes using the `@apply` directive.
