---
title: Création de formulaires avec des sections répétables
seo-title: Création de formulaires avec des sections répétables
description: Les sections répétables sont des panneaux qui peuvent être dynamiquement ajoutés ou supprimés dans un formulaire.
seo-description: Les sections répétables sont des panneaux qui peuvent être dynamiquement ajoutés ou supprimés dans un formulaire.
uuid: c3fa2aa4-a6b4-458e-8534-138e075290b1
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 01724ca0-6901-45e7-b045-f44814ed574e
feature: Formulaires adaptatifs
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 78%

---


# Création de formulaires avec des sections répétables {#creating-forms-with-repeatable-sections}

Les sections répétables sont des panneaux qui peuvent être ajoutés ou supprimés dynamiquement dans un formulaire.

Par exemple, lorsqu’elle dépose sa candidature pour un poste, la personne à la recherche d’un emploi fournit des informations sur son précédent poste telles que le nom de l’entreprise, le poste, le projet, etc. Les informations demandées par tous les employeurs nécessitent des sections différentes mais dont l’aspect est similaire. Dans ce scénario, le formulaire d’embauche fournit une section employeur et contient une option pour ajouter dynamiquement davantage de sections de ce type. Ces sections dynamiquement ajoutées sont appelées sections répétables.

Pour créer des panneaux répétables, vous pouvez utiliser l’une des méthodes suivantes :

## Utilisation du gestionnaire d’instances via des scripts  {#using-instance-manager-via-scripts-nbsp}

1. En mode d’édition, sélectionnez un panneau, puis appuyez sur ![cmppr](assets/cmppr.png). Dans la barre latérale, sous Propriétés, activez **Activer la répétition du panneau**. Spécifiez des valeurs pour les champs **[!UICONTROL Maximum]** et **[!UICONTROL Minimum.]**

   Le champ Maximum spécifie le nombre maximal de fois qu’un panneau peut s’afficher sur la page. Vous pouvez spécifier la valeur -1 dans le champ Nombre maximum pour que le panneau s’affiche un nombre illimité de fois.

   Le champ Minimum spécifie le nombre minimum de fois qu’un panneau peut s’afficher sur la page. Si vous spécifiez la valeur zéro dans le champ Nombre minimum, vous pouvez ultérieurement supprimer toutes les instances via des scripts une fois le rendu terminé.

   >[!NOTE]
   >
   >Pour créer un panneau non répétable, spécifiez une valeur dans les champs Maximum et Minimum. La mise en page en accordéon ne prend pas en charge la valeur -1 dans le champ Nombre maximum. Vous pouvez spécifier un nombre élevé pour exprimer une valeur infinie.

1. Le parent du panneau à répéter doit contenir des boutons d’ajout et de suppression pour gérer les instances des panneaux répétables. Pour insérer des boutons dans le parent et activer des scripts sur les boutons, procédez comme suit :

   1. A partir de la barre latérale, faites glisser un composant Bouton jusqu’au parent du panneau. Sélectionnez le composant et appuyez sur ![edit-rules](assets/edit-rules.png). Les règles du bouton s’ouvrent dans l’éditeur de règles.
   1. Dans la fenêtre Éditeur de règles Les règles, cliquez sur **créer**.

      Sélectionnez **Éditeur visuel** dans la ligne Objets et fonctions de formulaire.

      1. Dans la zone de la règle, sous QUAND, sélectionnez l’état **est cliqué**.
      1. Sous PUIS :

         * Pour créer un bouton d’ajout de panneau, sélectionnez **Ajouter l’instance**, puis faites glisser et déposez le panneau à l’aide de ![toggle-side-panel](assets/toggle-side-panel.png) ou sélectionnez-le à l’aide de **Déposez l’objet ou sélectionnez ici.**
         * Pour créer un bouton de suppression de panneau, sélectionnez **Supprimer l&#39;instance**, puis faites glisser et déposez le panneau à l&#39;aide de ![toggle-side-panel](assets/toggle-side-panel.png) ou sélectionnez-le à l&#39;aide de **Déposez l&#39;objet ou sélectionnez ici.**

      Sélectionnez **Éditeur de code** dans la ligne Objets et fonctions de formulaire. Cliquez sur **Modifier les règles** et dans la zone de code :

      * Pour créer un bouton d’ajout de panneau, spécifiez `this.panel.instanceManager.addInstance()`.
      * Pour créer un bouton de suppression de panneau, spécifiez `this.panel.instanceManager.removeInstance(this.panel.instanceIndex)`

      Cliquez sur **Terminé**.

      >[!NOTE]
      >
      >Si un champ appartient à un panneau répétable, vous ne pouvez pas y accéder directement via son nom dans vos scripts. Pour accéder au champ, spécifiez l&#39;instance répétable à laquelle le champ appartient à l&#39;aide de l&#39;API `instances` dans `InstanceManager`. La syntaxe à utiliser pour l&#39;API `instances` dans `InstanceManager` est la suivante :
      >
      >
      >`<panelName>.instanceManager.instances[<instanceNumber>].<fieldname>`
      >
      >
      >Par exemple, vous créez un formulaire adaptatif avec un panneau répétable contenant une zone de texte. Lorsque vous pré-remplissez le formulaire avec trois zones de texte répétables, le code xml ci-dessous est requis :
      >
      >
      >`<panel1><textbox1>AA1</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA2</panel1></textbox1>`
      >
      >
      >`<panel1><textbox1>AA3</panel1></textbox1>`
      >
      >
      >Pour lire les données AA1, spécifiez les paramètres suivants :
      >
      >
      >`Panel1.instanceManager.instances[0].textbox.value`
      >
      >
      >Pour lire les données AA2, spécifiez les paramètres suivants :
      >
      >
      >`Panel1.instanceManager.instances[1].textbox.value`
      >
      >
      >Pour plus d’informations, voir : Class: InstanceManager#instances dans [Référence API Java pour AEM Forms](https://adobe.com/go/learn_aemforms_documentation_63).

      >[!NOTE]
      >
      >Lorsque toutes les instances d’un panneau sont supprimées d’un formulaire adaptatif, pour ajouter une instance du panneau supprimé, utilisez la syntaxe _panelName pour capturer le gestionnaire d’instances du panneau et utilisez l’API addInstance du gestionnaire d’instances pour ajouter l’instance supprimée. Par exemple, _panelName.addInstance(). Elle ajoute une instance du panneau supprimé.















