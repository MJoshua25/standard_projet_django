à travers ce tutorial nous allons pas à pas démarrer un projet django

## 1. Installation
  1. Creer un dossier <> et l ouvrir avec VS code
  2. Dans le terminal de visual studio code creer l environnement virtuel et installer Django
  3.1. Sur iMAC python3 -m venv venv activer l environnement virtuel : source venv/bin/activate installer Django : pip3 install django
  3.1.2 Sur Windows python -m venv venv activer l environnement virtuel : source venv/Script/activate installer Django : pip install django

Creation dossiers
Creer un dossier <<projet_tuto>> dans le dossier <>

Ensuite creer deux dossier dans le dossier <<projet_tuto>> media_cdn et static_cdn

Puis dans ce dossier <<projet_tuto>> creer le projet et l application avec ses commandes: - Sur iMAC et Windows django-admin startproject myproject python manage.py startapp myapp

Le dossier myproject aura plusieurs fichiers a l interieur ouvrez le fichier settings.py et configurer ainsi:
Dans INSTALLED_APPS mettez le nom de votre application
    INSTALLED_APPS = [
    'myapp.apps.MyappConfig',

]
Dans TEMPLATES ajouter le nom du dossier qui contiendra les TEMPLATES
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
A la fin du settings.py ajouter ces routes
    STATIC_URL = '/static/'
    STATICFILES_DIRS = [
        os.path.join(BASE_DIR, 'static')
    ]
    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, '../media_cdn')
    STATIC_ROOT = os.path.join(BASE_DIR, '../static_cdn')
Dans le dossier myproject et dans le fichier urls.py completer avec ce code:
    from django.contrib import admin
    from django.urls import path,include
    from django.conf import settings
    from django.conf.urls.static import static

    urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),

    ]

    if settings.DEBUG:
        urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
Et creer le fichier urls.py dans le dossier myapp et ajouter ce code:
    from django.contrib import admin
    from django.urls import path,include
    from . import views

    app_name = 'myapp'
    urlpatterns = [
        path('', views.home, name='home'),
    
    ]
Dans le fichier views.py de myapp :
    def home(request):

        data={}
        return render(request, 'home.html',data)
Creer le dossier templates au meme niveau que les dossiers myapp et myproject et ajouter fichier html avec votre code html
Enfin lancer le serveur avec cette commande et ouvrez le lien qui s'affiche dans le votre navigateur
- commande pour lancer le serveur sur iMAC et Windows : 
    python manage.py runserver
