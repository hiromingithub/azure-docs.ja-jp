---
title: VM スケール セットとは | Microsoft Docs
description: VM スケール セットについて説明します。
keywords: Linux 仮想マシン,仮想マシン スケール セット
services: virtual-machines-linux
documentationcenter: ''
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager

ms.service: virtual-machine-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/24/2016
ms.author: gatneil

---
# 仮想マシン スケール セットとは
仮想マシン スケール セットを利用すれば、複数の VM を セットとして管理できます。大まかに言うと、スケール セットには次のような長所と短所があります。

長所:

1. 高可用性:各スケール セットでは、VM が 5 つの障害ドメイン (FD) と 5 つの更新ドメイン (UD) を持つ可用性セットに割り当てられ、可用性が保証されます (FD と UD の詳細については、「[Linux 仮想マシンの可用性管理](virtual-machines-linux-manage-availability.md)」を参照してください)。 
2. Azure Load Balancer および Application Gateway との容易な統合。
3. Azure 自動スケールとの容易な統合。
4. VM の簡略化されたデプロイ、管理、クリーンアップ。
5. カスタム イメージだけでなく、Windows や Linux の一般的なディストリビューションもサポート。

短所:

1. スケール セット内の VM インスタンスにデータ ディスクをアタッチすることはできません。代わりに、Blob Storage、Azure Files、Azure テーブルなどのストレージ ソリューションを使用する必要があります。

## Azure CLI を使用した簡易作成
[!INCLUDE [cli-vmss-quick-create](../../includes/virtual-machines-linux-cli-vmss-quick-create-include.md)]

## 次のステップ
全般的な情報については、[VM スケール セットのメイン ランディング ページ](https://azure.microsoft.com/services/virtual-machine-scale-sets/)をご覧ください。

ドキュメントについては、[スケール セットのメイン ドキュメント ページ](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md)をご覧ください。

スケール セットを使用した Resource Manager テンプレートの例については、[Azure クイックスタート テンプレートの GitHub リポジトリ](https://github.com/Azure/azure-quickstart-templates)で "vmss" を検索してください。

<!---HONumber=AcomDC_0413_2016-->