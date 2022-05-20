---
title: Mettre à jour des certificats expirés du service Reader Extension
description: 'Les documents étendus par Reader ne fonctionnent pas, mettre à jour les certificats '
source-git-commit: a26e4fb53458beae9b259e5ee5dc74a95264f9e1
workflow-type: ht
source-wordcount: '1581'
ht-degree: 100%

---


# Mettre à jour des certificats expirés du service Reader Extension {#Updating-expired-Reader-Extension-service-certificates}

Les clients Adobe Experience Manager Forms (AEM Forms) disposant de licences Adobe Managed Services ou On-premise Enterprise Base ont le droit d’utiliser le service Reader Extension. Le service permet à une entreprise de partager facilement des documents PDF interactifs en étendant la fonctionnalité d’Adobe Reader avec des droits d’utilisation supplémentaires. Le service ajoute des droits d’utilisation à un document PDF et active des fonctionnalités qui ne sont généralement pas disponibles à l’ouverture d’un document PDF dans Adobe Acrobat Reader DC, comme l’ajout de commentaires dans un document, le remplissage de formulaires et l’enregistrement du document. Les utilisateurs tiers n’ont pas besoin de disposer d’un logiciel supplémentaire ni de modules externes pour utiliser les documents définis avec des droits d’utilisation. Les documents PDF dotés de droits d’utilisation sont appelés des documents dont les droits sont activés. Un utilisateur qui ouvre un document PDF dont les droits sont activés dans Adobe Reader peut effectuer les opérations qui sont autorisées pour ce document.

Adobe exploite une infrastructure à clé publique (PKI) pour émettre les certificats numériques à utiliser dans le cadre de l’activation de licences et de fonctionnalités. Adobe a émis des certificats sous l’autorité de certification « Adobe Root CA », qui arrivera à expiration le 7 janvier 2023. Dès lors, tous les certificats émis sous cette autorité de certification arriveront également à expiration. Une fois le certificat expiré, toutes les fonctionnalités qui en dépendent ne fonctionneront plus. Par exemple, un document PDF étendu par Reader qui permet d’ajouter des commentaires à l’aide d’Adobe Acrobat Reader cessera de fonctionner pour les clients après le 7 janvier 2023. Pour résoudre ce problème, l’administrateur du service Reader Extension, à l’aide d’anciens certificats, doit obtenir et réappliquer de nouveaux certificats émis par la nouvelle autorité de certification racine G2 d’Adobe dans ses documents PDF (étend les documents PDF pour Reader avec de nouveaux certificats).

