---
title: Azure Data Lake Store に格納されているデータのセキュリティ保護 | Microsoft Docs
description: グループおよびアクセス制御リストを使用して Azure Data Lake Store 内のデータをセキュリティ保護する方法を説明する
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun

ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 09/06/2016
ms.author: nitinme

---
# Azure Data Lake Store に格納されているデータのセキュリティ保護
Azure Data Lake Store のデータをセキュリティで保護するには 3 つの手順が必要です。

1. まず、Azure Active Directory (AAD) でセキュリティ グループを作成します。Azure ポータルで、これらのセキュリティ グループを使用してロールベースのアクセス制御 (RBAC) を実装します。詳細については、「[Microsoft Azure でのロールベースのアクセス制御](../active-directory/role-based-access-control-configure.md)」を参照してください。
2. AAD セキュリティ グループを Azure Data Lake Store アカウントに割り当てます。これにより、ポータルから Data Lake Store アカウントへのアクセス、およびポータルまたは API による管理操作が制御されます。
3. AAD セキュリティ グループをアクセス制御リスト (ACL) として Data Lake Store ファイル システムに割り当てます。
4. さらに、Data Lake Store 内のデータにアクセスできるクライアントの IP アドレスの範囲を設定することもできます。

この記事では、Azure ポータルを使用して上記タスクを実行する方法について説明します。Data Lake Store でアカウントおよびデータのレベルでどのようにセキュリティが実装されるかについては、「[Security in Azure Data Lake Store (Azure Data Lake Store のセキュリティ)](data-lake-store-security-overview.md)」を参照してください。

## 前提条件
このチュートリアルを読み始める前に、次の項目を用意する必要があります。

