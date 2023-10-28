# Dcoker(DB) oracle

## 参考サイト
(【Docker】Oracleを無料で簡単にローカルに構築する)[https://zenn.dev/re24_1986/articles/29430f2f8b4b46]

## 環境
- Windws Linux(WSL)

## 手順

### ORACLE EXPRESS EDITIONのダウンロード

Oracle Database 21c Express Edition for Linux x64 ( OL7 )を使って環境構築  
[https://www.oracle.com/jp/database/technologies/xe-downloads.html](https://www.oracle.com/jp/database/technologies/xe-downloads.html)

### リポジトリにダウンロードしたOracleを配置

上でダウンロードしたOracleをクローンしたリポジトリの以下ディレクトリに配置  
```
./OracleDatabase/SingleInstance/dockerfiles/21.3.0
```

### イメージ作成シェルの実行
```
cd OracleDatabase/SingleInstance/dockerfiles
```
```
./buildContainerImage.sh -v 21.3.0 -x
```

**エラーが発生する際はPCを再起動**

### 生成物確認
```
$ docker images
REPOSITORY        TAG         IMAGE ID       CREATED       SIZE
oracle/database   21.3.0-xe   6d27683dbb4b   13 days ago   6.54GB
```

### ymlファイル作成
docker-compose.ymlを作成

### コンテナ作成＆起動
作成＆起動（docker-compose.ymlが存在するディレクトリで実行）  
```
docker-compose up -d
```

ログ確認  
```
docker-compose logs
```

ログ確認して以下のようなログが出てれば、Oracleが正常に起動  
（READYになるまで時間が掛かる）  
```
#########################
DATABASE IS READY TO USE!
#########################
```

### sqlplus起動
Oracleのコンテナに入る
```
docker exec -it oracle21c /bin/sh
```

sqlplus起動（作成ユーザーを確認）
```
sqlplus atman/atman@//localhost:1521/pdb01
```

___________________________________________________________
___________________________________________________________
# Docker Images from Oracle

This repository contains [Dockerfiles](https://docs.docker.com/engine/reference/builder/)
and samples to build [Docker](https://www.docker.com/what-docker) images for
Oracle commercial products and [Oracle sponsored open source projects](https://opensource.oracle.com).

## Container Images on GitHub

These images will require you to download any required Oracle commercial
software before installation. If you want commercial software downloaded for you,
 view [Pre-Built Images with Commercial Software](#pre-built-images-with-commercial-software).

### Oracle Commercial Products

- [Oracle Access Management](/OracleAccessManagement)
- [Oracle BI](/OracleBI)
- [Oracle Cloud Infrastructure Tools](/OracleCloudInfrastructure)
- [Oracle Coherence](/OracleCoherence)
- [Oracle Database](/OracleDatabase)
- [Oracle Essbase](/OracleEssbase)
- [Oracle FMW Infrastructure](/OracleFMWInfrastructure)
- [Oracle GoldenGate](/OracleGoldenGate)
- [Oracle HTTP Server](/OracleHTTPServer)
- [Oracle Identity Governance](/OracleIdentityGovernance)
- [Oracle Instant Client](/OracleInstantClient) (Basic, SDK and SQL*Plus)
- [Oracle Java](/OracleJava)
- [Oracle Rest Data Services](OracleRestDataServices) (ORDS)
- [Oracle SOA Suite](/OracleSOASuite)
- [Oracle Tuxedo](/OracleTuxedo)
- [Oracle Unified Directory](/OracleUnifiedDirectory)
- [Oracle Unified Directory Service Manager](/OracleUnifiedDirectorySM)
- [Oracle WebLogic Server](/OracleWebLogic)
- [Oracle WebCenter Content](/OracleWebCenterContent)
- [Oracle WebCenter Portal](/OracleWebCenterPortal)
- [Oracle WebCenter Sites](/OracleWebCenterSites)

### Oracle Sponsored Open Source Projects

- [GraalVM CE](https://github.com/graalvm/container/tree/master/community)
- [MySQL](https://github.com/mysql/mysql-docker)
- [Oracle OpenJDK](/OracleOpenJDK)
- [Oracle NoSQL Database](/NoSQL)
- [Oracle Linux](https://github.com/oracle/container-images)

### Community Contributions

- [Oracle Forms and Reports](https://github.com/oracle/docker-images/issues/212)
- [Oracle Unified Directory](Contrib/OracleUnifiedDirectory/)

### Archived Projects

- [ContainerCloud](/Archive/ContainerCloud)
- [Oracle Data Integrator](/Archive/OracleDataIntegrator)
- [Oracle Enterprise Data Quality](/Archive/OracleEDQ)
- [Oracle TSAM Plus](/Archive/OracleTuxedo/tsam)

## Pre-Built Images with Commercial Software

These sources already contain Oracle commercial software and require license
acceptance prior to download:

- [Oracle Container Registry](https://container-registry.oracle.com)

## Support

For support and certification information, please consult the documentation
for each product.

For support, bug reporting and feedback about the provided Dockerfiles, please
open an [issue on GitHub](https://github.com/oracle/docker-images/issues).

If you need general support with running containers on Oracle Linux, you can submit
a question under the [Containers and Orchestration](https://community.oracle.com/tech/apps-infra/categories/containers-and-orchestration)
category of the Applications and Infrastructure Community of Oracle Communities.

## Contributing

This project welcomes contributions from the community. Before submitting a pull request, please [review our contribution guide](./CONTRIBUTING.md)

## Security

Please consult the [security guide](./SECURITY.md) for our responsible security vulnerability disclosure process

## License

Copyright (c) 2019, 2023 Oracle and/or its affiliates.

Released under the Universal Permissive License v1.0 as shown at
<https://oss.oracle.com/licenses/upl/>.
