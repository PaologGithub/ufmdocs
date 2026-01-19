# Understanding the structure
This is the structure of a default UfM game:
```
/
|- assets/
|  |- game_assets/
|  |  |- ...
|  |- ursina_assets/
|  |  |- ...
|  |- logo.png
|
|- project/
|  |- builder/
|  |  |- ... [.py]
|  |- wheels/
|  |  |- ... [.whl]
|  |- settings.toml
|
|- src/
|  |- ... [.py]
|- ...
|- setup.py
```

In this section, I will go through each directory, explaining what they do, and what to do in them. 

> [!WARNING]
> This chapter is, I think, one of the most important one. It'll learn you how to create your basic game, etc etc. Please read it carefully, entirely. 

## `Assets` folder
The `assets` folder contains two subfolders: 
- `game_assets`: The folder you'll modify to include your own assets. Put your assets here, and use them with `ursina.application.asset_folder`.
- `ursina_assets`: The folder that contains ursina base assets. Normally, you won't modify this folder. Access it with `ursina.application.package_folder`

## `Project` folder
This folder is not a thing you'll modify much; you'll principally modify it when you set up your game, but then, you normally won't need to modify it much. There is these subfolders: 
- `builder`: You won't normally edit this folder; it's just some modules that'll get run. Maybe you'll modify it to change how your app get built.
- `wheels`: This folder includes basic python wheels, like Panda3D and Ursina. If you need to include wheels, put them in this folder. 
- `settings.toml`: This is the most important file in the folder. This is where you set up your game, and we'll learn now how to use this file:

### Using `project/settings.toml` 
This is the default `settings.toml`: 
```toml
[android]
# Identifier used by android
id          = "your.company.app.name"
# Version of your game
version     = "0.0.0"
# Name displayed in the settings page (not the launcher)
name        = "My ursina game"
# Icon of the application
icon        = "assets/logo.png"
# Classifiers of the application
classifiers = ["Topic :: Games/Entertainment"]

[application]
# Name displayed on the launcher
# Can now have spaces in it
# Uh no in reality
name        = "MyUrsinaGame"
# Main python file of the game
startfile   = "src/__main__.py"

[build]
# Android version code. NOT EQUAL to android.version, used by Google Play Store
# Each time you update your app on the Play Store, you should increment this by one.
vercode     = 0
# Platforms supported by your app
platforms   = ["android"]
# What file to includes
includes    = [
    "assets/game_assets/**",    # Game assets
    "assets/ursina_assets/**",  # Ursina assets, don't remove this.
    "assets/assets.gen",        # Generated list of assets
    "**/*.png",
    "**/*.jpg",
    "**/*.egg",
]

[assets]
# Ursina assets dir
ursina_dir  = "assets/ursina_assets"
# Game assets dir
game_dir    = "assets/game_assets"
```
I guess the comments are already straightforward, so I won't really go through it, but this is the file you'll need to modify first to make your game **your** game. 

## `Src` folder
This folder includes your application, with 2 main files:
- `__main__.py`: The main application (can be redefined in `project/settings.toml`)
> [!WARNING]
> When modifying the main file, make sure to include these two lines at the beginning: 
> ```py
> from setup_ursina_android import setup_ursina_android
> setup_ursina_android()
> ```
- `setup_ursina_android.py`: This file is here to set up ursina for android, and help you out. Modify it only if you know what you're doing.