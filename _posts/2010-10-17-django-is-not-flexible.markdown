---
layout: post
title:  "Django is not flexible"
date:   2010-10-17 20:47:46+05:30
categories: opinion
author: shabda
---
Django is not flexible at all because you can not do simple
things like.   

* Using various authentication mechanisms.  
You can authenticate via [Username](http://docs.djangoproject.com/en/dev/topics/auth/#authentication-in-web-requests),
[emails](http://www.davidcramer.net/code/224/logging-in-with-email-addresses-in-django.html),
[Facebook, Twitter](http://github.com/agiliq/Django-Socialauth) or any combination of these.

* Using different database backends.  
Use MySQL, PostgreSQL,
[Non-relational databases](http://www.allbuttonspressed.com/projects/djangoappengine),
[more](http://docs.djangoproject.com/en/dev/ref/databases/#using-a-3rd-party-database-backend)
or a [combination](http://docs.djangoproject.com/en/dev/topics/db/multi-db/).

* Use different mail sending strategies.  
Send mail via [smtp](http://docs.djangoproject.com/en/dev/topics/email/#smtp-backend),
[queue to database](http://github.com/jtauber/django-mailer),
[log to files](http://docs.djangoproject.com/en/dev/topics/email/#file-backend)
and more.

* Different file storage method.  
Store locally, [FTP](http://djangosnippets.org/snippets/1269/),
[Amazon S3](http://code.welldev.org/django-storages/wiki/S3Storage)
or [write your own](http://docs.djangoproject.com/en/dev/howto/custom-file-storage/).

* Store messages in [Sessions, cookies or others](http://docs.djangoproject.com/en/dev/ref/contrib/messages/#storage-backends).

* Cache things in [Files](http://docs.djangoproject.com/en/dev/topics/cache/#filesystem-caching),
[DB](http://docs.djangoproject.com/en/dev/topics/cache/#database-caching),
[Memcache](http://docs.djangoproject.com/en/dev/topics/cache/#memcached)
or [just fake it](http://docs.djangoproject.com/en/dev/topics/cache/#dummy-caching-for-development).

* Save sessions in files, DB, Memcache or cookies.

* Use [Jinja](http://www.davidcramer.net/code/479/using-jinja2-with-django.html),
[Mako or Gensi](http://djangosnippets.org/snippets/97/) as templating library.

----------------------------

One of the most lingering criticisms of Django has been
that it is not flexible. People have criticised its design
as too-tightly coupled, hard to extend, and inflexible.
As a result, people have recommended to roll their own
using SQLchemy, Jinja or web.py.  

I think this view is unfounded and wrong. You would be hard
pressed to get the choices and flexibility which Django offers.
Eg, while development I run with Sqlite, Dummy caching, and emails
on console, while on production I switch to PostgreSQL, Memcache, and
queued emails.  

Many apps use this backend pattern themselves.
[Django registeration](http://docs.b-list.org/django-registration/0.8/backend-api.html),
[Django-celery](http://ask.github.com/celery/getting-started/first-steps-with-django.html)
and our own [merchant](http://github.com/agiliq/merchant).  


I have always been annoyed at Django is inflexible meme, and the recent 
[Charles Leifer's post](http://charlesleifer.com/blog/django-patterns-pluggable-backends/)
put various Django plug points to make writing this too post easy to not do it.  

