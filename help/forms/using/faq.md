---
title: Questions fréquentes (FAQ) des formulaires HTML5
seo-title: Questions fréquentes (FAQ) des formulaires HTML5
description: Questions fréquentes (FAQ) sur la mise en page, la prise en charge des scripts, et les plages des formulaires HTML5.
seo-description: Questions fréquentes (FAQ) sur la mise en page, la prise en charge des scripts, et les plages des formulaires HTML5.
uuid: 398e31de-3e46-4288-b3cd-39d51fa17abc
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 4b676e7e-191f-4a19-8b8f-fc3e30244b59
docset: aem65
translation-type: tm+mt
source-git-commit: c74d9e86727f2deda62b8d1eb105b28ef4b6d184
workflow-type: tm+mt
source-wordcount: '1970'
ht-degree: 82%

---


# Questions fréquentes (FAQ) des formulaires HTML5{#frequently-asked-questions-faq-for-html-forms}

Questions fréquentes (FAQ) sur la mise en page, la prise en charge des scripts, et les plages des formulaires HTML5.

## Mise en page {#layout}

1. Pourquoi les codes à barres et le champ de signature ne s’affichent-ils pas dans mon formulaire ?

   Réponse : les champs de codes à barres et de signatures ne sont pas adaptés aux cas de figures impliquant du HTML ou des périphériques mobiles. Ces champs s’affichent sous la forme d’une zone non interactive. Cependant, AEM Forms Designer propose un nouveau champ de saisie tactile de signature qui peut être utilisé à la place du champ de signature. Vous pouvez également ajouter un [widget personnalisé](../../forms/using/custom-widgets.md) pour les codes à barres et l’intégrer.

1. Le texte enrichi est-il pris en charge par le champ de texte XFA ?

   Réponse : le champ XFA, qui supporte le contenu enrichi dans AEM Forms Designer, n’est pas pris en charge ; il est généré sous forme de texte normal sans prise en charge du style du texte à partir de l’interface utilisateur. En outre, les champs XFA possédant la propriété comb sont affichés sous forme de champs normaux, bien qu’il existe encore des restrictions quant au nombre de caractères autorisés en fonction de la valeur des chiffres comb.

1. Existe-t-il des restrictions concernant l’utilisation de sous-formulaires répétables ?

   Réponse : les sous-formulaires répétables doivent avoir un nombre initial d’au moins 1. Les sous-formulaires répétables avec un nombre initial de zéro ne sont pas pris en charge. Vous pouvez également choisir d’utiliser un sous-formulaire répétable et ne pas l’afficher lorsque le formulaire est chargé. Pour réaliser le cas d’utilisation : 

   1. Définissez le nombre initial de sous-formulaire répétable sur 1.

      ![nombre initial](assets/intial-count.png)

   1. Utilisez l’événement initialize du formulaire pour masquer l’instance principale du sous-formulaire. Par exemple, le code ci-dessous masque l’instance principale du sous-formulaire lors de l’initialisation du formulaire. Il vérifie également le type d’application pour s’assurer que le script est exécuté uniquement du côté client : 

      ```javascript
      if ((xfa.host.appType == "HTML 5" || xfa.host.appType == "Exchange-Pro" || xfa.host.appType == "Reader")&&(_RepeatSubform.count == 1)&&(form1.Page1.Subform1.RepeatSubform.Key.rawValue == null)) {
      RepeatSubform.presence = "hidden";
      }
      ```

   1. Ouvrez le script pour ajouter une instance du sous-formulaire pour la modifier. Ajoutez le code comme ci-dessous pour ajouter une instance du script de sous-formulaire.

      Le code ci-dessous vérifie l’instance masquée du sous-formulaire. Si l’instance masquée du sous-formulaire est trouvée, supprimez-la et insérez une nouvelle instance du sous-formulaire. Si l’instance masquée du sous-formulaire est introuvable, insérez simplement une nouvelle instance du sous-formulaire.

      ```javascript
      if (RepeatSubform.presence == "hidden")
      {
      RepeatSubform.instanceManager.insertInstance(0);
      RepeatSubform.instanceManager.removeInstance(1);
      }
      else
      {
      RepeatSubform.instanceManager.addInstance(1);
      }
      ```

   1. Ouvrez le script pour enlever une instance du sous-formulaire pour modification. Ajoutez le code comme suit pour supprimer une instance du script du sous-formulaire.

      Le code vérifie le nombre de sous-formulaires. Si le nombre de sous-formulaire a atteint 1, le code masque le sous-formulaire au lieu de le supprimer.

      ```javascript
      if (RepeatSubform.instanceManager.count == 1) {
      RepeatSubform.presence = "hidden";
      } else {
      RepeatSubform.instanceManager.removeInstance(RepeatSubform.instanceManager.count - 1);
      }
      ```

   1. Ouvrez l’événement presubmit du formulaire pour le modifier. Ajoutez le script suivant à l’événement pour supprimer l’instance masquée du script avant de le modifier. Il empêche l’envoi de données du sous-formulaire masqué lors de l’envoi.

      ```javascript
      if(RepeatSubform.instanceManager.count == 1 && RepeatSubform.presence == "hidden") {
      RepeatSubform.instanceManager.removeInstance(0);
      }
      ```

