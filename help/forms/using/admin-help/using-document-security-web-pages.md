---
title: Utilisation des pages Web de Document Security
seo-title: Utilisation des pages Web de Document Security
description: Découvrez comment vous connecter, naviguer et utiliser les pages Web de sécurité des documents.
seo-description: Découvrez comment vous connecter, naviguer et utiliser les pages Web de sécurité des documents.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 97%

---

# Utilisation des pages Web de Document Security {#using-the-document-security-webpages}

Les utilisateurs et les administrateurs utilisent les pages Web de Document Security pour créer et gérer des stratégies, gérer des documents protégés par une stratégie et contrôler les événements associés aux documents protégés par une stratégie. Les administrateurs utilisent également les pages Web pour créer des jeux de stratégies, désigner des coordinateurs de jeux de stratégies, configurer les paramètres par défaut de Document Security, gérer l’enregistrement et les comptes des utilisateurs invités, et contrôler et gérer les événements concernant les serveurs, les stratégies, les utilisateurs et les documents.

>[!NOTE]
>
>Vous pouvez également ouvrir une session Document Security par l’intermédiaire d’Acrobat et d’autres applications clientes à l’aide de votre compte utilisateur (voir [Configuration de l’accès à Document Security à partir d’applications clientes](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)).

Pour ouvrir les pages Web, vous devez disposer d’un navigateur, ainsi que de l’URL et de vos informations de connexion à Document Security. L’URL des utilisateurs diffère de celle des administrateurs.

Comme Document Security référence les répertoires existants de votre entreprise dans les informations utilisateur, votre compte Document Security peut être identique à celui que vous utilisez pour vous connecter à votre réseau et à d’autres applications. Pour obtenir des informations sur votre compte, contactez votre administrateur ou votre administrateur système.

Pour ouvrir une session en tant qu’administrateur, vous devez avoir le rôle d’administrateur. Vous pouvez utiliser le compte de super-administrateur par défaut créé lors de l’installation.

## Ouverture d’une session de pages Web {#log-in-to-the-web-pages}

Pour ouvrir une session de pages Web à l’aide d’un navigateur, vous devez disposer d’un compte et de l’URL Document Security. L’URL des utilisateurs diffère de celle des administrateurs. Les administrateurs peuvent également se connecter aux pages utilisateur pour créer des stratégies.

Si vous avez accès à plusieurs installations de Document Security, vous avez besoin de l’URL de l’instance de Document Security à laquelle vous souhaitez accéder. Contactez votre administrateur si vous ne disposez pas de cette information. L’URL par défaut des pages utilisateur est `https://[host]:[port]/edc`. Dans certains cas, le numéro de port n’est pas nécessaire. Renseignez-vous auprès de votre administrateur pour plus de précisions.

L’URL par défaut pour les administrateurs est `https://[host]:[port]/adminui`.

A l’intention des administrateurs, un compte de super-administrateur par défaut est créé lors de l’installation. Vous pouvez utiliser ce compte pour ouvrir une session à la première installation de Document Security.

>[!NOTE]
>
>Vous pouvez également accéder aux pages Web à partir d’Acrobat et d’autres applications clientes. Pour plus de détails, consultez l’aide d’Acrobat ou l’aide des extensions d’Acrobat Reader DC appropriée.

1. Saisissez l’URL dans votre navigateur :

   URL de Document Security : `https://[host]:[port]/edc`

   ou URL d’Administration Console : `https://[host]:[port]/adminui`

1. Dans la fenêtre d’ouverture de session, saisissez votre nom d’utilisateur et votre mot de passe, puis cliquez sur OK.
1. Dans Administration Console, cliquez sur Services > Sécurité des documents.

>[!NOTE]
>
>lorsque vous travaillez sur des pages Web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette opération risque de capturer des données non souhaitées et d’entraîner des problèmes d’affichage.

## Navigation dans les pages Web  {#navigating-the-web-pages}

Lorsque vous vous connectez aux pages Web utilisateur, vous voyez apparaître des liens vous permettant d’accéder aux pages utilisateur Stratégies, Documents et Evénements.

Lorsque vous ouvrez une session dans Administration Console et que vous vous rendez sur la page principale de Document Security, deux liens supplémentaires peuvent apparaître, l’un pour la page Configuration, l’autre pour la page Utilisateurs invités et locaux. La page Utilisateurs invités et locaux n’est visible que si l’enregistrement des utilisateurs invités est activé.

Cliquez sur ces liens pour accéder aux pages vous permettant de créer et de gérer les stratégies et les documents protégés par une stratégie.

**Affichage d’une page**

1. Cliquez sur le nom de la page. Par exemple, cliquez sur Stratégies.

**Revenir à la page précédente**

1. Dans la partie supérieure de la page, cliquez sur le lien de navigation correspondant à la page sur laquelle vous souhaitez revenir.

**Actualisation des données d’une page**

1. Dans la page principale, cliquez sur le lien correspondant à la page que vous souhaitez actualiser.

>[!NOTE]
>
>lorsque vous travaillez sur des pages Web, évitez d’utiliser les boutons du navigateur, tels que le bouton Précédent, le bouton Actualiser, ainsi que les flèches permettant d’afficher la page précédente ou suivante, car cette opération risque de capturer des données non souhaitées et d’entraîner des problèmes d’affichage.

## Configuration de l’accès à Document Security à partir d’applications clientes  {#setting-up-access-to-document-security-from-client-applications}

Les applications clientes doivent être configurées pour se connecter à Document Security afin de protéger des documents, d’ouvrir des documents protégés par une stratégie et de se connecter aux pages Web de Document Security. Consultez l’*Aide d’Acrobat* ou l’*Aide de Rights Management Extension* pour plus d’informations sur la configuration de la connexion à partir de l’application cliente.

L’accès à Document Security est effectué via SSL (Secure Sockets Layer). Vous devez installer le certificat du site Web dans votre banque de certificats pour pouvoir accéder à Document Security à partir des applications clientes.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Ces instructions s’appliquent à Internet Explorer, mais vous pouvez installer le certificat à l’aide de tout navigateur pris en charge. Pour plus d’informations, consultez l’Aide de votre navigateur.

**Installation du certificat du serveur à l’aide d’Internet Explorer**

1. Ouvrez votre navigateur Web et saisissez l’URL de base de Document Security dans le champ Adresse. Par exemple, saisissez `https://[host]:[port]`. Une boîte de dialogue Alerte de sécurité apparaît.
1. Cliquez sur Afficher le certificat, puis sur Installer le certificat et sélectionnez les paramètres par défaut de l’installation. Le certificat doit être installé avec les autorités de certification racine approuvées.
1. Fermez votre session de navigateur.
1. Ouvrez une autre fenêtre du navigateur et saisissez la même URL dans le champ Adresse. Aucune boîte de dialogue Alerte de sécurité ne doit s’afficher. Ce test confirme que le certificat est correctement installé.

## Fermeture d’une session de pages Web  {#log-out-of-the-web-pages}

Fermez votre session lorsque vous avez fini d’utiliser les pages Web, afin d’utiliser votre navigateur Web en toute sécurité pour d’autres activités. Selon la configuration de Document Security, il peut se révéler nécessaire de fermer le navigateur pour fermer totalement la session.

1. Dans l’angle supérieur droit de la page, cliquez sur Fermeture de la session.
1. Si un message apparaît dans la page Fermeture de la session, refermez la fenêtre du navigateur pour fermer totalement la session. Dans le cas contraire, vous pouvez continuer à utiliser votre navigateur pour d’autres activités.
