---
title: Azure ポータルを使用した Azure SQL Database の計画されたフェールオーバーまたは計画されていないフェールオーバーの開始 | Microsoft Docs
description: Azure ポータルを使用した Azure SQL Database の計画されたフェールオーバーまたは計画されていないフェールオーバーの開始
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: ''

ms.service: sql-database
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 08/29/2016
ms.author: sstein

---
# Azure ポータルを使用した Azure SQL Database の計画されたフェールオーバーまたは計画されていないフェールオーバーの開始
> [!div class="op_single_selector"]
> * [Azure ポータル](sql-database-geo-replication-failover-portal.md)
> * [PowerShell](sql-database-geo-replication-failover-powershell.md)
> * [T-SQL](sql-database-geo-replication-failover-transact-sql.md)
> 
> 

この記事では、[Azure ポータル](http://portal.azure.com)を使用して、セカンダリ SQL Database へのフェールオーバーを開始する方法について説明します。geo レプリケーションを構成する場合は、[Azure SQL Database の geo レプリケーションの構成](sql-database-geo-replication-portal.md)に関するページをご覧ください。

## フェールオーバーの開始
セカンダリ データベースは、プライマリ データベースとして使用するように切り替えることができます。

1. [Azure ポータル](http://portal.azure.com)で、geo レプリケーション パートナーシップのプライマリ データベースを参照します。
2. [SQL Database] ブレードで、**[すべての設定]**、**[geo レプリケーション]** の順に選択します。
3. **[セカンダリ]** ボックスの一覧で、新しいプライマリとして使用するデータベースを選択し、**[フェールオーバー]** をクリックします。
   
    ![フェールオーバー][2]
4. **[はい]** をクリックして、フェールオーバーを開始します。

このコマンドは、セカンダリ データベースをプライマリ ロールに即座に切り替えます。

ロールの切り替え中に、わずかですが両方のデータベースが使用できなくなる期間 (0 ～ 25 秒程度) が生じます。プライマリ データベースに複数のセカンダリ データベースがある場合は、コマンドによって、新しいプライマリに接続するように他のセカンダリが自動的に再構成されます。通常の状況では、操作全体が完了するのに 1 分かかりません。

> [!NOTE]
> コマンドが発行されたときに、プライマリがオンラインでトランザクションをコミット中の場合、一部のデータが失われる可能性があります。
> 
> 

## 次のステップ
* フェールオーバー後は、サーバーおよびデータベースの認証要件が新しいプライマリで構成されていることを確認してください。詳細については、[障害復旧後の SQL Database のセキュリティ](sql-database-geo-replication-security-config.md)に関するページを参照してください。
* 復旧前後の手順や障害復旧訓練の実施など、アクティブ geo レプリケーションを使用した障害後の復旧については、[障害復旧の訓練](sql-database-disaster-recovery.md)に関するページをご覧ください。
* アクティブ geo レプリケーションについては、Sasha Nosov の [geo レプリケーションの新機能](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/)に関するブログ記事をご覧ください。
* アクティブ geo レプリケーションを使用したクラウド アプリケーションの設計については、[geo レプリケーションを使用したビジネス継続性のためのクラウド アプリケーション設計](sql-database-designing-cloud-solutions-for-disaster-recovery.md)に関するページをご覧ください。
* エラスティック データベース プールでのアクティブ geo レプリケーションの使用については、[エラスティック プールの障害復旧戦略](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)に関するページをご覧ください。
* ビジネス継続性の概要については、[ビジネス継続性の概要](sql-database-business-continuity.md)に関するページをご覧ください。

<!--Image references-->
[1]: ./media/sql-database-geo-replication-failover-portal/failover.png
[2]: ./media/sql-database-geo-replication-failover-portal/secondaries.png

<!---HONumber=AcomDC_0831_2016-->