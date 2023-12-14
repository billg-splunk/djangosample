# djangosample

Sample app built from [w3schools](https://www.w3schools.com/django/index.php)

## To run (starting from the root of this project folder)
```
# Install venv (you may need to install python3-venv first
python3 -m venv venv
source venv/bin/activate

# Install Django
python3 -m pip install Django

# Run the server
cd djangoexample
python3 manage.py runserver 0.0.0.0:8000
```

## Connecting locally
```
curl http://localhost:8000/members/
```

## Connecting from multipass host (for example)
```
multipass info <host>
# Use the IP address, for example
curl http://<ip address>:8000/members/
```