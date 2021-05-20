---
title: Affichage de l’avatar de l’utilisateur
seo-title: Affichage de l’avatar de l’utilisateur
description: Comment personnaliser l’espace de travail AEM Forms pour afficher l’image d’un utilisateur connecté.
seo-description: Comment personnaliser l’espace de travail AEM Forms pour afficher l’image d’un utilisateur connecté.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 80%

---

# Affichage de l’avatar de l’utilisateur {#displaying-the-user-avatar}

L’avatar de l’utilisateur connecté s’affiche dans le coin supérieur droit de l’espace de travail AEM Forms. Les avatars de rapports directs dans la hiérarchie de l’entreprise sont affichés également dans la vue du gestionnaire. Vous pouvez configurer l’espace de travail AEM Forms pour sélectionner les images de l’utilisateur dans votre base de données, par exemple le serveur LDAP.

>[!NOTE]
>
>le rapport d’aspect des images de l’utilisateur est de 1:1.

1. Créez un DSC, à l’aide des détails mentionnés dans l’étape suivante. Pour plus d’informations, voir la rubrique &quot;Développement de composants pour AEM Forms&quot; dans le guide [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) .
1. Dans le DSC, définissez une nouvelle SPI qui expose les méthodes getCurrentUserImageUrl et getUserImageUrl afin d’obtenir l’URL d’image d’un utilisateur d’AEM Forms. Voici un exemple de fragment de code Java™ :

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. Créez un fichier component.xml. Assurez-vous que spec-id est comme dans le fragment de code ci-dessous.

   Le fragment de code suivant est un exemple. Personnalisez-le pour l’adapter à vos besoins spécifiques.

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. Déployez DSC via Workbench. Redémarrez le service `ProcessManagementClientSessionService`.
1. Il se peut que vous ayez à actualiser votre navigateur ou à vous déconnecter/connecter de nouveau avec l’utilisateur.
