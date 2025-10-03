# Creating the aab
AAB is a special type of package. The acronym is for 'Android App Bundle', and is used to publish your app on the Google Play Store.

However, this is not easy to directly install an AAB to a device. Second however, Panda3D build your app as an AAB bundle, not an APK one.

To create the aab, this is pretty straightforward; you just need to use `setup.py` script, like this:
```bash
python3.13 setup.py bdist_apps
```

However, this method can only be used for development use. To release your app, you'll need to build the AAB with a certificate, which you'll learn in the next page.