---
title: Créer le modèle de page AEM personnalisé avec des composants de formulaire Adobe Campaign
description: Créer un modèle de page personnalisé qui utilise des composants de formulaire Adobe Campaign
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: de5c634a-c0d7-4e69-b941-d2fbfe83117d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 100%
---

# Créer le modèle de page AEM personnalisé avec des composants de formulaire Adobe Campaign{#creating-custom-aem-page-template-with-adobe-campaign-form-components}

Cette page vous explique comment créer un modèle de page personnalisé qui utilise des composants [Formulaire Adobe Campaign](/help/sites-authoring/adobe-campaign-components.md) en examinant le mode d’implémentation du modèle Geometrixx-outdoors (`/apps/geometrixx-outdoors/components/page_campaign_profile`). Elle vous donne également des informations importantes dont vous pourriez avoir besoin lors de la création de votre propre modèle personnalisé.

>[!CAUTION]
>
>Les composants d’e-mail AEM ont été abandonnés. En raison de la nature de l’e-mail, qui fusionne contenu et style, les composants d’e-mail fournis prêts à l’emploi par AEM ne sont que rarement réutilisés, car il est nécessaire de mettre en œuvre des styles personnalisés dans les composants requis pour les projets.
>
>Les composants d’e-mail peuvent être implémentés au niveau du projet. Les composants d’e-mail AEM obsolètes illustrent la manière dont cela peut être réalisé. Toutefois, n’utilisez pas ces composants obsolètes sur les projets.


Pour créer un modèle de page AEM personnalisé à l’aide des composants de formulaire Adobe Campaign, assurez-vous que vous disposez des éléments suivants :

1. **resourceSuperType correct**

   Assurez-vous que le composant de page hérite de `mcm/campaign/components/profile`.

   Cela est nécessaire pour que les servlets obtiennent et enregistrent des informations.

   * `com.day.cq.mcm.campaign.servlets.TemplateListServlet`
   * `com.day.cq.mcm.campaign.servlets.SaveProfileServlet`

   ![chlimage_1-201](assets/chlimage_1-201.png)

1. **Paramètres de ClientContext**

   Lorsque vous observez les paramètres de ClientContext (`/etc/designs/geometrixx-outdoors/jcr:content/page_campaign_profile`), vous voyez ceci :

   * ClientContext pointe vers `/etc/clientcontext/campaign`.
   * Il existe également un nœud *config* supplémentaire.

   ![chlimage_1-202](assets/chlimage_1-202.png)

1. **head.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/head.jsp)**

   Dans **head.jsp**, les lignes suivantes qui utilisent **clientcontext-config** et **cloudservice-hook** :

   ```
   <cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub"/>
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
   ```

1. **body.jsp (/apps/geometrixx-outdoors/components/page_campaign_profile/body.jsp)**

   Dans le fichier **body.jsp**, les Cloud Services sont chargés au bas de la page :

   ```
   <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
   ```

1. **Propriétés de page Campaign**

   Pour pouvoir sélectionner un modèle Adobe Campaign, les propriétés de page sont étendues avec l’onglet **Campagne** :

   `/apps/geometrixx-outdoors/components/page_campaign_profile/dialog/items/tabs/items/campaign`

   ![chlimage_1-203](assets/chlimage_1-203.png)

1. **Paramètres de modèle**

   Les valeurs par défaut suivantes sont affichées dans le modèle (`/apps/geometrixx-outdoors/templates/campaign_profile/jcr:content`) :

   | **acMapping** | mapRecipient (pour Adobe Campaign 6.1), profile (pour Adobe Campaign Standard) |
   |---|---|
   | **acTemplateId** | courrier |

   ![chlimage_1-204](assets/chlimage_1-204.png)
