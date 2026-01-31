# 架构原理文档说明 (咕咕咕)
## 一. 目录级别
架构的目录级别为：
```markdown
├── framework
│   ├── actuator   # 执行器模块。用于处理异步任务的执行与调度。
│   │   ├── subscription   # 订阅类。用于将一个异步 Supplier 包装一个 CompletableFuture 对象。可主动、间接提交结果。
│   │   ├── task           # 任务类。用于封装一个异步 Supplier，可定时、重复执行。
│   │   ├── task_stage     # 任务阶段类。用于在执行任务的 Supplier 前后插入额外的处理逻辑 （类似于 AOP ）。
│   │   └── timer          # 定时器类。用于定时执行一个任务。
│   │
│   ├── cache     # 缓存模块。用于处理定时清理的缓存逻辑。
│   │   ├── CacheService   # 缓存服务接口，用于处理缓存的定时清理逻辑。
│   │   └── Cache CDT      # 缓存数据结构实例。
│   │
│   ├── command   # 命令模块。用于解析、执行命令
│   │   ├── CommandArgumentProcessor      # 命令参数处理器接口。
│   │   ├── CommandExecutor               # 命令执行器接口。
│   │   ├── CommandDispatcher             # 命令调度器接口。
│   │   ├── CommandPermissionManager      # 命令权限管理器接口。
│   │   └── CommandScopeManager           # 命令作用域管理器接口。
│   │
│   ├── database  # 数据库模块。用于处理数据库连接与操作。
│   │   ├── base                # 基础数据库管理，包括将数据库任务异步化、事务化等。每个数据库都需要调用此模块。
│   │   ├── easy_data           # 用于在 namespace 获取一个 target 集合，每个 target 都有一个 key-value 的数据域。
│   │   ├── config_data         # 根据 key 注册一个配置数据。可以注册、注销、修改数据域。(基于 easy_data 实现)
│   │   │  ├── ConfigDataService                # 配置数据总服务接口，只需要调用此接口即可操作配置数据。
│   │   │  ├── ConfigDataGetService             # 配置数据获取服务接口，被 ConfigDataService 调用。
│   │   │  ├── ConfigDataRegisterService        # 配置数据注册服务接口，被 ConfigDataService 调用。
│   │   │  └── ConfigDataSetService             # 配置数据设置数据域服务接口，被 ConfigDataService 调用。
│   │   └── item_data           # 用于存储基于线程安全的可修改 amount:Integer 数据域的数据库。每个数据域除了 amount 外还可以存储一个可 JSON 化的 meta 数据。
│   │
│   ├── description  # 描述模块。用于处理描述信息的生成与格式化，例如 Command、Config 中的描述信息。
│   │   ├── @Description       # 描述注解，用于标记需要描述的信息。
│   │   └── @Hide              # 隐藏注解，用于标记不需要对用户显示的信息。
│   │
│   ├── event        # 事件模块。用于处理事件的发布与订阅，基于观察者模式实现。
│   │   ├── EventService       # 事件服务接口，用于推送事件并通知相关监听器。
│   │   ├── @EventListener     # 事件监听器注解，用于标记事件监听器方法。标记了才会处理相关 handler 方法。
│   │   └── @EventHandler      # 事件处理器注解，用于标记 listener 方法中的 handler 方法。需要在方法中将监听的事件作为参数。
│   │
│   ├── lifecycle    # 生命周期模块。用于处理组件的生命周期管理。
│   │   ├── ILivable         # 生命周期接口。明确死亡后将会被销毁、释放资源。
│   │   └── IPausable        # 可暂停接口。明确暂停后将会停止相关功能的运行，但不会被销毁、释放资源。
│   │   
│   ├── logger       # 日志模块。用于处理日志的记录与输出。
│   │
│   ├── plugin       # 插件模块。用于处理插件的加载与管理。
│   │
│   ├── response     # API 响应模块。用于异步订阅 api 并在获得响应后处理结果。
│   │
│   └── state        # 状态模块。用于处理游戏类型应用中的状态管理。
│
└── 
```

## 二. 使用说明
|          架构           | 用法                                                                                                                                                                             | api                                                                                                                                                   |
|:---------------------:|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| actuator.subscription | 1. 手动创建一个 SubscriptionTaskConfig<br>2. 如果是主动的，则直接返回 Result；否则用 SubscriptionDispatcher 提交 <br>3. 使用 SubscriptionDispatcher 订阅获取 CompletableFuture<br>4. 使用 Future 处理 Result<br> | 1. SubscriptionTaskConfig: 用于包装一个 Supplier<br>2. SubscriptionDispatcher: 将 SubscriptionTaskConfig 提交并返回 future<br>3. SubscriptionResult: future 提交的结果 |
|    actuator.timer     |                                                                                                                                                                                |                                                                                                                                                       |
|         cache         |                                                                                                                                                                                |                                                                                                                                                       |
|        command        |                                                                                                                                                                                |                                                                                                                                                       |
|       database        |                                                                                                                                                                                |                                                                                                                                                       |
|      description      |                                                                                                                                                                                |                                                                                                                                                       |
|         event         |                                                                                                                                                                                |                                                                                                                                                       |
|       lifecycle       |                                                                                                                                                                                |                                                                                                                                                       |
|        logger         |                                                                                                                                                                                |                                                                                                                                                       |
|        plugin         |                                                                                                                                                                                |                                                                                                                                                       |
|       response        |                                                                                                                                                                                |                                                                                                                                                       |
|         state         |                                                                                                                                                                                |                                                                                                                                                       | 

