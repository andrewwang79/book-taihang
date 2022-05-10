# 功能

## 配置界面访问
1. Broker配置界面，依托锐影现有配置管理的用户管理功能，并不需要独立访问入口

## 租户
1. 一个租户对应于多个系统，用于管理对应于多个院区的集成
1. 一次集成（一家医院）能够对应多个租户，即能够同时与多个院区进行集成
1. 添加租户：租户名（不可重复），租户编码（必须全局唯一，自动生成），租户备注
1. 修改租户：租户名，租户备注
1. 不能删除租户
1. 能够禁用租户
1. 一个租户最多对应一个检查信息获取端/一个影像获取端

## 系统
1. 一个系统最多对应于一个检查信息获取端和一个影像获取端
1. 一个租户能够对应多个系统，即能够同时与多个第三方系统进行集成。多科室/多系统场景
1. 系统连接配置参数：查询频率，启动查询时间，查询条件（Study_Instance_UID）
1. 查询参数：Modality，Body_Part，Study_Datetime，Study_Characteristics

## 检查信息获取端
1. 一个系统最多对应一个检查信息获取端
1. 一个检查信息获取端最多对应一种集成方式（DB或者Webservice或者插件）
1. 以下三种方式可以添加/修改/删除
    1. DB集成方式
        1. 一个检查信息获取端最多对应一个DB实体（即一种DB品牌）
        1. 默认支持的DB品牌类型可选择/修改，不可删除
        1. DB连接串可修改
        1. DB连接可测试
    1. Webservice方式（接收或者请求）
        1. 一个检查信息获取端最多对应一种Webservice
        1. 接收型的Webserice，可以配置本地IP/Port，提交表单参数
        1. 表单参数可以添加/修改/删除
        1. 能够测试Webservice启动/连接/接收
        1. 请求型的Webservice，可以配置对方IP/Port，请求参数
        1. 请求参数可以添加/修改/删除
        1. 能够测试Webservice连接/请求
    1. 外挂插件方式
        1. 当上述两种方式均不支持的集成场场景下，采用外挂插件的方式
        1. 集成插件方式下，可以对插件调用进行测试
1. 获取的检查信息，能够进行映射操作
    * DB集成方式下，数据表字段的名能够做映射
    ```
    Accession_Number 检查编号
    Modality 设备类型
    Study_Characteristics 检查方法
    Body_Part 检查部位
    Study_Datetime 检查时间
    Study_Status 检查状态
    Study_Instance_UID 检查唯一编号
    Patient_ID 患者编号
    Patient_Name 患者姓名
    Patient_Name_Other 患者姓名（其他）
    Patient_Age 患者年龄
    Patient_Birthdate 患者生日
    Paitent_Sex 患者性别
    Report_Dateime 报告日期
    Report_Finding 检查所见
    Report_Diagnose 检查结论
    Positive 阴阳性
    ```
    * 所有集成方式下，数据字段的值能够做映射
    ```
    Modality（设备类型）：DR，CT，MRI，MG，US，SC，SR，RF，OT
    Study_Characteristics(检查方法）：CTE，CTA
    Body_Part（检查部位）：Lung，Chest，Pelvis，Hip Joint，Head，Orbits，Inner，Sella，Sinus，Nasopharynx，Parotid，Larynx，等
    Patient_Sex（患者性别）：M，F，O
    ```

## 影像获取端
1. 一个系统最多对应一个影像获取端
1. 一个影像获取端最多对应一种集成方式（DICOM Q/R，DICOM SCP，Webservice，FTP，445共享文件）

| 集成方式 | 说明 | 可以配置 |
| :-: | - | - |
| DICOM Q/R | 选择此种集成方式时，检查信息获取端必须已经被配置，否则无法获取检查信息 | 本地AE Title，IP Address，Port <br> 对方AE Title，IP Address，Port |
| DICOM SCP |  | 本地AE Title，IP Address，Port |
| Webservice | 请求型Webservice | 对方IP/Port，请求参数，连接用户名/密码 <br> 请求参数的拼装/解析，能够通过script插件形式完成 |
| FTP（下载/上传） |  | 对方IP/Port，连接用户名/密码 <br> 请求参数的拼装/解析，能够通过script插件形式完成 |
| 445共享文件夹 |  | 可以配置对方IP，连接用户名/密码 <br> 请求参数的拼装/解析，能够通过script插件形式完成 |
