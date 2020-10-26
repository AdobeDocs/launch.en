---
title: Getting started with Experience Platform Launch Server Side
seo-title: Getting started with Experience Platform Launch Server Side
description: Getting started with Experience Platform Launch Server Side
seo-description: Getting started with Experience Platform Launch Server Side
---

# Getting started with Experience Platform Launch Server Side (Beta)

>[!NOTE]
>
>This beta documentation describes features that are not yet publicly available. It is subject to change and might not be complete or correct.

To use Adobe Experience Platform Launch Server Side, data must be sent to Adobe Experience Platform Edge
Network using one of three options:

* Adobe Experience Platform Web SDK
* Adobe Experience Platform Mobile SDK
* Server-to-Server API (coming in H2 2021)

>[!NOTE]
>The Platform Web SDK and Platform Mobile SDK do not require deployment through Platform Launch Client Side. However, using Platform Launch Client Side to deploy these SDKs is the recommended approach.

After you send data to Edge network, you can toggle on Adobe solutions to send data there. To send data to
a non-Adobe solution, you need to set that up in Platform Launch Server Side.

## Prerequisites

* Platform Launch Server Side
* Adobe Experience Platform Web or Mobile SDK, configured to send data to Edge Network
* Data should be in Experience Data Model (XDM) (This mapping can be done server-side.)

## Create an XDM schema

In Adobe Experience Platform, create your schema.

1. Create a new schema by clicking “Create Schema” and selecting the `XDM ExperienceEvent` option.

1. Give the schema a name and short description.

1. You can add the “ExperienceEvent web details” mixin by clicking **[!UICONTROL Add]** next to **[!UICONTROL Mixins]**. 

    >[!NOTE]
    >
    >Multiple mixins can be added, if desired.

1. Save the schema and note the name you gave it.

For more information about schemas, see [Experience Data Model (XDM) System Help](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html).

## Create Platform Launch Server Side property

In Platform Launch, create a property of type "Edge."

1. Click **[!UICONTROL New property]**. 

1. Name the property. 

1. Choose the “Edge” platform type.

1. Click **[!UICONTROL Save]**.

After you create the property, go to the **[!UICONTROL Environments]** tab for the new property and make
note of the environment IDs. You can copy the Environment ID from the **[!UICONTROL Environments]** tab to paste it when
creating an Edge configuration, if the Adobe Org used in Edge Configuration differs from the Adobe Org used
in Platform Launch Server Side. Otherwise, you can select the environment from a drop-down menu.

## Create Edge Configuration

In Adobe Experience Platform Edge Configuration, create your edge configuration. You will need the Environment ID generated when you created the server-side property.

1. Open the Adobe Experience Platform Edge Configuration interface through Platform Launch, from the link in the left rail.

1. Click **[!UICONTROL New Edge Configuration]**.

1. Name the configuration and provide an optional description. 
    The description helps to identify configurations ina  list of several configurations. 

1. Click **[!UICONTROL Save]**.



## Enable Launch Server Side

Next, configure Edge Network to send data to Launch Server Side, and to other Adobe products.

1. In the Edge Configuration UI, select the property you created.

1. Select the Development, Production, or Staging environment.

    Or, to send data to a Launch Server Side environment outside the Adobe org, click **[!UICONTROL Switch to Advanced Mode] and paste in an ID. The ID is provided when you create a Server Side property.

1. Toggle on the necessary tools and configure as required.

    * Adobe Analytics requires a report suite ID.

    * Platform Launch Server Side requires an environment ID, which is the publish path for the Launch Server Side property.

After configuring, make note of the Environment IDs for the new property.

## Configure the Platform Web SDK extension for Platform Launch Client Side to send data to the Edge configuration that you created

In Platform Launch Client Side, create your property, then use the Adobe Experience Platform Web SDK extension to configure it.

1. Name the property.

    You can have multiple instances of Alloy. For example, you might have different pre- and post-paywall tracking properties.

1. Select the Org ID.

1. Select the Edge Domain.

See the [Web SDK extension documentation](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) for more configuration options.

## Create a Platform Launch Client Side rule to send data to Platform Web SDK

After all of the above is in place, you can build necessary data definitions, rules, and so on that leverage both Platform Launch Server Side and Platform Launch Client Side, but that need only a single request from the page.

Create a new page load rule using the Platform Web SDK extension and the “Send Event” action type:

1. Open the **[!UICONTROL Rules]** tab, then click **[!UICONTROL Create New Rule]**.

1. Name the rule.

1. Click the **[!UICONTROL Events Add]** icon.

1. Add an event by choosing an extension and one of the event types available for that extension, then
configure the settings for the event. 
    For example, select **[!UICONTROL Core - Window Loaded]**.

1. Add an action using the Platform Web SDK extension. Select **[!UICONTROL Send Event]** from the **[!UICONTROL Action Type]** list, select the desired Instance (Alloy instance configured earlier), and then select a data element to add to the XDM Data block within the Alloy hit.

1. The rest of the settings can be left as default for this example, so click **[UICONTROL Save]**.

For another example, you might create a rule that sends the data layer to Edge if the user hovers over a specified button.

## Summary

With the following in place, you can now create Platform Launch Server Side rules to forward data to
non-Adobe destinations.

* Experience Data Model schema (Note the name you gave it.)
* Platform Launch Server Side property (Keep track of the environment IDs.)
* Adobe Experience Platform Edge Configuration (Note the environment ID.)
* Platform Launch Client Side property
