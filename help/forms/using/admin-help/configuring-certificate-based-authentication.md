---
title: Configuration de l’authentification avec certificat
seo-title: Configuration de l’authentification avec certificat
description: Importez un certificat d’une autorité de certification dans Trust Store et créez un mappage de certificats pour l’authentification basée sur certificat.
seo-description: Importez un certificat d’une autorité de certification dans Trust Store et créez un mappage de certificats pour l’authentification basée sur certificat.
uuid: 9802a969-6d29-4b80-a4ed-06eb6e66e046
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d958ae65-3008-4d68-9e11-4346e149827f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 94%

---


# Configuration de l’authentification avec certificat {#configuring-certificate-based-authentication}

En général, User Management effectue l’authentification à l’aide d’un nom d’utilisateur et d’un mot de passe. User Management prend également en charge l’authentification par certificat, qui vous permet d’authentifier des utilisateurs via Acrobat ou automatiquement. Pour plus d’informations sur l’authentification des utilisateurs par programmation, consultez [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).

Pour utiliser l’authentification par certificat, importez dans Trust Store un certificat d’une autorité de certification en qui vous avez confiance, puis créez un mappage de certificat.

## Importation du certificat d’une autorité de certification {#import-the-ca-certificate}

Lors de l’importation du certificat, sélectionnez les options Approbation d’authentification de certificat et Approbation d’identité, et d’autres options selon les besoins. Pour plus d’informations sur l’importation de certificats, voir [Gestion de certificats](/help/forms/using/admin-help/certificates.md#managing-certificates).

## Configuration du mappage de certificat  {#configuring-certificate-mapping}

Pour activer l’authentification des utilisateurs par certificat, créez un mappage de certificat. Un *mappage de certificats* associe les attributs d’un certificat et ceux des utilisateurs d’un domaine. Vous pouvez mapper plusieurs certificats au même domaine.

Lorsque vous testez un certificat, User Management télécharge les contrôles pour vérifier que le certificat répond aux critères suivants :

* Le certificat est valide.
* L’émetteur spécifié peut vérifier le certificat.
* Le certificat contient l’attribut requis pour le mappage.
* Le mappage que vous avez spécifié mappe le certificat à un seul utilisateur dans la base de données AEM Forms. Les contrôles portent à la fois sur les utilisateurs actuels et obsolètes (supprimés), pour déterminer s’ils répondent aux critères de mappage. Le test du certificat échoue si au moins un utilisateur, qu’il soit obsolète ou non, possède la valeur d’attribut considérée.

>[!NOTE]
>
>Vous ne pouvez pas modifier un mappage de certificat existant.

**Ajout d’un mappage de certificat**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Cliquez sur Nouveau mappage de certificats et dans la liste Pour l’émetteur, sélectionnez l’alias du certificat tel que configuré dans Trust Store Management.
1. Mappez l’un des attributs du certificat à un attribut d’utilisateur. Par exemple, vous pouvez mapper le nom commun du certificat à l’ID de connexion de l’utilisateur.

   Si le contenu de l’attribut dans le certificat est différent du contenu de l’attribut de l’utilisateur dans la base de données de User Management, vous pouvez utiliser une expression régulière Java (regex) pour faire correspondre les deux attributs. Par exemple, si les noms communs des certificats sont du type *Alex Dupont (Authentification)* et *Alex Dupont (Signature)* et si le nom commun dans la base de données de User Management est *Alex Dupont*, vous pouvez utiliser une expression regex pour extraire la partie requise de l’attribut du certificat (en l’occurrence, *Alex Dupont*). L’expression régulière que vous spécifiez doit être conforme à la spécification regex Java.

   Vous pouvez transformer cette expression en spécifiant l’ordre des groupes dans la zone Ordre personnalisé. L&#39;ordre personnalisé est utilisé avec la méthode `java.util.regex.Matcher.replaceAll()`. Le comportement observé correspond à celui de cette méthode et la chaîne d’entrée (l’ordre personnalisé) doit être spécifiée en conséquence.

   Pour tester l’expression regex, saisissez une valeur dans la zone Paramètre de test, puis cliquez sur Tester.

   Vous pouvez utiliser les caractères suivants dans l’expression regex :

   *  : (n’importe quel caractère)
   * &amp;ast; (0 occurrence ou plus)
   * () (spécifier le groupe entre parenthèses)
   * \ (permet d’utiliser un caractère regex en tant que caractère normal)
   * $n (permet de faire référence au énième groupe)

   Exemples d’expressions régulières :

   * Pour extraire « Alex Dupont » de « Alex Dupont (Authentification) »

      **Regex :** (.&amp;ast;) \(Authentification\)

   * Pour extraire « Alex Dupont » de « Alex (Authentification) Dupont »

      **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

   * Pour extraire « Dupont Alex » de « Alex (Authentification) Dupont »

      **Regex :** (.&amp;ast;)\(Authentification\) (.&amp;ast;)

      Ordre personnalisé : $2 $1 (renvoyer le second groupe concaténé au premier groupe, capturé par un caractère espace)

   * Pour extraire « adupont@orgexemple.fr » de « smtp:adupont@orgexemple.fr »

      **Regex :** smtp:(.&amp;ast;)
   Pour plus de détails sur l’utilisation des expressions régulières, reportez-vous au [Didacticiel Java sur les expressions régulières](https://java.sun.com/docs/books/tutorial/essential/regex/).

1. Dans la liste Pour le domaine, sélectionnez le domaine de l’utilisateur.
1. Pour tester cette configuration, cliquez successivement sur Parcourir pour télécharger un exemple de certificat utilisateur, sur Tester le certificat, et, si la configuration est correcte, sur OK.

**Modification d’un mappage de certificat**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration.
1. Cliquez sur Mappage de certificats.
1. Sélectionnez le mappage de certificats à modifier et modifiez sa configuration. Vous pouvez mettre à jour l’expression régulière et l’ordre personnalisé.
1. Pour tester vos modifications, cliquez successivement sur Parcourir pour télécharger un exemple de certificat, sur Tester le certificat, puis sur OK.

**Suppression d’un mappage de certificats**

1. Dans Administration Console, cliquez sur Paramètres > User Management > Configuration > Mappage de certificats.
1. Activez la case à cocher correspondant au mappage de certificat à supprimer, cliquez sur Supprimer puis sur OK.

