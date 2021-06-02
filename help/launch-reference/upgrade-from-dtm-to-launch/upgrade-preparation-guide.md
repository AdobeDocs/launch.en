---
title: Upgrade Preparation Guide
description: Follow this preparation guide to get started upgrading from Dynamic Tag Management (DTM) to Adobe Experience Platform Launch.
---

# Upgrade preparation guide

Adobe Experience Platform Launch is an entirely different system than DTM. Conceptually, they achieve the same goal, but the way they do so is different.

* The`_satellite`object looks different in [!DNL Platform Launch]  than it does in DTM.
* The relationships between extensions, rules, and data elements are also different than before.
* Some things that exist in both systems have moved to different locations or are accessed in different ways.

The [!UICONTROL Upgrade Assistant] creates a [!DNL Platform Launch]  property that works as closely as possible to the on-page behavior that you had in DTM. Refer to the following information about what moves and where it moves to in cases where the behavior differs from what you might expect.

Examples of differences that are further defined below:

* Rule components and data elements that aren't doing anything in your DTM property are not copied to [!DNL Platform Launch] .  Example: `Data Element` conditions defined by a data element that does not exist are not copied.
* Many conditions have been updated so the options available in the condition are slightly different in [!DNL Platform Launch] .  Example: The `Operating System` condition no longer supports Blackberry.
* Many resources are called something new in [!DNL Platform Launch] , so they are copied with the new name.  Example: `Page Top` events move to `Library Loaded` events.
* Many very specific conditions have been replaced by a more generic `Value Comparison` condition in [!DNL Platform Launch] .  This enables more options, provides consistency with all the comparison operators, and simplifies maintainance as well. Example: the `Cart Amount` condition has been replaced by the `Value Comparison` condition.

## Properties {#properties}

### Name {#name}

The name of your DTM property is copied to [!DNL Platform Launch] . `(DTM - yyyy-mm-dd hh:mm:ss)` is added to the end of the [!DNL Platform Launch]  property name so you know exactly when it was migrated. You can remove this timestamp from your [!DNL Platform Launch]  property name.

### Domains {#domains}

The domains on your DTM property are copied to [!DNL Platform Launch] .

If you have the same domain listed multiple times in DTM, it only appears on your [!DNL Platform Launch]  property once. Domains in [!DNL Platform Launch]  appear in lower case.

If you don't have at least one valid domain defined on your DTM property, it is not copied.

### Advanced Settings {#advanced-settings}

The advanced settings on your DTM property are copied to [!DNL Platform Launch] .

## Tools

When you upgrade to [!DNL Platform Launch] , the most commonly used DTM tools are converted into an installed [!DNL Platform Launch]  extension on your property.

### Adobe Analytics Tool {#adobe-analytics-tool}

#### Tool Selection {#tool-selection}

DTM allows you to install multiple instances of the Analytics tool to your property. [!DNL Platform Launch]  only allows a single instance of each Extension to be installed. Thus, only one Analytics tool is copied to [!DNL Platform Launch]  during the upgrade.

The tool instance that is copied is determined by transforming the names to lower case, then sorting alphabetically. Whichever tool comes first is the one that is copied.

You can control which tool instance to copy by changing the name of the tool.

#### App Measurement Version {#app-measurement-version}

DTM gives you several different options to deploy App Measurement. Each is supported in [!DNL Platform Launch] , so whichever method you use, you'll get the same method in [!DNL Platform Launch] .

If you're using `Managed by Adobe` in the DTM tool, be aware that it lets you select any of the five most recent versions of App Measurement. The Adobe Analytics extension for [!DNL Platform Launch]  uses the latest version of App Measurement, so depending on your selection there, copying to [!DNL Platform Launch]  may result in a different version of App Measurement being used. If you want the version to match, modify your DTM tool to use the same version as [!DNL Platform Launch]  before you upgrade.

#### Initial Beacon {#initial-beacon}

In DTM, an Analytics beacon is fired on every page when App Measurement loads, even if no rules have been defined. In [!DNL Platform Launch] , this beacon call is controlled by a rule and does not happen automatically. The upgrade process creates this rule for you unless you use the `Page code is already present` option in DTM. This rule is called "Migrated from DTM: Adobe Analytics - Send beacon on every page" and has the following definition:

* Event: `Page Bottom`  This most closely matches the DTM behavior even though [!DNL Platform Launch]  recommends`Library Load` rather than `Page Bottom` in most cases.
* Conditions: None
* Exceptions: None
* Actions: `Adobe Analytics - Send Beacon`

The Upgrade Assistant creates this rule in [!DNL Platform Launch] , as long as an Analytics tool is installed in DTM. If you used a `return false` inside custom code in DTM to suppress the initial beacon call, then you should leave the [!DNL Platform Launch]  rule out of your library (or delete it) after the upgrade is complete.

#### Other {#other}

Analytics tools that don't define a production report suite are not copied to [!DNL Platform Launch] .

