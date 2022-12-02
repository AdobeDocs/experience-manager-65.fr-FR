---
title: Traitement des demandes RGPD pour AEM Foundation
seo-title: Handling GDPR Requests for the AEM Foundation
description: Traitement des demandes RGPD pour AEM Foundation
seo-description: null
uuid: d470061c-bbcf-4d86-9ce3-6f24a764ca39
contentOwner: sarchiz
discoiquuid: 8ee843b6-8cea-45fc-be6c-99c043f075d4
exl-id: 411d40ab-6be8-4658-87f6-74d2ac1a4913
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 100%

---

# Traitement des demandes RGPD pour AEM Foundation{#handling-gdpr-requests-for-the-aem-foundation}

>[!IMPORTANT]
>
>Le RGPD est utilisé comme exemple dans les sections ci-dessous, mais les détails couverts sont applicables à toutes les réglementations de protection des données et de confidentialité, comme le RGPD, le CCPA, etc.

## Prise en charge du RGPD par AEM Foundation {#aem-foundation-gdpr-support}

En ce qui concerne AEM Foundation, les données personnelles stockées sont conservées dans le profil utilisateur. Par conséquent, les informations fournies dans cet article expliquent principalement comment accéder à ces profils utilisateur et les supprimer pour répondre respectivement aux demandes d’accès et de suppression dans le cadre du RGPD.

## Accès à un profil utilisateur {#accessing-a-user-profile}

### Étapes manuelles {#manual-steps}

1. Ouvrez la console d’administration des utilisateurs en accédant à **[!UICONTROL Paramètres – Sécurité – Utilisateurs]** ou en accédant directement à `https://<serveraddress>:<serverport>/libs/granite/security/content/useradmin.html`.

   ![useradmin2](assets/useradmin2.png)

1. Recherchez ensuite l’utilisateur en question en saisissant le nom dans la barre de recherche située en haut de la page :

   ![usersearch](assets/usersearch.png)

1. Enfin, ouvrez le profil utilisateur en cliquant dessus, puis consultez les informations sous l’onglet **[!UICONTROL Détails]**.

   ![userprofile_small](assets/userprofile_small.png)

### API HTTP  {#http-api}

Comme mentionné, Adobe fournit des API pour accéder aux données utilisateur, afin de faciliter l’automatisation. Il existe plusieurs types d’API que vous pouvez utiliser :

**API UserProperties**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**API Sling**

*Découverte du répertoire de base (home) des utilisateurs :*

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

*Récupération des données utilisateur*

Utilisation du chemin de nœud de la propriété home de la charge utile JSON renvoyée par la commande ci-dessus :

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Désactivation d’un utilisateur et suppression des profils associés {#disabling-a-user-and-deleting-the-associated-profiles}

### Désactivation d’un utilisateur {#disable-user}

1. Ouvrez la console Administration utilisateur et recherchez l’utilisateur en question, comme décrit ci-dessus.
1. Survolez l’utilisateur avec le curseur, puis cliquez sur l’icône sélectionnée. Le profil devient gris pour indiquer qu’il est sélectionné.

1. Appuyez sur le bouton Désactiver dans le menu supérieur pour désactiver l’utilisateur :

   ![userdisable](assets/userdisable.png)

1. Enfin, confirmez l’action :

   ![image2018-2-6_1-40-58](assets/image2018-2-6_1-40-58.png)

   L’interface utilisateur indique alors que l’utilisateur a été désactivé en grisant la carte de profil et en y ajoutant un cadenas :

   ![disableduser](assets/disableduser.png)

### Suppression des informations d’un profil utilisateur {#delete-user-profile-information}

1. Connectez-vous à CRXDE Lite, puis recherchez l’`[!UICONTROL userId]` :

   ![image2018-2-6_1-57-11](assets/image2018-2-6_1-57-11.png)

1. Ouvrez le nœud de l’utilisateur qui se trouve sous `[!UICONTROL /home/users]` par défaut :

   ![image2018-2-6_1-58-25](assets/image2018-2-6_1-58-25.png)

1. Supprimez les nœuds de profil et tous leurs enfants. Il existe deux formats de nœuds de profil, selon la version d’AEM :

   1. Le profil privé par défaut sous `[!UICONTROL /profile]`
   1. `[!UICONTROL /profiles]`, pour les nouveaux profils créés à l’aide d’AEM 6.5

   ![image2018-2-6_2-0-4](assets/image2018-2-6_2-0-4.png)

### API HTTP  {#http-api-1}

Les procédures suivantes utilisent l’outil de ligne de commande `curl` pour illustrer comment désactiver l’`userId` **[!UICONTROL cavery]** et supprimer ses profils disponibles à l’emplacement par défaut.

* *Découverte du répertoire de base (home) de l’utilisateur*

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

* *Désactivation de l’utilisateur*

Utilisation du chemin de nœud de la propriété home de la charge utile JSON renvoyé par la commande ci-dessus :

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (GDPR in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

* *Suppression du ou des profils utilisateur*

Utilisation du chemin de nœud de la propriété home de la charge utile JSON renvoyé par la commande de découverte de compte et les emplacements de nœuds de profil prêts à l’emploi connus :

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
