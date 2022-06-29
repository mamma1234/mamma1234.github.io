---
layout: post
title: 'Django Rest Framework'
description:
headline:
modified: 2019-11-20
category: webdevelopment
imagefeature:
tags: [Django, React, Rest, Framework]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record

## 개념

-   Django REST framework

## python3

### 가상환경

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    },
    'mfedi': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db1.sqlite3'),
    },
}

post\router.py

DATABASE_ROUTERS = ['post.router.MultiDBRouter']

class MultiDBRouter(object):
    def __init__(self):
        self.model_list = ['mfedi', 'default']

    def db_for_read(self, model, **hints):
        if model._meta.app_label in self.model_list:
            return model._meta.app_label

        return None

    def db_for_write(self, model, **hints):
        if model._meta.app_label in self.model_list:
            print('db_for_write: %s' % model._meta.app_label)
            return model._meta.app_label

        return None

    def allow_relation(self, obj1, obj2, **hints):
        if obj1._meta.app_label in self.model_list or \
                obj2._meta.app_label in self.model_list:
            return True

        return None

    def allow_migrate(self, db, app_label, model_name=None, **hints):
        if app_label == 'post':
            return db in self.model_list
        elif db == 'default':
            return True

        return None


class Meta:
        app_label = 'mfedi'
```
