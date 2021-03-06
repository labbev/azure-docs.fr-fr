---
title: 'Didacticiel : Intégration d’Azure Active Directory à Cisco Cloud | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Cisco Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: db1cea1d-ff0a-4f0d-b5fd-50ca32702d56
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2018
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: d2f4d379f01d072bbfdcd95cd5bb19ccc0f9546d
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56166366"
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-cloud"></a>Tutoriel : Intégration d’Azure Active Directory à Cisco Cloud

Ce tutoriel explique comment intégrer Cisco Cloud avec Azure Active Directory (Azure AD).

L’intégration de Cisco Cloud avec Azure AD offre les avantages suivants :

- Vous pouvez contrôler qui a accès à Cisco Cloud.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à Cisco Cloud (authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD avec Cisco Cloud, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Cisco Cloud pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de Cisco Cloud à partir de la galerie
1. Configuration et test de l’authentification unique Azure AD

## <a name="adding-cisco-cloud-from-the-gallery"></a>Ajout de Cisco Cloud à partir de la galerie
Pour configurer l’intégration de Cisco Cloud à Azure AD, vous devez ajouter Cisco Cloud, disponible dans la galerie, à votre liste d’applications SaaS managées.

**Pour ajouter Cisco Cloud à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Bouton Azure Active Directory][1]

1. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Panneau Applications d’entreprise][2]
    
1. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Bouton Nouvelle application][3]

