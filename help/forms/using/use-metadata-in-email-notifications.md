---
title: Utilisation de métadonnées dans une notification électronique
description: Utiliser des métadonnées pour renseigner des informations dans une notification par e-mail Forms Workflow
topic-tags: publish
docset: aem65
exl-id: 18cfc4be-676d-4f08-afc1-4f11bb48dab6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: ht
source-wordcount: '871'
ht-degree: 100%

---

# Utilisation de métadonnées dans une notification électronique {#use-metadata-in-an-email-notification}

Vous pouvez utiliser l’étape Affecter une tâche pour créer et affecter des tâches à un utilisateur ou une utilisatrice ou à un groupe. Lorsqu’une tâche est affectée à un utilisateur, une utilisatrice ou un groupe, une notification est envoyée par e-mail à la personne définie ou à chaque membre du groupe défini. Une [notification par e-mail](../../forms/using/use-custom-email-template-assign-task-step.md) classique contient le lien de la tâche affectée et des informations relatives à la tâche.

Vous pouvez utiliser des métadonnées dans un modèle d’e-mail pour remplir de manière dynamique les informations d’une notification par e-mail. Par exemple, la valeur du titre, de la description, de l’échéance, de la priorité, du workflow et de la dernière date dans la notification par e-mail suivante est sélectionnée dynamiquement au moment de l’exécution (lorsqu’une notification par e-mail est générée).

![Modèle d’e-mail par défaut](assets/default_email_template_metadata_new.png)

Les métadonnées sont stockées dans des paires clé-valeur. Vous pouvez spécifier la clé dans le modèle d’e-mail et la clé est remplacée par une valeur au moment de l’exécution (lorsqu’une notification par e-mail est générée). Par exemple, dans l’exemple de code ci-dessous, la clé est « $ {workitem_title} ». Elle est remplacée par la valeur « Demande-Prêt » à l’exécution.

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## Utiliser des métadonnées générées par le système dans une notification par e-mail {#using-system-generated-metadata-in-an-email-notification}

Une application AEM Forms fournit plusieurs variables de métadonnées (paires clé-valeur) prêtes à l’emploi. Vous pouvez utiliser ces variables dans un modèle d’e-mail. La valeur de la variable est basée sur l’application de formulaires associée. Le tableau suivant répertorie toutes les variables de métadonnées prêtes à l’emploi :

<table>
 <tbody> 
  <tr> 
   <td>Clé</td> 
   <td>Description</td> 
  </tr> 
  <tr> 
   <td>workitem_title</td> 
   <td>Titre de l’application de formulaires associée.</td> 
  </tr> 
  <tr> 
   <td>workitem_url</td> 
   <td>URL d’accès à l’application de formulaires associée.</td> 
  </tr> 
  <tr> 
   <td>workitem_description</td> 
   <td>Description de l’application de formulaires associée.</td> 
  </tr> 
  <tr> 
   <td>workitem_priority</td> 
   <td>Priorité spécifiée pour l’application de formulaires associée.</td> 
  </tr> 
  <tr> 
   <td>workitem_due_date</td> 
   <td>Date de dernière action sur l’application de formulaires associée.</td> 
  </tr> 
  <tr> 
   <td>workitem_workflow</td> 
   <td>Nom du workflow associé à l’application de formulaires.</td> 
  </tr> 
  <tr> 
   <td>workitem_assign_timestamp</td> 
   <td>Date et heure auxquelles l’élément de workflow a été affecté à la personne désignée actuelle.</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>Nom de la personne désignée actuelle.</td> 
  </tr> 
  <tr> 
   <td>host_prefix</td> 
   <td>URL du serveur de création. Par exemple, https://10.41.42.66:4502<br />. </td> 
  </tr> 
  <tr> 
   <td>publish_prefix</td> 
   <td>URL du serveur de publication. Par exemple, https://10.41.42.66:4503.</td> 
  </tr> 
 </tbody> 
</table>

## Utiliser des métadonnées personnalisées dans une notification par e-mail {#using-custom-metadata-in-an-email-notification}

Vous pouvez également utiliser des métadonnées personnalisées dans une notification par e-mail. Les métadonnées personnalisées contiennent des informations en plus des métadonnées générées par le système. Par exemple, les détails de la politique récupérés à partir d’une base de données. Vous pouvez utiliser une offre groupée ECMAScript ou OSGi pour ajouter des métadonnées personnalisées dans le référentiel crx :

