# django-unslash

Django Middleware that can automatically remove trailing URL slashes and 301 
redirect to the non-slash-terminated URL. This behavior is performed if the
initial URL ends in a slash and is invalid, removing the trailing slash
produces a valid URL, and `REMOVE_SLASH` is set to True. Otherwise there is
no effect.

For example, foo.com/bar/ will be redirected to foo.com/bar if you don't
have a valid URL pattern for foo.com/bar/ but do have a valid pattern for
foo.com/bar and `REMOVE_SLASH=True`.

This middleware provides the inverse of the Django CommonMiddleware 
`APPEND_SLASH` feature.


## Install

To install `django-unslash`,

```
pip install django-unslash
```

If you're using a `requirements.txt` file, add `django-unslash>=0.1` to it.


## Usage

Modify your Django `settings.py` file to add `unslash.middlware.UnslashMiddleware`
to your `MIDDLEWARE_CLASSES` just before or after `django.middleware.common.CommonMiddleware`.

```python
MIDDLEWARE_CLASSES = (
    # ...
    'unslash.middleware.UnslashMiddleware',
    'django.middleware.common.CommonMiddleware',
    # ...
)
```

Set `REMOVE_SLASH` to True and `APPEND_SLASH` to False,

```python
APPEND_SLASH = False
REMOVE_SLASH = True
```

If `REMOVE_SLASH` is False or unset, the UnslashMiddleware has no effect and you are free to use the Django CommonMiddleware append slash feature with `APPEND_SLASH=True`.


## Rationale

Web applications should have a URL structure which either (1) uses trailing
slashes and redirects to append slashes if invalid unslashed URLs are accessed.
(2) uses no trailing slash URLs and removes and redirects to unslahed URLs if
invalid slash terminated URLs are accessed. The prior is the Django default, 
while the later is possible by adding this middleware to your project.


## Tests


## Notes

Based closely on Django's APPEND_SLASH CommonMiddleware [implementation](https://github.com/django/django/blob/master/django/middleware/common.py).


## License

[MIT License](LICENSE)
    