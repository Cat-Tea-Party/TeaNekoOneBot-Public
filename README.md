# teaNekoOneBot
## 1. 介绍
茶茶喵机器人。

从 OneBot11 协议获取 api 并进行解析。

## 2. 功能
| 功能   | 描述         | 完成 |
|------|------------|----|
| 签到   | 每日签到获取猫猫币  | ✅  |

## 3. 游戏
| 游戏                        | 描述                            | 完成 |
|---------------------------|-------------------------------|----|
| 骰子娘                       | 用输入 `/d` 投投骰子                 | ✅  |
| 真心话                       | 使用骰子作为基底，进行真心话的游戏             | ✅  |
| [猫猫帝国](docs/game/猫猫帝国.md) | 以基础品种猫咪作为底层打工猫, 建设猫猫帝国的放置挂机游戏 | 🚧 |


## 4. 原理
具体请看 [原理细节](docs/details.md)。

## 5. 使用
### 环境
| 环境  | 版本 |
|-----|----|
| JDK | 21 |

### 部署
1. 安装 gradle 和 JDK 21。
2. clone 本项目。
3. 在 src/main/resources/application.properties 中配置环境，例如数据库。具体配置请参考文档 [application 说明]()
4. 开启 Lagrange / LLOneBot 正向 websocket。监听端口一般设置为 8081。
5. `gradle build` 进行配置环境
6. `gradle bootrun` 运行项目

## 6. 贡献说明
### 代码规范
1. 

### 提交规范
使用 Git 提交代码，提交信息格式如下：
```
[类型] 描述
```
类型包括：'feat', 'fix', 'docs', 'style', 'refactor', 'test', 'chore'。

描述为本次提交的简要描述。

### 代码合并
1. Fork 本项目
2. 提交代码
3. 创建 Pull Request
4. 等待合并

## 7. 相关文档
- [OneBot 11协议](https://github.com/botuniverse/onebot-11/blob/master/api/public.md)
- [LLOneBot 项目](https://github.com/LLOneBot/LLOneBot)
- [LLOneBot 文档](https://llonebot.github.io/zh-CN/)
- [LLOneBot API](https://llonebot.apifox.cn/)
- [Lagrange 项目](https://github.com/LagrangeDev/Lagrange.Core/blob/master/README_zh.md)
- [Lagrange 文档](https://lagrangedev.github.io/Lagrange.Doc/)
- [Lagrange API](https://lagrange-onebot.apifox.cn/)