### Utilisation de ECMAScript pour ajouter des métadonnées personnalisées  {#use-ecmascript-to-add-custom-metadata}

[ECMAScript](https://fr.wikipedia.org/wiki/ECMAScript) est un langage de script. Il est utilisé pour les applications de script et de serveur côté client. Pour utiliser ECMAScript afin d’ajouter des métadonnées personnalisées pour un modèle d’e-mail, procédez comme suit :

1. Connectez-vous à CRX DE avec un compte d’administration. L’URL est https://&#39;[server]:[port]&#39;/crx/de/index.jsp

1. Accédez à /apps/fd/dashboard/scripts/metadataScripts. Créez un fichier avec l’extension .ecma. Par exemple, usermetadata.ecma.

   Si le chemin ci-dessus n’existe pas, créez-le.

1. Ajoutez du code au fichier .ecma qui possède la logique pour générer des métadonnées personnalisées dans des paires clé-valeur. Par exemple, le code ECMAScript suivant génère des métadonnées personnalisées pour une police d’assurance :

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. Cliquez sur Enregistrer tout. Désormais, le script peut être sélectionné dans le modèle de workflow AEM.

   ![assigntask-metadata](assets/assigntask-metadata.png)

1. (Facultatif) Spécifiez le titre du script :

   Si vous ne spécifiez pas le titre, le champ Métadonnées personnalisées affiche le chemin d’accès complet au fichier ECMAScript. Pour définir un titre significatif pour le script, procédez comme suit :

   1. Développez le nœud du script, cliquez avec le bouton droit de la souris sur **[!UICONTROL jcr:content]**, puis cliquez sur **[!UICONTROL Mixins]**.
   1. Saisissez mix:title dans la boîte de dialogue Modifier les mixins, puis cliquez sur **+**.
   1. Ajoutez une propriété avec les valeurs suivantes.

      | Nom | jcr:title |
      |---|---|
      | Type | Chaîne |
      | Valeur | Indiquez le titre du script. Par exemple, des métadonnées personnalisées pour la personne titulaire de la police. La valeur spécifiée s’affiche à l’étape Affecter une tâche. |

### Utiliser un bundle OSGi et une interface Java pour ajouter des métadonnées personnalisées {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

Vous pouvez utiliser l’interface Java WorkitemUserMetadataService pour ajouter des métadonnées personnalisées pour les modèles d’e-mail. Vous pouvez créer un bundle OSGi qui utilise l’interface Java WorkitemUserMetadataService et la déploie sur le serveur AEM Forms. Les métadonnées peuvent être sélectionnées à l’étape Affecter une tâche.

Pour créer un bundle OSGi avec une interface Java, ajoutez les fichiers jar [SDK client AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr) et [jar granite](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) en tant que dépendances externes au projet de bundle OSGi. Vous pouvez utiliser n’importe quel IDE Java pour créer un bundle OSGi. La procédure suivante décrit l’utilisation d’Eclipse pour créer un bundle OSGi :

1. Ouvrez Eclipse IDE. Accédez à Fichier > Nouveau projet.

1. Sur l’écran de sélection de l’assistant, sélectionnez Projet Maven puis cliquez sur Suivant.

1. Sur le nouveau projet Maven, conservez les valeurs par défaut, puis cliquez sur Suivant. Sélectionnez un archétype, puis cliquez sur Suivant. Par exemple, maven-archetype-quickstart. Indiquez l’ID de groupe, l’ID d’artefact, la version et le package du projet, puis cliquez sur Terminer. Le projet est créé.

1. Ouvrez le fichier pom.xml pour modifier et remplacer tout le contenu du fichier par ce qui suit :

1. Ajoutez le code source qui utilise l’interface Java WorkitemUserMetadataService pour ajouter des métadonnées personnalisées aux modèles d’e-mail. Un exemple de code est répertorié ci-dessous :

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. Ouvrez une invite de commande et accédez au répertoire contenant le projet de bundle OSGi. Utilisez la commande suivante pour créer le bundle OSGi :

   `mvn clean install`

1. Chargez le bundle sur un serveur AEM Forms. Vous pouvez utiliser le gestionnaire de modules AEM pour importer le bundle dans le serveur AEM Forms.

Une fois le bundle importé, vous pouvez sélectionner les métadonnées dans l’étape Affecter une tâche et les utiliser dans un modèle de courrier électronique.
