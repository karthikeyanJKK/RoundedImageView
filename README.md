# RoundedImageView


A fast ImageView (and Drawable) that supports rounded corners (and ovals or circles) based on the original [example from Indian Guy](https://jkkappzone.in/). It supports many additional features including ovals, rounded rectangles, ScaleTypes and TileModes.

![RoundedImageView screenshot](https://raw.github.com/karthikeyanjkk/RoundedImageView/master/screenshot.png)
![RoundedImageView screenshot with ovals](https://raw.github.com/karthikeyanjkk/RoundedImageView/master/screenshot-oval.png)

There are many ways to create rounded corners in android, but this is the fastest and best one that I know of because it:
* does **not** create a copy of the original bitmap
* does **not** use a clipPath which is not hardware accelerated and not anti-aliased.
* does **not** use setXfermode to clip the bitmap and draw twice to the canvas.

If you know of a better method, let me know (or even better open a pull request)!

Also has proper support for:
* Borders (with Colors and ColorStateLists)
* Ovals and Circles
* All `ScaleType`s
  * Borders are drawn at view edge, not bitmap edge
  * Except on edges where the bitmap is smaller than the view
  * Borders are **not** scaled up/down with the image (correct width and radius are maintained)
* Anti-aliasing
* Transparent backgrounds
* Hardware acceleration
* Support for LayerDrawables (including TransitionDrawables)
* TileModes for repeating drawables

## Known Issues

- VectorDrawables are **not** supported. This library is designed for BitmapDrawables only. Other drawables will likely fail or cause high memory usage. 
- ColorDrawables are poorly supported, use your own rounded VectorDrawables instead if you want less memory pressure.
- Glide transforms are **not** supported, please use [karthikeyanjkk/glide-transformations](https://github.com/karthikeyanjkk/glide-transformations) if you want to round images loaded from Glide.

## Gradle


Add the following to your `build.gradle` to use:
```
repositories {
    mavenCentral()
}

dependencies {
    implementation 'com.karthikeyanjkk:roundedimageview:2.3.0'
}
```


## Usage

Define in xml:

```xml
<com.karthikeyanjkk.roundedimageview.RoundedImageView
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:id="@+id/imageView1"
        android:src="@drawable/photo1"
        android:scaleType="fitCenter"
        app:riv_corner_radius="30dip"
        app:riv_border_width="2dip"
        app:riv_border_color="#333333"
        app:riv_mutate_background="true"
        app:riv_tile_mode="repeat"
        app:riv_oval="true" />
```

Or in code:

```java
RoundedImageView riv = new RoundedImageView(context);
riv.setScaleType(ScaleType.CENTER_CROP);
riv.setCornerRadius((float) 10);
riv.setBorderWidth((float) 2);
riv.setBorderColor(Color.DKGRAY);
riv.mutateBackground(true);
riv.setImageDrawable(drawable);
riv.setBackground(backgroundDrawable);
riv.setOval(true);
riv.setTileModeX(Shader.TileMode.REPEAT);
riv.setTileModeY(Shader.TileMode.REPEAT);
```

### Picasso

To make a Transformation for Picasso:

```java
Transformation transformation = new RoundedTransformationBuilder()
          .borderColor(Color.BLACK)
          .borderWidthDp(3)
          .cornerRadiusDp(30)
          .oval(false)
          .build();

Picasso.with(context)
    .load(url)
    .fit()
    .transform(transformation)
    .into(imageView);
```

## Changelog

Nothing yet....




## License

    Copyright 2021 karthikeyanJKK

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
