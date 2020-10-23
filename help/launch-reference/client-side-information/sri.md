---
title: Subresource integrity (SRI)
seo-title: Subresource integrity (SRI) in Adobe Experience Platform Launch
description: Subresource integrity (SRI) in Adobe Experience Platform Launch
seo-description: Subresource integrity (SRI) in Adobe Experience Platform Launch
---

# Subresource integrity (SRI) in Adobe Experience Platform Launch

Modern websites are built by referencing images, content, and scripts from various locations around the web. Sub-resource integrity (SRI) allows a browser to verify that the contents of a requested file have not been unexpectedly modified.

While their use cases compliment each other, SRI is different from a Content Security Policy (CSP), which ensures that only files from trusted sources are allowed on your website. SRI goes one step further by ensuring that the contents of these files match your expectations.

>[!NOTE]
>
>For more detailed information about SRI, refer to the [MDN web docs](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity).

The SRI validation process can be summarized as follows:

1. You generate a cryptographic hash of the asset that you want to validate.
1. On your website, the hash is placed in the HTML element that loads the file as the element's `integrity` attribute.
1. When the browser sees the `integrity` attribute, the browser requests the resource and independently generates its own version of the cryptographic hash.
1. The browser compares the `integrity` hash with the one it generated. If they match, the asset is allowed. If they do not match, the asset is blocked.

## Limitations in tag management systems

As a tag management system (TMS), [!DNL Launch] provides a compiled JavaScript library that you load onto your pages with a single `<script>` element (embed code). The dynamic functionality afforded by the TMS is accomplished by swapping out the contents of that script dynamically without requiring you to change anything else.

When the script contents change, however, so does the cryptographic hash of those contents. Therefore, the only way to make SRI work with a TMS is to update your embed code at the same time that you publish a new library. For many, this defeats the primary purpose of using a TMS in the first place.

The next best security option for [!DNL Launch] is to implement a Content Security Policy. For more information, see the guide on [CSPs in [!DNL Launch]](./content-security-policy-csp.md).

## Integrating SRI into library deployment

If you still wish to use SRI for your library builds, you must use self-hosting. If you are using Adobe-managed hosting, there is no way to use SRI without having some amount of time where the new library contents do not match the `integrity` attribute of the embed code.

Automating the process of updating your embed codes will vary in complexity depending on the structure of your site, but the general steps can be summarized as follows:

1. Retrieve the production library, either through SFTP delivery or downloading the archive from the user interface.
1. Generate the cryptographic hash of the main library.
1. Coordinate your site deployment so that the `integrity` attributes for all embed codes are updated to the new hash.

>[!IMPORTANT]
>
>This approach only covers the main [!DNL Launch] library. It does not include any of the smaller files that may exist.

## Next steps

This document covered the limitations of using SRI in [!DNL Launch], and the steps required to integrate it into your library deployments despite those limitations. If you have not already, it is strongly recommended that you read the guide on [CSPs in [!DNL Launch]](./content-security-policy-csp.md) for an alternative security option.