1. Dans la zone de recherche, entrez **Cisco Cloud**, sélectionnez **Cisco Cloud** dans le panneau des résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Cisco Cloud dans la liste des résultats](./media/ciscocloud-tutorial/tutorial_ciscocloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Cisco Cloud sur un utilisateur de test nommé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir quel utilisateur dans Cisco Cloud équivaut à quel utilisateur dans Azure AD. En d’autres termes, vous devez établir une relation de lien entre un utilisateur Azure AD et l’utilisateur associé dans Cisco Cloud.

Pour configurer et tester l’authentification unique Azure AD avec Cisco Cloud, vous devez suivre les indications des sections suivantes :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
1. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
1. **[Créer un utilisateur de test Cisco Cloud](#create-a-cisco-cloud-test-user)** pour avoir un équivalent de Britta Simon dans Cisco Cloud, lié à la représentation Azure AD associée.
1. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
1. **[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Cisco Cloud.

**Pour configurer l’authentification unique Azure AD avec Cisco Cloud, procédez comme suit :**

1. Dans le portail Azure, sur la page d’intégration de l’application **Cisco Cloud**, cliquez sur **Authentification unique**.

    ![Lien Configurer l’authentification unique][4]

1. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.

    ![Boîte de dialogue Authentification unique](./media/ciscocloud-tutorial/tutorial_ciscocloud_samlbase.png)

1. Dans la section **Domaine et URL Cisco Cloud**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en **Mode initié par IDP** :

    ![Informations d’authentification unique dans Domaine et URL Cisco Cloud](./media/ciscocloud-tutorial/tutorial_ciscocloud_url.png)

    a. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `<subdomain>.cisco.com`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<subdomain>.cisco.com/sp/ACS.saml2`

1. Si vous souhaitez configurer l’application en **mode démarré par le fournisseur de service**, cochez **Afficher les paramètres d’URL avancés**, puis effectuez les étapes suivantes :

    ![Informations d’authentification unique dans Domaine et URL Cisco Cloud](./media/ciscocloud-tutorial/tutorial_ciscocloud_url1.png)

    Dans la zone de texte **URL d’authentification**, tapez l’URL `https://<subdomain>.cloudapps.cisco.com`

    > [!NOTE]
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’identificateur, l’URL d’authentification et l’URL de réponse réels. Pour obtenir ces valeurs, contactez [l’équipe du support client Cisco Cloud](mailto:cpr-ops@cisco.com).

1. L’application Cisco Cloud attend les assertions SAML dans un format spécifique. Configurez les revendications suivantes pour cette application. Vous pouvez gérer les valeurs de ces attributs à partir de la section **Attributs utilisateur** sur la page d’intégration des applications.
 La capture d’écran suivante en présente un exemple.

    ![Configurer l'authentification unique](./media/ciscocloud-tutorial/attribute.png)

1. Dans la section **Attributs utilisateur**, cliquez sur **Afficher et modifier tous les autres attributs utilisateur** pour développer les attributs. Dans chacun des attributs affichés, procédez comme suit :

    | Nom de l'attribut | Valeur de l’attribut |
    | ---------------| ----------------|
    | country      |user.country |
    | société      |user.companyname |

    a. Cliquez sur **Ajouter un attribut** pour ouvrir la boîte de dialogue **Ajouter un attribut**.

    ![Configure Single Sign-On](./media/ciscocloud-tutorial/tutorial_attribute_04.png)

    ![Configure Single Sign-On](./media/ciscocloud-tutorial/tutorial_attribute_05.png)

    b. Dans la zone de texte **Attribut**, indiquez le nom d’attribut pour cette ligne.

    c. Dans la liste **Valeur** , saisissez la valeur d’attribut affichée pour cette ligne.

    d. Laissez le champ **Espace de noms** vide.

    e. Cliquez sur **OK**.

1. Dans la section  **Certificat de signature SAML** , cliquez sur le bouton Copier pour copier l’**URL des métadonnées de fédération de l’application**, puis collez-la dans le Bloc-notes.

    ![Lien Téléchargement de certificat](./media/ciscocloud-tutorial/tutorial_ciscocloud_certificate.png)

1. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/ciscocloud-tutorial/tutorial_general_400.png)

1. Pour configurer l’authentification unique côté **Cisco Cloud**, vous devez envoyer **l’URL des métadonnées de fédération de l’application** à [l’équipe du support technique Cisco Cloud](mailto:cpr-ops@cisco.com). Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

   ![Créer un utilisateur de test Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.

    ![Bouton Azure Active Directory](./media/ciscocloud-tutorial/create_aaduser_01.png)

1. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/ciscocloud-tutorial/create_aaduser_02.png)

1. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.

    ![Bouton Ajouter](./media/ciscocloud-tutorial/create_aaduser_03.png)

1. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :

    ![Boîte de dialogue Utilisateur](./media/ciscocloud-tutorial/create_aaduser_04.png)

    a. Dans la zone **Nom**, tapez **BrittaSimon**.

    b. Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.

    c. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="create-a-cisco-cloud-test-user"></a>Créer un utilisateur de test Cisco Cloud

Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Cisco Cloud. Collaborez avec l' [équipe de support technique de Cisco Cloud](mailto:cpr-ops@cisco.com) pour ajouter des utilisateurs dans la plateforme Cisco Cloud. Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Cisco Cloud.

![Attribuer le rôle utilisateur][200] 

**Pour affecter Britta Simon à Cisco Cloud, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

1. Dans la liste des applications, sélectionnez **Cisco Cloud**.

    ![Lien Cisco Cloud dans la liste des applications](./media/ciscocloud-tutorial/tutorial_ciscocloud_app.png)  

1. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Lien « Utilisateurs et groupes »][202]

1. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Volet Ajouter une attribution][203]

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

1. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

1. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Cisco Cloud dans le panneau d’accès, vous devriez être authentifié automatiquement auprès de votre application Cisco Cloud.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ciscocloud-tutorial/tutorial_general_01.png
[2]: ./media/ciscocloud-tutorial/tutorial_general_02.png
[3]: ./media/ciscocloud-tutorial/tutorial_general_03.png
[4]: ./media/ciscocloud-tutorial/tutorial_general_04.png

[100]: ./media/ciscocloud-tutorial/tutorial_general_100.png

[200]: ./media/ciscocloud-tutorial/tutorial_general_200.png
[201]: ./media/ciscocloud-tutorial/tutorial_general_201.png
[202]: ./media/ciscocloud-tutorial/tutorial_general_202.png
[203]: ./media/ciscocloud-tutorial/tutorial_general_203.png

