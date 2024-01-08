---
title: Exportation de fragments d’expérience vers Adobe Target
description: Découvrez comment exporter des fragments d’expérience Adobe Experience Manager (AEM) vers Adobe Target.
contentOwner: carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: f2921349-de8f-4bc1-afa2-aeace99cfc5c
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '1513'
ht-degree: 62%

---

# Exportation de fragments d’expérience vers Adobe Target {#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>Certaines fonctionnalités de cette page nécessitent l’application d’AEM 6.5.3.0 (ou version ultérieure).
>
>6.5.3.0 :
>
>* Les **domaines de l’externaliseur** peuvent maintenant être sélectionnés.
>  **Remarque :** Les domaines de l’externaliseur ne sont pertinents que pour le contenu du fragment d’expérience envoyé à Target, et non pour les métadonnées telles que Afficher le contenu de l’offre.
>
>6.5.2.0 :
>
>* Les fragments d’expérience peuvent être exportés vers :
>
>   * l’espace de travail par défaut ;
>   * un espace de travail donné, spécifié dans la configuration cloud.
>   * **Remarque :** l’exportation vers des espaces de travail spécifiques nécessite Adobe Target Premium.
>
>* AEM doit être [intégré à Adobe Target à l’aide d’IMS](/help/sites-administering/integration-target-ims.md).
>
>AEM 6.5.0.0 et 6.5.1.0 :
>
>* Les fragments d’expérience AEM sont exportés dans l’espace de travail par défaut d’Adobe Target.
>* AEM doit être intégré à Adobe Target conformément aux instructions de la section [Intégration à Adobe Target](/help/sites-administering/target.md).

Vous pouvez exporter les [Fragments d’expérience](/help/sites-authoring/experience-fragments.md), créés dans Adobe Experience Manager (AEM), dans Adobe Target (Target). Ils peuvent ensuite être utilisés comme offres dans les activités Target, pour tester et personnaliser des expériences à grande échelle.

Il existe trois options de format pour exporter un fragment d’expérience vers Adobe Target :

* HTML (par défaut) : prise en charge de la diffusion de contenu web et hybride
* JSON : prise en charge de la diffusion de contenu découplé
* HTML et JSON

Les fragments d’expérience AEM peuvent être exportés vers l’espace de travail par défaut dans Adobe Target ou vers des espaces de travail définis par l’utilisateur pour Adobe Target. Cette opération s’effectue à l’aide de la console Adobe Developer, pour laquelle AEM doit être [intégré à Adobe Target à l’aide d’IMS](/help/sites-administering/integration-target-ims.md).

>[!NOTE]
>
>Les espaces de travail Adobe Target n’existent pas dans Adobe Target lui-même. Ils sont définis et gérés dans Adobe IMS (Identity Management System), puis sélectionnés pour une utilisation dans toutes les solutions à l’aide de la console Adobe Developer.

>[!NOTE]
>
>Les espaces de travail Adobe Target peuvent être utilisés pour permettre aux membres d’une organisation (groupe) de créer et de gérer des offres et des activités pour cette organisation uniquement ; sans donner accès à d’autres utilisateurs. Par exemple, les organisations spécifiques à un pays avec une préoccupation mondiale.

