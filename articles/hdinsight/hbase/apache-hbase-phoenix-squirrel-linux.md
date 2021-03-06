---
title: Utiliser Apache Phoenix et SQLLine avec HBase dans Azure HDInsight
description: Découvrez comment utiliser Apache Phoenix dans HDInsight. Découvrez également comment installer et configurer SQLLine sur votre ordinateur pour vous connecter à un cluster HBase dans HDInsight.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/03/2018
ms.author: hrasheed
ms.openlocfilehash: 51707baeba4a511d2766161afacd512a4338cf24
ms.sourcegitcommit: e68df5b9c04b11c8f24d616f4e687fe4e773253c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53653983"
---
# <a name="use-apache-phoenix-with-linux-based-apache-hbase-clusters-in-hdinsight"></a>Utiliser Apache Phoenix avec les clusters Apache HBase basés sur Linux dans HDInsight
Découvrez comment utiliser [Apache Phoenix](https://phoenix.apache.org/) dans Azure HDInsight et comment utiliser SQLLine. Pour plus d’informations sur Phoenix, consultez [Apache Phoenix en 15 minutes ou moins](https://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Pour en savoir plus sur la grammaire Phoenix, consultez [Grammaire Apache Phoenix](https://phoenix.apache.org/language/index.html).

> [!NOTE]  
> Pour plus d’informations sur la version de Phoenix avec HDInsight, consultez [Nouveautés des versions de cluster Apache Hadoop fournies par HDInsight](../hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Utiliser SQLLine
[SQLLine](http://sqlline.sourceforge.net/) est un utilitaire de ligne de commande pour exécuter SQL.

### <a name="prerequisites"></a>Prérequis
Avant de pouvoir utiliser SQLLine, vous devez disposer des éléments suivants :

* **Un cluster Apache HBase dans HDInsight** Pour en créer un, consultez [Prise en main d’un exemple Apache HBase dans HDInsight](./apache-hbase-tutorial-get-started-linux.md).

Quand vous vous connectez à un cluster HBase, vous devez vous connecter à l’une des machines virtuelles [Apache ZooKeeper](https://zookeeper.apache.org/). Chaque cluster HDInsight a trois machines virtuelles ZooKeeper.

**Pour connaître le nom d’hôte ZooKeeper**

1. Ouvrez [Apache Ambari](https://ambari.apache.org/) en accédant à la page **https://\<nom du cluster\>.azurehdinsight.net**.
2. Pour vous connecter, entrez le nom d’utilisateur (cluster) HTTP et le mot de passe.
3. Dans le menu de gauche, sélectionnez **ZooKeeper**. Trois instances de **serveur ZooKeeper** apparaissent dans la liste.
4. Sélectionnez l’une de ces instances de **serveur ZooKeeper**. Dans le volet **Résumé**, recherchez le **nom d’hôte**. Il ressemble à *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**Pour utiliser SQLLine**

1. Connectez-vous au cluster à l’aide de SSH. Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](../hdinsight-hadoop-linux-use-ssh-unix.md).

2. Dans SSH, utilisez les commandes suivantes pour exécuter SQLLine :

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ZOOKEEPER SERVER FQDN>:2181:/hbase-unsecure
3. Pour créer une table HBase et insérer des données, exécutez les commandes suivantes :

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Apache Phoenix](https://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment utiliser Apache Phoenix dans HDInsight. Pour en savoir plus, consultez les articles suivants :

* [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview].
  Apache HBase est une base de données NoSQL open source Apache basée sur Apache Hadoop qui fournit un accès aléatoire et une forte cohérence pour de vastes quantités de données non structurées et semi-structurées.
* [Provisionnement des clusters Apache HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet].
  Avec l’intégration du réseau virtuel, les clusters Apache HBase peuvent être déployés sur le même réseau virtuel que vos applications pour permettre à celles-ci de communiquer directement avec HBase.
* [Configuration de la réplication Apache HBase dans HDInsight](apache-hbase-replication.md). Découvrez comment configurer la réplication Apache HBase entre deux centres de données Azure.


[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]:apache-hbase-provision-vnet.md
[hdinsight-hbase-overview]:apache-hbase-overview.md


