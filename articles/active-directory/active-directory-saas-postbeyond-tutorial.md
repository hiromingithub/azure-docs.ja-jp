---
title: 'チュートリアル: Azure Active Directory と PostBeyond の統合 | Microsoft Docs'
description: Azure Active Directory と PostBeyond の間でシングル サインオンを構成する方法について確認します。
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''

ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2016
ms.author: jeedes

---
# チュートリアル: Azure Active Directory と PostBeyond の統合
このチュートリアルでは、PostBeyond と Azure Active Directory (Azure AD) を統合する方法について説明します。

PostBeyond と Azure AD の統合には、次の利点があります。

* PostBeyond にアクセスする Azure AD ユーザーを制御できます。
* ユーザーが自分の Azure AD アカウントで PostBeyond に自動的にサインオン (シングル サインオン) できるように、設定が可能です。
* 1 つの中央サイト (Azure クラシック ポータル) でアカウントを管理できます。

SaaS アプリと Azure AD の統合の詳細については、「[Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](active-directory-appssoaccess-whatis.md)」を参照してください。

## 前提条件
PostBeyond と Azure AD の統合を構成するには、次のものが必要です。

* Azure AD サブスクリプション
* **PostBeyond** でのシングル サインオンが有効なサブスクリプション

> [!NOTE]
> このチュートリアルの手順をテストする場合、運用環境を使用しないことをお勧めします。
> 
> 

このチュートリアルの手順をテストするには、次の推奨事項に従ってください。

* 必要な場合を除き、運用環境は使用しないでください。
* Azure AD の評価環境がない場合は、[こちら](https://azure.microsoft.com/pricing/free-trial/)から 1 か月の評価版を入手できます。

## シナリオの説明
このチュートリアルでは、テスト環境で Azure AD のシングル サインオンをテストします。このチュートリアルで説明するシナリオは、主に次の 2 つの要素で構成されています。

1. ギャラリーからの PostBeyond の追加
2. Azure AD シングル サインオンの構成とテスト

## ギャラリーからの PostBeyond の追加
Azure AD への PostBeyond の統合を構成するには、ギャラリーから管理対象 SaaS アプリの一覧に PostBeyond を追加する必要があります。

**ギャラリーから PostBeyond を追加するには、次の手順に従います。**

1. **Azure クラシック ポータル**の左側のナビゲーション ウィンドウで、**[Active Directory]** をクリックします。
   
    ![Active Directory][1]
2. **[ディレクトリ]** の一覧から、ディレクトリ統合を有効にするディレクトリを選択します。
3. アプリケーション ビューを開くには、ディレクトリ ビューでトップ メニューの **[アプリケーション]** をクリックします。
   
    ![アプリケーション][2]
4. ページの下部にある **[追加]** をクリックします。
   
    ![アプリケーション][3]
5. **[実行する内容]** ダイアログで、**[ギャラリーからアプリケーションを追加します]** をクリックします。
   
    ![アプリケーション][4]
6. 検索ボックスに「**PostBeyond**」と入力します。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_01.png)
7. 結果ウィンドウで **[PostBeyond]** を選択し、**[完了]** をクリックしてアプリケーションを追加します。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_02.png)

## Azure AD シングル サインオンの構成とテスト
このセクションでは、"Britta Simon" というテスト ユーザーに基づいて、PostBeyond で Azure AD のシングル サインオンを構成し、テストします。

シングル サインオンを機能させるには、Azure AD ユーザーに対応する PostBeyond ユーザーが Azure AD で認識されている必要があります。言い換えると、Azure AD ユーザーと PostBeyond の関連ユーザーの間で、リンク関係が確立されている必要があります。このリンク関係を確立するには、Azure AD の **[ユーザー名]** の値を PostBeyond の **[Username (ユーザー名)]** の値として割り当てます。

PostBeyond で Azure AD のシングル サインオンを構成してテストするには、次の構成要素を完了する必要があります。

