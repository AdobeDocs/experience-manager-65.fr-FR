---
title: Nouveau service de rendu et d’envoi
description: Définissez les services de rendu et de soumission dans Workbench pour afficher le formulaire XDP au format HTML ou PDF en fonction de l’appareil à partir duquel vous y accédez.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 46de0101-9607-4429-84c3-7c1f34d2da27
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '891'
ht-degree: 100%

---

# Nouveau service de rendu et d’envoi{#new-render-and-submit-service}

## Présentation {#introduction}

Dans Workbench, lorsque vous définissez une opération `AssignTask`, spécifiez un formulaire particulier (XDP ou PDF). Spécifiez également un ensemble de services de rendu et de soumission, via un profil d’action.

Un XDP peut être rendu sous la forme d’un formulaire PDF ou d’un formulaire HTML. Les nouvelles fonctionnalités incluent la possibilité d’effectuer les actions suivantes :

* Rendre et soumettre un formulaire XDP au format HTML
* Rendre et soumettre un formulaire XDP au format PDF sur ordinateur et au format HTML sur les appareils mobiles (par exemple, un iPad)

### Nouveau service HTML de Forms {#new-html-forms-service}

Le nouveau service HTML de Forms exploite la nouvelle fonction dans Forms pour prendre en charge le rendu de formulaire XDP au format HTML. Le nouveau service HTML de Forms expose les méthodes suivantes :

```java
/*
 * Generates a URL (for the HTML Form) to be passed to client, given a TaskContext.
 * The output of this API is something like this - /lc/content/xfaforms/profiles/default.ws.html?ContentRoot=repository://Applications/MyApplication/MyFolder&template=MyForm.xdp
 * @param taskContext task context
 * @param profileName Forms servlet URL.
 * @return form URL string
 */
public String generateFormURL(TaskContext taskContext, String profileName);

/*
 * Render the XDP Form as HTML. Can be used directly for updating the runtimeMap in render.
 * It adds the following keys to the map -
 * hint:new html form = true
 * newHTMLFormURL = the URL returned after calling 'generateFormURL' API.
 * @param TaskContext taskContext
 * @param profileName Forms servlet URL.
 * @param runtimeMap runtime map<string,object> associated with form rendering.
 * return runtimeMap
 */
public Map<String, Object> renderHTMLForm (TaskContext taskContext, String profileName, Map<String,Object> runtimeMap);
```

Vous trouverez plus d’informations sur les profils de formulaire mobile dans [Création d’un profil personnalisé](/help/forms/using/custom-profile.md).

## Nouveaux processus de rendu et de soumission de formulaires HTML {#new-html-form-render-amp-submit-processes}

Pour chaque opération « AssignTask », spécifiez un processus de rendu et d’envoi avec le formulaire. Ces processus sont appelés par les API TaskManager `renderForm` et `submitForm` pour autoriser la gestion personnalisée. Sémantique de ces processus pour le nouveau formulaire HTML :

### Rendre un nouveau formulaire HTML {#render-a-new-html-form}

Le nouveau processus de rendu HTML, comme tout processus de rendu, a les paramètres d’E/S suivants :

Entrée - `taskContext`

Sortie - `runtimeMap`

Sortie - `outFormDoc`

Cette méthode simule le comportement exact de l’API `renderHTMLForm` du NewHTMLFormsService. Elle appelle l’API `generateFormURL` pour obtenir l’URL pour le rendu HTML du formulaire. Il remplit ensuite le runtimeMap avec la ou les clés ou valeurs suivantes :

Nouveau formulaire HTML = true

newHTMLFormURL = l’URL renvoyé après avoir appelé l’API `generateFormURL`.

### Soumettre un nouveau formulaire HTML {#submit-a-new-html-form}

Ce processus de soumission d’un nouveau formulaire HTML fonctionne avec les paramètres d’E/S suivants :

Entrée - `taskContext`

Sortie - `runtimeMap`

Sortie - `outputDocument`

Le processus définit le `outputDocument` sur le `inputDocument` récupéré de `taskContext`.

## Processus de rendu ou de soumission par défaut et profils d’action {#default-render-or-submit-processes-and-action-profiles}

Les services de rendu et de soumission par défaut permettent de prendre en charge le rendu des fichiers PDF sur un ordinateur de bureau et du HTML sur les appareils mobiles (iPad).

### Rendu du formulaire par défaut {#default-render-form}

Ce processus rend un formulaire XDP sur plusieurs plates-formes en toute simplicité. Le processus récupère l’agent utilisateur de `taskContext`, et utilise les données pour appeler le processus pour le rendu HTML ou PDF.

