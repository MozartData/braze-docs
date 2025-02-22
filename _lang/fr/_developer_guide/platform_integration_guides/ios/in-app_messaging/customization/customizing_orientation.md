---
nav_title: Personnalisation de l’orientation
article_title: Personnalisation de l’orientation des messages in-app pour iOS
platform: iOS
page_order: 3
description: "Cet article de référence explique comment définir l’orientation des messages in-app pour votre application iOS."
channel:
  - messages in-app

---

# Personnalisation de l’orientation

## Définir l’orientation pour tous les messages in-app

Pour définir une orientation fixe pour tous les messages in-app, vous pouvez définir la propriété `supportedOrientationMask` sur `ABKInAppMessageUIController`. Ajoutez le code suivant après l’appel de votre application à `startWithApiKey:inApplication:withLaunchOptions:` :

{% tabs %}
{% tab OBJECTIVE-C %}

```objc
// Configurer une orientation portrait fixe des messages in-app.
// Utiliser UIInterfaceOrientationMaskLandscape pour afficher les message in-app en mode paysage
id<ABKInAppMessageUIControlling> inAppMessageUIController = [Appboy sharedInstance].inAppMessageController.inAppMessageUIController;
((ABKInAppMessageUIController *)inAppMessageUIController).supportedOrientationMask = UIInterfaceOrientationMaskPortrait;
```

{% endtab %}
{% tab swift %}

```swift
// Configurer une orientation portrait des messages in-app
// Utiliser le mode portrait pour afficher les messages in-app en paysage
if let controller = Appboy.sharedInstance()?.inAppMessageController.inAppMessageUIController as? ABKInAppMessageUIController {
  controller.supportedOrientationMask = .portrait
}
```

{% endtab %}
{% endtabs %}

Ensuite, tous les messages in-app seront affichés dans l’orientation prise en charge, quelle que soit l’orientation du périphérique. Notez que l’orientation du périphérique doit également être prise en charge par la propriété `orientation` du message in-app à afficher.

## Définition de l’orientation par message in-app

Vous pouvez également définir l’orientation message par message. Pour ce faire, définissez un [délégué de message in-app][1]. Ensuite, dans votre méthode de délégation `beforeInAppMessageDisplayed:`, définissez la propriété `orientation` sur le `ABKInAppMessage` :

{% tabs %}
{% tab OBJECTIVE-C %}

```objc
// Configurer une orientation portrait des messages in-app
inAppMessage.orientation = ABKInAppMessageOrientationPortrait;

// Configurer une orientation paysage des inAppMessage
inAppMessage.orientation = ABKInAppMessageOrientationLandscape;
```

{% endtab %}
{% tab swift %}

```swift    
  // Configurer une orientation portrait des messages in-app
  inAppMessage.orientation = ABKInAppMessageOrientation.portrait

  // Configurer une orientation paysage des inAppMessage
  inAppMessage.orientation = ABKInAppMessageOrientation.landscape
```

{% endtab %}
{% endtabs %}

Les messages in-app ne s’affichent pas si l’orientation du périphérique ne correspond pas à la propriété `orientation` sur le message in-app.

{% alert note %}
Pour les iPads, les messages in-app apparaissent dans le style d’orientation préféré de l’utilisateur, quelle que soit l’orientation réelle de l’écran.
{% endalert %}

## Déclarations de méthode

Pour plus d’informations, voir le fichier d’en-tête suivant :

- [`ABKInAppMessage.h`][14]

[1]: {{site.baseurl}}/developer_guide/platform_integration_guides/ios/in-app_messaging/customization/setting_delegates/
[14]: https://github.com/Appboy/appboy-ios-sdk/blob/master/AppboyKit/include/ABKInAppMessage.h