1. **[Azure AD シングル サインオンの構成](#configuring-azure-ad-single-single-sign-on)** - ユーザーがこの機能を使用できるようにします。
2. **[Azure AD のテスト ユーザーの作成](#creating-an-azure-ad-test-user)** - Britta Simon で Azure AD のシングル サインオンをテストします。
3. **[PostBeyond のテスト ユーザーの作成](#creating-a-PostBeyond-test-user)** - PostBeyond で Britta Simon に対応するユーザーを作成し、Azure AD の Britta Simon にリンクさせます。
4. **[Azure AD テスト ユーザーの割り当て](#assigning-the-azure-ad-test-user)** - Britta Simon が Azure AD のシングル サインオンを使用できるようにします。
5. **[シングル サインオンのテスト](#testing-single-sign-on)** - 構成が機能するかどうかを確認します。

### Azure AD シングル サインオンの構成
このセクションの目的は、Azure クラシック ポータルで Azure AD のシングル サインオンを有効にすることと、PostBeyond アプリケーションでシングル サインオンを構成することです。

**PostBeyond で Azure AD シングル サインオンを構成するには、次の手順に従います。**

1. 上部のメニューで **[クイック スタート]** をクリックします。
   
    ![Configure Single Sign-On][6]
2. クラシック ポータルの **PostBeyond** アプリケーション統合ページで **[シングル サインオンの構成]** をクリックし、**[シングル サインオンの構成]** ダイアログを開きます。
   
    ![Configure Single Sign-On][7]
3. **[ユーザーの PostBeyond へのアクセスを設定してください]** ページで、**[Azure AD のシングル サインオン]** を選択し、**[次へ]** をクリックします。
   
    ![Configure Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_06.png)
4. **[アプリケーション設定の構成]** ダイアログ ページで、次の手順に従います。
   
    ![Configure Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_07.png)

    a.[サインオン URL] ボックスに、`https://app.postbeyond.com` という形式で URL を入力します。

    b.**[次へ]** をクリックします。

1. **[PostBeyond でのシングル サインオンの構成]** ページで、**[証明書のダウンロード]** をクリックし、コンピューターにファイルを保存します。また、発行者の URL、シングル サインオン サービス URL、シングル サインアウト サービス URL の値をコピーします。構成された SSO を取得するには、この情報を PostBeyond サポートと共有する必要があります。
   
    ![Configure Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_08.png)
2. アプリケーション用に構成された SSO を入手するために、PostBeyond のサポート チーム (<mailto:sso@postbeyond.com>) に問い合わせます。SSO を構成し、次の情報を共有するための適切な手続きについてサポートを受けることができます。
   
   * ダウンロードした証明書
   * **発行者の URL**
   * **SAML SSO URL**
   *  **シングル サインアウト サービス URL**
3. クラシック ポータルで、シングル サインオンの構成確認を選択し、**[次へ]** をクリックします。
   
    ![Azure AD Single Sign-On][10]
4. **[シングル サインオンの確認]** ページで **[完了]** をクリックします。
   
    ![Azure AD Single Sign-On][11]

### Azure AD のテスト ユーザーの作成
このセクションでは、クラシック ポータルで Britta Simon というテスト ユーザーを作成します。

![Azure AD ユーザーの作成][20]

**Azure AD でテスト ユーザーを作成するには、次の手順に従います。**

1. **Azure クラシック ポータル**の左側のナビゲーション ウィンドウで、**[Active Directory]** をクリックします。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_09.png)
2. **[ディレクトリ]** の一覧から、ディレクトリ統合を有効にするディレクトリを選択します。
3. 上部のメニューで **[ユーザー]** をクリックして、ユーザーの一覧を表示します。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_03.png)
4. 下部にあるツール バーで **[ユーザーの追加]** をクリックして、**[ユーザーの追加]** ダイアログ ボックスを開きます。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_04.png)
5. **[このユーザーに関する情報の入力]** ダイアログ ページで、次の手順に従います。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_05.png)
   
    a.[ユーザーの種類] として [組織内の新しいユーザー] を選択します。
   
    b.**[ユーザー名]** ボックスに「**BrittaSimon**」と入力します。
   
    c.**[次へ]** をクリックします。
6. **[ユーザー プロファイル]** ダイアログ ページで、次の手順に従います。
   
   ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_06.png)
   
   a.**[名]** ボックスに「**Britta**」と入力します。
   
   b.**[姓]** ボックスに「**Simon**」と入力します。
   
   c.**[表示名]** ボックスに「**Britta Simon**」と入力します。
   
   d.**[ロール]** 一覧で **[ユーザー]** を選択します。
   
   e.**[次へ]** をクリックします。
7. **[一時パスワードの取得]** ダイアログ ページで、**[作成]** をクリックします。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_07.png)
8. **[一時パスワードの取得]** ダイアログ ページで、次の手順に従います。
   
    ![Azure AD のテスト ユーザーの作成](./media/active-directory-saas-postbeyond-tutorial/create_aaduser_08.png)
   
    a.**[新しいパスワード]** の値を書き留めます。
   
    b.**[完了]** をクリックします。

### PostBeyond テスト ユーザーの作成
このセクションでは、PostBeyond で Britta Simon というユーザーを作成します。PostBeyond に Britta Simon を追加する方法がわからない場合は、PostBeyond サポート チームと協力してテスト ユーザーを追加し、SSO を有効にしてください。連絡先は <mailto:sso@postbeyond.com> です。

### Azure AD テスト ユーザーの割り当て
このセクションでは、Britta Simon に PostBeyond へのアクセスを許可することで、このユーザーが Azure シングル サインオンを使用できるようにします。

![ユーザーの割り当て][200]

**PostBeyond に Britta Simon を割り当てるには、次の手順を実行します。**

1. クラシック ポータルでアプリケーション ビューを開くために、ディレクトリ ビューでトップ メニューの **[アプリケーション]** をクリックします。
   
    ![ユーザーの割り当て][201]
2. アプリケーションの一覧で **[PostBeyond]** を選択します。
   
    ![Configure Single Sign-On](./media/active-directory-saas-postbeyond-tutorial/tutorial_postbeyond_09.png)
3. 上部のメニューで **[ユーザー]** をクリックします。
   
    ![ユーザーの割り当て][203]
4. [すべてのユーザー] の一覧で **[Britta Simon]** を選択します。
5. 下部にあるツール バーで **[割り当て]** をクリックします。
   
    ![ユーザーの割り当て][205]

### シングル サインオンのテスト
このセクションの目的は、アクセス パネルを使用して Azure AD のシングル サインオン構成をテストすることです。

アクセス パネルの [PostBeyond] タイルをクリックすると、PostBeyond サインイン ページに移動します。**[Sign in with Office 365 (Office 365 でサインイン)]** をクリックし、Azure AD の資格情報を入力すると、PostBeyond へのログインが行われます。

## その他のリソース
* [SaaS アプリと Azure Active Directory を統合する方法に関するチュートリアルの一覧](active-directory-saas-tutorial-list.md)
* [Azure Active Directory のアプリケーション アクセスとシングル サインオンとは](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_06.png
[7]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-postbeyond-tutorial/tutorial_general_205.png

<!---HONumber=AcomDC_0817_2016-->