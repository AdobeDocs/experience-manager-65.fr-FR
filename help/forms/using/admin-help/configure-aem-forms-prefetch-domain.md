---
title: Configurer AEM Forms pour prérécupérer des informations de domaine
description: Configurez AEM Forms pour prérécupérer les informations de domaine si le temps de réponse est plus lent en raison de groupes profondément imbriqués ou si vous faites partie de nombreux groupes.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 100%

---

# Configurer AEM Forms pour prérécupérer des informations de domaine {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Le temps de réponse peut être plus lent pour les personnes qui appartiennent à de nombreux groupes (par exemple, 500 ou plus) ou si les groupes sont profondément imbriqués (par exemple, 30 niveaux). Si vous rencontrez ce problème, vous pouvez configurer AEM Forms pour prérécupérer les informations de certains domaines.

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration]**.
1. Pour exporter le paramètre de configuration en cours dans un fichier, cliquez sur **[!UICONTROL Exporter]**, puis enregistrez le fichier de configuration dans un autre emplacement.
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

   Dans cet exemple, plusieurs domaines sont configurés pour la prérécupération. Les noms de domaine sont séparés par un « / ». Ceci est illustré dans l’exemple ci-dessus avec *Domain_Name1*, *Domain_Name2*, et *Domain_Name3*.

1. Pour importer le fichier mis à jour, dans User Management, cliquez sur **[!UICONTROL Configuration > Importer et exporter des fichiers de configuration]**.
1. Cliquez sur **[!UICONTROL Parcourir]** pour trouver le fichier, puis sur Importer et enfin sur **[!UICONTROL OK]**.
