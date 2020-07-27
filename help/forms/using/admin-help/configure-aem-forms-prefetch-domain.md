---
title: Configurer AEM Forms pour la prélecture des informations de domaine
seo-title: Configurer AEM Forms pour la prélecture des informations de domaine
description: Configurez AEM Forms pour prérécupérer les informations de domaine si vous rencontrez un délai de réponse plus lent en raison de groupes imbriqués profondément ou si vous êtes membre de nombreux groupes.
seo-description: Configurez AEM Forms pour prérécupérer les informations de domaine si vous rencontrez un délai de réponse plus lent en raison de groupes imbriqués profondément ou si vous êtes membre de nombreux groupes.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 72%

---


# Configurer AEM Forms pour la prélecture des informations de domaine {#configure-aem-forms-to-prefetchdomain-information}

Les utilisateurs appartenant à de nombreux groupes (500 ou plus par exemple) ou dont les groupes sont imbriqués profondément (30 niveaux) peuvent connaître un ralentissement du temps de réponse. Si vous rencontrez ce problème, vous pouvez configurer AEM Forms pour la prélecture des informations provenant de certains domaines.

1. In administration console, click **[!UICONTROL Settings > User Management > Configuration > Import And Export Configuration Files]**.
1. To export the current configuration setting to a file, click **[!UICONTROL Export]** and save the configuration file in another location.
1. Ajoutez le nœud suivant (en gras) :

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   Dans cet exemple, plusieurs domaines sont configurés pour la prélecture. Les noms de domaines sont séparés par un « / », comme le montre l’exemple ci-dessus avec *Domain_Name1*, *Domain_Name2* et *Domain_Name3*.

1. To import the updated file, in User Management, click **[!UICONTROL Configuration > Import And Export Configuration Files]**.
1. Click **[!UICONTROL Browse]** to find the file, click Import, and then click **[!UICONTROL OK]**.

