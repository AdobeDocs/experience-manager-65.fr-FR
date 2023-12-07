---
title: Configurer l’authentification basée sur certificat
description: Importez un certificat d’autorité de certification dans Trust Store et créez un mappage de certificats pour l’authentification par certificat.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 9cbea8c8-4d42-446b-b98d-c090709624d7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 5%

---

# Configurer l’authentification basée sur certificat {#configuring-certificate-based-authentication}

User Management effectue généralement l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe. User Management prend également en charge l’authentification par certificat, que vous pouvez utiliser pour authentifier les utilisateurs via Acrobat ou pour authentifier les utilisateurs par programmation. Pour plus d’informations sur l’authentification des utilisateurs par programmation, voir [Programmation avec les AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).

Pour utiliser l’authentification par certificat, importez un certificat de l’autorité de certification en qui vous avez confiance dans Trust Store, puis créez un mappage de certificat.

## Importation du certificat de l’autorité de certification {#import-the-ca-certificate}

Lors de l’importation du certificat, sélectionnez les options Approbation d’authentification de certificat et Approbation d’identité , ainsi que toute autre option nécessaire. Pour plus d’informations sur l’importation de certificats, voir [Gestion des certificats](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configuration du mappage de certificats {#configuring-certificate-mapping}

Pour activer l’authentification par certificat pour les utilisateurs, créez un mappage de certificat. A *mappage de certificat* définit une map entre les attributs d’un certificat et les attributs des utilisateurs dans un domaine. Vous pouvez mapper plusieurs certificats au même domaine.

Lorsque vous testez un certificat, User Management télécharge les vérifications de certificat pour s’assurer qu’il répond aux exigences suivantes :

* Le certificat est valide.
* L’émetteur que vous avez spécifié peut vérifier le certificat.
* Le certificat contient l’attribut requis pour le mappage.
* Le mappage que vous avez spécifié mappe le certificat à un seul utilisateur de la base de données AEM forms. Les utilisateurs actuels et obsolètes (supprimés) sont vérifiés pour déterminer s’ils correspondent aux critères de mappage. Par conséquent, le test du certificat échoue si plusieurs utilisateurs, y compris les utilisateurs obsolètes, ont la valeur d’attribut en cours de prise en compte.

>[!NOTE]
>
>Vous ne pouvez pas modifier un mappage de certificat existant.

**Ajout d’un mappage de certificat**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cliquez sur Nouveau mappage de certificats et, dans la liste Pour l’émetteur, sélectionnez l’alias du certificat tel que configuré dans Trust Store Management.
1. Mappez l’un des attributs du certificat à l’attribut d’un utilisateur. Par exemple, vous pouvez mapper le nom commun du certificat à l’ID de connexion de l’utilisateur.

   Si le contenu de l’attribut dans le certificat est différent du contenu de l’attribut de l’utilisateur dans la base de données User Management, vous pouvez utiliser une expression régulière Java (regex) pour faire correspondre les deux attributs. Par exemple, si les noms communs des certificats sont des noms comme *Alex Pink (authentification)* et *Alex Pink (signature)* et le nom commun dans la base de données User Management est *Alex Pink*, vous utilisez une expression régulière pour extraire la partie requise de l’attribut de certificat (dans cet exemple, *Alex Pink*.) L’expression régulière que vous spécifiez doit être conforme à la spécification regex Java.

   Vous pouvez transformer l’expression en spécifiant l’ordre des groupes dans la zone Ordre personnalisé. L’ordre personnalisé s’utilise avec la méthode `java.util.regex.Matcher.replaceAll()`. Le comportement affiché correspond au comportement de cette méthode et la chaîne d’entrée (l’ordre personnalisé) doit être spécifiée en conséquence.

   Pour tester l’expression régulière, saisissez une valeur dans la zone Paramètre de test et cliquez sur Tester.

   Vous pouvez utiliser les caractères suivants dans l’expression régulière :

   *  : (n’importe quel caractère)
   * &amp;ast; (0 ou plus d’occurrences)
   * () (spécifier le groupe entre crochets)
   * \ (utilisé pour échapper un caractère regex à un caractère normal)
   * $n (utilisé pour faire référence au énième groupe)

   Exemples d’expressions régulières :

   * Pour extraire &quot;Alex Dupont&quot; de &quot;Alex Dupont (Authentification)&quot;

     **Regex :** (.&amp;ast;) \(Authentification\)

   * Pour extraire &quot;Alex Pink&quot; de &quot;Alex (Authentification) Pink&quot;

     **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

   * Pour extraire &quot;Alex rose&quot; de &quot;Alex (Authentification) rose&quot;

     **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

     Ordre personnalisé : 2 $ 1 (renvoyer le deuxième groupe, concaténé au premier groupe, capturé par un espace blanc)

   * Pour extraire &quot;apink@sampleorg.com&quot; de &quot;smtp:apink@sampleorg.com&quot;

     **Regex :** smtp:(.&amp;ast;)

   Pour plus d’informations sur l’utilisation des expressions régulières, voir [Tutoriel Java sur les expressions régulières](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Dans la liste Pour le domaine , sélectionnez le domaine de l’utilisateur.
1. Pour tester cette configuration, cliquez sur Parcourir pour télécharger un exemple de certificat utilisateur, cliquez sur Tester le certificat et, si la configuration est correcte, cliquez sur OK.

**Modification d’un mappage de certificat existant**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration.
1. Cliquez sur Mappage de certificats.
1. Sélectionnez le mappage de certificats à modifier et modifiez sa configuration. Vous pouvez mettre à jour l’expression régulière et l’ordre personnalisé.
1. Pour tester vos modifications, cliquez sur Parcourir pour télécharger un exemple de certificat, cliquez sur Tester le certificat, puis sur OK.

**Suppression d’un mappage de certificat**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cochez la case correspondant au mappage de certificat à supprimer, cliquez sur Supprimer, puis sur OK.
