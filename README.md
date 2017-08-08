# NOTE

AWS has released the beta version of their Python X-ray SDK - check it out here: https://aws.amazon.com/about-aws/whats-new/2017/08/aws-x-ray-sdk-for-python-beta/

# xrayvision

Utilities and wrappers for using [AWS X-Ray](https://aws.amazon.com/xray/) with Python

## WSGI Apps

Simply add the middleware to your app. For example, if you use Flask:
```python
from xrayvision.ext.wsgi import XRayMiddleware

app = Flask(__name__)
app.wsgi_app = XRayMiddleware(app.wsgi_app)
```

You can add subsegments with the `global_segment`:
```python
from xrayvision import global_segment

...

with global_segment.add_subsegment('my custom loop') as segment:
    try:
        # do stuff
    except:
        segment.add_exception()
```

## Requests

Requests must be patched as early as possible in your code.
```python
import requests
import xrayvision

xrayvision.patch('requests')
```
