---
title: 'Didacticiel : Intégration d’Azure Active Directory à Sciforma | Microsoft Docs'
description: Découvrez comment configurer l’authentification unique entre Azure Active Directory et Sciforma.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: abbfb5ac-7687-4153-b263-8090102dae37
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1572a6af5523f6b8ea18c0e7f4365cd6ed20dea9
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56180043"
---
# <a name="tutorial-azure-active-directory-integration-with-sciforma"></a>Tutoriel : Intégration d’Azure Active Directory à Sciforma

L’objectif de ce didacticiel est de vous apprendre à intégrer Sciforma à Azure Active Directory (Azure AD).

Intégrer Sciforma à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler l’accès à Sciforma
- Vous pouvez autoriser les utilisateurs à être automatiquement connectés à Sciforma (via l’authentification unique) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l'intégration d'Azure AD avec Sciforma, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Sciforma pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajouter Sciforma à partir de la galerie
1. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sciforma-from-the-gallery"></a>Ajouter Sciforma à partir de la galerie
Pour configurer l'intégration de Sciforma à Azure AD, vous devez ajouter Sciforma, disponible dans la galerie, à votre liste d'applications SaaS gérées.

**Pour ajouter Sciforma à partir de la galerie, réalisez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

1. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![APPLICATIONS][2]
    
1. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![APPLICATIONS][3]

1. Dans la zone de recherche, entrez **Sciforma**.

    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/tutorial_sciforma_search.png)

1. Dans le panneau de résultats, sélectionnez **Sciforma**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/tutorial_sciforma_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Sciforma, grâce à un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Sciforma correspondant dans Azure AD. En d’autres termes, il faut établir une relation entre l’utilisateur Azure AD et l’utilisateur Sciforma associé.

Dans Sciforma, assignez la valeur du **nom de l’utilisateur** dans Azure AD comme valeur du **Nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec Sciforma, vous devez compléter les blocs de construction suivants :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
1. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
1. **[Création d’un utilisateur de test Sciforma](#creating-a-sciforma-test-user)** pour avoir un équivalent de Britta Simon dans Sciforma qui est lié à la représentation d’un utilisateur Azure AD.
1. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** : permet à Britta Simon d’utiliser l’authentification unique Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Sciforma.

**Pour configurer l’authentification unique Azure AD avec Sciforma, réalisez les étapes suivantes :**

1. Dans le portail Azure, sur la page d’intégration de l’application **Sciforma**, cliquez sur **Authentification unique**.

    ![Configurer l'authentification unique][4]

1. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l'authentification unique](./media/sciforma-tutorial/tutorial_sciforma_samlbase.png)

1. Sur la section **Domaine et URL Sciforma**, réalisez les étapes suivantes :

    ![Configurer l'authentification unique](./media/sciforma-tutorial/tutorial_sciforma_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<subdomain>.sciforma.net/sciforma/main.html`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<subdomain>.sciforma.net/sciforma/saml`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez l’[équipe de support technique Sciforma](https://www.sciforma.com/about/contact). 
 


1. Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Configure Single Sign-On](./media/sciforma-tutorial/tutorial_sciforma_certificate.png) 

1. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l'authentification unique](./media/sciforma-tutorial/tutorial_general_400.png)

1. Pour configurer l’authentification unique côté **Sciforma**, vous devez envoyer le fichier **XML des métadonnées** téléchargé à [l’équipe de support Sciforma](https://www.sciforma.com/about/contact).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Pour en savoir plus sur la fonctionnalité de documentation incorporée, accédez à : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/create_aaduser_01.png) 

1. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/create_aaduser_02.png) 

1. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/create_aaduser_03.png) 

1. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/sciforma-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-a-sciforma-test-user"></a>Créer un utilisateur de test de Sciforma

Vous n’avez rien à faire pour configurer l’approvisionnement des utilisateurs dans Sciforma. Lorsqu’un utilisateur tente de se connecter à Sciforma à l’aide du panneau d’accès, Sciforma vérifie si cet utilisateur existe.  

* Si aucun compte d’utilisateur n’est disponible, Sciforma le crée automatiquement.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à Sciforma.

![Affecter des utilisateurs][200] 

**Pour assigner Britta Simon à Sciforma, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

1. Dans la liste des applications, sélectionnez **Sciforma**.

    ![Configurer l'authentification unique](./media/sciforma-tutorial/tutorial_sciforma_app.png) 

1. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

1. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

1. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

1. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

1. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/sciforma-tutorial/tutorial_general_01.png
[2]: ./media/sciforma-tutorial/tutorial_general_02.png
[3]: ./media/sciforma-tutorial/tutorial_general_03.png
[4]: ./media/sciforma-tutorial/tutorial_general_04.png

[100]: ./media/sciforma-tutorial/tutorial_general_100.png

[200]: ./media/sciforma-tutorial/tutorial_general_200.png
[201]: ./media/sciforma-tutorial/tutorial_general_201.png
[202]: ./media/sciforma-tutorial/tutorial_general_202.png
[203]: ./media/sciforma-tutorial/tutorial_general_203.png

