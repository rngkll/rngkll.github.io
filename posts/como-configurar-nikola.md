.. title: Itilizar nikola por primera vez
.. slug: utilizar-nikola
.. date: 2012-03-30 23:00:00 UTC-03:00
.. tags: nikola, python, blog, markdown
.. author: Alvaro Segura Del Barco
.. link: https://getnikola.com/
.. description: Guía de como configurar nikola
.. category: guias

# Instalación

# Utilizar markdown
Para utilizar markdown para crear los post se debe usar uno de los múltiples lenguajes de marcado ligero soportado, para eso se debe de editar el archivo config.py en la raíz del sitio en Nikola.

Primero se debe de verificar que este en la estructura **COMPILERS**
```
# 'rest' is reStructuredText
# 'markdown' is MarkDown
# 'html' assumes the file is HTML and just copies it
COMPILERS = {
    "rest": ('.rst', '.txt'),
    "markdown": ('.md', '.mdown', '.markdown'),
    "textile": ('.textile',),
    "txt2tags": ('.t2t',),
    "bbcode": ('.bb',),
    #"wiki": ('.wiki',),
    "ipynb": ('.ipynb',),
    "html": ('.html', '.htm'),
    # PHP files are rendered the usual way (i.e. with the full templates).
    # The resulting files have .php extensions, making it possible to run
    # them without reconfiguring your server to recognize them.
    "php": ('.php',),
    # Pandoc detects the input from the source filename
    # but is disabled by default as it would conflict
    # with many of the others.
    # "pandoc": ('.rst', '.md', '.txt'),
}
```
Luego se debe de agregar a la estructura del tipo de entrada, en el ejemplo de abajo se agregó la linea, `("posts/*.md", "posts", "post.tmpl")` a los dos tipos de entras **POST** y **PAGES**.

```
POSTS = (
    ("posts/*.rst", "posts", "post.tmpl"),
    ("posts/*.txt", "posts", "post.tmpl"),
    ("posts/*.md", "posts", "post.tmpl"),
)
PAGES = (
    ("stories/*.rst", "stories", "story.tmpl"),
    ("stories/*.txt", "stories", "story.tmpl"),
    ("stories/*.md", "stories", "story.tmpl"),
)
```

