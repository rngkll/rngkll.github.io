.. title: Utilizar Nikola por primera vez
.. slug: utilizar-nikola
.. date: 2015-08-20 23:00:00 UTC-06:00
.. tags: nikola, python, blog, markdown, jaquerespeis
.. author: Alvaro Segura Del Barco
.. link: https://getnikola.com/
.. description: Guía de como configurar nikola
.. category: guias

# Instalación

La forma mas simple de instalar Nikola es con pip y virtual, también se podría utilizar uno de los paquetes de la distribución que se teste utilizando, en si son usuarios de Linux.

En el directorio del repositorio del sitio
```
virtualenv --python=python3 .env
source .env/bin/activate
pip3 install --upgrade "Nikola[extras]"
```
## Primeros usos

En este momento se tiene el sistema instalado, ahora hay que crear el contenido del primer sitio de prueba, estando en el directorio que va a mantener el código, se ejecuta el comando `nikola init --demo .`, luego se debe de construir el sitio con el comando `nikola build`.

El siguiente paso es ver el sitio, para lo que va a utilizar el comando `nikola serve -b`, pero es mucho mas fácil utilizar `nikola auto -b` para reconstrucciones automáticas.



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

```python
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
# Utilizar locales para Costa Rica
Este proceso debería funcionar para la mayoría de idiomas.

1. Generar el locale necesario con `locale-get <locale>
2. Definir cual es el locale que debe de utilizar Nikola por defecto.
```python
# What is the default language?
DEFAULT_LANG = "es"

# What other languages do you have?
# The format is {"translationcode" : "path/to/translation" }
# the path will be used as a prefix for the generated pages location
TRANSLATIONS = {
    DEFAULT_LANG: "es_CR",
    # Example for another language:
    # "es": "./es",
    "es": "./",
    "en": "./en",
}
```
3. Definir el locale que se va a utilizar para `es`, por defecto es `es_ES`.
```python
LOCALES = {
        "es":"es_CR.utf-8",
        }
```
El locale a utilizar puede ser probado, importando locale `import locale` y llamando al locale necesario `locale.setlocale(locale.LC_ALL, 'es_CR.utf-8')`
