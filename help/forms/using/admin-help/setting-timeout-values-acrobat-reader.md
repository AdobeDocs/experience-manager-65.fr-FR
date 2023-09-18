---
title: Définition des valeurs de délai d’expiration à utiliser avec les extensions Acrobat Reader DC
description: Découvrez comment définir des valeurs de délai d’expiration à utiliser avec les extensions Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 26%

---

# Définition des valeurs de délai d’expiration à utiliser avec les extensions Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Lorsque vous travaillez sur de nombreux fichiers de PDF dans Acrobat Reader DC Extensions, assurez-vous que les valeurs de délai d’expiration suivantes sont définies de manière appropriée afin d’empêcher les tâches d’expirer ou d’échouer :

**Délai avant suppression du document**

Cette valeur peut être définie dans la console d’administration. Cliquez sur Paramètres > Paramètres de Core System > Configurations, puis spécifiez une valeur pour Délai d’expiration par défaut du partage des documents.

**Délai de gestion des utilisateurs dans AEM Forms :** cette valeur peut être définie en modifiant le fichier config.xml. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Importer et exporter des fichiers de configuration, puis cliquez sur Exporter. Ouvrez le fichier config.xml exporté et modifiez les lignes suivantes :

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Enregistrez le fichier config.xml, puis réimportez-le dans la console d’administration.

**Délai d’expiration de session du serveur d’applications :** cette valeur peut être définie sur le serveur d’applications. Pour plus d’informations, consultez la documentation de votre serveur d’applications.
