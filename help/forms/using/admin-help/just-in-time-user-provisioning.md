---
title: Approvisionnement juste à temps
seo-title: Approvisionnement juste à temps
description: Utilisez l’approvisionnement juste à temps pour ajouter des utilisateurs à User Management après l’authentification réussie et pour affecter de manière dynamique les rôles et les groupes appropriés au nouvel utilisateur.
seo-description: Utilisez l’approvisionnement juste à temps pour ajouter des utilisateurs à User Management après l’authentification réussie et pour affecter de manière dynamique les rôles et les groupes appropriés au nouvel utilisateur.
uuid: a5ad4698-70bb-487b-a069-7133e2f420c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e80c3f98-baa1-45bc-b713-51a2eb5ec165
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 95%

---


# Approvisionnement juste à temps {#just-in-time-user-provisioning}

AEM Forms prend en charge l’approvisionnement juste à temps des utilisateurs n’existant pas encore dans Gestion des utilisateurs. Grâce à la fonction d’approvisionnement juste à temps, les utilisateurs sont automatiquement ajoutés à User Management une fois leurs informations d’identification authentifiées. En outre, les rôles et les groupes appropriés sont affectés de manière dynamique au nouvel utilisateur.

## Fonction de l’approvisonnement juste à temps {#need-for-just-in-time-user-provisioning}

Voici comment l’authentification traditionnelle fonctionne :

1. Lorsqu’un utilisateur tente de se connecter à AEM Forms, le gestionnaire des utilisateurs transmet les informations d’identification de ce dernier de manière séquentielle à tous les fournisseurs d’authentification disponibles. Les informations d’identification comprennent le nom d’utilisateur et le mot de passe, le ticket Kerberos, la signature PKCS7, etc.
1. Le fournisseur d’authentification valide les informations d’identification.
1. Il vérifie ensuite si l’utilisateur existe dans la base de données User Management. L’un des résultats suivants s’affiche :

   **Existe :** Si l’utilisateur est en cours et déverrouillé, User Management renvoie la réussite de l’authentification. Toutefois, si l’utilisateur n’est pas en cours ou s’il est verrouillé, User Management signale un échec d’authentification.

   **N&#39;existe pas :** User Management renvoie un échec d’authentification.

   **Non valide :** User Management renvoie un échec d’authentification.

1. L’état indiqué par le fournisseur d’authentification est évalué. Si ce dernier a confirmé l’authentification, l’utilisateur peut alors ouvrir une session. Dans le cas contraire, User Management vérifie auprès du fournisseur d’authentification suivant. (les étapes 2 et 3)
1. Un échec d’authentification est indiqué lorsqu’aucun fournisseur d’authentification disponible n’a pu valider les informations d’identification de l’utilisateur.

Lorsque l’approvisonnement juste à temps est mis en œuvre, un nouvel utilisateur est créé de manière dynamique dans User Management si l’un des fournisseurs d’authentification valide les informations d’identification de l’utilisateur (après l’étape 3 de la procédure d’authentification traditionnelle décrite ci-dessus).

## Mise en œuvre de l’approvisionnement juste à temps {#implement-just-in-time-user-provisioning}

### API pour l’approvisionnement juste à temps {#apis-for-just-in-time-provisioning}

AEM Forms fournit les API suivantes pour l’approvisionnement juste à temps :

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

### Remarques concernant la création d’un domaine de provisionnement juste à temps {#considerations-while-creating-a-just-in-time-enabled-domain}

* Lors de la création d’un `IdentityCreator` personnalisé pour un domaine hybride, assurez-vous qu’un mot de passe factice est spécifié pour l’utilisateur local. Ne laissez pas ce champ de mot de passe vide.
* Recommandation : utilisez `DomainSpecificAuthentication` pour valider les informations d’identification de l’utilisateur pour un domaine spécifique.

### Création d’un domaine d’approvisionnement juste à temps {#create-a-just-in-time-enabled-domain}

1. Ecrivez un DSC de la section « API pour l’approvisionnement juste à temps », qui met les API en œuvre.
1. Déployez le DSC sur le serveur Forms.
1. Créez un domaine de provisionnement juste à temps :

   * Dans Administration Console, cliquez sur Paramètres > User Management > Gestion des domaines > Nouveau domaine d’entreprise.
   * Configurez le domaine et sélectionnez Activer l’approvisionnement juste à temps <!--Fix broken link (See Setting up and managing domains).-->
   * Ajoutez des fournisseurs d’authentification. Durant l’ajout de fournisseurs d’authentification, dans l’écran de nouvelle authentification, sélectionnez un Créateur d’identité et un Fournisseur d’affectation enregistrés.

1. Enregistrez le nouveau domaine.

## Arrière-plan {#behind-the-scenes}

Supposons qu’un utilisateur essaie de se connecter à AEM Forms et qu’un fournisseur d’authentification accepte ses informations d’identification. Si l’utilisateur n’existe pas encore dans la base de données Gestion des utilisateurs, la vérification de son identité échoue. AEM Forms effectue alors les actions suivantes :

1. Création d’un objet `UserProvisioningBO` avec les données d’authentification et placement de l’objet dans une carte d’informations d’identification.
1. Extraction et appel des `UserProvisioningBO` et `IdentityCreator` enregistrés pour le domaine en se basant sur les informations du domaine renvoyées par `AssignmentProvider`.
1. Invoke `IdentityCreator`. Si une `AuthResponse` positive est renvoyée, extraction de `UserInfo` de la carte d’informations d’identification. Transmission de UserInfo à `AssignmentProvider` pour l’affectation des groupes et des rôles après la création de l’utilisateur.
1. Si l’utilisateur est correctement créé, renvoi de la tentative de connexion de l’utilisateur comme réussie.
1. Pour les domaines hybrides, extraction des informations de l’utilisateur des données d’authentification fournies au fournisseur d’authentification. Si l’information est correctement extraite, création de l’utilisateur par la même occasion.

>[!NOTE]
>
>la fonction d’approvisionnement juste à temps comprend une mise en œuvre par défaut de `IdentityCreator` que vous pouvez utiliser pour créer des utilisateurs de manière dynamique. Les utilisateurs sont créés avec les informations associées aux annuaires dans ce domaine.

