---
title: Icons
old_permalink: /versions/v9.0.0/guides/icons.html
previous___FILE: ./assets.md
next___FILE: ./using-custom-fonts.md
---

As trendy as it is these days, not every app has to use emoji for all icons 😳 -- maybe you want to pull in a popular set through an icon font like FontAwesome, Glyphicons or Ionicons, or you just use some PNGs that you carefully picked out on [The Noun Project](https://thenounproject.com/) (Expo does not currently support SVGs). Let's look at how to do both of these approaches.

## @exponent/vector-icons

This library is installed by default on the template project that you create through XDE. It includes eight icon sets, you can browse all of the icons using the [@exponent/vector-icons directory](https://exponent.github.io/vector-icons/).

    import React from 'react';
    import { Ionicons } from '@exponent/vector-icons';

![](./vector-icons-directory.png)

```javascript
export default class IconExample extends React.Component {
  render() {
    return (
      <Ionicons name="md-checkmark-circle" size={32} color="green" />
    );
  }
}
```

This component loads the Ionicons font if it hasn't been loaded already, and renders a checkmark icon that I found through the vector-icons directory mentioned above. `@exponent/vector-icons` is built on top of [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) and uses a similar API. The only difference is `@exponent/vector-icons` uses a more idiomatic `import` style:

`import { Ionicons } from '@exponent/vector-icons';` instead of.. `import Ionicons from 'react-native-vector-icons/Ionicons';`.

> **Note:** As with any custom font in Expo, you may want to preload icon fonts before rendering your app. The font object is available as a static property on the font component, so in the case above it is `Ionicons.font`, which evaluates to `{ionicons: require('path/to/ionicons.ttf')}`. [Read more about preloading assets](assets.html#all-about-assets).

## Icon images

If you know how to use the react-native `<Image>` component this will be a breeze.

```javascript
import React from 'react';
import { Image } from 'react-native';

export default class SlackIcon extends React.Component {
  render() {
    return (
      <Image
        source={require('../assets/images/slack-icon.png')}
        fadeDuration={0}
        style={{width: 20, height: 20}}
      />
    );
  }
}
```

Let's assume that our `SlackIcon` class is located in `my-project/components/SlackIcon.js`, and our icon images are in `my-project/assets/images`, in order to refer to the image we use require and include the relative path. You can provide versions of your icon at various pixel densities and the appropriate image will be automatically used for you. In this example, we actually have `slack-icon@2x.png` and `slack-icon@3x.png`, so if I view this on an iPhone 6s the image I will see is `slack-icon@3x.png`. More on this in the [Images guide in the react-native documentation](https://facebook.github.io/react-native/docs/images.html#static-image-resources).

We also set the `fadeDuration` (an Android specific property) to `0` because we usually want the icon to appear immediately rather than fade in over several hundred milliseconds.
