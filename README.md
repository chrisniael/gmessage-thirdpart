# gmessage-thirdpart
即信手机端第三方工具


* [自动上报健康状态](#自动上报健康状态) : [report-health.sh](./report-health.sh)
* ...

## 自动上报健康状态

修改 [report-health.sh](./report-health.sh) 脚本文件顶部的若干个参数配置

* 登陆信息

    ```bash
    # 账号 + 密码登陆
    user=""
    passwd=""

    # sid + key 登陆
    login_response_sid=""
    login_response_key=""
    ```


    这里可以使用两种方式登陆，二选一：

    * 账号 + 密码

        账号为域账号全称，但不带域，例如：shenyu.tommy，反馈好像部分员工的账号没有权限用账号密码登陆，只能使用手机短信验证身份的方式登陆，这样的用户只能使用 sid + key 的方式，也推荐下面这种方式，还有就是使用账号密码的方式登陆还会导致手机 App 端登陆退出（即信只允许同时使用一个 key 来操作，新登陆会生成新的 key）

    * sid + key

        推荐使用这个方式，能保持手机端 App 登陆状态不失效，唯一麻烦的地方是，得手动去抓取一下账号对应的 sid 和 key 的值。抓取手机 App HTTP(S) 包的方法请自行 Google，Mac 上推荐使用 ProxyMac。

        使用账号密码登陆，则 sid 和 key 的值在下面这个请求的 response 里：

        ```HTTP
        GET /WFM/SecretVerify.aspx?... HTTP/1.1
        Host: mwf.corp.sdo.com
        ```
 
        使用手机验证码登陆，则 sid 和 key 的值在哪个请求的 response 里还没有跑，待补充...

* 健康信息

    ```bash
    # 健康信息
    liveInCity="上海市-上海市-浦东新区"  # 您现在居住的城市
    todayIsWork=1  # 您今日是否办公，1：是，0：否
    workPlace="家里"  # 您今日的办公地点，可选值：公司，家里，其他
    currentLocalCity="上海市-上海市-浦东新区"  # 您现在的办公城市
    isContact="均无以上五种情况"  # 您是否存在以下情况
    healthStatus="良好"  # 您的今日健康状况
    isOutGuonian=1  # 春节期间是否离沪
    leaveShanggaiTime="2020-01-23 00:00:00" # 离沪日期
    fromLocation="江苏省-南通市"  # 您从哪里返沪
    comebackTime="2020-2-5"  # 返沪日期
    way="自驾"  # 返沪方式
    comebackPassCity="南通"  # 中途停留城市
    livingStyle="合租"  # 您现在的居住方式
    detailLivingAddr="上海"  # 您所在工作城市的居住地址
    familyCotenancyType="均无以上四种情况"  # 您的家庭成员/合租人是否存在以下情况？如本人居住，则选择均无以上四种情况
    familyCotenancyIsGeli="是"  # 您的家庭成员/合租人员是否处于自我隔离期？如本人居住，择选否
    familyCotenancyGeliEndTime="2020-2-20"  # 您的家庭成员/合租人员隔离期何时结束？
    commutingMode="自驾(汽车/自行车/电瓶车)"  # 您日常的通勤方式
    oneCommutingTime="30分钟内"  # 您日程的单程通勤时间

    ```