L’expiration des certificats a un impact sur les piles AEM Forms sur JEE et AEM Forms sur OSGi. Ces deux piles comportent un ensemble d’instructions différent. Dès que vous respectez les [conditions préalables](#Pre-requisites) et que vous [disposez des nouveaux certificats](#obtain-the-certificates), en fonction de votre pile, sélectionnez l’un des chemins suivants :

* [Mise à jour des certificats pour un environnement AEM Forms sur JEE](#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment)
* [Mise à jour des certificats pour un environnement AEM Forms sur OSGi](#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment)

>[!NOTE]
>
>Dans ce document, les termes « certificats » et « informations d’identification » sont utilisés de manière interchangeable.

## Prérequis {#Pre-requisites}

La mise à jour des certificats nécessite l’utilisation d’actions disponibles sur la console d’administration AEM Forms et les API Reader Extension fournies par AEM Forms. Ce document est destiné aux utilisateurs et aux administrateurs maîtrisant l’utilisation des API Adobe Experience Manager Forms. Avant de commencer, vérifiez les points suivants :

* L’utilisateur dispose de droits d’administrateur sur l’environnement AEM Forms sous-jacent.
* L’utilisateur a configuré l’[environnement de développement](https://experienceleague.adobe.com/docs/experience-manager-65/developing/devtools/howto-projects-eclipse.html?lang=fr) et y a accès.
* Vous disposez des certificats.

### Obtention des certificats {#obtain-the-certificates}

Les informations d’identification des droits sont fournies sous la forme d’un certificat numérique contenant la clé publique, la clé privée et le mot de passe permettant d’accéder à ces informations.

Si votre entreprise achète une version de production de Reader Extensions, les informations d’identification des droits de production sont fournies par Adobe Licensing Website (LWS). Les informations d’identification des droits de production sont propres à votre entreprise et permettent d’activer les droits d’utilisation spécifiques dont vous avez besoin.

Si vous avez obtenu Reader Extensions par l’intermédiaire d’un partenaire ou d’un fournisseur ayant intégré Reader Extensions à son logiciel, les informations d’identification des droits vous sont fournies par ce partenaire, lequel les a obtenues d’Adobe.

>[!NOTE]
>
>les informations d’identification des droits ne peuvent pas être utilisées pour la signature d’un document ni pour l’identification. Pour ces opérations, servez-vous d’un certificat autosigné ou d’un certificat d’identité obtenu auprès d’une autorité de certification.

Les types d’informations d’identification des droits suivants sont disponibles :

**Informations d’identification d’évaluation** : informations d’identification ayant une courte période de validité fournies aux clients souhaitant évaluer Reader Extensions. Les droits d’utilisation appliqués aux documents utilisant ces informations d’identification expirent en même temps que les informations d’identification. Ce type d’informations d’identification n’est valide que pendant deux à trois mois.

**Production** : informations d’identification ayant une longue période de validité fournies aux clients qui ont acheté le produit complet. Les certificats de production sont propres à chaque client, mais ils peuvent être installés sur plusieurs systèmes.

Si vous avez déjà utilisé des certificats pour étendre les fichiers PDF pour Reader, téléchargez un certificat de production à partir de [Adobe Licensing Website (LWS)](https://licensing.adobe.com/).

## Mise à jour et application de certificats pour un environnement AEM Forms sur JEE {#Updating-and-Applying-certificates-for-an-AEM-Forms-on-JEE-environment}

La mise à jour et l’application de nouveaux certificats sur la pile AEM Forms sur JEE nécessite l’importation de nouvelles informations d’identification, la suppression des droits d’utilisation des documents PDF existants et l’application de droits d’utilisation. Vous pouvez utiliser la console d’administration pour importer des informations d’identification et des API d’extension de Reader AEM Forms afin de supprimer et d’appliquer des droits d’utilisation.

### Importer et configurer des informations d’identification

Vous pouvez utiliser les pages Trust Store Management pour importer des informations d’identification nouvelles ou de remplacement. Trust Store peut comporter plusieurs jeux d’informations d’identification des extensions Reader. Vous devez désigner l’un de ces jeux d’informations d’identification en tant que valeurs par défaut des informations d’identification de Reader Extensions. Les informations d’identification par défaut sont utilisées lorsqu’un utilisateur de Workbench ne parvient pas à déterminer quelles informations d’identification utiliser lors de la création du processus. Ces règles s’appliquent aux informations d’identification par défaut :

* Si vous importez un jeu d’informations d’identification pour les extensions Reader et que Trust Store n’en comporte pas d’autres, il est défini comme valeur par défaut.
* Si vous importez un jeu d’informations d’identification pour les extensions Reader avec l’option Par défaut sélectionnée, le type par défaut est supprimé du jeu d’informations d’identification par défaut existant. Le jeu d’informations d’identification importé devient la valeur par défaut.
* Vous ne pouvez pas supprimer un jeu d’informations d’identification des extensions Reader par défaut. Il vous faut au préalable définir un autre jeu d’informations d’identification comme valeur par défaut. Il existe néanmoins une exception à cette règle : s’il n’existe qu’un seul jeu d’informations d’identification, vous pouvez le supprimer, même s’il s’agit de la valeur par défaut.
* Vous ne pouvez pas mettre à jour un jeu d’informations d’identification des extensions Reader par défaut.

Pour importer les informations d’identification :

1. Dans Administration Console, cliquez sur Paramètres > Trust Store Management > Informations d’identification locales.
1. Cliquez sur Importer, puis sous Type de Trust Store, sélectionnez Informations d’identification des extensions d’Acrobat Reader DC.
1. (Facultatif) Pour indiquer qu’il s’agit des informations d’identification par défaut à utiliser avec les extensions d’Acrobat Reader DC, sélectionnez Par défaut.
1. Dans la zone Alias, saisissez un identificateur pour les informations d’identification. Cet identifiant sert de nom d’affichage aux informations d’identification dans les extensions d’Acrobat Reader DC. Il permet également d’accéder automatiquement aux informations d’identification via le SDK d’AEM Forms.
1. Cliquez sur Choisir un fichier pour accéder aux informations d’identification, saisissez le mot de passe correspondant, puis cliquez sur OK.

Si le message d’erreur « Échec de l’importation des informations d’identification en raison d’un format de fichier incorrect ou d’un mot de passe incorrect » s’affiche, assurez-vous que le mot de passe est valide.

vous pouvez également importer et supprimer des informations d’identification automatiquement (Voir [Programmation avec AEM Forms](../../developing/credentials.md)).

### Supprimer les droits d’utilisation des documents PDF définis avec des droits d’utilisation

Supprimez les droits d’utilisation des documents PDF définis avec des droits d’utilisation existants avant d’appliquer les droits d’utilisation avec les dernières informations d’identification. AEM Forms on JEE fournit des API pour supprimer les droits d’utilisation. Pour obtenir des instructions détaillées, voir [Supprimer des droits d’utilisation des documents PDF](../../developing/assigning-usage-rights.md#removing-usage-rights-from-pdf-documents).

Pour supprimer les droits d’utilisation des processus AEM Forms on JEE développés dans Workbench, voir [Aide pour Workbench](https://helpx.adobe.com/content/dam/help/fr/experience-manager/6-5/forms/pdf/WorkbenchHelp.pdf).

### Appliquer des droits d’utilisation aux documents PDF

Après avoir importé de nouvelles informations d’identification et supprimé les documents PDF définis avec des droits d’utilisation existants, appliquez les droits d’utilisation aux documents PDF à l’aide des nouvelles informations d’identification. Vous pouvez appliquer des droits d’utilisation aux documents PDF à l’aide de l’API client Java Extensions Acrobat Reader DC et de service web.  Pour plus d’informations, voir [Appliquer des droits d’utilisation aux documents PDF](../../developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents).


## Mettre à jour et appliquer des certificats pour un environnement AEM Forms sur OSGi {#Updating-and-applying-certificates-for-an-AEM-Forms-on-OSGi-environment}

La mise à jour et l’application de nouveaux certificats sur la pile AEM Forms on OSGi nécessite l’importation de nouvelles informations d’identification, la suppression des droits d’utilisation des documents PDF existants et l’application de droits d’utilisation. Vous pouvez utiliser la console d’administration pour importer des informations d’identification et des API d’extension de Reader AEM Forms afin de supprimer et d’appliquer des droits d’utilisation.

### Importer des informations d’identification {#Import-credentials}

Dans un environnement AEM Forms on OSGi, des informations d’identification d’extension Reader sont associées à l’utilisateur fd-service. Avant d’ajouter des informations d’identification pour le magasin de clés fd-user, procédez comme suit pour créer un magasin de clés :

1. Connectez-vous à votre instance de création AEM en tant qu’administrateur.
1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
1. Faites défiler la liste des utilisateurs jusqu’à ce que vous trouviez un compte utilisateur fd-service.
1. Cliquez sur utilisateur **[!UICONTROL fd-service]**.
1. Cliquez sur l’onglet Keystore.
1. Cliquez sur **[!UICONTROL Créer un KeyStore]**.
1. Définissez le mot de passe d’accès KeyStore et enregistrez vos paramètres pour créer le mot de passe KeyStore.

Après avoir créé le KeyStore, ajoutez les informations d’identification à l’utilisateur fd-service. La vidéo suivante explique les étapes :

>[!VIDEO](https://images-tv.adobe.com/mpcv3/5577/8db8e554-f04b-4fae-8108-b9b5e0eb03ad_1627925794.854x480at800_h264.mp4)

La commande suivante répertorie les détails du fichier pfx. Avant d’exécuter la commande, accédez au répertoire contenant le fichier .pfx.

`keytool -v -list -storetype pkcs12 -keystore <name of your .pfx file>`

Par exemple, keytool -v -list -storetype pkcs12 -keystore 1005566.pfx où 1005566.pfx est le nom du fichier pfx.

### Supprimer les droits d’utilisation des documents PDF définis avec des droits d’utilisation

Supprimez les droits d’utilisation des documents PDF définis avec des droits d’utilisation existants avant d’appliquer les droits d’utilisation avec les dernières informations d’identification. Vous pouvez supprimer les droits d’utilisation du document en appelant l’API removeUsageRights depuis docAssuranceServiceAPI. Pour plus d’informations, voir le document [Supprimer les droits d’utilisation](/help/forms/using/aem-document-services-programmatically.md#removing-usage-rights).

### Appliquer des droits d’utilisation aux documents PDF

Pour appliquer des droits d’utilisation dans un environnement AEM Forms on OSGi, créez un service OSGi personnalisé pour appliquer des droits d’utilisation aux documents. Vous pouvez également créer une servlet avec une méthode POST pour renvoyer le PDF étendu Reader à l’utilisateur. Pour obtenir des instructions détaillées, voir [Appliquer des extensions Reader](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/document-services/apply-reader-extension-rights-to-pdf.html?lang=fr).

## Foire aux questions

**Qui dois-je contacter si j’ai des questions supplémentaires ?**

Vous pouvez contacter l’ [Assistance Adobe](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=fr#support) ou créer un ticket d’assistance.

**Que se passe-t-il si je n’ai pas mis à jour mon certificat avant le 7 janvier 2023 ?**

Lors de la tentative d’ouverture d’un document PDF étendu Reader avec d’anciens certificats, les utilisateurs reçoivent un message d’erreur et ne peuvent plus accéder aux fonctionnalités étendues de Reader. Voici un exemple d’erreur.

`The document has been changed since it was created and use of extended features in no longer available. Please contact the author for the orignal version of this document.`

**Le nom de la nouvelle description a-t-il changé ?**

Les nouveaux certificats d’extension de Reader mentionnent G3-P24 comme nom de programme dans la description. Dans les anciens certificats, le nom de programme P24 a été mentionné dans la description.