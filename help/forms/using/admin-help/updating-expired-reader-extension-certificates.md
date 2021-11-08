---
title: Mise à jour des certificats du service d’extension de Reader expirés
description: 'Reader des documents étendus qui ne fonctionnent pas, mise à jour des certificats '
source-git-commit: a26e4fb53458beae9b259e5ee5dc74a95264f9e1
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 26%

---


# Mise à jour des certificats du service d’extension de Reader expirés {#Updating-expired-Reader-Extension-service-certificates}

Les clients Adobe Experience Manager Forms (AEM Forms) disposant de licences Adobe Managed Services ou On-premise Enterprise Base ont le droit d’utiliser le service Reader Extension. Le service permet à une entreprise de partager facilement des documents de PDF interactifs en étendant la fonctionnalité d’Adobe Reader avec des droits d’utilisation supplémentaires. Le service ajoute des droits d’utilisation à un document de PDF et active des fonctionnalités qui ne sont généralement pas disponibles lorsqu’un document de PDF est ouvert à l’aide d’Adobe Acrobat Reader DC, telles que l’ajout de commentaires à un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document PDF dont les droits sont activés dans Adobe Reader peut effectuer les opérations qui sont autorisées pour ce document.

Adobe tire parti d’une infrastructure à clé publique (PKI) pour émettre des certificats numériques à utiliser dans le cadre de l’activation de licences et de fonctionnalités. Adobe a émis des certificats sous l’autorité de certification &quot;Adobe Root CA&quot;, qui expirera le 7 janvier 2023. Cela entraîne l’expiration de tous les certificats émis sous cette autorité de certification. Une fois le certificat expiré, toutes les fonctionnalités qui dépendent des certificats ne fonctionnent plus. Par exemple, un document de PDF étendu au lecteur qui permet d’ajouter des commentaires à l’aide de Adobe Acrobat Reader cesse de fonctionner pour les clients après le 7 janvier 2023. Pour résoudre ce problème, l’administrateur du service Reader Extension, à l’aide d’anciens certificats, doit obtenir et réappliquer de nouveaux certificats émis par la nouvelle autorité de certification racine G2 Adobe à leurs documents de PDF (le lecteur étend les documents de PDF avec de nouveaux certificats).

