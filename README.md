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

## To add instrumentation (Splunk Open Telemetry distribution)
First, [install the otel collector](https://docs.splunk.com/observability/en/gdi/get-data-in/compute/linux.html), then run the following
```
# Install the instrumentation
python3 -m pip install "splunk-opentelemetry[all]"
export OTEL_SERVICE_NAME=djangosample
export OTEL_RESOURCE_ATTRIBUTES='deployment.environment=sample,service.version=1.0'
export DJANGO_SETTINGS_MODULE=djangosample.settings
splunk-py-trace-bootstrap
splunk-py-trace python3 manage.py runserver 0.0.0.0:8000 --noreload
```

## Connect
You will need to hit the endpoint a few times to generate traces.

### Connecting locally
From the same system you can use localhost
```
curl http://localhost:8000/members/
```

### Connecting from multipass host (for example)
We set the authorized hosts to a wildcard(*) so you can also do this from the multipass host if you wish to.
```
multipass info <host>
# Use the IP address, for example
curl http://<ip address>:8000/members/
```

## Debugging Tracing
To see if traces are being sent you can enable zpages. These are on by default but to be able to view these remotely you can make the following change
* Edit `/etc/otel/collector/agent_config.yaml`
* Change the zpages endpoint to `endpoint: 0.0.0.0:55679`
* Restart the collector with `sudo systemctl restart splunk-otel-collector.service`