1. Existe-t-il des restrictions concernant l’utilisation de sous-formulaires masqués ?

   Réponse : un sous-formulaire masqué avec une hiérarchie complexe fractionnée sur plusieurs pages génère des problèmes de mise en page. Une façon de contourner ce problème consiste à marquer le sous-formulaire visible au début, puis de le masquer dans un script d’initialisation basé sur une logique ou des données.

1. Pourquoi un texte est-il tronqué ou s’affiche-t-il incorrectement dans HTML5 ?

   Réponse : lorsque l’espace attribué à un champ de texte constitué d’une illustration ou d’une légende est insuffisant et ne lui permet pas d’afficher le contenu, le texte apparaît tronqué dans le formulaire pour périphériques mobiles généré. Cette troncature est également visible dans la vue de conception de AEM Forms Designer. Bien que cette troncature puisse être prise en charge dans les fichiers PDF, ce n’est pas le cas dans les formulaires HTML5. Pour éviter ce problème, assurez-vous de prévoir un espace suffisant pour qu’un champ de texte constitué d’une illustration ou d’une légende puisse s’afficher sans être tronqué dans le mode de conception de AEM Forms Designer.

1. Je constate des problèmes de mise en page liés à du contenu manquant ou à des chevauchements. Quelle en est la raison ?

   Réponse : S’il existe un élément Texte de dessin ou Image de dessin avec un autre élément se chevauchant à la même position (un rectangle, par exemple), le contenu Texte de dessin n’est pas visible s’il apparaît plus loin dans l’ordre de document (dans la vue de la hiérarchie de Designer AEM Forms). Le format PDF prend en charge la mise en calque transparente mais ce n’est pas le cas du HTML et des navigateurs.

1. Pourquoi certaines polices affichées dans le formulaire HTML sont-elles différentes de celles utilisées lors de la conception du formulaire ?

   Réponse : les formulaires HTML5 n’intègrent pas de polices (contrairement aux formulaires PDF où les polices sont intégrées au formulaire). Pour la version HTML du formulaire à générer comme prévu, assurez -vous que les polices indiquées dans le XDP sont disponibles sur le serveur et sur l’ordinateur client. Si les polices requises ne sont pas disponibles sur le serveur, les polices de secours sont utilisées. De plus, si vous utilisez des polices dans le modèle de formulaire qui ne sont pas disponibles sur le périphérique client, les polices par défaut du navigateur sont utilisées pour le rendu du texte.

1. Les attributs d’alignement vertical et horizontal sont-ils pris en charge dans les formulaires HTML ? 

   Oui, ils le sont. L’attribut vAlign n’est pas pris en charge dans Internet Explorer et dans le champ multiligne.

1. Les formulaires HTML5 prennent-ils en charge les caractères de l’hébreu ?

   Les formulaires HTML5 prennent en charge les caractères de l’hébreu tous les navigateurs, à l’exception de Microsoft Internet Explorer.

1. Existe-t-il des limites de caractères dans les champs numériques des formulaires HTML5 ?

   Réponse : Oui, les formulaires HTML5 ont quelques limites. Si le nombre de chiffres dépasse celui indiqué dans la clause d’image, les numéros ne sont pas traduits et s’affichent dans les paramètres régionaux anglais.

