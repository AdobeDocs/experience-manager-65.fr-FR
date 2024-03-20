---
title: Configuration de AEM forms pour la prérécupération des informations de domaine
description: Configurez AEM forms pour prérécupérer les informations de domaine si le temps de réponse est plus lent en raison de groupes profondément imbriqués ou si vous êtes membre de nombreux groupes.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 32%

---

# Configuration de AEM forms pour la prérécupération des informations de domaine {#configure-aem-forms-to-prefetchdomain-information}

Les utilisateurs peuvent avoir un temps de réponse plus lent s’ils appartiennent à de nombreux groupes (par exemple, 500 ou plus) ou si les groupes sont profondément imbriqués (par exemple, 30 niveaux). Si vous rencontrez ce problème, vous pouvez configurer AEM forms pour prérécupérer les informations de certains domaines.

1. Dans la console d’administration, cliquez sur **[!UICONTROL Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration]**.
1. Pour exporter le paramètre de configuration en cours dans un fichier, cliquez sur **[!UICONTROL Exporter]**, puis enregistrez le fichier de configuration dans un autre emplacement.
1. Ajoutez le noeud suivant (en gras) :

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

   Dans cet exemple, plusieurs domaines sont configurés pour la prérécupération. Les noms de domaine sont séparés par un &quot;/&quot;. Ceci est illustré dans l’exemple ci-dessus avec *Domain_Name1*, *Domain_Name2*, et *Domain_Name3*.

1. Pour importer le fichier mis à jour, dans User Management, cliquez sur **[!UICONTROL Configuration > Importer et exporter des fichiers de configuration]**.
1. Cliquez sur **[!UICONTROL Parcourir]** pour trouver le fichier, puis sur Importer et enfin sur **[!UICONTROL OK]**.
