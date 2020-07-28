---
title: Core Release Notes
seo-title: Core extension Release Notes in Adobe Experience Platform Launch
description: Release notes for the Adobe Experience Platform Launch core extension
seo-description: Release notes for the Adobe Experience Platform Launch core extension
---

# Core Extension Release Notes

## July 28, 2020

v1.8.3

* Fixed a bug where the CSP nonce was read only once upon extension startup instead of being pulled fresh during custom code action invocation.

## July 13th, 2020

v1.8.2

* Fixed a bug where the custom code action was throwing an error for HTML code that contains tokens without a tag name (eg. comments).

## July 10th, 2020

v1.8.1

* Fixed a bug where custom HTML entities inside attributes of `script` and `style` tags were not correctly decoded before being written to the page."
* Fixed a bug where an error happens when an external custom code action has no content. External custom code action is the action that is loaded from a different file than the library (this happens when the event triggering the rule is not libraryLoaded or pageBottom)

## July 6th, 2020

v1.8.0

* **Promises in Custom Code** - Custom Code conditions and JavaScript actions that do not execute in the global scope can now return Promises.  You can use them to have subsequent conditions and actions wait for the completion of an asynchronous process in your Custom Code before moving on to the next item.
* **Callbacks in HTML Custom Code Actions** - You can achieve the same thing in HTML Custom Code actions using the `onCustomCodeSuccess()` and `onCustomCodeFailure()` callbacks.

Please refer to the [Core Extension reference](./overview.md) in the Conditions > Custom Code and Actions > Custom Code for more detailed information.

## April 7th, 2020

v1.7.3

* **Text field length increase** - Text input fields were changed to a flex layout in order to better utilize the user’s screen width, and give more space for longer text strings.

## November 1st, 2019

v1.7.0

* **Access to `event` Variable Within Custom Code Data Element** - You can now reference the event from within a custom code data element when run within the context of a rule. The object will contain useful information about the event that triggered the rule. Many thanks to [Stewart Schilling](https://twitter.com/sdi_stewart) for this contribution.

## October 7th, 2019

v1.6.2

* **New “Constant” Data Element Type** - The Core extension now includes a new data element type called `Constant`.  This can be used when you need to store a constant value that will be referenced in various conditions, actions or custom code. Many thanks to [Jan Exner](https://twitter.com/jexner) for this contribution.

## September 11, 2019

v1.6.1

* **Support for CSP Nonce** - The Core extension now has an optional configuration parameter. You can add a data element that references a nonce. If configured, all inline scripts that Launch adds to the page use the nonce that you’ve configured. This change supports the use of a Content Security Policy with a nonce so that Launch scripts can still load in a CSP environment.  You can read more about using Launch with a CSP [here](https://docs.adobe.com/content/help/en/launch/using/reference/client-side-info/content-security-policy-csp.html).

## June 18, 2019

v1.5.0

* **Direct Call Logging** - Browser logging for direct call rules will now provide additional details when it is passed.

## May 8, 2019

v1.4.3

* **Input Fields** - Input fields are much longer now!
* **Custom Event** - Custom event type can now be used with events dispatched off of window.
* **Bug Fix** - fixed a bug where the Value Comparison Condition wouldn’t hold a 0 value.
* **Bug Fix** - exchange\_url field has been updated, so you can now see the Core Extension listing in Adobe Exchange.

## January 8, 2019

v1.4.2

* **Enters Viewport event** - Previously the Enters Viewport event would only trigger one time per page. This behavior can now be configured to trigger each time the element enters the viewport.
* **Custom Event event** - Custom Events can now contain contextual data that can be used inside of conditions and actions.
* **Click event** - When you set a link delay on the Click event, that will now register properly for descendants of the anchor and not just on the anchor itself.

## November 8, 2018

* **Persist Cohort option** - The option to persist a cohort has been added to the Sampling condition. This has the effect of keeping a user in or out of the sample cohort across sessions. For example, if the “persist cohort” checkbox is checked and the condition returns true the first time it is run for a given visitor, it will return true on all subsequent runs of the condition for the same visitor. Similarly, if the “persist cohort” checkbox is checked and the condition returns false the first time it is run for a given visitor, it will return false on all subsequent runs of the condition for the same visitor.
* **Bug Fix** - Fixed an issue where a rule using a Page Bottom event and a Custom Code action on a page where Launch was being loaded synchronously but improperly installed (no call to `_satellite.pageBottom()`) would clear website content.
* **Bug Fix** - Fixed an issue where the Enters Viewport would not function if the Launch library was loaded asynchronously and finished loading after the browser’s DOMContentLoaded event was fired.

## May 24, 2018

* **Feature** - Added a Value Comparison condition, this compares two values using any of several available operators. This replaces the functionality of several older conditions that were far too specific.
* **Feature** - Added a Max Frequency condition, this condition allows you to specify the number of times the condition should return true within a time period or event occurrence. Examples: 5 times per Day, 2 times per Visit.

## April 11, 2018

* **Feature** - Data elements can now reference other data elements.

## March 20, 2018

* **Bug fix** - Custom code windows were throwing `document.write` errors and not executing in async deployments
* **Bug fix** - Main modules were not included in a library
* **Bug fix** - Problems occurred with min and max values on the Random Number data element

## January 10, 2018

* **Feature** - Random Number Data Element
* **Feature** - Page Info Data Element
* **Feature** - Date Condition
* **Feature** - Sampling Condition

