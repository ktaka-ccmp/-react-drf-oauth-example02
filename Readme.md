# React.js + Django Rest Framework

## Howto run Reac.js+Django pages using this repo.

### Django (backend)

Prepare venv and install packages
~~~
python3 -m venv .venv
source .venv/bin/activate
pip install django djangorestframework django-cors-headers coreapi python-decouple
~~~

Edit, backend/backend/.env
~~~
ORIGIN_SERVER=http://react.example.com:3000
~~~
(Replace 'react.example.com:3000' with your server & port.)\\

Run server
~~~
cd backend/
python manage.py runserver [::]:8000
~~~

(Optional) Test to see if it's working
~~~
# curl -s  http://localhost:8000/api/customer/| jq .results[1]
{
  "id": 2,
  "enjoy_jards_macale": true,
  "name": "UYcSutJqGjGxXtutiahlRqoALIkSYD",
  "email": "QhNkQJLCam@example.com",
  "age": -1653201221,
  "bio": "vjHxWOqXSzudaCKLsNLHTetbRGKmZqaHwMdIMKgfisgkYvUBZsYFnJJXfRoWlkbEaSNWRUENyVXDiYaeGtxyOyUsDtpNoRvNGgzBSVWknAcfnCuTMqmvNRpwKahIQhYIlZJnHWSswjIPNiroLAbICBKCwYmwdSaMEwBrTsrrkjHLmRZMacaJcpkDoFvFNOFGeCfGjrHaKqVSxhgxattUkjlvkFjfOUZqjXGGIROPnViSwSZWGONybXdqnvPeOlhlwiktOQwytarzxcNlFCIwVfrYJqUPjdIxJKxRTsRRgNuF",
  "days_since_last_login": -9134197483796524000,
  "birthday": "2022-09-17",
  "last_shopping": "2022-09-18T07:27:16.971715+09:00"
}
~~~

### React (frontend)

Install node.js (Here is an example for Debian.)
~~~
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
~~~

Module install
~~~
npm install axios react-router-dom reactstrap bootstrap
~~~

Edit frontend/.env
~~~
REACT_APP_API_SERVER=http://api.example.com:8000
~~~
(Replace 'api.example.com:8000' with your server & port.)\\

Run server
~~~
PORT=3000 npm start 
~~~


## Prep. How this repo was created.

### Django

~~~
python3 -m venv .venv
source .venv/bin/activate
~~~

~~~
pip install django djangorestframework django-cors-headers coreapi python-decouple
django-admin startproject backend
cd backend/
django-admin startapp restapi
python manage.py createsuperuser --email admin@example.com --username admin
~~~

Edit files
~~~
backend/backend/settings.py
backend/backend/urls.py
backend/restapi/serializers.py
backend/restapi/views.py
backend/restapi/urls.py
backend/restapi/models.py
backend/backend/.env
~~~

Create database
~~~
./backend/manage.py migrate
~~~

Generate dummy data using model\_bakery
~~~
pip install model_bakery
vi backend/restapi/test-models.py
./backend/manage.py test restapi
~~~

Run server
~~~
cd backend/
./backend/manage.py runserver [::]:8000
~~~

Test
~~~
curl -H 'Accept: application/json' http://localhost:8000/api/customer
~~~

### React.js

Install node.js
~~~
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs
~~~

Create project
~~~
npx create-react-app frontend
cd frontend/
npm start 
~~~

Module install
~~~
npm install axios react-router-dom reactstrap bootstrap
~~~

Files modified or newly created:
~~~
frontend/src/index.js
frontend/src/Customer.js
frontend/src/App.js
frontend/.env
~~~

Original files kept as is:
~~~
public/index.html
public/manifest.json
public/robots.txt
public/favicon.ico
.gitignore
package-lock.json
package.json
~~~

Run server
~~~
PORT=3000 npm start 
~~~

Test => See the page using a browser.



## Directory structure

### backend (Django)

~~~
# tree -a
.
├── backend
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── db.sqlite3
├── manage.py
└── restapi
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── migrations
    │   └── __init__.py
    ├── models.py
    ├── serializers.py
    ├── test_models.py
    ├── urls.py
    └── views.py

3 directories, 16 files
~~~

### frontend (React.js)

~~~
# tree -a
.
├── .gitignore
├── package-lock.json
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── manifest.json
│   └── robots.txt
└── src
    ├── App.js
    ├── Customer.js
    └── index.js

2 directories, 10 files
~~~
