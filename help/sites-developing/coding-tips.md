---
title: Conseils pour bien coder
seo-title: Conseils pour bien coder
description: Conseils relatifs au codage pour AEM
seo-description: Conseils relatifs au codage pour AEM
uuid: 1bb1cc6a-3606-4ef4-a8dd-7c08a7cf5189
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 4adce3b4-f209-4a01-b116-a5e01c4cc123
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 88%

---


# Conseils pour bien coder{#coding-tips}

## Utiliser les taglibs ou HTL autant que possible {#use-taglibs-or-htl-as-much-as-possible}

L’ajout de scriptlets à des pages JSP complique le débogage du code. Par ailleurs, avec l’ajout de scriptlets à des pages JSP, il est difficile de séparer la logique métier de la partie Vue, ce qui constitue une violation du principe de responsabilité unique et du modèle de conception MVC.

### Écrire un code lisible {#write-readable-code}

Le code est écrit une seule fois, mais lu plusieurs fois. Mieux vaut déployer des efforts en amont pour nettoyer le code écrit pour qu’il soit facilement lu par les auteurs du code et d’autres développeurs.

### Choisir des noms représentatifs de l’intention {#choose-intention-revealing-names}

Idéalement, un autre programmeur ne devrait pas avoir à ouvrir un module pour en comprendre la fonction. De même, la fonction d’une méthode doit être comprise sans devoir être lue. Plus nous adhérons à ces principes, plus le code écrit est simple à lire et facile à modifier.

Dans la base de code AEM, les conventions suivantes sont utilisées :


* Une implémentation unique d&#39;une interface est nommée `<Interface>Impl`, c&#39;est-à-dire `ReaderImpl`.
* Plusieurs implémentations d’une interface sont nommées `<Variant><Interface>`, c’est-à-dire `JcrReader` et `FileSystemReader`.
* Les classes de base abstraites sont nommées `Abstract<Interface>` ou `Abstract<Variant><Interface>`.
* Les packages sont nommés `com.adobe.product.module`.  Chaque artefact Maven ou bundle OSGi doit avoir son propre module.
* Les implémentations Java sont placées dans un module impl sous leur API.


Notez que ces conventions ne doivent pas nécessairement s’appliquer aux implémentations des clients, mais il est important qu’elles soient définies et respectées pour que le code soit maintenable.

Idéalement, les noms doivent décrire clairement leur intention. Un test de code courant pour les noms qui ne sont pas aussi clairs qu&#39;ils devraient l&#39;être est la présence de commentaires expliquant à quoi sert la variable ou la méthode :

<table>
 <tbody>
  <tr>
   <td><p><strong>Manque de clarté</strong></p> </td>
   <td><p><strong>Effacer</strong></p> </td>
  </tr>
  <tr>
   <td><p>int d; //elapsed time in days</p> </td>
   <td><p>int elapsedTimeInDays;</p> </td>
  </tr>
  <tr>
   <td><p>//get tagged images<br /> public List getItems() {}</p> </td>
   <td><p>public List getTaggedImages() {}</p> </td>
  </tr>
 </tbody>
</table>

### Ne pas se répéter  {#don-t-repeat-yourself}

DRY indique que le même ensemble de code ne doit jamais être dupliqué. Cela s’applique également aux éléments de type littéraux de chaîne. La duplication de code ouvre la porte à des erreurs chaque fois que quelque chose doit être modifié. Il faut absolument l’éliminer.

### Éviter les règles CSS nues {#avoid-naked-css-rules}

Les règles CSS doivent être spécifiques à votre élément cible dans le contexte de votre application. Par exemple, une règle CSS appliquée à *.content .center* serait trop générale et pourrait finir par se répercuter sur de nombreux contenus dans votre système, obligeant les autres à contourner ce style. *.myapp-* centertextserait une règle plus spécifique car elle spécifie la  ** texture centrée dans le contexte de votre application.

### Ne pas utiliser d’API obsolètes {#eliminate-usage-of-deprecated-apis}

Lorsqu’une API est devenue obsolète, il est toujours préférable de suivre la nouvelle approche recommandée au lieu de continuer à utiliser l’API obsolète. Cela garantit la fluidité des mises à niveau.

### Écrire du code localisable {#write-localizable-code}

Toutes les chaînes qui ne sont pas fournies par un auteur doivent être enveloppées dans un appel au dictionnaire l18n d’AEM via *I18n.get()* en JSP/Java et *CQ.I18n.get ()* en JavaScript. Cette implémentation retourne la chaîne qui lui a été transmise si aucune n’est trouvée, ce qui permet de mettre en œuvre la localisation après l’implémentation des fonctionnalités dans la langue principale.

### Échapper les chemins de ressources pour garantir la sécurité {#escape-resource-paths-for-safety}

Bien que les chemins du JCR ne doivent pas contenir d’espaces, leur présence n’altère pas le fonctionnement du code. Jackrabbit fournit une classe utilitaire Text avec les méthodes *escape()* et *escapePath ()*. Pour les pages JSP, l’IU de Granite expose une fonction *granite:encodeURIPath () EL*.

### Utiliser l’API XSS et/ou HTL pour se protéger contre les attaques de script entre sites {#use-the-xss-api-and-or-htl-to-protect-against-cross-site-scripting-attacks}

AEM propose une API XSS pour nettoyer facilement les paramètres et garantir la sécurité contre des attaques de script entre sites. En outre, HTL propose des protections intégrées directement dans le langage de modèle. Un aide-mémoire API est disponible en téléchargement sur [Développement - Recommandations et meilleures pratiques](/help/sites-developing/dev-guidelines-bestpractices.md).

### Implémenter une journalisation appropriée {#implement-appropriate-logging}

Pour le code Java, AEM prend en charge slf4j comme API standard pour la journalisation des messages. Elle doit être utilisée avec les configurations mises à disposition via la console OSGi, pour des raisons de cohérence dans l’administration. Slf4j expose cinq niveaux de journalisation différents. Suivez les recommandations ci-après pour choisir le niveau auquel consigner un message :

* ERROR : si des éléments de code ne fonctionnent pas correctement et que le traitement ne peut pas continuer. L’erreur se produit notamment à la suite d’une exception inattendue. Il est généralement utile d’inclure des traces de pile dans ces scénarios.
* WARN : si des éléments de code ne fonctionnent pas correctement, mais que le traitement peut continuer. C’est souvent le résultat d’une exception attendue, par exemple, *PathNotFoundException*.
* INFO : informations utiles lors de la surveillance d’un système. Gardez à l’esprit qu’il s’agit de la valeur par défaut et que la plupart des clients la laissent sur leurs environnements. Par conséquent, ne les utilisez pas excessivement.
* DEBUG : informations de niveau inférieur sur le traitement. Utile lors du débogage d’un problème lié au support.
* TRACE : informations de niveau le plus bas, par exemple, entrée/sortie de méthodes. Niveau généralement utilisé par les développeurs uniquement.

Dans le cas de JavaScript, *console.log* ne doit être utilisé que pendant le développement et toutes les informations du journal doivent être supprimées avant sa diffusion.

### Éviter la programmation bête et méchante {#avoid-cargo-cult-programming}

Évitez de copier du code sans comprendre sa fonction. En cas de doute, il est toujours préférable de demander à quelqu’un qui a plus d’expérience avec le module ou l’API qui pose un problème.
