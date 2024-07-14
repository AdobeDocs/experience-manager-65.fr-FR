---
title: Approvisionnement juste à temps d’utilisateurs
description: Utilisez l’approvisionnement juste à temps pour ajouter des utilisateurs et des utilisatrices à User Management après l’authentification réussie et pour affecter de manière dynamique les rôles et les groupes appropriés au nouvel utilisateur ou à la nouvelle utilisatrice.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7bde0a09-192a-44a8-83d0-c18e335e9afa
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 100%

---

# Approvisionnement juste à temps {#just-in-time-user-provisioning}

AEM Forms prend en charge l’approvisionnement juste à temps d’utilisateurs et d’utilisatrices n’existant pas encore dans User Management. Grâce à la fonction d’approvisionnement juste à temps, les utilisateurs et les utilisatrices sont automatiquement ajoutés à User Management une fois leurs informations d’identification authentifiées. En outre, les rôles et groupes appropriés sont affectés dynamiquement au nouvel utilisateur ou à la nouvelle utilisatrice.

## Fonction de l’approvisionnement juste à temps d’utilisateurs et d’utilisatrices {#need-for-just-in-time-user-provisioning}

Voici comment l’authentification traditionnelle fonctionne :

1. Lorsqu’un utilisateur ou une utilisatrice tente de se connecter à AEM Forms, User Management transmet les informations d’identification de l’utilisateur ou de l’utilisatrice de manière séquentielle à tous les fournisseurs d’authentification disponibles. (Les informations d’identification comprennent le nom d’utilisateur ou d’utilisatrice et le mot de passe, le ticket Kerberos, la signature PKCS7, etc.)
1. Le fournisseur d’authentification valide les informations d’identification.
1. Le fournisseur d’authentification vérifie ensuite si l’utilisateur ou l’utilisatrice existe dans la base de données User Management. Voici les résultats possibles :

   **Existe :** si l’utilisateur est en cours et déverrouillé, User Management renvoie un succès d’authentification. Toutefois, si l’utilisateur n’est pas en cours ou s’il est verrouillé, User Management signale un échec d’authentification.

   **N’existe pas :** User Management renvoie un échec d’authentification.

   **Non valide :** User Management renvoie un échec d’authentification.

1. Le résultat renvoyé par le fournisseur d’authentification est évalué. Si le fournisseur d’authentification renvoie une authentification réussie, l’utilisateur ou l’utilisatrice est autorisés à se connecter. Dans le cas contraire, User Management vérifie auprès du fournisseur d’authentification suivant (étapes 2 et 3).
1. Un échec de l’authentification est renvoyé si aucun fournisseur d’authentification disponible ne valide les informations d’identification de l’utilisateur ou de l’utilisatrice.

Lors de l’implémentation de l’approvisionnement juste à temps, une nouvelle personne est créée dynamiquement dans User Management si l’un des fournisseurs d’authentification valide les informations d’identification de celle-ci. (Après l’étape 3 de la procédure d’authentification traditionnelle décrite ci-dessus.)

## Implémentation de l’approvisionnement juste à temps {#implement-just-in-time-user-provisioning}

### API pour l’approvisionnement juste à temps {#apis-for-just-in-time-provisioning}

AEM forms fournit les API suivantes pour l’approvisionnement juste à temps :

