---
title: Event Hubs メッセージングの例外 | Microsoft Docs
description: Azure Event Hubs メッセージングの例外と推奨アクションの一覧。
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: ''

ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: sethm

---
# Event Hubs メッセージングの例外
この記事では、Azure Service Bus のメッセージング API によって生成される例外を示します。この API セットには、Event Hubs が含まれます。このリファレンスは変更される可能性があるため、最新情報をご確認ください。

## 例外のカテゴリ
メッセージング API で生成される例外をカテゴリ別に分類し、修復のために実行できる関連するアクションと共に以下に示します。例外の意味と原因は、メッセージング エンティティの種類 (リレー、キュー/トピック、Event Hubs) によって異なる場合があります。

1. ユーザー コードのエラー ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)、[System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx)、[System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx)、[System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx))。一般アクション: 処理を実行する前にコードの修正を試みます。
2. セットアップ/構成エラー ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingentitynotfoundexception.aspx)、[System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx))。一般アクション: 構成を確認し、必要に応じて変更します。
3. 一時的な例外 ([Microsoft.ServiceBus.Messaging.MessagingException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingexception.aspx)、[Microsoft.ServiceBus.Messaging.ServerBusyException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.serverbusyexception.aspx)、[Microsoft.ServiceBus.Messaging.MessagingCommunicationException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingcommunicationexception.aspx))。一般アクション: 操作をやり直すか、ユーザーに通知します。
4. その他の例外 ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx)、[System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx)、[Microsoft.ServiceBus.Messaging.MessageLockLostException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagelocklostexception.aspx)、[Microsoft.ServiceBus.Messaging.SessionLockLostException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sessionlocklostexception.aspx))。全般的なアクション: 例外の種類に固有。次のセクションの表を参照してください。

## 例外の種類
次の表は、メッセージングの例外の種類および原因と実行できる推奨アクションを示したものです。

