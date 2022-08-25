__LocalDB Django REST API__

localdb-django-restapi  

A projekt szerkezete és a lényegesebb fileok leírása:  

=api  
=-__ pycache __  
=-__ init.py __  
=-serializers.py  
=-urls.py <= `path('add/', views.addItem)` az adatok felvitelére szolgáló weblap url-je  
=-views.py <= `GET` RESTAPI `def getData(request)`, `POST` RESTAPI `def addItem(request)`  

=base <= webalkalmazás mappája; benne az `models.py` definiálja az `Item` modelljét.

=connector  
=-__ pycache __  
=-__ init.py __  
=-asgi.py  
=-settings.py <= ebben a fileban definiált (többek között) a REST API framework `INSTALLED APPS ... 'rest_framework',` valamint az adatbázis kapcsolat (jelen esetben localdb default)  
=-urls.py <= a default `admin.site.urls` mellett az API urljei is definiáltak, mint `api.urls`  
=-wsgi.py

=templates  
=-index.hhtml <= web frontend dokumentum előkészítve 
  
=.gitattributes  
=db.sqlite3 <= lokális adatbázis, az adatok mentéséhez és fetcheléséhez  
=manage.py <= init  

Az API webes környezetben való futtatásához használt a `python manage.py runserver` commandot a rootra (localdb-django-restapi) mutató terminálban.
A default nézed a `GET` API, ami az adatbázisban található adatokat adja vissza `JSON` formában. A `POST` nézethez való átugráshoz a böngészőben a `localhost` IP utána az `/add/` felvitele szükséges (a definiált api url-nek megfelelően). A felvitelre `JSON` formátumban van lehetőség.  
Egy példa a felvitelere:  
`{`  
`"name":"Adat létrehozva a POST API segítségével"`  
`}`  

Ezután az API létrehozza a fenti rekordot és rögzíti az adatbáziban. A `GET` nézetre visszatérve az adatbázisban megtekinthető. Az API ellátja egy egyedi Id-vel, valamint a létrehozás timestampjével.