L’expiration des certificats a un impact sur les piles AEM Forms on JEE et AEM Forms on OSGi. Les deux piles ont un ensemble d’instructions différent. Après la réunion du [conditions préalables](#Pre-requisites) et [obtention de nouveaux certificats](#obtain-the-certificates), en fonction de votre pile, sélectionnez l’un des chemins suivants :

* [Mise à jour des certificats pour un environnement AEM Forms on JEE](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [Mise à jour des certificats pour un environnement AEM Forms sur OSGi](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>Le document utilise les termes certificats et informations d’identification de manière interchangeable.

## Prérequis {#Pre-requisites}

La mise à jour des certificats nécessite l’utilisation d’actions disponibles sur la console d’administration AEM Forms et les API Reader Extension fournies par AEM Forms. Ce document est destiné aux utilisateurs et administrateurs maîtrisant l’utilisation des API Forms d’Adobe Experience Manager. Avant de commencer, assurez-vous que :

* l’utilisateur dispose de droits d’administrateur sur l’environnement AEM Forms sous-jacent.
* l’utilisateur a configuré la variable [environnement de développement](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html) et y a accès.
* obtenir les certificats.

### Obtention des certificats {#obtain-the-certificates}

Les informations d’identification des droits sont fournies sous la forme d’un certificat numérique contenant la clé publique, la clé privée et le mot de passe permettant d’accéder à ces informations.

Si votre entreprise achète une version de production d’extensions Reader, les informations d’identification des droits de production sont fournies par le site de licences d’Adobe (LWS). Les informations d’identification des droits de production sont propres à votre entreprise et permettent d’activer les droits d’utilisation spécifiques dont vous avez besoin.

Si vous avez obtenu Reader Extensions par l’intermédiaire d’un partenaire ou d’un fournisseur ayant intégré Reader Extensions à son logiciel, les informations d’identification des droits vous sont fournies par ce partenaire, lequel les a obtenues d’Adobe.

>[!NOTE]
>
>les informations d’identification des droits ne peuvent pas être utilisées pour la signature d’un document ni pour l’identification. Pour ces opérations, servez-vous d’un certificat autosigné ou d’un certificat d’identité obtenu auprès d’une autorité de certification.

Les types d’informations d’identification des droits suivants sont disponibles :

**Évaluation client**: Informations d’identification ayant une courte période de validité fournies aux clients qui souhaitent évaluer les extensions de Reader. Les droits d’utilisation appliqués aux documents utilisant ces informations d’identification expirent en même temps que les informations d’identification. Ce type d’informations d’identification n’est valide que pendant deux à trois mois.

**Production**: Informations d’identification ayant une longue période de validité fournies aux clients qui ont acheté le produit complet. Les certificats de production sont propres à chaque client, mais ils peuvent être installés sur plusieurs systèmes.

Si vous avez déjà utilisé des certificats pour étendre les fichiers de PDF, téléchargez un certificat de production à partir de [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

## Mise à jour et application de certificats pour un environnement AEM Forms on JEE {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

La mise à jour et l’application de nouveaux certificats sur la pile AEM Forms on JEE nécessite l’importation de nouvelles informations d’identification, la suppression des droits d’utilisation des documents de PDF existants et l’application de droits d’utilisation. Vous pouvez utiliser la console d’administration pour importer des informations d’identification et des API d’extension de Reader AEM Forms afin de supprimer et d’appliquer des droits d’utilisation.

### Importation et configuration des informations d’identification

Vous pouvez utiliser les pages Trust Store Management pour importer des informations d’identification nouvelles ou de remplacement. Trust Store peut contenir plusieurs informations d’identification d’extensions de Reader. Vous devez désigner l’un de ces jeux d’informations d’identification en tant que valeurs par défaut des informations d’identification de Reader Extensions. Les informations d’identification par défaut sont utilisées lorsqu’un utilisateur de Workbench ne parvient pas à déterminer quelles informations d’identification utiliser lors de la création du processus. Ces règles s’appliquent aux informations d’identification par défaut :

* Si vous importez des informations d’identification Reader Extensions et que Trust Store ne contient aucune autre information d’identification Reader Extensions, cette valeur est définie comme valeur par défaut.
* Si vous importez des informations d’identification Reader Extensions avec l’option Par défaut sélectionnée, le type par défaut est supprimé d’un jeu d’informations d’identification par défaut existant. Le jeu d’informations d’identification importé devient la valeur par défaut.
* Vous ne pouvez pas supprimer des informations d’identification Reader Extensions par défaut. Il vous faut au préalable définir un autre jeu d’informations d’identification comme valeur par défaut. Il existe néanmoins une exception à cette règle : s’il n’existe qu’un seul jeu d’informations d’identification, vous pouvez le supprimer, même s’il s’agit de la valeur par défaut.
* Vous ne pouvez pas mettre à jour des informations d’identification Reader Extensions par défaut.

Pour importer les informations d’identification :

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur Importer, puis sous Type de Trust Store, sélectionnez Informations d’identification des extensions d’Acrobat Reader DC.
1. (Facultatif) Pour indiquer qu’il s’agit des informations d’identification par défaut à utiliser avec les extensions d’Acrobat Reader DC, sélectionnez Par défaut.
1. Dans la zone Alias, saisissez un identificateur pour les informations d’identification. Cet identifiant sert de nom d’affichage aux informations d’identification dans les extensions d’Acrobat Reader DC. Il permet également d’accéder automatiquement aux informations d’identification via le SDK d’AEM Forms.
1. Cliquez sur Choisir un fichier pour accéder aux informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

Si le message d’erreur &quot;Échec de l’importation des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect&quot; s’affiche, vérifiez que le mot de passe est valide.

vous pouvez également importer et supprimer des informations d’identification automatiquement (Voir [Programmation avec AEM Forms](../../developing/credentials.md)).

### Suppression des droits d’utilisation des documents de PDF dont les droits sont activés

Supprimez les droits d’utilisation des documents de PDF activés pour les droits existants avant d’appliquer les droits d’utilisation avec les dernières informations d’identification. AEM Forms on JEE fournit des API pour supprimer les droits d’utilisation. Pour obtenir des instructions détaillées, voir [Suppression des droits d’utilisation des documents de PDF](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Pour supprimer les droits d’utilisation des processus AEM Forms on JEE développés dans Workbench, voir [Aide de Workbench](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Application des droits d’utilisation aux documents de PDF

Après avoir importé de nouvelles informations d’identification et supprimé les droits d’utilisation des documents de PDF activés pour les droits existants, appliquez les droits d’utilisation aux documents de PDF à l’aide des nouvelles informations d’identification. Vous pouvez appliquer des droits d’utilisation aux documents de PDF à l’aide de l’API client Java Acrobat Reader DC extensions et du service Web.  Pour plus d’informations, voir [Application des droits d’utilisation aux documents du PDF](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Mise à jour et application de certificats pour un environnement AEM Forms sur OSGi {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

La mise à jour et l’application de nouveaux certificats sur la pile AEM Forms on OSGi nécessite l’importation de nouvelles informations d’identification, la suppression des droits d’utilisation des documents de PDF existants et l’application de droits d’utilisation. Vous pouvez utiliser la console d’administration pour importer des informations d’identification et des API d’extension de Reader AEM Forms afin de supprimer et d’appliquer des droits d’utilisation.

### Importation des informations d’identification {#Import-credentials}

Dans un environnement AEM Forms on OSGi, des informations d’identification d’extension de Reader sont associées à l’utilisateur de fd-service. Avant d’ajouter des informations d’identification pour le magasin de clés fd-user, procédez comme suit pour créer un magasin de clés :

1. Connectez-vous à votre instance d’auteur AEM en tant qu’administrateur.
1. Accédez à **[!UICONTROL Outils ]**> **[!UICONTROL Sécurité ]**> **[!UICONTROL Utilisateurs]**.
1. Faites défiler la liste des utilisateurs jusqu’à ce que vous trouviez un compte utilisateur fd-service.
1. Cliquez sur **[!UICONTROL fd-service]** utilisateur.
1. Cliquez sur l’onglet KeyStore .
1. Cliquez sur **[!UICONTROL Créer un KeyStore]**.
1. Définissez le mot de passe d’accès KeyStore et enregistrez vos paramètres pour créer le mot de passe KeyStore.

Après avoir créé le KeyStore, ajoutez les informations d’identification à l’utilisateur de fd-service. La vidéo suivante explique les étapes :

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

La commande suivante répertorie les détails du fichier pfx. Avant d’exécuter la commande, accédez au répertoire contenant le fichier .pfx.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Par exemple, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx où 1005566.pfx est le nom de mon fichier pfx

### Suppression des droits d’utilisation des documents de PDF dont les droits sont activés

Supprimez les droits d’utilisation des documents de PDF activés pour les droits existants avant d’appliquer les droits d’utilisation avec les dernières informations d’identification. Vous pouvez supprimer les droits d’utilisation d’un document en appelant l’API removeUsageRights depuis l’API docAssuranceService. Pour plus d’informations, voir [Supprimer les droits d’utilisation](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights) document.

### Application des droits d’utilisation aux documents de PDF

Pour appliquer des droits d’utilisation dans un environnement AEM Forms on OSGi, créez un service OSGi personnalisé pour appliquer des droits d’utilisation aux documents. Vous pouvez également créer une servlet avec une méthode de POST pour renvoyer le PDF étendu Reader à l’utilisateur. Pour obtenir des instructions détaillées, voir [Application d’extensions de Reader](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html).

## Questions fréquentes

**Qui dois-je contacter si j’ai des questions supplémentaires ?**

Vous pouvez contacter [Prise en charge des Adobes](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou soulevez un ticket d’assistance.

**Que se passe-t-il si je n’ai pas mis à jour mon certificat avant le 7 janvier 2023 ?**

Lors de la tentative d’ouverture d’un Reader de documents de PDF étendu avec d’anciens certificats, les utilisateurs reçoivent un message d’erreur et ne peuvent plus accéder aux fonctionnalités étendues par le lecteur. Voici un exemple d’erreur.

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**Le nom de la nouvelle description a-t-il changé ?**

Les nouveaux certificats d’extension de Reader mentionnent G3-P24 comme nom de programme dans la description. Dans les anciens certificats, le nom de programme P24 a été mentionné dans la description.