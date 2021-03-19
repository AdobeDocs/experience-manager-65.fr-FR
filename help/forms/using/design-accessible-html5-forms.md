---
title: Conception de formulaires HTML5 accessibles
seo-title: Conception de formulaires HTML5 accessibles
description: Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5. Ces formulaires prennent en charge la navigation par onglets et sont certifiés pour être compatibles avec les lecteurs d’écran courants.
seo-description: Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5. Ces formulaires prennent en charge la navigation par onglets et sont certifiés pour être compatibles avec les lecteurs d’écran courants.
uuid: 1ce5ba39-69ea-4d0e-96ea-e2a38b21d6b7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8711ad33-396b-4572-b2ee-71e9f45f4ebe
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 89%

---


# Conception de formulaires HTML5 accessibles {#designing-accessible-html-forms}

Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5 pour générer des formulaires HTML accessibles. Ces formulaires prennent en charge la navigation par onglets (sauf Mozilla Firefox) et sont certifiés compatibles avec les lecteurs d’écran les plus courants. Pour générer un formulaire HTML5 avec de bonnes fonctions d’accessibilité, concevez le modèle de formulaire XFA en fonction de quelques directives de conception de base. Les directives de conception comprennent la configuration des onglets dans l’ordre approprié et fournissent le contenu du texte vocal pour chaque commande du formulaire. AEM Forms Designer prend en charge la définition de ces attributs de contrôle de formulaire pour générer un formulaire PDF et HTML5 accessible.

*Remarque : la navigation par onglets ne couvre pas les champs protégés tels que les champs de calcul affichant la somme des valeurs. Pour que le logiciel d’écran lise la valeur d’un champ protégé, placez un champ vide en lecture seule au-dessus ou à côté du champ protégé. Attribuez la valeur du champ protégé au nouveau champ en lecture seule. Le lecteur d’écran ou la navigation par onglets peut sélectionner ce champ en lecture seule et traduire ainsi la valeur du champ protégé à l’oral.*

AEM Forms Designer comprend plusieurs options de texte vocal qui peuvent être transmises aux lecteurs d’écran. Pour chaque objet d’un formulaire, l’utilisateur peut spécifier un ou plusieurs paramètres pour le texte du lecteur d’écran :

* Texte du lecteur d’écran personnalisé, qui peut être défini à l’aide de la palette Accessibilité. Les auteurs peuvent annoter les noms des boutons et des champs, ainsi que leur rôle.
* Infobulles, qui peuvent être définies dans la palette Accessibilité.
* Légendes des champs sur le formulaire.
* Noms des objets, tels qu’indiqués dans l’option Nom de l’onglet Liaison.

![accessibilité](assets/accessibility.png)

Lorsque plusieurs options (infobulles, texte de lecteur d’écran et légende, par exemple) sont disponibles sur une commande de formulaire, le lecteur d’écran n’utilise qu’une seule de ces propriétés. L’ordre par défaut est le suivant : texte de lecteur d’écran personnalisé, infobulles, légende et nom. Vous pouvez remplacer cet ordre par défaut à l’aide de l’option **Précédence** du lecteur d’écran dans la palette Accessibilité.
