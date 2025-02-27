---
title: "Integrate Dynamics 365 for Marketing with forms published on an external website (Dynamics 365 for Marketing) | Microsoft Docs"
description: "How to publish a form on an external site and capture the submissions in Dynamics 365 for Marketing"
keywords: marketing form, embed
ms.date: 04/01/2019
ms.service: dynamics-365-marketing
ms.custom: 
  - dyn365-marketing
ms.topic: article
applies_to: 
  - Dynamics 365 for Customer Engagement (online)
ms.assetid: 8c8063dc-3d69-46f3-9e11-722098542777
author: kamaybac
ms.author: kamaybac
manager: shellyha
ms.reviewer:
topic-status: Drafting
search.audienceType: 
  - admin
  - customizer
  - enduser
search.app: 
  - D365CE
  - D365Mktg
---

# Integrate with landing pages published on an external website

[!INCLUDE[pn-dynamics-365](../includes/pn-dynamics-365.md)] provides a complete solution for designing, publishing, and hosting landing pages on a [!INCLUDE[pn-microsoftcrm](../includes/pn-dynamics-365.md)] portal running on your [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] instance. However, you can also create or embed forms on your own external website that submit values back to [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)]. These external pages function similarly to native [!INCLUDE[pn-dynamics-365](../includes/pn-dynamics-365.md)] landing pages, so they will generate contacts and/or leads in your database when submitted. However, a few limitations apply, depending on how you implement the external forms.

There are two basic methods for integrating an external form page with [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)]:

- *Embed* a Dynamics 365 for marketing form on an external page
- Use *form capture* to integrate [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] with a form created externally

The third way of publishing a marketing page is to place a [native marketing form](marketing-forms.md) on a [native marketing page](create-deploy-marketing-pages.md) created and published by [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] on a [!INCLUDE[pn-microsoftcrm](../includes/pn-dynamics-365.md)] portal.

The following table summarizes the capabilities available with each of these approaches.

|   | Embedded marketing form | Captured external form | Native marketing page |
| --- | --- | --- | --- |
| Form design | Dynamics 365 | External/CMS | Dynamics 365 |
| Page design and publishing | External/CMS | External/CMS | Dynamics 365 |
| Form prefill | Yes | No | Yes |
| Subscription center functionality | Yes | No | Yes |
| Forward to a friend functionality | No | No | Yes |
| Link to forms from email messages | Yes | Yes | Yes |
| Launch inbound campaigns | Yes | Yes | Yes |
| Use form visits or submissions as criteria for journey triggers | Yes | Yes | Yes |
| Requires Dynamics 365 portal | No | No | Yes |
| Requires external website | Yes | Yes | No |
| Generate leads and/or contacts | Yes | Yes | Yes |
| Match and update leads and/or contacts | Yes | Yes | Yes |
| Requires form-capture script | No | Yes | No |
| Website-tracking script | Automatic | Recommended | Automatic |

<a name="embed-form"></a>

## Embed a Dynamics 365 for marketing form on an external page

An embedded form is a marketing form that you design using the [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] form designer, and which you then embed on an external page using JavaScript code generated for you.

<a name="create-embedded"></a>

### Create an embedded form

To design a form in Dynamics 365 for Marketing that you can embed on an external website:

1. In [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)], go to **Marketing** > **Internet marketing** > **Marketing forms**.