1. Pourquoi les formulaires HTML sont-ils plus volumineux que les formulaires PDF ?

   De nombreuses structures et objets de données intermédiaires tels que les DOM du formulaire, les DOM de données, les DOM de disposition sont requis pour rendre un XDP sur un formulaire HTML.

   Pour les formulaires PDF, Adobe Acrobat dispose d’un moteur XTG intégré pour créer des structures de données intermédiaires, et des objets. Acrobat prend également en charge la présentation et les scripts.

   Pour les formulaires HTML5, les navigateurs n’ont pas de moteur XTG intégré pour créer les structures de données intermédiaires, et les objets à partir d’octets bruts XDP. Ainsi, pour les formulaires HTML5, les objets intermédiaires sont générés sur le serveur et envoyés au client. Sur le client, les scripts basés sur JavaScript et le moteur de mise en page utilisent ces structures intermédiaires.

   La taille de la structure intermédiaire dépend de la taille du XDP original et des données fusionnées avec XDP.

1. Existe-t-il des restrictions concernant l’utilisation des tableaux dans mon xdp ?

   Réponse : Les tableaux complexes provoquent des problèmes de rendu.

   * La section (SubformSet) à l’intérieur d’un tableau n’est pas prise en charge.
   * Les lignes d’en-tête ou de pied de page dans certains tableaux sont marquées pour la répétition. Le fractionnement de ces tableaux sur plusieurs pages peut conduire à certains problèmes.

1. Les tableaux accessibles sont-ils soumis à des restrictions ?

   Réponse : Oui, les tableaux accessibles présentent les restrictions suivantes :

   * Les tableaux imbriqués et le sous-formulaire à l’intérieur d’un tableau ne sont pas pris en charge.
   * Les en-têtes sont uniquement pris en charge pour la ligne supérieure ou les colonnes de gauche du tableau. Les en-têtes ne sont pas pris en charge pour les éléments de mi-tableau. Vous pouvez appliquer des en-têtes à plusieurs lignes et les en-têtes de colonne sont pris en charge si toutes les lignes et colonnes sont associées à la ligne la plus élevée ou la colonne la plus à gauche du tableau.
   * `Rowspan`et `colspan` ne sont pas pris en charge depuis un emplacement aléatoire du tableau.

   * Vous ne pouvez pas dynamiquement ajouter ou supprimer l’occurrence des lignes contenant des éléments possédant une valeur rowspan supérieure à 1.

1. Quel est l’ordre de lecture de l’info-bulle et de la légende pour les lecteurs d’écran ?

   * Lorsqu’il y a une légende et une info-bulle, seule la légende est lue. Si la légende n’est pas disponible, l’info-bulle est lue. Vous pouvez également spécifier la priorité de lecture dans un fichier XDP en utilisant le concepteur de formulaires
   * Lorsque vous survolez un élément, l’info-bulle s’affiche. Si aucune info-bulle n’est disponible, le texte vocal s’affiche. Si aucun texte vocal n’est disponible, le nom du champ s’affiche.

1. Lorsque vous survolez un champ, une info-bulle s’affiche. Comment désactiver cette fonction ?

   Pour désactiver l’affichage d’info-bulle lorsque vous survolez un champ, choisissez Aucun dans le panneau Accessibilité de Designer.

1. Dans Designer, un utilisateur peut configurer les propriétés personnalisées d’aspect des boutons radio et des cases à cocher. Lors du rendu des formulaires, les formulaires HTML5 prennent-ils en compte ces propriétés d’aspect personnalisées ?

   Réponse : Les formulaires HTML5 ignorent les propriétés personnalisées d’aspect des boutons radio et des cases à cocher. Les boutons radio et les cases à cocher s’affichent selon les spécifications du navigateur sous-jacent.

1. Lorsqu’un formulaire HTML5 est ouvert dans un navigateur pris en charge, la bordure des champs placés de manière adjacente n’est pas alignée correctement ou les sous-formulaires se chevauchent. Lorsque le même formulaire HTML5 est prévisualisé dans Forms Designer, les champs et la mise en page semblent correctement alignés et les sous-formulaires apparaissent dans la bonne position. Comment corriger le problème ?

   Lorsqu’un sous-formulaire peut enchaîner un contenu et qu’il présente un élément de bordure masqué, la bordure des champs placés de manière adjacente n’est pas alignée correctement ou les sous-formulaires se chevauchent. Pour résoudre le problème, vous pouvez supprimer ou commenter les éléments &lt;border> masqués du fichier XDP correspondant. Par exemple, l’élément &lt;border> suivant est marqué comme commentaire :

   ```xml
               <!--<border>
                  <edge presence="hidden"/>
                  <corner thickness="0.175mm" presence="hidden"/>
               </border> -->
   ```

