This document contains instructions on how to install the cube bookstore website.

# Dependencies #

The steps below assume the most basic setup, using sqlite and django's test server. Use Django's documentation for how to use production applications like Apache or MySQL. There are a few dependencies on a client for TWU's authentication system (twuPass), which are not released with the main website. The twuPass module uses python-suds.

Before starting, make sure you have [python 2.x](http://python.org/download/), [django](http://www.djangoproject.com/), and [subversion](http://subversion.tigris.org/) installed. If not using the twuPass authentication backend, some modifications will need to be made to the code. If you are using twuPass however, make sure [setuptools](http://pypi.python.org/pypi/setuptools) and suds are installed as well, and that you are using python 2.5+.

<a href='Hidden comment: 
Put a link to how to modify code for non twuPass users if that ever happens
'></a>

# Steps #
The steps below are the minimum necessary to get the website up and running for testing purposes. For a production setup, please expand on these steps by referring to django's documentation.

  1. [Get the cube-bookstore code](http://code.google.com/p/cube-bookstore/source/checkout)
  1. copy cube/settings-dist.py. to cube/settings.py
  1. open cube/settings.py in your favourite text editor
  1. put your name and email address into the ADMINS tuple.
  1. Set the DATABASE\_ENGINE to 'sqlite3'
  1. Set the DATABASE\_PATH to be where you want the database file to be stored
  1. set the MEDIA\_ROOT to the absolute path of cube-bookstore's media folder
  1. set MEDIA\_URL to '(your-domain)/site\_media/'. e.g. 'localhost:8000/site\_media/' By default urls.py is setup to serve media files via django's test server. Don't do this for production situations.
  1. add the absolute path to the templates folder to TEMPLATE\_DIRS.
  1. now open cube/urls.py and find the site\_media entry. In the dictionary, change the 'document\_root's value to the absolute path of where your media files are.
  1. At this point you will either need to setup twuPass with the provided documentation, or modify the website to use a different authentication backend.
  1. now if you run the unitests ('python cube/manage.py test') then they should all pass successfully.
  1. To run the website, execute
    1. python cube/manage.py syncdb
    1. python cube/manage.py runserver