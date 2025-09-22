# Setting up your game
## Understanding `setup.py`
Now, we'll actually set up the game. In this part, we'll take a look at the `setup.py` file, which look like this:
```python3.13
from setuptools import setup

app_id = "your.company.app.name"

# Set renderer to pandagles2 (shaders) with pandagles (FFP) as fallback
# Add application id to PRC Data so that we can get it in the app
PRC_DATA = f'''
load-display pandagles2
aux-display pandagles

notify-level info
gl-debug true

android-app-id {app_id}
'''

setup(
    # The name of the app
    name='My ursina game',
    # The version of the app
    version='0.0.0',
    options={
        'build_apps': {
            # Uniquely identifies the app
            'application_id': app_id,

            # Update this for every version uploaded to the Play Store
            'android_version_code': 0,
            
            'platforms': ['android'],

            # Tell here the entry py file. It will be executed at the launch of the app
            # In this file will be your ursina code
            'gui_apps': {
                'mygame': 'game/__main__.py',
            },
            'plugins': [
                # Use of pandagles2/pandagles instead of pandagl
                'pandagles2',
                'pandagles',
                'p3openal_audio',
            ],
            # Here put all the resources you need
            'include_patterns': [
            	'game/**',
                # Don't remove this, it is to include ursina assets
                'ursina_assets/**',
                '**/*.png',
                '**/*.jpg',
                '**/*.egg',
            ],
            'extra_prc_data': PRC_DATA,

            # Here, you can change the icon
            'icons': {'*': 'logo.png'},
        },
    },
    # Choosing a classifier in the Games category makes it marked a "Game"
    classifiers=['Topic :: Games/Entertainment'],
)
```
We can see a lot of information. Let's break through it:
1. There is the `setuptools` import.
2. Then, there's the `app_id`. You define here the application id, which **is not** the application display name. It should look like this: `com.company.app_name`.
    - Me, I like to use `pao.paolog.my_app`
3. Then, there are some `PRC_DATA`. This doesn't do much, but can let you save data during the build, and load them into your app.
    - For example, to get the application id, the `setup_ursina_android` gets the `android-app-id` from the `PRC_DATA`.
4. Then, there's the `setup` function, with:
    1. `name`: Displayed inside the settings page of your app, but not on the launcher though.
    2. `version`: The version of your game.
    3. `options/build_apps`: Where you put your app settings:
        1. `application_id`: Normally, you'll change `app_id`, and not this.
        2. `android_version_code`: This **is not** the app version, but the Google Play version.
        3. `platforms`: Define which platforms are used (here, only `android`)
        4. `gui_apps`: Define each `app_name` with `python_file`. `app_name` is the displayed name on the android launcher.
        5. `plugins`: Which plugins to use.
        6. `include_patterns`: Which file to include into your apk.
        7. `extra_prc_data`: Just define `PRC_DATA` into the app.
    4. `classifiers`: How your app should be classed. It can be:
        - `'Topic :: Games/Entertainment'` = Game
        - `'Topic :: Audio'` = Audio
        - `'Topic :: Graphics'` / `'Topic :: Editors'` = Image
        - `'Topic :: Usenet News'` = News
        - `'Topic :: Office/Business'` = Productivity
        - `'Topic :: Chat'` = Social
        - `'Topic :: Video'` = Video

## Setting up your game
To make your game your own game, you need to change these lines:
1. Line 14: Change `name='My ursina game'` → `name='Your game name'`
2. Line 16: Change `version='0.0.0'` → `version='Your game version'`
3. Line 20: Change `application_id` → `application_id: 'com.yourcompany.yourgame'`
4. Line 23: If you plan to publish your game into the playstore, you'll need to increment the android_version_code by one each time before uploading it
5. Line 30: Change `'mygame': 'game/__main__.py'` → `'yourappdisplayname': 'path/to/your/entry/python_file.py'`
6. Line 50 (Optional): Change `'icons'` → `'icons': {'*': 'mylogo.png'}`

Make sure to **not** remove `ursina_assets` folder, or `ursina_assets/**` at line 42 in setup.py, because it is needed to run ursina.

Then, you can put your ursina game inside the game folder. Into the first 2 lines of your main script, add these lines:

```python
from setup_ursina_android import setup_ursina_android
setup_ursina_android()
```

It is required to run ursina, because it sets up ursina assets. Make sure you put them at the 2 first lines, not after.

If your game needs some requirements, add them in requirements.txt. Do not remove anything, just add.