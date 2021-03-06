---
title: "モノのインターネット用の Azure ソリューション | Microsoft Docs"
description: "サンプル ソリューション アーキテクチャや、それが、Azure IoT Hub、デバイス SDK、および構成済みソリューションとどのように関連するかなど、Azure での IoT の概要。"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/05/2016
ms.author: dobett
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 2dbf639abfa505eb329769bcc346efb5f1db443e


---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>次のステップ
Azure IoT Hub は、アプリケーション バックエンドと何百万ものデバイスとの間に信頼性のある保護された双方向通信を確立できるサービスです。 これによりアプリケーション バックエンドから次のことを実行できるようになります。

* デバイスから大量のテレメトリを受信する。
* デバイスからストリーム イベント プロセッサにデータをルーティングする。
* デバイスからアップロードされたファイルを受信する。
* クラウドからデバイスへのコマンドを特定のデバイスに送信する。

IoT Hub を使用して、独自のソリューション バックエンドを実装できます。 さらに、IoT Hub には、デバイスと、デバイスのセキュリティ資格情報と、デバイスがハブに接続するための権限とをプロビジョニングするために使用するデバイス ID レジストリが含まれています。 IoT Hub の詳細については、「[Azure IoT Hub とは][lnk-iot-hub]」を参照してください。

Azure IoT Hub では、標準ベースのデバイス管理が可能となっており、リモートからデバイスを管理、構成、更新することができます。詳細については、[IoT Hub によるデバイス管理の概要][lnk-device-management]に関するページを参照してください。

クライアント アプリケーションを各種デバイス ハードウェア プラットフォームやオペレーティング システムに実装するために、IoT デバイス SDK を使用できます。 IoT デバイス SDK には、テレメトリを IoT Hub に送信し、クラウドからデバイスへのコマンドを受信する操作を容易にするライブラリが含まれています。 これらの SDK を使用すると、さまざまなネットワーク プロトコルのうちのいずれかを選択して IoT Hub と通信することができます。 詳細については、[デバイス SDK][lnk-device-sdks] に関する情報を参照してください。

実際にコードを作成してサンプルを実行するには、[IoT Hub の使用][lnk-getstarted]に関するチュートリアルを参照してください。

構成済みソリューションのコレクションである [Azure IoT Suite][lnk-iot-suite] もご確認ください。 IoT Suite を使用すると、リモート モニタリング、資産管理、予測メンテナンスなど、一般的な IoT シナリオに対処するための IoT プロジェクトをすばやく開始してスケーリングできます。

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks/blob/master/readme.md
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md



<!--HONumber=Nov16_HO2-->


