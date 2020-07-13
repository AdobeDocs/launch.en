---
title: Adobe Audience Manager Extension
seo-title: Adobe Audience Manager Extension for Adobe Experience Platform Launch
description: Integrate the DIL code used by Audience Manager with your properties in Adobe Experience Platform Launch.
seo-description: Adobe Audience Manager Extension for Adobe Experience Platform Launch
---

# Adobe Audience Manager Extension

With the [!DNL Audience Manager] extension, you can integrate the DIL code used by [!DNL Audience Manager] with your properties in [!DNL Adobe Experience Platform] [!DNL Launch].

Use this reference for information about the options available when using this extension to build a rule.

>[!NOTE]
>
>This extension is not meant to be used for server-side forwarding of Adobe Analytics data. For server-side forwarding, use the [Adobe Analytics extension](adobe-analytics-extension.md).

## Configure the Adobe Audience Manager extension

If the [!DNL Adobe Audience Manager] extension is not yet installed, open your property, then click **[!UICONTROL Extensions > Catalog]**, hover over the [!DNL Adobe Audience Manager] extension, and click **[!UICONTROL Install]**.

To configure the extension, open the [!UICONTROL Extensions] tab, hover over the extension, and then click **[!UICONTROL Configure]**.

### DIL Settings

Configure your DIL settings. The following configuration options are available:

![](/help/assets/ext-aam-config.png)

#### DIL Version

Shows the Data Integration Library (DIL) version.

This setting cannot be changed.

#### Exclude Specific Paths

If the URL matches any of the excluded paths, the extension is not loaded.

Click **[!UICONTROL Add Path]** to specify an excluded URL.

Enable Regex if the URL is a regular expression.

#### Use DIL Site Catalyst Module

The [SiteCatalyst module](https://docs.adobe.com/content/help/en/audience-manager/user-guide/dil-api/dil-modules.html#sitecat-init) works with DIL to send Analytics tag elements to [!DNL Audience Manager].

Use the Code Editor to configure the siteCatalyst.init file.

You can also create a note containing information about this configuration.

#### Use DIL Google Analytics Module

Enable the [Google Analytics module](https://docs.adobe.com/content/help/en/audience-manager/user-guide/dil-api/dil-modules.html#ga-submit-universal-analytics).

#### DIL.create Initialization Properties

Add initialization properties used by [DIL.create](https://docs.adobe.com/content/help/en/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html#dil-create) and the namespace subproperty for the [visitorService object](https://docs.adobe.com/content/help/en/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html#visitor-service-props). Two sample use cases are included in the code comments, in the Code Editor.

Click **[!UICONTROL Choose an Item]** to add additional properties.

Hover over the "i" icons to learn what each property does. You can find more information for the properties in the [Audience Manager DIL documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/dil-api/class-level-dil-methods/dil-create.html#dil-create).

Click **[!UICONTROL Save]** when you have finished configuring the extension.

## Adobe Audience Manager extension action types

This topic describes the action types available in the [!DNL Audience Manager] extension.

The [!DNL Adobe Audience Manager] extension provides the following actions in the Then portion of a rule:

### Run Custom Code

Run the custom code configured in the Code Editor.

Enter the desired code in the Code Editor, then provide a name for the code. This code becomes available in the Then portion of the rule builder.

![](/help/assets/ext-aam-then.png)

You can also add a note with information about the configuration.
