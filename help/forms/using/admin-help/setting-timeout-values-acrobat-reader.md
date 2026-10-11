---
title: Configuration des délais d’expiration à utiliser avec Extensions Acrobat Reader DC
description: Découvrez comment définir des délais d’expiration à utiliser avec les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%
---
# Configuration des délais d’expiration à utiliser avec Extensions Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Lorsque vous travaillez sur de nombreux fichiers PDF dans Extensions Acrobat Reader DC, configurez comme suit les valeurs de délai d’expiration suivantes pour éviter l’expiration et l’échec des travaux :

**Délai d’expiration avant suppression du document**

Cette valeur peut être définie dans la console d’administration. Cliquez sur Paramètres > Paramètres de Core System > Configurations, puis indiquez une valeur dans le champ Délai d’expiration par défaut avant suppression du document.

**Délai d’expiration de gestion des utilisateurs dans AEM Forms :** cette valeur peut être définie en modifiant le fichier config.xml. Dans la console d’administration, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration, puis sur Exporter. Ouvrez le fichier config.xml exporté, puis modifiez les lignes ci-après de la façon suivante :

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Enregistrez le fichier config.xml, puis réimportez-le dans la console d’administration.

**Délai d’expiration de session du serveur d’applications :** cette valeur peut être définie sur le serveur d’applications. Pour plus d’informations, consultez la documentation de votre serveur d’applications.
