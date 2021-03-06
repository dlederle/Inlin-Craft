Inlin for Craft
===========
A tiny plugin for inlining files in Craft templates.

*This is the Craft 3.x version of Inlin, for the Craft 2.x version see the [master branch](https://github.com/aelvan/Inlin-Craft/tree/master).*

Requirements
---
This plugin requires Craft CMS 3.0.0 or later.

Installation
---
To install the plugin, follow these instructions.

1. Open your terminal and go to your Craft project:

        cd /path/to/project

2. Then tell Composer to load the plugin:

        composer require aelvan/inlin

3. In the Control Panel, go to Settings → Plugins and click the “Install” button for Inlin.


Usage
---
Use it like this:

    {{ craft.inlin.er('/build/svg/my.svg') | raw }}
    
    <script>{{ craft.inlin.er('/build/js/my.js') | raw }}</script>
    
    <style type="text/css">{{ craft.inlin.er('/build/css/my.css') | raw }}</style>

Why? [Sometimes](http://css-tricks.com/svg-sprites-use-better-icon-fonts/) it
[makes sense](http://www.yottaa.com/blog/bid/306224/Inlining-for-Performance-When-to-Let-the-Cache-Go),
performance or workflow wise, to inline resources instead of requesting them.

To include a remote file, pass in true as the second parameter:

	{{ craft.inlin.er('http://example.com/remote/path.svg', true) | raw }}

Warning
---
Understand that inserting filedata in your templates, especially when passing it through Twig's raw filter,
is a potential security risk. And the path is relative to your document root, so the path could point to a
file anywhere on your server. **Make sure you never, ever let a third party control what is inserted.**
In case you're thinking "meh", insert this into your template:

    {{ craft.inlin.er('/../config/db.php') | raw }}

*"With great power, comes great responsibility" -Voltaire*


Configuration
---
Inlin needs to know the public document root to know where your files are located. By default
Inlin will use `@webroot`, but on some server configurations this is not the correct
path. You can configure the path by creating a config file called `inline.php` in your config folder, 
and adding the `publicRoot` setting.

#### Example

    'publicRoot' => '/path/to/website/public/',

