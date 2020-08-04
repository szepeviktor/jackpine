# Jackpine Cookbook

## Author Box

>A section that displays author information on a post

In your `templates\single.twig`, add the following section:

```twig
<div class="flex flex-col">
    <img src="{{ post.author.avatar | resize(48, 48) }}" alt="" class="rounded-lg">
    <p>by <a href="{{ post.author.link }}">{{ post.author }}</a></p>
</div>
```

Change the `resize(width, height)` filter to whatever size makes sense.

## Comment Section 

?>By default, Jackpine limits comment nesting to two comments deep and enforces this in the WordPress dashboard. Jackpine's out-of-the-box comment styling is built around this assumption. To change comment nesting settings, follow the instructions below.

To change the default comment nesting depth, locate this section in your ```functions.php``` file, located in the main directory of your theme:

```php
/** Limit comment depth to two. If you need more, you will need to adjust the Tailwind styling */
add_filter( 'thread_comments_depth_max', function( $max )
{
    return 2;
} );
``` 

You can then specify a new **maximum** comment depth, or eliminate the section altogether to return full control of comment nesting to the **Settings > Discussion** section of the WordPress dashboard.

## Copyright Notice

>A simple copyright notice using Twig that automatically displays the current year

```twig
<p>© {{"now"|date('Y')}}. All rights reserved.</p>
```

## Dropdown Menu

>Create a simple dropdown menu with Tailwind CSS and Alpine.js

This dropdown menu uses Alpine.js to display child items when a user hovers over a parent item.

First, let's register a new menu in WordPress. In your `functions.php` file, add the following to your `add_to_context()` function:

```php
public function add_to_context($context)
{
    ...
    $context['top_menu'] = new Menu();

    return $context;
}
```

Now, head over to your `templates\header.twig` file and replace the contents with the following:

```twig
<nav id="nav-main" class="flex flex-row" role="navigation">
    {% if items|default(top_menu.items) %}
        {% for item in items|default(top_menu.items) %}
            {% if item.children %}
                <div x-data="{ hover: false }" class="relative">
                    <a id="menu-item-{{ item.id }}" href="{{ item.link }}" class="text-lg mx-4 flex items-center" @mouseenter="{hover=true}" @mouseleave="{hover=false}">{{ item.name }}</a>
                    <ul id="menu-item-list-{{ item.id }}" class="absolute ml-4 flex flex-col whitespace-no-wrap" x-show="hover" @mouseenter="{hover=true}" @mouseleave="{hover=false}">
                        {% for child in item.children %}
                            <li id="menu-item-child-{{ child.id }}">
                                <a href="{{ child.link }}" class="">{{ child.title }}</a>
                            </li>
                        {% endfor %}
                    </ul>
                </div>
            {%  else %}
                <a id="menu-item-{{ item.id }}" href="{{ item.link }}" class="text-lg mx-4">{{ item.name }}</a>
            {% endif %}
        {% endfor %}
    {% endif %}
</nav>

```

## Post Content

>Apply beautiful, readable styling to user-created posts and pages by adding a couple of classes to the div that will contain the content.

[(Read the Tailwind CSS Typography Plugin docs here)](https://github.com/tailwindlabs/tailwindcss-typography)

In your ```templates\page.twig``` and ```templates\single.twig``` template files, locate the following section:

```twig
<div>
    {{post.content}}
</div>
```

Apply the ```prose``` class to the div to automatically apply styling to the post content, then add one of the following classes to control the size of the text:

- **prose-sm**
- **prose**
- **prose-lg**
- **prose-xl**
- **prose-2xl**

The finished result should look something like this:

```twig
<div class="prose prose-lg">
    {{post.content}}
</div>
```

## Post Date 

>A simple way to display the date and time a post was published

In your `templates\single.twig`, add the following:

```twig
<time datetime="{{ post.date|date('Y-m-d H:i:s') }}">{{ post.date }}</time>
```

## Tag Cloud
>Display a list of tags for a WordPress post

In your `templates\single.twig`, add the following and style it however you'd like with Tailwind CSS classes:

```twig
<div>
    <p>
        {% for tag in post.tags %}
            {% if loop.last %}
                <a href="{{ tag.link }}">{{ tag }}</a>
            {% else %}
                <a href="{{ tag.link }}">{{ tag }}</a>,
            {% endif %}
        {% endfor %}
    </p>
</div>
```