1. Pourquoi les lecteurs d’écran ne fonctionnent pas correctement avec l’objet de champ Date/Heure ?

   Les lecteurs d’écran ne prennent pas en charge les champs Date/Heure. Cependant, vous pouvez saisir manuellement la date et l’heure du champ pour que le lecteur d’écran le lise. Utilisez du texte d’info-bulle ou de lecteur d’écran pour indiquer à l’utilisateur de sélectionner manuellement la date et l’heure du champ.

1. Les formulaires HTML5 prennent-ils en charge les modèles d’affichage des champs flottants ?

   Réponse : Les formulaires HTML5 ne prennent pas en charge les modèles d’affichage pour les champs flottants.

### Script {#scripting}

1. Existe-t-il des restrictions de mise en œuvre JavaScript pour les formulaires HTML ?

   Réponse:

   * La prise en charge du script xfa.connectionSet est limitée. Pour connectionSet, seul l’appel côté serveur du service Web est pris en charge. For detailed information, see [Scripting Support](/help/forms/using/scripting-support.md).
   * Il n’existe aucune prise en charge de $record et $data dans les scripts côté client. Cependant, si les scripts sont écrits dans un bloc formReady ou layoutReady, les scripts fonctionnent toujours car ces événements s’exécutent côté serveur.
   * Les scripts spécifiques des éléments XFA constitués d’illustrations (ou les éléments de texte constitués de légendes quand il s’agit de champs) ne sont pas pris en charge.

1. Existe-t-il des restrictions concernant l’utilisation de formCalc ?

   Réponse : seul un sous-ensemble de scripts formCalc est actuellement implémenté. For detailed information, see [Scripting Support](/help/forms/using/scripting-support.md).

1. Existe-t-il une convention de dénomination recommandée et des mots-clés réservés à éviter ?

   * Dans AEM Forms Designer, il est recommandé de ne pas faire commencer le nom d’un objet (tel qu’un sous-formulaire ou un champ de texte) par un tiret bas (_). Pour utiliser un trait de soulignement au début du nom, ajoutez un préfixe après le trait de soulignement, _&lt;prefix>&lt;objectname>.
   * Toutes les API des formulaires HTML5 API sont des mots-clés réservés. Pour les API/fonctions personnalisées, utilisez un nom différent de celui des [API de formulaires HTML5](/help/forms/using/scripting-support.md).

1. Les formulaires HTML5 prennent-ils en charge les champs flottants ?

   Oui, les formulaires HTML5 prennent en charge les champs flottants. Pour permettre l’utilisation de champs flottants, ajoutez la propriété suivante au profil de rendu :

   >[!NOTE]
   >
   >Le flottement des champs n’est pas activé par défaut. Vous pouvez utiliser Forms Designer pour définir la propriété de flottement des champs.

   1. Open CRXde lite and navigate to the `/content/xfaforms/profiles/default` node.
   1. Add a property `mfDataDependentFloatingField`of type String and set the value of the property to `true`.
   1. Cliquez sur **Enregistrer tout**. Désormais, les champs flottants sont activés pour les formulaires HTML à l’aide du profil de rendu mis à jour.

      >[!NOTE]
      >
      >Pour activer les champs flottants pour un formulaire spécifique sans mettre à jour le profil de rendu, transmettez la propriété mfDataDependentFloatingField=true en tant que paramètre d’URL.

1. Les formulaires HTML5 exécutent-ils le script d’initialisation et forment-ils des événements prêts plusieurs fois ?

   Oui, les scripts d’initialisation et les événements prêts pour le formulaire sont exécutés plusieurs fois, au moins une fois sur le serveur et une fois côté client. Il est conseillé d’écrire des scripts tels que initialize ou form:ready événements en fonction d’une logique métier (données de formulaire ou de champ) afin que l’action soit exécutée en fonction de l’état des données et de l’idempotent (si les données sont identiques).

### Conception XDP {#designing-xdp}

1. Existe -t-il des mots-clés réservés dans les formulaires HTML5 ?

   Réponse : toutes les API des formulaires HTML5 sont des mots-clés réservés. Pour les API/fonctions personnalisées, utilisez un nom différent de celui des [API de formulaires HTML5](/help/forms/using/scripting-support.md). Outre les mots-clés réservés, si vous utilisez des noms d’objet qui commencent par un tiret bas (_), il est recommandé d’ajouter un préfixe unique à sa suite. L’ajout d’un préfixe permet d’éviter tout conflit possible avec les API internes des formulaires HTML5. Par exemple, `_fpField1`
