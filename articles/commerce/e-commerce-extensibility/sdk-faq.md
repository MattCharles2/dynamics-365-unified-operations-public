---
# required metadata

title: Dynamics 365 Commerce online SDK FAQ
description: This topic summarizes answers to questions frequently asked by users of the Dynamics 365 Commerce online software development kit (SDK).
author: samjarawan
manager: annbe
ms.date: 11/04/2020
ms.topic: article
ms.prod: 
ms.service: dynamics-365-commerce
ms.technology: 

# optional metadata

# ms.search.form: 
audience: Developer
# ms.devlang: 
ms.reviewer: v-chgri
ms.search.scope: Retail, Core, Operations
# ms.tgt_pltfrm: 
ms.custom: 
ms.assetid: 
ms.search.region: Global
# ms.search.industry: 
ms.author: samjar
ms.search.validFrom: 2019-10-31
ms.dyn365.ops.version: Release 10.0.5

---
# Dynamics 365 Commerce online SDK FAQ

[!include [banner](../includes/banner.md)]

This topic summarizes answers to questions frequently asked by users of the Dynamics 365 Commerce online software development kit (SDK).

## After upgrading to module library version 9.24 (10.0.14 release), cloned modules that use data actions may display the error, "UserAuthorizationException. Customer account number on the request was wrong".

The following list of [core data actions](core-data-actions.md) have a signature change that moves the user account number parameter to the second parameter (instead of the first) and is now set as an optional parameter. In most scenarios where the user account number is no longer needed, the data action will execute in the context of the current signed-in user. In some custom scenarios where the user account number is different than the user account number of the signed-in user, you can fetch the user account number by using the **get-customer** data action and passing it to the data action.

Core data actions with signature changes include:
 
- **add-address**
- **get-address**
- **get-customer**
- **get-loyalty-card**
- **get-loyalty-transaction-estimation**
- **issue-loyalty**

The module library modules have been updated with the correct calling pattern to the above data actions, so you won't receive any errors in these modules. However, if one of the modules was previously [cloned](clone-starter-module.md) it will still have the older data action signature and display this error at runtime, "UserAuthorizationException. Customer account number on the request was wrong". The signatures will need to be updated accordingly. One way to resolve this issue is to temporarily clone the module library module again with a new name, then differentiate the new module code with the previously cloned custom module and merge the changes. The temporary module can then be deleted.

## Additional resources

[Core data actions](core-data-actions.md)

[Clone a module library module](clone-starter-module.md)

[Best practices for Dynamics 365 Commerce development](best-practices-dev.md)