>[!NOTE]
>
>Pour plus d’informations, consultez également :
>
>* [Développement d’Adobe Target](https://developers.adobetarget.com/)
>* [Composants principaux - Fragments d’expérience](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)
>

## Prérequis {#prerequisites}

>[!CAUTION]
>
>Certaines fonctionnalités de cette page nécessitent l’application d’AEM 6.5.3.0.

Plusieurs actions sont requises :

1. Vous devez [intégrer AEM à Adobe Target à l’aide d’IMS](/help/sites-administering/integration-target-ims.md).
2. Les fragments d’expérience sont exportés à partir de l’instance d’auteur AEM. Vous devez donc [Configuration de l’externaliseur de liens d’AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer) sur l’instance d’auteur pour vous assurer que toutes les références contenues dans le fragment d’expérience sont externalisées pour la diffusion web.

   >[!NOTE]
   >
   >Pour la réécriture de liens, non couverte par le format par défaut, il existe un [fournisseur de réécriture de liens des fragments d’expérience](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Vous pouvez ainsi développer des règles personnalisées pour votre instance.

## Ajoutez la configuration du cloud {#add-the-cloud-configuration}

Avant d’exporter un fragment, vous devez ajouter la variable **Configuration du cloud** pour **Adobe Target** au fragment ou au dossier. Vous pouvez ainsi :

* définir les options de format à utiliser pour l&#39;export ;
* sélectionner un espace de travail Target comme destination ;
* sélectionner un domaine Externalizer pour réécrire des références dans le fragment d’expérience (facultatif) ;

Vous pouvez sélectionner les options obligatoires dans les **propriétés de page** du dossier ou du fragment concerné. La spécification sera héritée, le cas échéant.

1. Accédez à la console **Fragments d’expérience**.

1. Ouvrez les **propriétés de page** pour le dossier ou le fragment approprié.

   >[!NOTE]
   >
   >Si vous ajoutez la configuration cloud au dossier parent Fragment d’expérience, celle-ci est héritée par tous les enfants.
   >
   >
   >Si vous ajoutez la configuration cloud au fragment d’expérience lui-même, celle-ci est héritée par toutes les variations.

1. Sélectionnez l’onglet **Services cloud**.

1. Sous **Configuration du service cloud**, sélectionnez **Adobe Target** dans la liste déroulante.

   >[!NOTE]
   >
   >Le format JSON d’une offre de fragment d’expérience peut être personnalisé. Pour ce faire, définissez un composant de fragment d’expérience client, puis annotez comment exporter ses propriétés dans le modèle Sling du composant.
   >
   >Voir le composant principal :
   >
   >[Composants principaux - Fragments d’expérience](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/experience-fragment.html)

   Sous **Adobe Target** sélectionnez :

   * la configuration appropriée ;
   * l’option de format requise ;
   * un espace de travail Adobe Target ;
   * si nécessaire : domaine Externalizer

   >[!CAUTION]
   >
   >Le domaine Externalizer est facultatif.
   >
   >Un externaliseur d’AEM est configuré lorsque vous souhaitez que le contenu exporté pointe vers un *publier* domaine. Pour plus d’informations, voir [Configuration de l’externaliseur de liens d’AEM](/help/sites-administering/target-requirements.md#configuring-the-aem-link-externalizer).
   >
   >Notez également que les domaines de l’externaliseur sont pertinents uniquement pour le contenu du fragment d’expérience envoyé à Target, et non pour les métadonnées telles que Afficher le contenu de l’offre.

   Par exemple, pour un dossier :

   ![Dossier - Cloud Services](assets/xf-target-integration-01.png "Dossier - Cloud Services")

1. **Enregistrer et fermer**.

## Exportation d’un fragment d’expérience vers Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>Pour les contenus multimédias, comme les images, une seule référence est exportée vers Target. La ressource elle-même reste stockée dans AEM Assets et est diffusée à partir de l’instance de publication AEM.
>
>C’est pourquoi le fragment d’expérience, avec toutes les ressources associées, doit être publié avant l’exportation vers Target.

Pour exporter un fragment d’expérience d’AEM vers Target (après avoir spécifié la configuration cloud) :

1. Accédez à la console Fragment d’expérience.
1. Sélectionnez le fragment d’expérience que vous souhaitez exporter vers Target.

   >[!NOTE]
   >
   >Il doit s’agir d’une variation web de fragment d’expérience.

1. Cliquez sur **Exporter vers Adobe Target**.

   >[!NOTE]
   >
   >Si le fragment d’expérience a déjà été exporté, sélectionnez **Mettre à jour dans Adobe Target**.

1. Cliquez sur **Exportation sans publication** ou **Publier** selon les besoins.

   >[!NOTE]
   >
   >Sélection **Publier** publie immédiatement le fragment d’expérience et l’envoie à Target.

1. Cliquez sur **OK** dans la boîte de dialogue de confirmation.

   Votre fragment d’expérience doit maintenant se trouver dans Target.

   >[!NOTE]
   >
   >[Divers détails](/help/sites-authoring/experience-fragments.md#details-of-your-experience-fragment) sur l’exportation sont visibles dans la vue **Liste** de la console et dans les **Propriétés**.

   >[!NOTE]
   >
   >Lors de l’affichage d’un fragment d’expérience dans Adobe Target, la date de *dernière modification* affichée correspond à la date de la dernière modification du fragment dans AEM, et non à celle de la dernière exportation du fragment vers Adobe Target.

>[!NOTE]
>
>Vous pouvez également effectuer l’exportation à partir de l’éditeur de page à l’aide de commandes comparables dans le menu [Informations sur la page](/help/sites-authoring/author-environment-tools.md#page-information).

## Utilisation de vos fragments d’expérience dans Adobe Target {#using-your-experience-fragments-in-adobe-target}

Après avoir effectué les tâches précédentes, le fragment d’expérience s’affiche sur la page Offres dans Adobe Target. Consultez la [documentation spécifique de Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html) pour en savoir plus sur ce que vous pouvez y réaliser.

>[!NOTE]
>
>Lors de l’affichage d’un fragment d’expérience dans Adobe Target, la date de *dernière modification* affichée correspond à la date de la dernière modification du fragment dans AEM, et non à celle de la dernière exportation du fragment vers Adobe Target.

## Suppression d’un fragment d’expérience déjà exporté vers Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

La suppression d’un fragment d’expérience qui a déjà été exporté vers Target peut entraîner des problèmes si le fragment est déjà utilisé dans une offre dans Adobe Target. La suppression du fragment rendrait l’offre inutilisable, car le fragment de contenu est fourni par AEM.

Pour éviter de telles situations :

* Si le fragment d’expérience n’est pas actuellement utilisé dans une activité, AEM permet à l’utilisateur ou à l’utilisatrice de le supprimer sans message d’avertissement.
* Si le fragment d’expérience est en cours d’utilisation par une activité dans Adobe Target, un message d’erreur avertit l’utilisateur AEM des conséquences possibles de la suppression du fragment sur l’activité.

  Le message d’erreur apparu dans AEM n’empêche pas à l’utilisateur de forcer la suppression du fragment d’expérience. Lorsque le fragment d’expérience est supprimé :

   * l’offre Target qui utilise le fragment d’expérience AEM peut souffrir d’un comportement indésirable ;

      * l’offre effectue toujours le rendu, car le code HTML du fragment d’expérience a été transmis à Target ;
      * les références du fragment d’expérience peuvent ne pas fonctionner correctement si les ressources référencées ont également été supprimées dans AEM.

   * Toute modification supplémentaire apportée au fragment d’expérience est impossible, car le fragment d’expérience n’existe plus dans AEM.


## Suppression de bibliothèques clientes des fragments d’expérience exportés vers Target {#removing-clientlibs-from-fragments-exported-target}

Les fragments d’expérience contiennent des balises HTML complètes et toutes les bibliothèques clientes (CSS/JS) nécessaires pour effectuer le rendu du fragment tel qu’il a été créé par l’auteur de contenu du fragment d’expérience. Cela est intentionnel.

Lors de l’utilisation d’une offre de fragment d’expérience avec Adobe Target sur une page diffusée par AEM, la page ciblée contient déjà toutes les bibliothèques clientes nécessaires. En outre, le code HTML superflu dans l’offre de fragment d’expérience n’est pas nécessaire non plus (voir les [Considérations](#considerations)).

Voici un pseudo-exemple du code HTML d’une offre de fragment d’expérience :

```html
<!DOCTYPE>
<html>
   <head>
      <title>…</title>
      <!-- all the client libraries (css/js) -->
      …
   </head>
   <body>
        <!--/* Actual XF Offer content would appear here... */-->
   </body>
</html>
```

À un niveau élevé, lorsqu’AEM exporte un fragment d’expérience vers Adobe Target, il le fait à l’aide de plusieurs sélecteurs Sling supplémentaires. Par exemple, l’URL du fragment d’expérience exporté peut se présenter comme suit (remarque `nocloudconfigs.atoffer`) :

* http://www.your-aem-instance.com/content/experience-fragments/my-offers/my-xf-offer.nocloudconfigs.atoffer.html

La variable `nocloudconfigs` Le sélecteur est défini à l’aide de HTL et peut être superposé en le copiant à partir de :

* /libs/cq/experience-fragments/components/xfpage/nocloudconfigs.html

La variable `atoffer` Le sélecteur est appliqué après traitement à l’aide de [Sling Rewriter](/help/sites-developing/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html). Vous pouvez utiliser les deux pour supprimer les bibliothèques clientes.

### Exemple {#example}

À cet effet, illustrons comment le faire avec `nocloudconfigs`.

>[!NOTE]
>
>Voir [Modèles modifiables](/help/sites-developing/templates.md#editable-templates) pour plus de détails.

#### Recouvrements {#overlays}

Dans cet exemple particulier, les [recouvrements](/help/sites-developing/overlays.md) inclus suppriment les bibliothèques clientes *et* le code html superflu. Nous partons du principe que vous avez déjà créé le type de modèle de fragment d’expérience. Les fichiers nécessaires à la copie depuis `/libs/cq/experience-fragments/components/xfpage/` inclure :

* `nocloudconfigs.html`
* `head.nocloudconfigs.html`
* `body.nocloudconfigs.html`

#### Recouvrements de type modèle {#template-type-overlays}

Pour les besoins de cet exemple, nous vous proposons la structure suivante :

![Recouvrements de type modèle](assets/xf-target-integration-02.png "Recouvrement de type modèle")

Le contenu de ces fichiers est le suivant :

* `body.nocloudconfigs.html`

  ![body.nocloudconfigs.html](assets/xf-target-integration-03.png "body.nocloudconfigs.html")

* `head.nocloudconfigs.html`

  ![head.nocloudconfigs.html](assets/xf-target-integration-04.png "head.nocloudconfigs.html")

* `nocloudconfigs.html`

  ![nocloudconfigs.html](assets/xf-target-integration-05.png "nocloudconfigs.html")

>[!NOTE]
>
>Pour utiliser `data-sly-unwrap` pour supprimer la balise body, vous devez `nocloudconfigs.html`.

### Considérations {#considerations}

Si vous devez prendre en charge les sites AEM et les sites non AEM à l’aide d’offres de fragments d’expérience dans Adobe Target, vous devez créer deux fragments d’expérience (deux types de modèles différents) :

* Un avec le recouvrement pour supprimer les bibliothèques clientes ou le code html en trop

* Un qui ne dispose pas du recouvrement et qui inclut donc les bibliothèques clientes requises