à travers ce tutorial nous allons pas à pas démarrer un projet django

## 1. Installation
  1. Creer un dossier <> et l ouvrir avec VS code
  2. Dans le terminal de visual studio code creer l environnement virtuel et installer Django
    * Sur iMAC python3 -m venv venv activer l environnement virtuel : source venv/bin/activate installer Django : pip3 install django
    * Sur Windows python -m venv venv activer l environnement virtuel : source venv/Script/activate installer Django : pip install django

## 2. Creation dossiers
  1. Créer le projet en exécutant la commande `django-admin startproject projet_tuto`
  2. Créer les dossiers suivants:
    2.1. media_cdn : où seront stockés les fichiers des models
    2.2. statut_cdn : où seront stockés les fichiers static
    
## 3. settings.py
Dans TEMPLATES ajouter le nom du dossier qui contiendra les TEMPLATES
```python
    TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': ['templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
  ]
  ```
A la fin du fichier, remplacer `STATIC_URL = '/static/'`
par :
```python
    STATIC_URL = '/static/'
    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static')
    ]
    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, '../media_cdn')
    STATIC_ROOT = os.path.join(BASE_DIR, '../static_cdn')
```

## 4. urls.py
  Contenu du fichier:
```python
    from django.contrib import admin
    from django.urls import path,include
    from django.conf import settings
    from django.conf.urls.static import static

    urlpatterns = [
      path('admin/', admin.site.urls),
    ]

    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
```

## 5. fin
  executer cette commande pour l'instant: `python manage.py runserver`
