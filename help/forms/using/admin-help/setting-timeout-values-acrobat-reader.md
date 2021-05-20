---
title: Configuration des délais d’expiration à utiliser avec les extensions d’Acrobat Reader DC
seo-title: Configuration des délais d’expiration à utiliser avec les extensions d’Acrobat Reader DC
description: Découvrez comment définir des délais d’expiration à utiliser avec les extensions d’Acrobat Reader DC.
seo-description: Découvrez comment définir des délais d’expiration à utiliser avec les extensions d’Acrobat Reader DC.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 85%

---

# Configuration des délais d’expiration à utiliser avec les extensions d’Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Lorsque vous travaillez sur de nombreux fichiers PDF dans les extensions d’Acrobat Reader DC, configurez comme suit les valeurs de délai d’expiration suivantes pour éviter l’expiration et l’échec des travaux :

**Délai avant suppression du document**

vous pouvez définir cette valeur dans Administration Console. Cliquez sur Paramètres > Paramètres de Core System > Configurations, puis indiquez une valeur dans le champ Délai par défaut avant suppression du document.

**User Manager AEM forms Timeout :** cette valeur peut être définie en modifiant le fichier config.xml. Dans Administration Console, cliquez sur Paramètres > Gestion des utilisateurs > Configuration > Importer et exporter des fichiers de configuration, puis sur Exporter. Ouvrez le fichier config.xml exporté, puis modifiez les lignes ci-après de la façon suivante :

&lt;entry key= &quot;assertionValidityInMinutes&quot; value= &quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Enregistrez le fichier config.xml, puis réimportez-le dans Administration Console.

**Délai d’expiration de la session du serveur d’applications :** cette valeur peut être définie sur le serveur d’applications. Pour plus d’informations, consultez la documentation de votre serveur d’applications.
