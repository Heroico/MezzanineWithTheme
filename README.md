MezzanineWithTheme
==================

This is a simple test of a site created with Mezzanine CMS, using a custom theme.


Prerequisites:
==============
Mezzanine CMS (which is django based, which is python based).
A tool like PyEnv or VirtualEnv should help too.


The Way This Project Was Rolled:
================================
First, a mezzanine project was created. As in Mezzanine Site:

``` bash
# Install from PyPI
$ pip install mezzanine

# Create a project
$ mezzanine-project mezzanine-theme
$ cd mezzanine-theme

# Create a database
$ python manage.py createdb

# Run the web server
$ python manage.py runserver
```

Then, the Theme was plugged in.

From the point of view of Mezzanine CMS, a Theme is a "Django App".
(A Theme/App, actually, doesn't "need" any python code, and could consist
in nothing but templates and assets (css,js,img))

So, once the Mezzanine Project was created, 
a Django App was created within that subproject with the following

``` bash
# Setup django app
$ django-admin.py startapp testtheme
```

This created a bunch of things, most of which are not needed.

Then, I brought in some assets from a cool theme in:
[Mezzanine Themes github project](https://github.com/renyi/mezzanine-themes)

Particularly, the business template. 

``` bash
# Install from PyPI
$ cp -r path/to/business/theme/templates testtheme/templates
$ cp -r path/to/business/theme/static testtheme/static
```

The last step is configuring the Mezzanine Project/Django Site to actually use this theme.
You have to do this in *settings.py* at the root of your project.

``` python
INSTALLED_APPS = ( 
 "testtheme", 
 "django.contrib.admin", 
 "django.contrib.auth", 
 ... # more apps listed
 ```
 
 That's it. Is actually easier than it looks in the web. The issue is,
 most people dealing with this already know a lot and don't realize
 that a n00b might get lost.
 
Notes:
======
 
The actual templates I used from Renyi were a little bit out of date with current Django template system.
To fix them, any parameter passed into a {% url %} block command has to be enclosed in strings.
 
Alternatively, you could just call:
``` bash
$ python manage.py collecttemplates 
```
This will copy all templates used by the current mezzanine project into your folder, so that you have them at hand.
Note that they will override the default ones.