1. [Create the form](create-deploy-marketing-pages.md) and add the required fields to it as usual.

   - Configure all [field elements](content-blocks-reference.md#form-content-elements) just as you would with standard marketing forms.
   - Make [layout and style settings](design-digital-content.md#work-with-the-designer) just as you would with standard marketing forms.
   - You can use CSS on your external page to further style the imported marketing form. When you're done designing your form in [!INCLUDE[pn-dynamics-365](../includes/pn-dynamics-365.md)], open its **Designer** > **HTML** tab to see the CSS classes assigned to each element.

1. Save the form and go live.

1. On going live, a **Form hosting** tab appears. Open it.    
  ![The form hosting tab](media/marketing-form-hosting.png "The form hosting tab")

1. In the **Related marketing form pages** column, select **Add new form page** (open the ellipsis menu here to find this command if you don't see it). A quick-create flyout slides in. A _form page_ is a virtual page where you can make a few extra configuration settings for forms that will be embedded externally.

1. Use the quick-create form to set up your form options. The settings here are the same as those for a [form element](content-blocks-reference.md#the-form-element-for-marketing-pages) placed on a [!INCLUDE[pn-dynamics-365](../includes/pn-dynamics-365.md)] marketing page.

1. Select **Save** to create the new form page and go back to the **Form hosting** tab for your form.

1. If your form **does not** use prefill, then do the following:

    1. In the **Whitelist rules** column, select **Add new form whitelist rule** (open the ellipsis menu here to find this command if you don't see it). A quick-create flyout slides in. 

    1. In the **Name** field, enter the domain name of the website where you will host the form. You can whitelist as many domains as you want, but your form will only work on those domains that you whitelist.

1. If your form **does** use prefill (including all subscription center forms), then you must authenticate the domain(s) where you'll use the form rather than use the whitelist, so the **Whitelist rules** column isn't shown here for forms with prefill enabled. [!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Enable prefilling on embedded forms](#form-prefil)

1. Select the form page name in the **Related marketing form pages** column to open its settings and view the embed code.

1. Copy the embed code and paste it onto the page of your website where you want to use it.
     > [!NOTE]
     > Depending on what type of web server and CMS system you are using, you may need to adjust the code (for example, by escaping some special characters), or adjust your system settings to allow scripts such as this one to be pasted in. See your web server and CMS documentation for details.

<a name="form-prefil"></a>

### Enable prefilling on embedded forms

Form prefilling enables your forms to include prefilled values for known contacts. Prefilling makes your forms easier for contacts to use and can therefore help to increase your submission rates. The feature uses cookies to identify contacts that have previously submitted a form or opened a subscription center using a personalized link sent in email.

Because form prefilling requires the form to fetch contact values from your [!INCLUDE[pn-microsoftcrm](../includes/pn-microsoftcrm.md)] database, a few extra security measures are in place to help protect contacts' privacy. This means that contacts need to opt-in for form prefilling and that you must authenticate each external domain where you'll embed the form. The solution only allows prefilled values to be shown to contacts whose contact record has the _allow-prefill_ flag set. Contacts can set or clear their allow-prefill flag themselves using a landing any page form, provided the form includes the setting. [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] users can also edit a contact record directly to edit this setting for that contact.

To create a form with prefilling that you can embed on an external website:

1. Set up domain authentication for the external domain (website) where you will host your form and be sure to mark the **Enable prefilled forms** check box. You don't need to also enable email authentication on that domain, but you can. For instructions, see [Authenticate your domains](marketing-settings.md#authenticate-your-domains).

    ![Enable prefilling on an authenticated domain](media/authenticated-domains-prefill.png "Enable prefilling on an authenticated domain")

1. Create a form with the required fields and design elements as described in [Create, view, and manage marketing forms](marketing-forms.md).

1. Enable prefilling for the form as described in [Enable prefilling for forms](form-prefill.md).

1. Save the form and then go to the **Form hosting** tab (first available on save) to set up a _form page_ for it as described in [Create an embedded form](#create-embedded). Note that you don't need to add authenticated domains to the whitelist on the **Form hosting** tab because authenticated domains provide even better security than the whitelist provided here.

1. As described in [Create an embedded form](#create-embedded), copy the JavaScript code generated for the new form page and paste it onto a web page or CMS page for your website.

### Embed a subscription center as a hosted form

You can embed a subscription center form on an external site just as you can a standard landing page form. The only difference is that you must set the **Form type** to **subscription center**. Subscription centers require prefilling, so you must authenticate your external domain, set up the form, and embed the generated form code on your page as described in the previous section.

<a name="form-capture"></a>

## Use form capture to integrate a form created externally

Form capture makes it possible for forms created on an external website to submit information directly to [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)]. The resulting solution works just like a native marketing page created in the marketing app, except that prefill isn't supported. This makes it easier for page designers to create forms that match the rest of their site's graphical design and features, and which also submit values to [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)].

To enable form capture, you must generate a form-capture JavaScript in [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] and add that script to your external form page. Then you'll be able to load that page into [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] to map its fields to marketing fields. At run time, the form-capture JavaScript captures each form submission and submits the values to [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] for processing and storage.

> [!NOTE]
> The form capture feature currently ignores hidden input fields (`<input type="hidden">`) in the target form. One way to work around this is to change the hidden field to use a type other than hidden, and then add a style attribute to hide it, such as:<br>`<input type="text" style="visibility:hidden" name="field name" id="fieldID" />`

### Capture a new external form

To set up a form capture:

1. Use your CMS system and other coding tools to design a page with an input form that has the required fields and features.

1. Sign in to [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] and go to **Marketing** > **Internet Marketing** > **Marketing form fields**. Each of the records listed here establishes a mapping between a field available for use in a marketing form and an actual field from the contact and/or lead entity in the underlying database. Check to make sure that each of the fields required by your external form is correctly mapped here, and add any missing fields if necessary. [!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Create and manage input fields for use in forms](marketing-fields.md)

1. Go to **Marketing** > **Internet Marketing** > **Websites**. Each of the website records listed here (if any) provides both a website-tracking and form-capture code for a specific website or sub-site.

1. Find the website you want to work with, or select **New** to create a new one.

1. Your new or existing website record opens. Here you can enter and read information and settings for your website. You'll also find results and analytics gathered for the current site so far (if any). The following settings and information are most important when setting up a website for form capture:

   - **Name**: Shows a name for the website record, which you'll see in the list view and anywhere else you need to identify the record.
   - **URL**: Shows the address of the site (or sub-site) where you'll use the codes generated by this record. This isn't required, nor is it used in the generated codes, but this can be important information to help you and other users know where the code is being used.

1. If you're working with a new website record, then select **Save** on the command bar to generate the website-tracking and form-capture codes. After you've saved the record at least once, you'll see the following:
   - **JavaScript code**: This is the website-tracking code, which you must copy onto each webpage (or CMS template) for which you want to track page visits and clicks. [!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Monitor how visitors use your website](register-engagement.md#monitor-visitors)
   - **Form capture code**: This is the form-capture code, which you must copy onto each webpage (or CMS template) that includes a form that you want to capture for use with [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)].

    Take a copy of each of these codes, or keep this page open as you continue with this procedure.

1. Return to your externally designed form page and paste the form-capture code you found anywhere in the `<body>` of the page. The page should usually also include a website-tracking code because this will enable [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] to collect visitor insights and customer journey triggers to react to page visits or submissions. If your CMS page templates are already set up to place a website-tracking code, then don't add a new one, but if they aren't consider adding the website-tracking code too. <!-- [kamaybac] confirm details about tracking code -->

1. Publish your form page to make it available over the internet. Note its URL.

1. In [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)], go to **Marketing** > **Internet Marketing** > **Marketing forms**.

1. Select **New form capture** on the command bar to create a new marketing form that captures information submitted through a form on your external site.

1. A new from-capture marketing-form record opens, showing the **Designer** > **Enter form detail** tab. Enter the **Form URL** for your external form page and then select **Next**.    
    ![Enter the page URL for your external form](media/form-capture-url.png "Enter the page URL for your external form")

    > [!IMPORTANT]
    > The page at the URL you specify here must include exactly one form-capture script, and it must use a website ID for a website record saved on the same [!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] instance as the marketing form you are creating. If you see an error, then check your page to make sure it contains the correct script.

1. The  **Designer** > **Select form** tab opens. If the page at your URL includes more than one form, then each available form is listed here. You must create a marketing-form record for each form, so if you do have more than one form then you must pick just one of them to link to the current marketing-form record. A **Fields preview** for the selected form is provided, which may help you identify the form you want. Choose a form (if needed) and then select **Next** to continue.    
    ![Choose a form from the target page](media/form-capture-select-form.png "Choose a form from the target page")

1. The  **Designer** > **Map fields** tab opens. Each field from the external form is listed here using its external label. Map each **Source field** shown here to a marketing-form field in the **Dynamics 365 field** column.    
    ![Map form fields](media/form-capture-map-fields.png "Map form fields")

    > [!NOTE]
    > You should already have created all the required marketing-form fields at the start of the procedure, but you can also quick-create missing marketing-form fields from here if needed by selecting **New** from any of the lookup fields in the **Dynamics 365 field** column.

    > [!NOTE]
    > Each lookup field only allows you to choose from marketing form fields that have the same type as the external field. If you can't find the form field you are looking for, it could be because the types don't match. In this case, either change your external form to use the field type expected by the existing form field, edit the form field type, or create a new form field.

    > [!NOTE]
    > If your external form has changed since you last captured it, select **Rescan** here to load the latest field list.

1. Go to the **Summary** tab and finish setting up your marketing form just as you would a native marketing form. Be sure to provide a **Name** that makes sense, decide whether to update contacts, leads, or both, and choose your matching strategies for finding existing records to update. [!INCLUDE[proc-more-information](../includes/proc-more-information.md)] [Form summary and configuration](marketing-forms.md#form-summary)

    > [!NOTE]
    > Form-capture forms don't support prefill, so don't try to set up prefilling for them.

1. Select **Save** on the command bar to save your marketing form.

1. Select **Go live** on the command bar to activate your new marketing form so that it can begin to accept data from your external form.

### Edit a live form-capture form

When a form-capture form is live, all it's settings are read only. If you update your external form or need to edit your form-capture form for any reason, do the following:

1. Open the relevant marketing form record.
1. Select **Edit** on the command bar to put the record into live-edit mode. (The form remains active in this mode.)
1. You can now make changes on the **Summary** tab as needed, but the field mappings on the **Design** tab remain locked. If you need to edit the field mappings, select **Sync form** on the command bar to load the latest version of your external form and unlock these settings.
1. Select **Save** on the command bar when you're done editing the record. Your changes are saved and the form goes live again automatically. (Select **Cancel edit** to discard your unsaved changes and go back to the live state.)

## Reference hosted or captured forms in emails and customer journeys

Once you have a captured or hosted form set up, you're ready to start using it in your marketing emails and customer journeys. Here, both hosted and captured forms work in exactly the same way.

### Link to an external form from an email message

Unlike local landing pages, there is no [design element](content-blocks-reference.md) dedicated to external forms. Therefore, use either a button element or a standard text link to link to your embedded form using its page URL from your webserver.

### Use external forms with journey triggers

[!INCLUDE[pn-marketing-business-app-module-name](../includes/pn-marketing-business-app-module-name.md)] includes a _marketing form_ tile for customer journeys. It works just like the marketing page tile, both to enable customer journey triggers to react to form visits and submissions, and to create inbound campaigns.

To set up a journey that invites contacts to visit an external form and then reacts to form visits and/or submissions:

1. Create and go live with a [marketing email message](email-design.md) that includes a link to the page where you are hosting the form.

1. Create a customer journey as usual.

1. Start the journey with a segment that targets the contacts you want to invite to visit your landing page.

1. At the location where you want the journey to send the message, add a **Marketing email message** tile that references your message.

1. Drag a **Marketing form** tile from the **Toolbox** onto your **Marketing email** message tile to add the form as a child of that message. Then follow this message tile with a **Trigger** tile.

    ![Marketing-form and trigger tiles](media/journey-host-form-trigger1.png "Marketing-form and trigger tiles")

1. Expand the Marketing email message tile to see the **Marketing form** tile you just added to it. Select the **Marketing form** tile, open the **Properties** panel, and configure it to reference the form record that created the JavaScript (form page) you have embedded on your external site.

    ![Assign a form page to the form tile](media/journey-host-form-trigger2.png "Assign a form page to the form tile")

1. Select the **Trigger** tile and open its **Properties** panel.

1. Select **New** next to the **Set rules** heading in the trigger properties.

    ![Trigger properties](media/journey-host-form-trigger3.png "Trigger properties")

1. A new rule is added to the trigger. Set the **Source** to the name of the **Marketing form** tile that you added to the **Marketing email message** tile, and set the **Condition** to **Marketing form visited** (to trigger when a contact loads the form) or to **Marketing form contact registered** (to trigger when a contact submits the form).

    ![Conditions for a form-based trigger](media/journey-host-form-trigger4.png "Conditions for a form-based trigger")

1. Continue designing your customer journey as required.

1. Save and go live.

### Use external forms with inbound campaigns

You can create an inbound campaign by placing a **Marketing form** tile at the start of a journey, and then configure the tile to reference the marketing-form record that created the embedded or captured form you are using on your external site. This will cause each contact that submits the form to be added to the journey, just as though they had joined a segment targeted by the journey. You could already [do something similar for marketing pages hosted on a Dynamics 365 portal](create-inbound-customer-journey.md), but now you can also do it with an externally hosted marketing forms.

![Inbound campaign from a hosted form](media/journey-host-form-trigger5.png "Inbound campaign from a hosted form")