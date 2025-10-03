# Converting your AAB to APKs

An APKs file is a `.zip`-like file that contains one `.apk` for each processor architecture.
This type of file is required for C++ application, because compiling for C++ gives you one binary that only works for one processor architecture.
So, because Panda3D is written in C++, we need to have this kind of file.

To convert an AAB to APKs, you need to use `Java` and `BundleTool` (check requirements step to see where to install.)

Then, use this command:
```bash
java -jar Path/To/BundleTool.jar --bundle ./dist/*.aab --output ./dist/app.apks
```

However, you can build you app to a single APK.
**WARNING:** I don't know why, but some people got assets error (not loading or buggy pngs) while using this. This is not recommended.
To do this, you can use the `--universal` flag
```bash
java -jar Path/To/BundleTool.jar --bundle ./dist/*.aab --output ./dist/app.apk --universal
```