
## 使用说明

APP_ID: 公众平台 appID

APP_SECRET: 公众平台 appSecret

TEMPLATE_ID: 模板 ID

USER_ID: 接收人的 OpenID 多个用换行分隔

BIRTHDAY: 倒数日（原生日），换行分隔，见更新说明。格式如 05-20，1999-11-04 这种

START_DATE: 正数日期，格式：2008-08-08

CITY: 城市，不要加市，准确到地级市。比如：北京、天津、广州、承德。

启用自己项目下的 Action！

ps. 有一些注意事项在此补充

1. 第一次登录微信公众平台测试号给的 app secret 是错误的，刷新一下页面即可
2. 生日的日期格式是：`05-20`，纪念日的格式是 `2022-08-09`，请注意区分。城市请写到地级市，比如：`北京`，`广州`，`承德`
3. 变量中粘贴的各种英文字符串不要有空格，不要有换行，除了模板之外都没有换行
4. Github Actions 的定时任务，在 workflow 的定义是 `0 0 * * *`，是 UTC 时间的零点，北京时间的八点。但是由于 Github 同一时间任务太多，因此会有延迟
5. 

示例模板：

今天是 {{ date.DATA }} {{ week_day.DATA }}

今天天气：{{ weather.DATA }}

湿度：{{ humidity.DATA }}

风向风力：{{ wind.DATA }}

空气指数：{{ air_data.DATA }}

空气质量：{{ air_quality.DATA }}

当前温度：{{ temperature.DATA }}

最低气温：{{ lowest.DATA }}

最高气温：{{ highest.DATA }}

我们已经相恋 {{ love_days.DATA }} 天啦

距离你的生日还有：{{ birthday_left.DATA }} 天

距离老子的生日还有：{{ birthday_left_1.DATA }} 天

距离墨子的生日还有：{{ birthday_left_2.DATA }} 天

距离韩非子的生日还有：{{ birthday_left_3.DATA }} 天

{{ words.DATA }}

## 代码使用
如果你有一个自己的服务器，或是不会关机的电脑，可以通过如下方式使用代码。本项目使用Python3。

注意：以下步骤面向具有一定编程基础的同学，需要了解git和Python的基本使用。如果你是纯小白，建议参考上面的[教程](#使用说明)通过Github Actions来使用本项目。如果仍想尝试通过代码方式运行，请先安装好git和Python3，git的安装教程可参考[这里](https://www.liaoxuefeng.com/wiki/896043488029600/896067074338496)，Python3的安装可参考[这里](https://www.liaoxuefeng.com/wiki/1016959663602400/1016959856222624)。

1. 首先clone本仓库：

```bash
git clone https://github.com/rxrw/daily_morning.git
```

2. 安装依赖：

```bash
cd daily_morning

pip3 install -r requirements.txt
```

3. 根据示例完成配置文件`config.yaml`。 `app_id`、 `app_secret`、 `user_ids` 和 `template_id` 的配置可参考[使用说明](#使用说明)

4. 运行代码`timer.py`，即可实现每日定时发送：

```bash
python3 timer.py
```

附：当然，如果你有多个女朋友，你可以在微信公众平台上为她们设置不同的模板，并且为每个人分别建立一个配置文件，例如：`xiaomei.yaml` 和`xiaohong.yaml`（注意在配置时千万不要写错了`user_ids`）。然后同时运行两个服务：
```bash
python3 timer.py --cfg xiaomei.yaml &

python3 timer.py --cfg xiaohong.yaml &
```
