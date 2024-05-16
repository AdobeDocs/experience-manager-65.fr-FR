---
title: Affichage de l’avatar de l’utilisateur
description: Comment personnaliser l’espace de travail AEM Forms pour afficher l’image d’une personne connectée.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '189'
ht-degree: 100%

---

# Affichage de l’avatar de l’utilisateur {#displaying-the-user-avatar}

L’avatar de l’utilisateur connecté s’affiche dans le coin supérieur droit de l’espace de travail AEM Forms. Les avatars de rapports directs dans la hiérarchie de l’entreprise sont affichés également dans la vue du gestionnaire. Vous pouvez configurer l’espace de travail AEM Forms pour choisir les images de l’utilisateur dans la base de données, par exemple le serveur LDAP.

>[!NOTE]
>
>le rapport d’aspect des images de l’utilisateur est de 1:1.

1. Créez un DSC, à l’aide des détails mentionnés dans l’étape suivante. Pour plus d’informations, voir la section « Développement des composants d’AEM Forms » dans le guide [Programmer avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).
1. Dans le DSC, définissez une nouvelle SPI qui expose les méthodes getCurrentUserImageUrl et getUserImageUrl afin d’obtenir l’URL d’image d’un utilisateur d’AEM Forms. Voici un exemple d’extrait de code Java™ :

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

1. Créez un fichier component.xml. Assurez-vous que spec-id apparaît comme illustré dans l’extrait de code ci-dessous.

   Le fragment de code suivant est un exemple. Personnalisez-le selon vos besoins.

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
