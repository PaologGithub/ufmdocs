# Installing the APKs
You may be tempted to install your game on your device (I dunno why did I put 'tempted', but maybe you'll want to play your game... maybe...)

To install your game, ensure you have one device connected to ADB (check with `adb devices`).
**WARNING:** You need to have **only one** device connected to ADB, or else BundleTool will throw you an error.

To install your apks, use this command:
```bash
java -jar Path/To/BundleTool.jar install-apks --apks=./dist/*.apks
```

You may be tempted/need to use other method, which will we talk in the next step.