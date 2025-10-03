# Creating the AAB with a certificate

This is a sub-part of the 2.1 step. So, I assume that you read the 2.1 step before this one.

First, you need to create a certificate. To do that, you need OpenSSL (I didn't put OpenSSL as dependency, but you'll need to install it if you want to use certificates.)

To create the certificate, do this:
```bash
openssl genpkey -algorithm RSA -aes256 -out private.pem
openssl req -new -x509 -sha256 -days 365 -key private.pem > cert.pem
```

Then, you need to modify `setup.py` like this:
```python
from setuptools import setup

# ...

setup(
    # ...
    options={
        'build_apps': {
            # ...
        },
        'bdist_apps': {
            'signing_certificate': 'cert.pem',
            'signing_private_key': 'private.pem',
            # optional: Panda will otherwise ask passphrase on command-line
            #'signing_passphrase': 'panda3d_is_cool',
        },
    },
    # ...
)
```

**WARNING:** Putting your `signing_passphrase` on a public repo is really bad. If you need to do that, you can use a `.env` environnment. Because `setup.py` is a python file, you can use `python-dotenv` in it.

And, to build your application, use this command: 
```bash
python setup.py bdist_apps
```