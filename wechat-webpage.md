# 微信网页推广

## 项目简介

有意思的海报很容易在社交网络上传播。海报是用户接触这个项目的第一印象，海报需要精心社交，活泼、有意思、夺人眼球。才能促使用户常按海报，识别二维码开始答题。

在微信网页内，让用户回答婚恋观等一些问题，计算答题人和出题人的契合度，系统给 ta 推送一个与 ta 答案最一致的一个人的小程序名片的二维码，如果答题用户未注册小程序，引导答题者注册小程序。

## 需求

- 用户基本信息：openid、昵称和头像

  在微信网页中通过 [微信公众平台网页授权机制](https://developers.weixin.qq.com/doc/offiaccount/OA_Web_Apps/Wechat_webpage_authorization.html) 获取微信用户基本信息，需要后端与微信服务器通信获取用户信息。

  <img src="https://person-blog-1255441669.cos.ap-beijing.myqcloud.com/images/20200118102532.jpg" width = "100px" alt="图片" align=center />

  用户同意授权后，获取 code，前端传 code 到后端，后端使用 code 换取网页授权 access_token, 拉取用户基本信息，返回前端。

- 题库信息

  <img src="https://person-blog-1255441669.cos.ap-beijing.myqcloud.com/images/20200118111636.jpeg" width = "100px" alt="图片" align=center />

  题库为趣味性较强的单选题，题库由志愿者上传到数据库。一道题目应包含 id、题干和若干选项。

  用户从题库中选择若干道题目，设置好答案，生成海报，引导用户保存海报，分享。

- 海报生成

  海报中包含用户昵称、头像。

  海报图可以在 HTML5 canvas 中渲染背景图，文字，头像等信息，但是渲染后的 canvas 由于使用了远程服务器头像图片，由于 H5 安全设置，无法导出为图片，用户无法常按图片保存。（也有可能，我太水，不会弄 😅）。所以需要后端生成海报。

  <img src="https://person-blog-1255441669.cos.ap-beijing.myqcloud.com/images/20200118112208.JPG" width = "100px" alt="图片" align=center />

## 接口需求

- 用户信息：微信 openid、昵称、头像

  微信用户昵称和头像，前端引导用户打开 https://open.weixin.qq.com/connect/oauth2/authorize?appid=APPID&redirect_uri=REDIRECT_URI&response_type=code&scope=SCOPE&state=STATE#wechat_redirect ，用户同意授权后前端获得 code，前端使用 code 去后端获取用户 id、昵称和头像。

- 题目： id、题干、题目选项

- 用户答题数据：出题人 openid、答题人 openid、题目 id、出题人选择的选项、答题人选择的选项

- 契合度：答完题之后根据答题情况计算契合度。
