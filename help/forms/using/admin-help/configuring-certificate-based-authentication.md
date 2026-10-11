---
title: Configurer l’authentification basée sur certificat
description: Importez un certificat d’une autorité de certification (CA) dans Trust Store et créez un mappage de certificat pour l’authentification basée sur certificat.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '739'
ht-degree: 88%
---
# Configurer l’authentification basée sur certificat {#configuring-certificate-based-authentication}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

User Management effectue généralement l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe. User Management prend également en charge l’authentification par certificat, qui vous permet d’authentifier des utilisateurs ou utilisatrices via Acrobat ou par programmation. Pour plus d’informations sur l’authentification des utilisateurs et utilisatrices par programmation, voir [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).

Pour utiliser l’authentification par certificat, importez dans Trust Store un certificat d’une autorité de certification (CA) en qui vous avez confiance, puis créez un mappage de certificat.

## Importer le certificat de l’autorité de certification {#import-the-ca-certificate}

Lors de l’import du certificat, sélectionnez les options Approbation d’authentification de certificat et Approbation d’identité, et d’autres options selon les besoins. Pour plus d’informations sur l’import de certificats, voir [Gestion des certificats](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configuration du mappage de certificats {#configuring-certificate-mapping}

Pour activer l’authentification par certificat pour les utilisateurs et utilisatrices, créez un mappage de certificat. Un *mappage de certificats* associe les attributs d’un certificat et ceux des utilisateurs et utilisatrices d’un domaine. Vous pouvez mapper plusieurs certificats au même domaine.

Lorsque vous testez un certificat, User Management charge les vérifications de certificat pour s’assurer qu’il répond aux critères suivants :

* Le certificat est valide.
* L’émetteur que vous avez spécifié peut vérifier le certificat.
* Le certificat contient l’attribut requis pour le mappage.
* Le mappage que vous avez spécifié mappe le certificat à un seul utilisateur ou utilisatrice de la base de données AEM Forms. Les utilisateurs et utilisatrices actuels et obsolètes (supprimés) sont vérifiés pour déterminer s’ils correspondent aux critères de mappage. Le test du certificat échoue si au moins un utilisateur ou une utilisatrice, obsolète ou non, possède la valeur d’attribut considérée.

>[!NOTE]
>
>Vous ne pouvez pas modifier un mappage de certificat existant.

**Ajout d’un mappage de certificat**

1. Dans la console d’administration cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cliquez sur Nouveau mappage de certificats et dans la liste Pour l’émetteur, sélectionnez l’alias du certificat tel que configuré dans Trust Store Management.
1. Mappez l’un des attributs du certificat à l’attribut d’un utilisateur ou d’une utilisatrice. Par exemple, vous pouvez mapper le nom commun du certificat à l’ID de connexion de l’utilisateur ou utilisatrice.

   Si le contenu de l’attribut dans le certificat est différent du contenu de l’attribut de l’utilisateur ou utilisatrice dans la base de données de User Management, vous pouvez utiliser une expression régulière Java (regex) pour faire correspondre les deux attributs. Par exemple, si les noms communs des certificats sont des noms tels que *Alex Pink (authentification)* et *Alex Pink (signature)* et que le nom commun dans la base de données User Management est *Alex Pink*, vous utilisez une expression régulière pour extraire la partie requise de l’attribut de certificat (dans cet exemple, *Alex Pink*.) L’expression régulière que vous spécifiez doit être conforme à la spécification RegEx Java.

   Vous pouvez transformer l’expression en spécifiant l’ordre des groupes dans la zone Ordre personnalisé. L’ordre personnalisé s’utilise avec la méthode `java.util.regex.Matcher.replaceAll()`. Le comportement observé correspond à celui de cette méthode et la chaîne d’entrée (l’ordre personnalisé) doit être spécifiée en conséquence.

   Pour tester l’expression régulière, saisissez une valeur dans la zone Paramètre de test et cliquez sur Tester.

   Vous pouvez utiliser les caractères suivants dans l’expression régulière :

   * . (n’importe quel caractère)
   * &ast; (0 occurrence ou plus)
   * () (spécifier le groupe entre parenthèses)
   * \ (permet d’utiliser un caractère regex en tant que caractère normal)
   * $n (permet de faire référence au énième groupe)

   Exemples d’expressions régulières :

   * Pour extraire « Alex Pink » de « Alex Pink (Authentification) »

     **Regex:** (.&ast;) \(Authentification\)

   * Pour extraire « Alex Pink » de « Alex (Authentification) Pink »

     **Regex:** (.&ast;)\(Authentification\) (.&ast;)

   * Pour extraire « Pink Alex » de « Alex (Authentification) Pink »

     **Regex:** (.&ast;)\(Authentification\) (.&ast;)

     Ordre personnalisé : $2 $1 (renvoyer le deuxième groupe, concaténé au premier groupe, capturé par un espace blanc)

   * Pour extraire « apink@sampleorg.com » de « smtp:apink@sampleorg.com »

     **Regex:** smtp:(.&ast;)

   Pour plus d’informations sur l’utilisation des expressions régulières, voir [Tutoriel Java sur les expressions régulières](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Dans la liste Pour le domaine, sélectionnez le domaine de l’utilisateur ou de l’utilisatrice.
1. Pour tester cette configuration, cliquez sur Parcourir pour charger un exemple de certificat utilisateur, cliquez sur Tester le certificat et, si la configuration est correcte, cliquez sur OK.

**Modifier un mappage de certificat existant**

1. Dans la console d’administration, cliquez sur Paramètres > Gestion des utilisateurs > Configuration.
1. Cliquez sur Mappage de certificats.
1. Sélectionnez le mappage de certificats à modifier et modifiez sa configuration. Vous pouvez mettre à jour l’expression régulière et l’ordre personnalisé.
1. Pour tester vos modifications, cliquez sur Parcourir pour charger un exemple de certificat, cliquez sur Tester le certificat, puis sur OK.

**Supprimer un mappage de certificats**

1. Dans la console d’administration cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cochez la case du mappage de certificats à supprimer, cliquez sur Supprimer, puis cliquez sur OK.