```java
package com.adobe.idp.um.spi.authentication  ;
publ ic interface IdentityCreator {
/**
* Tries  to create a user with the  in formation  provided in the <code>UserProvisioningBO</code> object.
* If the user is successfully created, a valid AuthResponse is returned along with the information using which the user was created.
* It is the responsibility of the IdentityCreator to set the User obje ct  in the cre dential map with th e  ke y  <code>UMA u thenticationUtil.authenticatedUserKey</code>
* The credentials are available in the <code>UserProvisioningBO</code> object in the 'credentials' property.
* If the IdentityCreator is unable to create a user due to any reason, it returns <code>null</code>
* @param userBO An object of <code>com.adobe. i dp.um . spi.authenti c ationUserProvisioningBO</code>
* @return */public AuthResponse create(UserProvisioningBO userBO);
/**
* Returns the name of the IdentityCreator which will be registered in preferences.
* This name is used to associate the IdentityProvider with the Auth Provider Configuration in the domain.
* @return The name of the Identity Creator which is recognized in Configuration.
*/
public String getName();
}
package com.adobe.idp.um.spi.authentication;
import com.adobe.idp.um.api.infomodel.User;
public interface AssignmentProvider {
/**
* Tries to assign roles or permissions or group memberships to users created via Just-in-time provisioning.
* @param user The User created via the Just-in-time provisioning process.
* @return a Boolean flag indicating whether the assignment was successful or not.
*/
public Boolean assign(User user);
/**
* Returns the name of the AssignmentProvider through which it is registered under preferences.
* This name is used to associate the AssignmentProvider with the Auth Provider Configuration in the domain.
* @return The name of the AssignmentProvider which is recognized in Configuration.
*/public String getName();
}
```

### Éléments à prendre en compte lors de la création d’un domaine prenant en charge l’approvisionnement juste à temps {#considerations-while-creating-a-just-in-time-enabled-domain}

* Lors de la création d’un `IdentityCreator` personnalisé pour un domaine hybride, assurez-vous qu’un mot de passe factice est spécifié pour l’utilisateur local. Ne laissez pas ce champ de mot de passe vide.
* Recommandation : utilisez `DomainSpecificAuthentication` pour valider les informations d’identification de l’utilisateur pour un domaine spécifique.

### Créer un domaine d’approvisionnement juste à temps {#create-a-just-in-time-enabled-domain}

1. Écrivez un DSC qui met les API en œuvre dans la section « API pour l’approvisionnement juste à temps ».
1. Déployez le DSC sur le serveur Forms Server.
1. Créez un domaine prenant en charge l’approvisionnement juste à temps :

   * Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des domaines > Nouveau domaine d’entreprise.
   * Configurez le domaine et sélectionnez Activer l’approvisionnement juste à temps. <!--Fix broken link (See Setting up and managing domains).-->
   * Ajoutez des fournisseurs d’authentification. Lors de l’ajout de fournisseurs d’authentification, dans l’écran Nouvelle authentification, sélectionnez un créateur d’identités et un fournisseur d’affectation enregistrés.

1. Enregistrez le nouveau domaine.

## En arrière-plan {#behind-the-scenes}

Supposons qu’un utilisateur ou une utilisatrice essaie de se connecter à AEM Forms et qu’un fournisseur d’authentification accepte ses informations d’identification. Si l’utilisateur ou l’utilisatrice n’existe pas encore dans la base de données User Management, la vérification de l’identité de l’utilisateur ou de l’utilisatrice échoue. AEM Forms effectue alors les actions suivantes :

1. Création d’un objet `UserProvisioningBO` avec les données d’authentification et placement de l’objet dans une carte d’informations d’identification.
1. Extraction et appel des `UserProvisioningBO` et `IdentityCreator` enregistrés pour le domaine en se basant sur les informations du domaine renvoyées par `AssignmentProvider`.
1. Appelez `IdentityCreator`. Si une `AuthResponse` positive est renvoyée, extraction de `UserInfo` de la carte d’informations d’identification. Transmission de UserInfo à `AssignmentProvider` pour l’affectation des groupes et des rôles après la création de l’utilisateur.
1. Si la personne est correctement créée, renvoi de la tentative de connexion de la personne comme réussie.
1. Pour les domaines hybrides, extraction des informations de l’utilisateur ou de l’utilisatrice des données d’authentification fournies au fournisseur d’authentification. Si la récupération des informations réussit, création de l’utilisateur ou de l’utilisatrice par la même occasion.

>[!NOTE]
>
>la fonction d’approvisionnement juste à temps comprend une mise en œuvre par défaut de `IdentityCreator` que vous pouvez utiliser pour créer des utilisateurs de manière dynamique. Les utilisateurs sont créés avec les informations associées aux annuaires dans ce domaine.
