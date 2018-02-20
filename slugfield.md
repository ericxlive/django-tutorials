# django
Django tutorials

## SlugField

A SlugField is a way of generating a valid URL, generally using data already obtained. Plus, using the title of a post or name of a product to generate a URL. It's better to use a function in order to generate a URL, given a title (or other piece of data), rather than setting it manually.


```
from django.db import models

class Book(models.Model):

    (...)
    slug = models.SlugField(unique=True)

```

Still, in the same models.py file you will have to import

```
from django.util.text import slugify
```

After import, it's important add the code below in the root of the file

```
def pre_save_book_receiver(sender, instance, *args, *kwargs):
    slug = slugfy(instance.title)
    
pre_save.connect(pre_save_book_receiver, sender=Book)
```

First, it's important to check whether or not that slug exists in order to add a new one. 

```
def pre_save_book_receiver(sender, instance, *args, *kwargs):
    if not instance.slug:
        instance.slug = create_slug(instance)
    
pre_save.connect(pre_save_book_receiver, sender=Book)
```

### Recursively checking pre existent slug

There must be a piece of code checking recursively whether or not that slug exists.

```
def create_slug(instance, new_slug=None):
    slug = slugfy(instance.title)
    if new_slug is not None:
        slug = new_slug
    books = Book.objects.filter(slug=slug).order_by("-id")
    exists = books.exists()
    if exists:
        new_slug = "%s-%s" % (slug, books.first().id)
        return create_slug(instance, new_slug=new_slug)
    return slug
```

### Update the absolute URL return
```
def get_absolute_url(self):
    return reverse("books:detail", kwargs={"slug", self.slug})
```
