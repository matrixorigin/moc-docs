# 连接器

MatrixOne Intellogence 平台提供了一个强大的数据连接器，允许用户轻松地将存储在阿里云 OSS 或 AWS S3 上的数据导入到 MatrixOne Intellogence 平台中。只需提供必要的连接信息，即可实现数据的无缝导入，为后续的数据分析和处理提供便利。

## 如何使用连接器

进入到 MatrixOne Intelligence 工作区，依次点击**数据接入**>**连接器**>**创建连接器**，选择需要连接的数据源类型。

<div align="center">
    <img src=https://community-shared-data-1308875761.cos.ap-beijing.myqcloud.com/artwork/mocdocs/data-connect/connect-4.png
 width=100% heigth=100%/>
</div>

### 连接 OSS

要将阿里云 OSS 上的文件导入到 MatrixOne Intellogence 平台，您需要提供以下连接信息：

- Endpoint: OSS 服务的访问地址。例如：`https://oss-cn-hangzhou.aliyuncs.com`。
- AccessKeyId: 您的阿里云账号的 AccessKey ID。
- AccessKeySecret: 您的阿里云账号的 AccessKey Secret。
- 文件路径：OSS 上文件的路径。例如：`bucket-name/path/to/your/file.csv`。

<div align="center">
    <img src=https://community-shared-data-1308875761.cos.ap-beijing.myqcloud.com/artwork/mocdocs/data-connect/connect-1.png
 width=60% heigth=60%/>
</div>

### 连接 S3

要将 AWS S3 上的文件导入到 MatrixOne Intellogence 平台，您需要提供以下连接信息：

- Endpoint: S3 服务的访问地址。例如：`https://s3.amazonaws.com`。
- AccessKeyId: 您的 AWS 账号的 AccessKey ID。
- AccessKeySecret: 您的 AWS 账号的 AccessKey Secret。
- 文件路径：S3 上文件的路径。例如：`bucket-name/path/to/your/file.csv`。
- 地区：S3 存储桶所在的地区。例如：us-east-1。

<div align="center">
    <img src=https://community-shared-data-1308875761.cos.ap-beijing.myqcloud.com/artwork/mocdocs/data-connect/connect-2.png
 width=60% heigth=60%/>
</div>
