---
title: Concevoir des formulaires HTML5 accessibles
description: Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5. Ces formulaires prennent en charge la navigation par onglets et sont certifiés compatibles avec les lecteurs d’écran les plus courants.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: fca2f9b2-11a2-4db0-a370-c4046f32be63
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 95%
---
# Concevoir des formulaires HTML5 accessibles {#designing-accessible-html-forms}

Les formulaires HTML5 utilisent la norme d’accessibilité ARIA HTML5 pour générer des formulaires HTML accessibles. Ces formulaires prennent en charge la navigation par onglets (sauf Mozilla Firefox) et sont certifiés compatibles avec les lecteurs d’écran les plus courants. Pour générer un formulaire HTML5 avec les fonctions d’accessibilité appropriées, concevez le modèle de formulaire XFA à partir de quelques directives de conception de base. Les directives de conception comprennent la configuration des onglets dans l’ordre approprié et fournissent le contenu du texte vocal pour chaque commande du formulaire. AEM Forms Designer prend en charge le paramètre de ces attributs de commande du formulaire pour générer un formulaire en version PDF et HTML5 accessible.

*Remarque :Tabbed la navigation ne couvre pas les champs protégés tels que les champs de calcul affichant la somme des valeurs. Pour que le lecteur d’écran lise la valeur d’un champ protégé, placez un champ Lecture seule vide au-dessus ou en regard du champ protégé. Attribuez la valeur du champ protégé au nouveau champ en lecture seule. Le lecteur d’écran ou la navigation par onglets peut sélectionner ce champ en lecture seule et le définir comme la valeur du champ protégé.*

AEM Forms Designer comprend plusieurs options de texte vocal qui peuvent être transmises aux lecteurs d’écran. Pour chaque objet d’un formulaire, l’utilisateur ou l’utilisatrice peut spécifier l’un des paramètres suivants pour le texte du lecteur d’écran :

* Texte du lecteur d’écran personnalisé qui peut être défini à l’aide de la palette Accessibilité. Les auteurs et autrices peuvent annoter les noms des boutons et des champs, ainsi que leur rôle.
* Info-bulles, qui peuvent être définies dans la palette Accessibilité.
* Légendes des champs du formulaire.
* Noms des objets, tels que spécifiés dans l’option Nom de l’onglet Liaison.

![Accessibilité](assets/accessibility.png)

Lorsque plusieurs options telles que l’info-bulle, le texte du lecteur d’écran et la légende sont disponibles sur un contrôle de formulaire, le lecteur d’écran n’utilise qu’une seule de ces propriétés. L’ordre par défaut est Texte de lecteur d’écran personnalisé, info-bulle, Légende et Nom. Vous pouvez remplacer cet ordre par défaut à l’aide de l’option **Précédence** du lecteur d’écran dans la palette Accessibilité.
