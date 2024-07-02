---
title: Configurer l’authentification basée sur certificat
description: Importez un certificat d’une autorité de certification dans Trust Store et créez un mappage de certificats pour l’authentification basée sur certificat.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '718'
ht-degree: 100%

---

# Configurer l’authentification basée sur certificat {#configuring-certificate-based-authentication}

User Management effectue généralement l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe. User Management prend également en charge l’authentification par certificat, qui vous permet d’authentifier des utilisateurs ou utilisatrices via Acrobat ou par programmation. Pour plus d’informations sur l’authentification des utilisateurs et utilisatrices par programmation, voir [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).

Pour utiliser l’authentification par certificat, importez dans Trust Store un certificat d’une autorité de certification en qui vous avez confiance, puis créez un mappage de certificat.

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

   Si le contenu de l’attribut dans le certificat est différent du contenu de l’attribut de l’utilisateur ou utilisatrice dans la base de données de User Management, vous pouvez utiliser une expression régulière Java (regex) pour faire correspondre les deux attributs. Par exemple, si les noms communs des certificats sont des noms comme *Alex Pink (authentification)* et *Alex Pink (signature)* et le nom commun dans la base de données User Management est *Alex Pink*, vous utilisez une expression régulière pour extraire la partie requise de l’attribut de certificat (dans cet exemple, *Alex Pink*.) L’expression régulière que vous spécifiez doit être conforme à la spécification regex Java.

   Vous pouvez transformer l’expression en spécifiant l’ordre des groupes dans la zone Ordre personnalisé. L’ordre personnalisé s’utilise avec la méthode `java.util.regex.Matcher.replaceAll()`. Le comportement observé correspond à celui de cette méthode et la chaîne d’entrée (l’ordre personnalisé) doit être spécifiée en conséquence.

   Pour tester l’expression régulière, saisissez une valeur dans la zone Paramètre de test et cliquez sur Tester.

   Vous pouvez utiliser les caractères suivants dans l’expression régulière :

   *  : (n’importe quel caractère)
   * &amp;ast; (0 ou plus d’occurrences)
   * () (spécifier le groupe entre parenthèses)
   * \ (permet d’utiliser un caractère regex en tant que caractère normal)
   * $n (permet de faire référence au énième groupe)

   Exemples d’expressions régulières :

   * Pour extraire « Alex Pink » de « Alex Pink (Authentification) »

     **Regex :** (.&amp;ast;) \(Authentification\)

   * Pour extraire « Alex Pink » de « Alex (Authentification) Pink »

     **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

   * Pour extraire « Pink Alex » de « Alex (Authentification) Pink »

     **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

     Ordre personnalisé : $2 $1 (renvoyer le deuxième groupe, concaténé au premier groupe, capturé par un espace blanc)

   * Pour extraire « apink@sampleorg.com » de « smtp:apink@sampleorg.com »

     **Regex :** smtp:(.&amp;ast;)

   Pour plus d’informations sur l’utilisation des expressions régulières, voir [Tutoriel Java sur les expressions régulières](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Dans la liste Pour le domaine, sélectionnez le domaine de l’utilisateur ou de l’utilisatrice.
1. Pour tester cette configuration, cliquez sur Parcourir pour charger un exemple de certificat utilisateur, cliquez sur Tester le certificat et, si la configuration est correcte, cliquez sur OK.

**Modifier un mappage de certificat existant**

1. Dans la console d’administration cliquez sur Paramètres > User Management > Configuration.
1. Cliquez sur Mappage de certificats.
1. Sélectionnez le mappage de certificats à modifier et modifiez sa configuration. Vous pouvez mettre à jour l’expression régulière et l’ordre personnalisé.
1. Pour tester vos modifications, cliquez sur Parcourir pour charger un exemple de certificat, cliquez sur Tester le certificat, puis sur OK.

**Supprimer un mappage de certificats**

1. Dans la console d’administration cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cochez la case du mappage de certificats à supprimer, cliquez sur Supprimer, puis cliquez sur OK.
