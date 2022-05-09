---
title: Prepare your Microsoft 365 tenant
description: How to get started with Teams in Microsoft 365
ms.topic: how-to
ms.localizationpriority: high
keywords: Configure Microsoft 365 tenant Teams uploading
---

# Prepare your Microsoft 365 tenant

Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:

* Basic
* Standard
* Enterprise E1, E3, and E5
* Developer
* Education, Education Plus, and Education E5

> [!NOTE]
>
> * For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## Create your development environment

If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription. The subscription is free for 90 days and continues to renew as long as you are using it for development activity. If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits). It is active as long as your Visual Studio subscription is active. For more information, see [set up a Microsoft 365 developer subscription](/office/developer-program/office-365-developer-program-get-started).

## Enable Teams for your organization

Enable Teams for your organization and for more information, see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).

## Enable custom Teams apps and turn on custom app uploading

To turn on the custom app uploading or sideloading for your developer tenant:

1. Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.

2. Select **Show All** > **Teams**.

    ![Admin center menu](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > It can take up to 24 hours for the **Teams** option to appear. You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.

3. Navigate to **Teams apps** > **Setup Policies** > **Global**.

   ![Turn on sideload view](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Toggle **Upload custom apps** to the **On** position.

5. Select **Save**. Your test tenant can permit custom app sideloading.

    > [!Note]
    > It can take up to 24 hours for the sideloading to be active. In the interim, you can use **upload for \<your tenant>** to test your app. To upload the .zip package file of the app, see [upload custom apps](/microsoftteams/upload-custom-apps#upload).

    ![Upload app view](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

For complete information on how these settings interact, see [manage custom app policies and settings in Teams](/microsoftteams/teams-custom-app-policies-and-settings) and [manage app setup policies in Teams](/microsoftteams/teams-app-setup-policies).

## Next step

> [!div class="nextstepaction"]
> [Choose a test setup](~/concepts/build-and-test/debug.md)

## See also

[Add test data to your Microsoft 365 test tenant](~/concepts/build-and-test/test-data.md)