Evars that don't match the pattern of `eVar\#\#` are not copied to [!DNL Platform Launch] .

### Experience Cloud ID Tool {#experience-cloud-id-tool}

The Experience Cloud ID tool is copied to [!DNL Platform Launch] . There are a few things you should know about that tool.

#### Extension Configuration {#extension-configuration}

Some variables in the DTM tool are not supported in the [!DNL Platform Launch]  extension. The following variables are copied to [!DNL Platform Launch] :

* audienceManagerServer
* audienceManagerServerSecure
* cookieDomain
* cookieLifetime
* cookieName
* disableThirdPartyCalls
* idSyncAfterIDCallResult
* idSyncAttachIframeOnWindowLoad
* idSyncContainerID
* idSyncDisable3rdPartySyncing
* disableThirdPartyCookies
* idSyncDisableSyncs
* disableIdSyncs
* idSyncIDCallResult
* idSyncSSLUseAkamai
* isCoopSafe
* loadSSL
* loadTimeout
* marketingCloudServer
* marketingCloudServerSecure
* overwriteCrossDomainMCIDAndAID
* resetBeforeVersion
* sdidParamExpiry
* serverState
* sessionCookieName
* takeTimeoutMetrics
* trackingServer
* trackingServerSecure
* allowlistIframeDomains
* allowlistParentDomain

Variables that do not have a value are not copied to [!DNL Platform Launch] .

#### Set Customer IDs {#set-customer-ids}

If the ECID tool configuration in DTM contains data in the `Customer Settings` section, that data is copied into a [!DNL Platform Launch]  rule. The [!DNL Platform Launch]  rule has the following definition:

* Event: `Library Loaded`
* Conditions: None
* Exceptions: None
* Actions: `Experience Cloud ID - Set Customer IDs`

Customer IDs that don't have names or values are not copied.

If no valid customer IDs are found, no [!DNL Platform Launch]  rule is created.

### Google Universal Analytics {#google-universal-analytics}

#### Tool Selection {#tool-selection-1}

DTM allows you to install multiple instances of the Google Universal Analytics tool to your property. [!DNL Platform Launch]  only allows a single instance of each extension to be installed. Thus, only one tool is copied to [!DNL Platform Launch]  during the upgrade.

The tool instance that is copied is determined by transforming the names to lower case, then sorting alphabetically. Whichever tool comes first is the one that is copied over.

You can control which tool instance to copy by changing the name of the tool.

#### Initial Beacon {#initial-beacon-1}

In DTM, a beacon is fired on every page even if no rules are defined. In [!DNL Platform Launch] , this beacon call is controlled by a rule and does not happen automatically. The Upgrade process creates this rule for you unless you use the `Google Universal Analytics page code is already present` option. This rule is called **Migrated from DTM: Google Universal Analytics - Send beacon on every page** and has the following definition:

* Event: `Core - Page Bottom` (This most closely matches the DTM behavior even though [!DNL Platform Launch]  recommends`Library Load` rather than `Page Bottom` in most cases.)
* Conditions: None
* Exceptions: None
* Actions: `Google Univeral Analytics - Send Page View`

#### Hit Callback {#hit-callback}

If you have added any JavaScript code in the Hit Callback section inside the Google Universal Analytics tool, the Upgrade Assistant creates a matching rule for you in [!DNL Platform Launch] . The rule is called `Migrated from DTM: Google Universal Analytics - Hit Callback` and has the following definition:

* Event: `Google Universal Analytics - Hit Callback`
* Conditions: None
* Exceptions: None
* Actions: `Core - Custom Code`

#### Rules Definition {#rules-definition}

If you defined rules in DTM where **Event Category** or **Event Action** are missing from the rule definition, these event details are not copied to [!DNL Platform Launch] .

If you defined rules in DTM where **Event Value** is not a number, these event details are not copied to [!DNL Platform Launch] .

### Tools that are not copied {#tools-that-are-not-copied}

The following DTM tools installed on your property are not copied to [!DNL Platform Launch]  extensions.

* Adobe Audience Manager
* Adobe Media Optimizer
* Adobe Target
* AEM ContextHub
* Nielsen
* Google Analytics

## Data Elements {#data-elements}

In DTM, if a data element resolves to a value that is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) (e.g., `""`, `0`, `false`, `null`, `undefined`), the data element will fall back to the configured default value. In [!DNL Platform Launch] , the data element will _only_ fall back to the configured default value if the resolved value is `null` or `undefined` .

### Cookie {#cookie}

`Cookie` data element types that don't contain a cookie name are not copied to [!DNL Platform Launch] .

### CSS Selector {#css-selector}

In [!DNL Platform Launch] , the CSS Selector data element type is called DOM Attribute, so your CSS Selector data elements types are copied into DOM Attribute data element types.

`CSS Selector` data element types that don't contain a selector are not copied to [!DNL Platform Launch] .

