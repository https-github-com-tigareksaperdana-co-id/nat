# NAT带宽包计费说明 {#concept_u2s_hvc_zdb .concept}

NAT带宽包是对公网IP资源的封装，一个NAT带宽包由一个或多个公网IP组成。因此，NAT带宽包的费用包括公网IP保有费和流量费。

## 计费方式 {#section_fxd_lvc_zdb .section}

NAT带宽包支持按量付费。计费周期和账单周期都为1小时。在一个计费周期内，如果您使用的时间不足1小时，按1小时收费。

## 计费项 {#section_frq_wwc_zdb .section}

NAT带宽包的费用包括IP保有费和流量费：

-   公网IP费用=单价 × IP个数 × 保有时长

-   流量费 = 流量单价 × 出方向使用流量累计值

    -   流量费只统计出方向（阿里云数据中心指向互联网）流量的累计值，入方向流量不参与计费。

    -   修改带宽上限并不会影响单价。建议您根据实际需求来设置带宽，以免因为程序错误或恶意访问导致产生大量计费流量。


下表是各地域的流量价格和IP占有费。

**说明：** 若下表中的价格与购买页面的价格不一致，请以购买页为准。

|地域|IP租用费单价（USD/个/时）|流量单价（USD/GB）|
|:-|:---------------|:-----------|
|华北1（青岛）|0.003|0.113|
|华东1（杭州）、华东2（上海）、华北2（北京）、华北3（张家口）、华南1（深圳）|0.003|0.125|
|香港|0.009|0.156|
|亚太（新加坡\)|0.125|0.081|
|美东（弗吉尼亚）|0.005|0.078|
|美西（硅谷）|0.005|0.078|
|日本|0.005|0.12|
|中东东部（迪拜）|0.009|0.447|
|亚太东南2（悉尼）|0.006|0.13|
|亚太东南3（吉隆坡）|0.112|0.13|
|欧洲中部（法兰克福）|0.006|0.07|

