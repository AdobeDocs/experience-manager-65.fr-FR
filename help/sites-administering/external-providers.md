---
title: Analytics avec des fournisseurs externes
description: Découvrez Analytics avec des fournisseurs externes.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: 1ef5593495b4bf22d2635492a360168bccc1725d
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 41%

---


# Analytics avec des fournisseurs externes {#analytics-with-external-providers}

Analytics peut vous apporter des informations importantes et intéressantes sur l’utilisation de votre site web.

Différentes configurations sont disponibles par défaut pour l’intégration au service approprié, par exemple :

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Vous pouvez également configurer votre propre instance de la variable **Fragments de code Analytics générique** pour définir une nouvelle configuration de service.

Les informations sont ensuite collectées par de petits fragments de code ajoutés aux pages web. Par exemple :

>[!CAUTION]
>
>Ne pas placer de scripts dans `script` balises.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Ces fragments de code permettent de collecter des données et de générer des rapports. Les données réelles collectées dépendent du fournisseur et du fragment de code réel utilisé. Voici des exemples de statistiques :

* combien de visiteurs au fil du temps
* le nombre de pages visitées
* termes de recherche utilisés
* landing pages

>[!CAUTION]
>
>Le site de démonstration de Geometrixx-Outdoors est configuré de sorte que les attributs fournis dans les Propriétés de la page soient ajoutés au code source HTML (juste au-dessus de la balise `</html>` (balise de fin) dans la balise correspondante `js` script.
>
>Si votre propre dossier `/apps` n’hérite pas du composant Page par défaut (`/libs/foundation/components/page`), vous (ou les développeurs) devez vous assurer que les scripts `js` sont inclus, par exemple, en incluant `cq/cloudserviceconfigs/components/servicescomponents` ou en utilisant un mécanisme similaire.
>
>Sans cela, aucun des services (Générique, Analytics, Target, etc.) ne fonctionnera.

## Création d’un service avec un fragment de code générique {#creating-a-new-service-with-a-generic-snippet}

Pour la configuration de base, suivez les étapes suivantes :

1. Ouvrez la console **Outils**.
1. Dans le volet de gauche, développez **Configurations de Cloud Services**.
1. Double-cliquez **Fragment de code Analytics générique** pour ouvrir la page :

   ![Extrait de code Analytics générique](assets/analytics_genericoverview.png)

1. Cliquez sur + pour ajouter une nouvelle configuration à l’aide de la boîte de dialogue. Attribuez au minimum un nom, par exemple Google Analytics :

   ![Création d’une configuration](assets/analytics_addconfig.png)

1. Cliquez sur **Créer**, la boîte de dialogue Fragment de code s’ouvre immédiatement. Collez le fragment de code JavaScript approprié dans le champ :

   ![Modification du composant](assets/analytics_snippet.png)

1. Cliquez sur **OK** pour enregistrer.

## Utilisation de votre nouveau service dans des pages {#using-your-new-service-on-pages}

Après avoir créé la configuration du service, vous devez maintenant configurer les pages requises pour l’utiliser :

1. Accédez à la page.
1. Ouvrez les **Propriétés de page** dans le sidekick, puis l’onglet **Services cloud**.
1. Cliquez sur **Ajouter un service**, puis sélectionnez le service requis. Par exemple, la variable **Fragment de code Analytics générique**:

   ![Ajout d’un service cloud](assets/analytics_selectservice.png)

1. Cliquez sur **OK** pour enregistrer.
1. Vous revenez alors au **Cloud Services** . Le **fragment de code Analytics générique** figure maintenant dans la liste avec le message `Configuration reference missing`. Utilisez la liste déroulante pour sélectionner votre instance de service spécifique. Par exemple, google-analytics :

   ![Ajout de la configuration du service cloud](assets/analytics_selectspecificservice.png)

1. Cliquez sur **OK** pour enregistrer.

   Le fragment de code s’affiche désormais si vous affichez la source de la page.

   Une fois le temps écoulé, vous pouvez afficher les statistiques collectées.

   >[!NOTE]
   >
   >Si la configuration est associée à une page qui contient des pages enfants, ces pages héritent elles aussi du service.