`CSS Selector` data element types that use the `get the value of Other Attribute`, but have specified an empty string, are not copied to [!DNL Platform Launch] .

### JS Object {#js-object}

`JS Object` data element types that don't contain a path are not copied to [!DNL Platform Launch] .

### URL Parameter {#url-parameter}

`URL Parameter` data element types that don't contain a parameter name are not copied to [!DNL Platform Launch] .

## Rule Events {#rule-events}

### Page Top {#page-top}

In [!DNL Platform Launch] , the DTM `Page Top` event type is called `Library Load`, so all your DTM rules with `Page Top` events become [!DNL Platform Launch]  rules with a `Library Load` event.

## Rule Conditions {#rule-conditions}

### Browser {#browser}

The Browser condition in [!DNL Platform Launch]  has removed support for some older browsers that were supported in DTM. Only supported values are copied to [!DNL Platform Launch] .

Supported values in [!DNL Platform Launch] :

* Chrome
* IE
* Firefox
* Safari
* Mobile Safari

Unsupported values in [!DNL Platform Launch] :

* Opera
* IE Mobile
* Opera Mini
* Opera Mobile
* OmniWeb

If you use a Browser condition that contains only values that are now unsupported, the condition is not copied to [!DNL Platform Launch] .

### Cart Amount {#cart-amount}

The DTM `Cart Amount` condition has been replaced by the `Value Comparison` condition in [!DNL Platform Launch] , so any `Cart Amount` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

DTM `Cart Amount` conditions that don't define a data element, or that define a data element that no longer exists, are not copied to [!DNL Platform Launch] .

### Cart Item Quantity {#cart-item-quantity}

The DTM `Cart Item Quantity` condition has been replaced by the [!DNL Platform Launch]  `Value Comparison` condition, so any `Cart Item Quantity` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

DTM `Cart Item Quantity` conditions that don't define a data element, or that define a data element that no longer exists, are not copied to [!DNL Platform Launch] .

### Data Element {#data-element}

The DTM `Data Element` condition has been replaced by the [!DNL Platform Launch]  `Value Comparison` condition, so any `Data Element` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

DTM `Data Element` conditions that don't define a data element (or that define a data element that no longer exists) are not copied to [!DNL Platform Launch] .

### Device {#device}

This condition does not exist in [!DNL Platform Launch]  and is not copied over.

### Logged In {#logged-in}

The DTM `Logged In` condition has been replaced by the `Value Comparison` condition in [!DNL Platform Launch] , so any `Logged In` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

DTM `Logged In` conditions that don't define a data element, or that define a data element that no longer exists, are not copied to [!DNL Platform Launch] .

### Operating System {#operating-system}

The [!DNL Platform Launch]  `Operating System` condition has removed support for some older operating systems that were supported in DTM. Only supported values are copied over to [!DNL Platform Launch] .

Supported values in [!DNL Platform Launch] :

* Windows
* MacOS
* Linux
* iOS
* Android
* Unix

Unsupported values in [!DNL Platform Launch] :

* Symbian OS
* Maemo
* Blackberry

If you use an Operating System condition that contained only values that are now unsupported, the condition is not copied to [!DNL Platform Launch] .

### Previous Converter {#previous-converter}

The DTM `Previous Converter` condition has been replaced by the `Value Comparison` condition in [!DNL Platform Launch] , so any `Previous Converter` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

### Registered User {#registered-user}

The DTM `Registered User` condition has been replaced by the `Value Comparison` condition in [!DNL Platform Launch] , so any `Registered User` conditions are copied to [!DNL Platform Launch]  as `Value Comparison` conditions.

## Rule Actions {#rule-actions}

### Custom Scripts {#custom-scripts}

The contents of custom scripts are copied over as is. The code is not inpected to determine its purpose. It is simply copied to custom code in [!DNL Platform Launch] . There are a few things you should know about this process:

* Any custom script in DTM (Non-sequential, Sequential JS, Sequential HTML) without content is not copied to [!DNL Platform Launch] .
* ES6 is not supported in [!DNL Platform Launch] .  ES6 is not supported in DTM either, but the compiler wouldn't catch it because it didn't exist when the DTM compiler was developed.   

  >[!IMPORTANT]
  >
  >If you use ES6 code in DTM, the code is copied to [!DNL Platform Launch] , but your build fails with compile errors when you make the build. You can fix this before or after you upgrade.
* In custom code, it is common to reference the `_satellite` object and various properties and functions that it provides. [!DNL Platform Launch]  uses the `satellite` object, but it is not structured the same as before. Functions and properties that were supported in DTM move to [!DNL Platform Launch] , but many of the ones that were unsupported do not. If you use any of these functions in DTM, it is likely that your custom code needs to be updated. To see what is supported on the new [!DNL Platform Launch]  `satellite` object, refer to the [[!DNL Platform Launch]  Object Reference.](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/launch-object-reference.html)