## Utilisation de la mise en page en accordéon pour le panneau parent{#using-the-accordion-layout-for-the-parent-panel-nbsp}

Un panneau possède différentes options de mise en forme. La mise en page de l’option de conception en accordéon prend en charge les panneaux répétables. Pour créer un panneau répétable avec la mise en page de l’option de conception en accordéon, procédez comme suit : 

1. Sur le parent du panneau à répéter, appuyez sur ![cmppr](assets/cmppr.png). Vous pouvez afficher les propriétés dans la barre latérale. Dans le menu déroulant **Disposition**, sélectionnez **Accordéon**.
1. Dans un panneau à répéter, appuyez sur ![cmppr](assets/cmppr.png). Vous pouvez afficher les propriétés dans la barre latérale. Activez l’onglet **Activer la répétition du panneau** et spécifiez des valeurs pour les champs **Maximum** et **Minimum**.

   Vous pouvez désormais utiliser les boutons plus (+) et supprimer ( ![delete-panel](assets/delete-panel.png)) pour ajouter et supprimer les panneaux.

## Utilisation des sous-formulaires qui se répètent du modèle de formulaire (XDP/XSD) {#using-repeating-subforms-from-form-template-xdp-xsd}

Un sous-formulaire répétable est similaire aux panneaux répétables dans les formulaires adaptatifs. Dans AEM Forms Designer, procédez comme suit pour créer un sous-formulaire qui se répète :

1. Dans la palette Hiérarchie, sélectionnez le sous-formulaire parent du sous-formulaire à répéter.
1. Dans la palette Objet, cliquez sur l’onglet Sous-formulaire et sélectionnez Distribué dans la liste Contenu.
1. Sélectionnez le sous-formulaire à répéter.
1. Dans la palette Objet, cliquez sur l’onglet Sous-formulaire et sélectionnez Positionné ou Distribué dans la liste Contenu.
1. Cliquez sur l’onglet Liaison et sélectionnez Sous-formulaire pour chaque élément.
1. Pour spécifier le nombre minimum de répétitions, sélectionnez Min. de répétitions et saisissez un nombre dans la zone associée. Si cette option est réglée sur 0 et qu’aucune donnée n’est fournie pour les objets du sous-formulaire au moment de la fusion, le sous-formulaire n’est pas placé au cours du processus de génération du formulaire.
1. Pour spécifier le nombre maximum de répétitions, sélectionnez Max. de répétitions et saisissez un nombre dans la zone associée. Si vous n’indiquez rien dans la zone Max, le nombre de répétitions du sous-formulaire est illimité.
1. Pour spécifier un nombre précis de répétitions du sous-formulaire, quelle que soit la quantité de données, sélectionnez l’option Quantité initiale et tapez un nombre dans la zone associée. Si cette option est sélectionnée et s’il n’y a pas de données disponibles, ou si les données existantes sont inférieures à la valeur Quantité initiale, les occurrences vides du sous-formulaire apparaissent quand même sur le formulaire.
1. Ajoutez deux boutons dans le sous-formulaire parent : un pour ajouter une instance et un autre pour supprimer l’instance du sous-formulaire répétable. Pour les étapes détaillées, voir [Créer une action](https://help.adobe.com/en_US/AEMForms/6.1/DesignerHelp/WS107c29ade9134a2c74572b5612a87ca2b56-8000.2.html#WS107c29ade9134a2c-1f74d86012a87d4fe55-8000.2).
1. Liez maintenant le modèle de formulaire au formulaire adaptatif. Pour les étapes détaillées, voir [Création d’un formulaire adaptatif basé sur un modèle](/help/forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-a-template).
1. Utilisez les boutons créés à l’étape 9 pour ajouter et supprimer des sous-formulaires.

Le fichier .zip joint contient un exemple de sous-formulaire répétable.

[Obtenir le fichier](assets/samplerepeatablesubform.zip)

## Utilisation des paramètres de répétition d’un schéma XML (XSD) {#using-repeat-settings-of-an-xml-schema-xsd-br}

Vous pouvez créer des panneaux répétables à partir d’un schéma XML et de la propriété minOccurs et maxOccurs de n’importe quel élément de type complexe. Pour des informations détaillées sur le schéma XML, voir [Création de formulaires adaptatifs à l’aide du schéma XML en tant que modèle de formulaire](/help/forms/using/adaptive-form-xml-schema-form-model.md).

Dans le code suivant, le panneau `SampleType` utilise la propriété minOccurs et maxOccurs.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartDate" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Pour une mise en page autre qu’en accordéon, utilisez les composants Bouton des formulaires adaptatifs pour ajouter et supprimer des instances.