* **Azure サブスクリプション**。[Azure 無料試用版の取得](https://azure.microsoft.com/pricing/free-trial/)に関するページを参照してください。
* **Azure Data Lake Store アカウント**。このアカウントを作成する手順については、「[Azure Data Lake Store の使用を開始する](data-lake-store-get-started-portal.md)」を参照してください。

## ビデオで速習する
Data Lake Store に格納されているデータのセキュリティ保護の方法については、[こちらのビデオ](https://mix.office.com/watch/1q2mgzh9nn5lx)をご覧ください。

## Azure Active Directory でセキュリティ グループを作成する
AAD セキュリティ グループを作成する手順および AAD セキュリティ グループにユーザーを追加する手順については、「[Azure Active Directory のセキュリティ グループの管理](../active-directory/active-directory-accessmanagement-manage-groups.md)」を参照してください。

## ユーザーまたはセキュリティ グループを Azure Data Lake Store アカウントに割り当てる
ユーザーまたはセキュリティ グループを Azure Data Lake Store アカウントに割り当てる場合は、Azure ポータルと Azure リソース マネージャー API を使用して、アカウントに関する管理操作へのアクセスを制御します。

1. Azure Data Lake Store アカウントを開きます。左側のウィンドウで、**[参照]**、**[Data Lake Store]** の順にクリックし、[Data Lake Store] ブレードで、ユーザーまたはセキュリティ グループを割り当てるアカウント名をクリックします。
2. Data Lake Store アカウントのブレードで、ユーザー アイコンをクリックします。
   
    ![セキュリティ グループを Azure Data Lake Store アカウントに割り当てる](./media/data-lake-store-secure-data/adl.select.user.icon.png "セキュリティ グループを Azure Data Lake Store アカウントに割り当てる")
3. **[ユーザー]** ブレードには既定では、**[サブスクリプション管理者]** グループが所有者として表示されます。
   
    ![ユーザーとロールを追加する](./media/data-lake-store-secure-data/adl.add.group.roles.png "ユーザーとロールを追加する")
   
    グループを追加し関連するロールを割り当てるには 2 つの方法があります。
   
   * アカウントにユーザーまたはグループを追加して、ロールを割り当てる。あるいは、
   * ロールを追加し、ロールにユーザーまたはグループを割り当てる。
     
     このセクションでは、グループを追加してからロールを割り当てるという 1 番目の方法を説明します。同様の手順を実行して、ロールを選択してからグループをそのロールに割り当てることもできます。
4. **[ユーザー]** ブレードの **[追加]** をクリックして **[アクセス権の追加]** ブレードを開きます。**[アクセス権の追加]** ブレードで、**[ロールの選択]** をクリックし、ユーザーまたはグループのロールを選択します。
   
     ![ユーザーのロールを追加する](./media/data-lake-store-secure-data/adl.add.user.1.png "ユーザーのロールを追加する")
   
    **[所有者]** ロールと **[共同作成者]** ロールは、Data Lake アカウントでさまざまな管理機能へのアクセスを許可します。Data Lake 内のデータと対話するユーザーについては、該当するユーザーを **[閲覧者]** ロールに追加できます。これらのロールの適用範囲は、Azure Data Lake Store アカウントに関連する管理操作に限定されます。
   
    データ操作の場合、ユーザーが行える操作はファイル システムの個々のアクセス許可によって定義されます。そのため、閲覧者ロールを持つユーザーはアカウントに関連付けられた管理設定しか表示できません。しかし、場合によっては、そのユーザーに割り当てられているファイル システムのアクセス許可に基づいて、データの読み取りおよび書き込みができます。Data Lake Store ファイル システムのアクセス許可については、「[セキュリティ グループを ACL として Azure Data Lake Store ファイル システムに割り当てる](#filepermissions)」を参照してください。
5. **[アクセス権の追加]** ブレードの **[ユーザーの追加]** をクリックして **[ユーザーの追加]** ブレードを開きます。このブレードで、前に Azure Active Directory で作成したセキュリティ グループを検索します。検索対象のグループが多数存在する場合は、上部にあるテキスト ボックスを使用してグループ名をフィルター処理できます。**[選択]** をクリックします。
   
    ![セキュリティ グループを追加する](./media/data-lake-store-secure-data/adl.add.user.2.png "セキュリティ グループを追加する")
   
    一覧表示されていないグループまたはユーザーを追加する場合は、**[招待]** アイコンをクリックしてからユーザーまたはグループの電子メール アドレスを指定することで、該当するユーザーを招待することができます。
6. **[OK]** をクリックします。次に示すように追加したセキュリティ グループが表示されます。
   
    ![追加されたセキュリティ グループ](./media/data-lake-store-secure-data/adl.add.user.3.png "追加されたセキュリティ グループ")
7. これで、ユーザーまたはセキュリティ グループは、Azure Data Lake Store アカウントにアクセスできるようになりました。特定のユーザーにアクセス権を付与する場合は、対象ユーザーをセキュリティ グループに追加します。同様に、ユーザーのアクセス権を取り消す場合は、セキュリティ グループから対象ユーザーを削除します。アカウントには複数のセキュリティ グループを割り当てることもできます。

## <a name="filepermissions"></a>ユーザーまたはセキュリティ グループを ACL として Azure Data Lake Store ファイル システムに割り当てる
Azure Data Lake ファイル システムにユーザーまたはセキュリティ グループを割り当てて、Azure Data Lake Store に格納されたデータに対するアクセス制御を設定します。

> [!NOTE]
> 現在のリリースでは、Data Lake Store アカウントのルート ノードにのみ ACL を設定できます。さらに、ACL を追加および変更できるのは、[所有者] ロールが割り当てられているユーザーのみです。
> 
> 

1. Data Lake Store アカウントのブレードで、**[データ エクスプローラー]** をクリックします。
   
    ![Data Lake Store アカウントにディレクトリを作成する](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake アカウントにディレクトリを作成する")
2. **[データ エクスプローラー]** ブレードで、アカウントのルートをクリックし、アカウント ブレードの **[アクセス]** アイコンをクリックします。
   
    ![Data Lake ファイル システムに ACL を設定する](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake ファイル システムに ACL を設定する")
3. **[アクセス]** ブレードには、既にルートに割り当てられている標準アクセスとカスタム アクセスが一覧表示されます。**[追加]** アイコンをクリックして、カスタムレベルの ACL を追加します。
   
    ![標準アクセスとカスタム アクセスを一覧表示する](./media/data-lake-store-secure-data/adl.acl.2.png "標準アクセスとカスタム アクセスを一覧表示する")
   
   * **標準アクセス**は UNIX 形式のアクセスです。この場合は、読み取り、書き込み、実行 (rwx) を 3 つの個別のユーザー クラス (所有者、グループ、その他) に指定します。
   * **カスタム アクセス**は POSIX ACL に対応します。この場合、ファイルの所有者またはグループだけでなく、特定の名前付きユーザーまたはグループにもアクセス許可を設定することができます。
     
     詳細については、[HDFS ACL](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists) を参照してください。
4. **[追加]** アイコンをクリックして、**[カスタム アクセスの追加]** ブレードを開きます。このブレードの **[ユーザーまたはグループの選択]** をクリックし、**[ユーザーまたはグループの選択]** ブレードで前に Azure Active Directory で作成したセキュリティ グループを検索します。検索対象のグループが多数存在する場合は、上部にあるテキスト ボックスを使用してグループ名をフィルター処理できます。追加するグループをクリックして、**[選択]** をクリックします。
   
    ![グループを追加する](./media/data-lake-store-secure-data/adl.acl.3.png "グループを追加する")
5. **[アクセス許可の選択]** をクリックし、そのグループに割り当てるアクセス許可を選択し、**[OK]** をクリックします。
   
    ![グループにアクセス許可を割り当てる](./media/data-lake-store-secure-data/adl.acl.4.png "グループにアクセス許可を割り当てる")
   
    アクセス許可は次のように理解することができます。
   
   * **読み取り** - このアクセス許可がディレクトリに対して設定されている場合、そのディレクトリ内のファイルの名前を読み取ることができます。
   * **書き込み** - このアクセス許可がディレクトリに対して設定されている場合、ファイルの作成、削除、名前変更など、ディレクトリ内のエントリを変更することができます。
   * **実行** - このアクセス許可がディレクトリに対して設定されている場合、そのディレクトリ内のファイルのコンテンツにアクセスすることができます。また、ファイル名がわかっている場合は、ファイルのメタデータにアクセスすることもできます。ただし、**読み取り**アクセス許可も設定されていない限り、このアクセス許可でディレクトリ内のファイルを一覧表示することはできません。
     
     > [!NOTE]
     > **読み取りと実行**アクセス許可はディレクトリを列挙する場合に必要です。また、データへの読み取り専用アクセスをユーザーまたはグループに許可する場合にもしばしば必要となります。
     > 
     > 
6. **[カスタム アクセスの追加]** ブレードで **[OK]** をクリックします。新しく追加されたグループは、関連付けられたアクセス許可と一緒に **[アクセス]** ブレードに一覧表示されます。
   
    ![グループにアクセス許可を割り当てる](./media/data-lake-store-secure-data/adl.acl.5.png "グループにアクセス許可を割り当てる")
   
   > [!IMPORTANT]
   > 現在のリリースでは、**[カスタム アクセス]** に設定できるエントリは 9 個のみです。9 を超えるユーザーを追加する場合は、セキュリティ グループを作成し、セキュリティ グループにユーザーを追加して、それらのセキュリティ グループに Data Lake Store アカウントに対するアクセス権を付与します。　
   > 
   > 
7. 必要に応じて、グループを追加した後で、アクセス許可を変更することもできます。各種類のアクセス許可 (Read、Write、Execute) のチェック ボックスをオフにするかオンにするかは、セキュリティ グループにアクセス許可を割り当てるか、セキュリティ グループからアクセス許可を削除するかに応じて決定します。**[保存]** をクリックして変更を保存するか、**[破棄]** をクリックして変更を元に戻します。

## データ アクセス用の IP アドレスの範囲を設定する
Azure Data Lake Store では、データ ストアへのアクセスをネットワーク レベルでさらにロック ダウンできます。信頼されたクライアントに対して、ファイアウォールを有効にし、IP アドレスを指定し、IP アドレス範囲を定義することができます。ファイアウォールが有効になると、IP アドレスが定義済みの範囲内にあるクライアントだけがストアに接続できます。

![ファイアウォール設定と IP アクセス](./media/data-lake-store-secure-data/firewall-ip-access.png "ファイアウォール設定と IP アドレス")

## Azure Data Lake Store アカウントのセキュリティ グループを削除する
Azure Data Lake Store アカウントからセキュリティ グループを削除する場合は、Azure ポータルと Azure リソース マネージャー API を使用して、アカウントに関する管理操作へのアクセスを変更するだけです。

1. Data Lake Store アカウントのブレードで、ユーザー アイコンをクリックします。
   
    ![セキュリティ グループを Azure Data Lake アカウントに割り当てる](./media/data-lake-store-secure-data/adl.select.user.icon.png "セキュリティ グループを Azure Data Lake アカウントに割り当てる")
2. **[ユーザー]** ブレードで、削除するセキュリティ グループをクリックします。
   
    ![削除するセキュリティ グループ](./media/data-lake-store-secure-data/adl.add.user.3.png "削除するセキュリティ グループ")
3. セキュリティ グループのブレードで、**[削除]** をクリックします。
   
    ![削除されたセキュリティ グループ](./media/data-lake-store-secure-data/adl.remove.group.png "削除されたセキュリティ グループ")

## Azure Data Lake Store ファイル システムからセキュリティ グループ ACL を削除する
Azure Data Lake Store ファイル システムからセキュリティ グループの ACL を削除する場合は、Data Lake Store ストア内のデータへのアクセスを変更します。

1. Data Lake Store アカウントのブレードで、**[データ エクスプローラー]** をクリックします。
   
    ![Data Lake アカウントにディレクトリを作成する](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Data Lake アカウントにディレクトリを作成する")
2. **[データ エクスプローラー]** ブレードで、アカウントのルートをクリックし、アカウント ブレードの **[アクセス]** アイコンをクリックします。
   
    ![Data Lake ファイル システムに ACL を設定する](./media/data-lake-store-secure-data/adl.acl.1.png "Data Lake ファイル システムに ACL を設定する")
3. **[アクセス]** ブレードの **[カスタム アクセス]** セクションで、削除するセキュリティ グループをクリックします。**[カスタム アクセス]** ブレードで、**[削除]** をクリックし、**[OK]** をクリックします。
   
    ![グループにアクセス許可を割り当てる](./media/data-lake-store-secure-data/adl.remove.acl.png "グループにアクセス許可を割り当てる")

## 関連項目
* [Azure Data Lake Store の概要](data-lake-store-overview.md)
* [Azure Storage BLOB から Data Lake Store へのデータのコピー](data-lake-store-copy-data-azure-storage-blob.md)
* [Data Lake Store で Azure Data Lake Analytics を使用する](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Data Lake Store で Azure HDInsight を使用する](data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell で Data Lake Store の使用を開始する](data-lake-store-get-started-powershell.md)
* [.NET SDK で Azure Data Lake Store の使用を開始する](data-lake-store-get-started-net-sdk.md)
* [Data Lake Store の診断ログへのアクセス](data-lake-store-diagnostic-logs.md)

<!---HONumber=AcomDC_0914_2016-->