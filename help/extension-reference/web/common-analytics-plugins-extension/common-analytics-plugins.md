---
title: Common Analytics Plugins Extension
seo-title: Common Analytics Plugins Extension for Adobe Experience Platform Launch
description: Information about configuring the Common Analytics Plugins extension, and the options available when using this extension to augment the [!DNL Adobe Analytics] Extension.
seo-description: Common Analytics Plugins Extension for Adobe Experience Platform Launch
---

# Common Analytics Plugins Extension

Use this reference for information about configuring the Common Analytics Plugins extension, and the options available when using this extension to augment the [!DNL Adobe Analytics] Extension.

## Configure the Common Analytics Plugins extension

This section provides a reference for the options available when configuring the Common Analytics Plugins extension.

>[!IMPORTANT]
>
>The Common Analytics Plugins extension augments the [!DNL Adobe Analytics] extension. You must have the [!DNL Adobe Analytics] extension installed on your property for it to work. Additionally, you must make the tracker globally accessible in the [!DNL Adobe Analytics] extension.

No additional configuration is required at the extension level.

## Adding Plugins to the [!DNL Adobe Analytics] extension

In order to use the plugins provided in this extension, you must first initialize the plugins you intend to use in their own rule.

1. Create a new rule.
1. Add the Core - Library Loaded (Page Top) event.
1. Use either of the initialization methods below.

## Common Analytics Plugins extension action types

This section describes the action types available in the Common Analytics Plugins extension.

The Common Analytics Plugins extension provides the following actions:

* [Initialize](#initialize)
* [Initialize Plugin](#initialize-plugin)

### Initialize

>[!IMPORTANT]
>
>While this action is easier to implement, Adobe Consulting does not recommend that you use this action as it increases the weight of the plugin.

In this action, you are able to select each plugin you want to include in your implementation and save the changes. Select as many or as few as you intend to use during the implementation. Links to documentation on how to use each plugin and a brief description are provided in the Analytics [Plug-ins overview](https://docs.adobe.com/content/help/en/analytics/implementation/vars/plugins/impl-plugins.html).

### Initialize Plugin

These actions initialize the specific plugin you intend to use individually. To initialize all of the plugins you intend to use in your property, simply add the corresponding action to your rule and save the rule. While there is slightly more effort involved in configuring the extension this way, it provides greater code efficiency. As such, Adobe recommends this approach.