| **例外の種類** | **説明/原因/例** | **推奨アクション** | **自動/即時再試行に関する注意** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |サーバーは、[OperationTimeout](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) によって制御される指定された時間内に、要求された操作に対して応答しませんでした。サーバーで、要求された操作が完了した可能性があります。これは、ネットワークや他のインフラストラクチャの遅延が原因で発生することがあります。 |システム状態の整合性をチェックして、必要な場合は再試行してください。 |再試行によって解決する場合があります。再試行ロジックをコードに追加してください。 |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |要求されたユーザー操作はサーバーまたはサービス内で許可されていません。詳細については、例外メッセージを参照してください。たとえば、[Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx) は、**ReceiveAndDelete** モードでメッセージを受信した場合に、この例外を生成します。 |コードとドキュメントを確認します。要求した操作が有効なことを確かめてください。 |再試行によって解決することはありません。 |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |既に終了、中止、または破棄されたオブジェクトに対して操作を呼び出そうとしました。まれに、アンビエント トランザクションが既に破棄されている場合があります。 |コードを確認し、破棄されたオブジェクトに対して操作を呼び出していないことを確かめます。 |再試行によって解決することはありません。 |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |[TokenProvider](https://msdn.microsoft.com/library/azure/microsoft.servicebus.tokenprovider.aspx) オブジェクトはトークンを取得できませんでした。トークンが無効です。または、操作の実行に必要な要求がトークンに含まれていません。 |トークン プロバイダーが正しい値を使用して作成されていることを確認します。Access Control Service の構成を確認します。 |再試行によって解決する場合があります。再試行ロジックをコードに追加してください。 |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |メソッドに指定された 1 つまたは複数の引数が無効です。[NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.servicebus.namespacemanager.aspx) または [Create](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingfactory.create.aspx) に指定された URI にパス セグメントが含まれています。[NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.servicebus.namespacemanager.aspx) または [Create](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingfactory.create.aspx) に指定された URI スキームが無効です。プロパティ値が 32 KB を超えています。 |呼び出し元のコードを確認し、引数が正しいことを確かめます。 |再試行によって解決することはありません。 |
| [MessagingEntityNotFoundException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingentitynotfoundexception.aspx) |操作に関連付けられているエンティティが存在しないか、削除されました。 |エンティティが存在することを確認します。 |再試行によって解決することはありません。 |
| [MessageNotFoundException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagenotfoundexception.aspx) |特定のシーケンス番号を持つメッセージを受信しようとしました。このメッセージが見つかりません。 |メッセージがまだ受信されていないことを確認します。配信不能キューを確認し、メッセージが配信不能になっているかどうかを確かめます。 |再試行によって解決することはありません。 |
| [MessagingCommunicationException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingcommunicationexception.aspx) |クライアントから Event Hub への接続を確立できません。 |指定されたホスト名が正しく、ホストが到達可能なことを確認してください。 |断続的な接続の問題がある場合は、再試行によって解決することがあります。 |
| [ServerBusyException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.serverbusyexception.aspx) |この時点では、このサービスで要求を処理できません。 |クライアントは、しばらく待機してから操作をやり直すことができます。 |クライアントは、一定の間隔をおいてから再試行することができます。再試行の結果として別の例外が発生した場合は、その例外の再試行動作を確認します。 |
| [MessageLockLostException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagelocklostexception.aspx) |メッセージに関連付けられているロック トークンが期限切れになったか、ロック トークンが見つかりません。 |メッセージを破棄してください。 |再試行によって解決することはありません。 |
| [SessionLockLostException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sessionlocklostexception.aspx) |このセッションに関連付けられているロックが失われました。 |[MessageSession](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesession.aspx) オブジェクトを中止してください。 |再試行によって解決することはありません。 |
| [MessagingException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingexception.aspx) |次の場合にスローされる可能性がある一般メッセージング例外です。異なるエンティティの種類 (たとえば、トピック) に属する名前またはパスを使用して、[QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) を作成しようとした場合。256 KB を超えるメッセージを送信しようとした場合。サーバーまたはサービスで要求の処理中にエラーが発生しました。詳細については、例外メッセージを参照してください。これは通常、一時的な例外です。 |コードを確認し、メッセージ本文にシリアル化可能なオブジェクトのみを使用していることを確かめます (または、カスタム シリアライザーを使用します)。サポートされているプロパティ値の型をドキュメントで確認し、サポートされている型だけを使用します。[IsTransient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingexception.istransient.aspx) プロパティを確認します。それが **true** である場合は、操作を再試行できます。 |再試行動作は未定義であり、解決にならない場合もあります。 |
| [MessagingEntityAlreadyExistsException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingentityalreadyexistsexception.aspx) |そのサービスの名前空間で別のエンティティによって既に使用されている名前を持つエンティティを作成しようとしました。 |既存のエンティティを削除するか、作成するエンティティに別の名前を選択します。 |再試行によって解決することはありません。 |
| [QuotaExceededException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.quotaexceededexception.aspx) |メッセージング エンティティが最大許容サイズに達しています。 |エンティティまたはそのサブキューからメッセージを受信して、エンティティ内に領域を作成します。 |メッセージがそれまでに削除されている場合は、再試行によって解決することがあります。 |
|  | | | |
| [SessionCannotBeLockedException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.sessioncannotbelockedexception.aspx) |特定のセッション ID を持つセッションを使用しようとしましたが、セッションは現在別のクライアントによってロックされています。 |別のクライアントによるセッションのロックが解除されたことを確認します。 |セッションがそれまでに解放されている場合は、再試行によって解決することがあります。 |
| [TransactionSizeExceededException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.transactionsizeexceededexception_methods.aspx) |トランザクションの一部になっている操作が多すぎます。 |このトランザクションの一部である操作の数を減らします。 |再試行によって解決することはありません。 |
| [MessagingEntityDisabledException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagingentitydisabledexception.aspx) |無効になっているエンティティに対してランタイム操作を要求しました。 |エンティティをアクティブ化します。 |エンティティがそれまでにアクティブ化されている場合は、再試行によって解決することがあります。 |
| [MessageSizeExceededException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagesizeexceededexception.aspx) |メッセージ ペイロードが 256K の制限を超えています。ただし 256k の制限はメッセージの合計サイズであり、システム プロパティや .NET のオーバーヘッドも含めたサイズです。 |メッセージ ペイロードのサイズを小さくし、操作を再試行します。 |再試行によって解決することはありません。 |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |アンビエント トランザクション (*Transaction.Current*) が無効です。トランザクションは完了または中止された可能性がありますがなります。内部例外で追加情報が提供される場合があります。 | |再試行によって解決することはありません。 |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |未確定トランザクションに対して操作が試行されたか、トランザクションのコミットが試行され、トランザクションが未確定になりました。 |トランザクションは既にコミットされた可能性があるため、アプリケーションはこの例外を (特殊なケースとして) 処理する必要があります。 |- |

## QuotaExceededException
[QuotaExceededException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.quotaexceededexception.aspx) は、特定のエンティティのクォータが超過していることを示します。

### Event Hubs
Event Hubs には、Event Hub あたり 20 個のコンシューマー グループという上限があります。それ以上作成しようとすると、[QuotaExceededException](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.quotaexceededexception.aspx) が発生します。

## TimeoutException
[TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) は、ユーザーが開始した操作が操作タイムアウトより時間がかかっていることを示します。

### Event Hubs
Event Hubs では、タイムアウトは接続文字列の一部として、または [ServiceBusConnectionStringBuilder](https://msdn.microsoft.com/library/azure/microsoft.servicebus.servicebusconnectionstringbuilder.aspx) を通じて指定されます。エラー メッセージ自体はさまざまですが、これには常に現在の操作に指定されたタイムアウト値が含まれます。

### 一般的な原因
この例外の一般的な原因には、次の 2 つがあります。正しくない構成と、一時的なサービス エラーです。

1. **構成が正しくない** 操作状態に対して、操作タイムアウトが小さすぎる可能性があります。クライアント SDK の操作タイムアウトの既定値は 60 秒です。コードに小さすぎる値を設定していないかどうかを確認します。ネットワークの状態と CPU 使用率は、特定の操作が完了する時間に影響します。このため、操作タイムアウトに小さい値を設定することは推奨されません。
2. **一時的なサービス エラー** Event Hubs サービスで、要求の処理に遅延が発生する場合 (トラフィック量の多い場合など) があります。このような場合、操作が成功するまで、遅延後に操作を再試行できます。複数回試行しても同じ操作が失敗する場合は、「[Azure Status](https://azure.microsoft.com/status/)」にアクセスして、既知のサービス停止がないかどうかを確認してください。

## 次のステップ
Service Bus と Event Hubs の詳細な .NET API リファレンスについては、[MSDN の Azure のリファレンス](https://msdn.microsoft.com/library/azure/mt419900.aspx)を参照してください。

<!--------HONumber=AcomDC_0824_2016-->