![default-render-form](assets/default-render-form.png)

### Soumission du formulaire par défaut {#default-submit-form}

Ce processus envoie un formulaire XDP sur plusieurs plates-formes en toute simplicité. Il récupère l’agent utilisateur de `taskContext` et utilise les données pour appeler le processus pour l’envoi HTML ou PDF.

![default-submit-form](assets/default-submit-form.png)

## Basculer le rendu des formulaires mobiles du PDF au HTML {#switch-the-rendering-of-mobile-forms-from-pdf-to-html}

Les navigateurs retirent progressivement la prise en charge des plug-ins basés sur NPAPI, notamment les plug-ins pour Adobe Acrobat et Adobe Acrobat Reader. Vous pouvez modifier le rendu des formulaires mobiles de PDF en HTML en procédant comme suit :

1. Connectez-vous à Workbench en tant qu’utilisateur ou utilisatrice valide.
1. Sélectionnez **Fichier** > **Obtenir les applications**.

   La boîte de dialogue Obtenir les applications s’affiche.

1. Choisissez les applications pour lesquelles vous voulez changer le rendu de formulaire mobile, puis cliquez sur **OK**.
1. Ouvrez le processus pour lequel vous souhaitez modifier le rendu.
1. Ouvrez le point de départ/la tâche ciblé(e), accédez à la section Présentation et Données, puis cliquez sur **Gérer les profils d’action**.

   La boîte de dialogue Gérer les profils d’action apparaît.
1. Redéfinissez les configurations de profil de rendu par défaut de PDF à HTML, puis cliquez sur **OK**.
1. Enregistrez le processus.
1. Répétez les étapes afin de changer le rendu pour d’autres processus.
1. Déployez l’application adaptée aux processus que vous avez modifiés.

### Profil d’action par défaut {#default-action-profile}

Le profil d’action par défaut a rendu le formulaire XDP au format PDF. Ce comportement a maintenant été modifié pour utiliser les processus de rendu de formulaires par défaut et de soumission de formulaires par défaut.

Voici quelques questions fréquemment posées sur les profils d’action :

![gen_question_b_20](assets/gen_question_b_20.png) **Quels processus de rendu / d’envoi seront disponibles prêt à l’emploi ?**

* Render Guide (Guides est obsolète)
* Guide de rendu du formulaire
* Rendre le formulaire PDF
* Rendre le formulaire HTML
* Rendre le nouveau formulaire HTML (nouveau)
* Rendu de formulaire par défaut (nouveau)

Et des processus de soumission équivalents.

![gen_question_b_20](assets/gen_question_b_20.png) **Quels profils d’action seront disponibles prêt à l’emploi ?**

Pour les formulaires XDP :

* Par défaut (rendu/soumission à l’aide des nouveaux processus « Rendu/Soumission par défaut »)

![gen_question_b_20](assets/gen_question_b_20.png) **Que doit faire le concepteur du processus pour que le formulaire puisse être rendu au format HTML sur un périphérique et au format PDF sur un bureau ?**

Rien. Le profil d’action par défaut est choisi automatiquement et le mode de rendu est également pris en charge automatiquement.

![gen_question_b_20](assets/gen_question_b_20.png) **Que faire pour que le formulaire puisse être rendu au format HTML sur un bureau ?**

L’utilisateur doit sélectionner le bouton radio HTML pour le profil par défaut.

![gen_question_b_20](assets/gen_question_b_20.png) **Y aura-t-il un impact de mise à niveau en cas de changement du comportement du profil d’action par défaut ?**

Oui ; étant donné que le rendu précédent et les services d’envoi associés au profil d’action par défaut étaient différents, ils sont gérés en tant que personnalisations des formulaires existants. En cliquant sur **Restaurer les paramètres par défaut**, les services de rendu / d’envoi par défaut sont définis.

Si vous aviez modifié les services liés aux formulaires PDF de rendu/d’envoi existants ou aviez créé des services personnalisés (par exemple, custom1) et souhaitez maintenant utiliser la même fonctionnalité pour un rendu HTML : Vous devez répliquer le nouveau service de rendu/d’envoi (par exemple, en tant que custom2) et appliquer des personnalisations identiques. Maintenant, modifiez le profil d’action de votre fichier XDP pour commencer à utiliser les services custom2, au lieu du custom1 pour le rendu ou la soumission.

Que doit faire le concepteur de processus pour que le formulaire puisse être rendu au format HTML sur un appareil et au format PDF sur un bureau ?
Que doit faire le concepteur de processus pour que le formulaire puisse être rendu au format HTML sur un appareil et au format PDF sur un bureau ?
