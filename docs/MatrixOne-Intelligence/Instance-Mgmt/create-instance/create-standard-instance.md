# 创建实例

本篇文档将为您提供注册并创建标准实例的详细步骤。

## 步骤一：登录账号，开始创建

1. 登录您的 MO Intelligence 账号，进入实例管理平台。

    如果您还没有 MO Intelligence 账号，您可以点击[注册登录](https://www.matrixorigin.cn/moi-signup)开始注册，或者参照[快速体验 MatrixOne Intelligence](../../Get-Started/quickstart.md) 的注册指南。

2. 在菜单栏中点击**实例**进入实例列表页面，然后点击 **+创建实例**。

## 步骤二：选择实例

MO Intelligence 提供了两种实例类型：可自动扩缩容的 Serverless 实例和拥有独立稳定的计算资源的标准实例。在此选择**标准实例**。

## 步骤三：选择公有云服务商及地区

MO Intelligence 支持在阿里云创建标准实例。

| 地理区域    | 地区名 | 地点 |
| ----------- | ------ | ---- |
| 亚太 - 中国 | 华东 1 | 杭州 |

## 步骤四：配置实例容量

- 节点规格

目前 MO Intelligence 支持节点规格为：8 核 32GiB 和 16 核 64GiB，节点数范围为 1-10。您可根据业务需要来选择合适的节点规格。

- 存储

MO Intelligence 存储为**按量付费**，根据实际使用量按小时计费。

## 步骤五：选择付费方式

对于计算资源，MO Intelligence 提供了包年包月和按量付费两种付费方式。

- 包年包月

您可以根据需要选择合适的时长，在时长上方会有相应的折扣显示，剩余天数会显示在实例卡片右上侧，到期时间为周期后的下一日的 00:00:00，即当剩余天数显示为 0 时代表实例将在次日 00:00:00 到期。实例到期前可进行手动续费，但为了确保服务的连续性，避免因忘记续费而导致服务中断，我们推荐您开启**自动续费**，您可在购买时长下方开启到期自动续费的按钮，续费周期与您当前选择的时长一致，平台将在实例到期前 9 天发起自动扣款，届时请确保账户余额充足。对于已创建实例，您也可以在实例卡片下方点击续费按钮进行续费操作，自动续费开启后可随时取消。具体付款方式请查看下方的**步骤七**。

- 按量付费

按量付费先使用后收费，平台会每小时对前一小时的消费情况进行扣费。

## 步骤六：设置访问控制

### 管理员密码

在创建 MO Intelligence 实例时，您需要设置实例的最高权限管理员（admin）的密码。为了保障数据库的安全性，密码需符合以下规则：

- 至少包含 8 个字符
- 必须包含至少一个数字
- 必须包含至少一个大写字母
- 必须包含至少一个小写字母

### 网络策略

MatrixOne Intelligence 设置了两种网络安全策略

- 允许所有公网 IP 访问  
默认设置为**允许所有公网 IP 访问**
- 允许指定的 IP 访问  
建议设置为**允许指定的 IP 访问**，详情请参考[设置 IP 白名单](../../Security/IP-Access.md)章节。  
- 修改网络策略  
在控制台中，选择并点击进入你想要修改的数据库实例，点击进入**网络策略 > 编辑**，在弹框中可切换两种网络策略

## 步骤七：命名并创建实例

1. 系统将自动为实例分配一个名称，您也可以自定义名称，或者在实例创建完毕后点击实例图标进入概览页面修改实例名称。
2. 在右侧的概览中，您可以查看上述步骤中的实例规划。确认无误后，点击右侧的确认按钮。
3. 如果上述选择的付费方式为包年包月，相应款项会在创建实例时扣除，在支付页面会显示您实例配置的详情和付费方式。我们默认优先扣除代金券余额，代金券不足部分由现金补齐。您也可以选择自定义组合付费方式，但对于自动续费的金额不支持自定义组合付款方式。届时请确保您的账户有充足的余额，否则将无法进行下一步。
4. 实例将在点击创建后的几秒内完成创建。您可以通过监视实例卡片中的实例状态来确认是否创建成功。创建中状态为**创建中**，创建完成状态为**可用**。

!!! note
    除创建实例页面显示的费用外，存储空间费用、以及使用 SQL 造成的对象存储数据请求费用和公网流量费用会每小时按实际用量扣费。详情请参考[价格明细](../../Charging/price-detail/price-detail-standard.md)。

## 步骤八：获取 MO 实例的连接命令

在 MO Intelligence 实例管理平台的实例列表中，找到需要访问的 MatrixOne 实例，依次点击**连接 > 通过第三方工具连接**。

此时页面右侧弹出连接实例的命令窗口，SQL Client 下方选择客户端，复制下方的命令即可。

希望这些步骤有助于您成功创建 MatrixOne 实例！如果您需要更多帮助，请继续查看我们的文档或联系支持团队。
