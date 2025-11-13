# n8n-main (主应用) 环境变量
当启用外部任务运行器时，n8n-main 需要以下环境变量：

1. 任务运行器基础配置：

+ N8N_RUNNERS_ENABLED=true - 启用任务运行器功能
+ N8N_RUNNERS_MODE=external - 设置运行器模式为外部模式
+ N8N_RUNNERS_AUTH_TOKEN - 运行器认证令牌，用于安全连接
+ N8N_RUNNERS_GRANT_TOKEN - 运行器授权令牌（可选但推荐）
+ N8N_RUNNERS_BROKER_LISTEN_ADDRESS=0.0.0.0 - 任务代理监听地址

2. 任务代理配置：

+	N8N_RUNNERS_PATH - 任务运行器连接的端点路径（默认: /runners）
+ N8N_RUNNERS_BROKER_PORT - 任务代理监听端口（默认: 5679）

3. 运行器性能配置：

+ N8N_RUNNERS_MAX_PAYLOAD - 最大载荷大小（默认: 1GB）
+ N8N_RUNNERS_MAX_CONCURRENCY - 最大并发任务数（默认: 10）
+ N8N_RUNNERS_TASK_TIMEOUT - 任务超时时间（默认: 300秒）
+ N8N_RUNNERS_MAX_OLD_SPACE_SIZE - Node.js最大内存限制

# Runner 环境变量
外部运行器需要以下环境变量来连接到 n8n-main：

1. 连接配置：

+ N8N_RUNNERS_TASK_BROKER_URI - 任务代理URI（例如: http://n8n:5679）
+ N8N_RUNNERS_AUTH_TOKEN - 与n8n-main相同的认证令牌
+ N8N_RUNNERS_GRANT_TOKEN - 授权令牌（如果配置了的话）

2. 运行器配置：
+ N8N_RUNNERS_MAX_PAYLOAD - 最大载荷大小
+ N8N_RUNNERS_MAX_CONCURRENCY - 最大并发任务数
+ N8N_RUNNERS_TASK_TIMEOUT - 任务超时时间
+ N8N_RUNNERS_AUTO_SHUTDOWN_TIMEOUT - 自动关闭超时时间
+ N8N_RUNNERS_GRACEFUL_SHUTDOWN_TIMEOUT - 优雅关闭超时时间

3. 安全配置：

+ N8N_RUNNERS_STDLIB_ALLOW - 允许的标准库列表
+ N8N_RUNNERS_EXTERNAL_ALLOW - 允许的外部模块列表
+ N8N_RUNNERS_BUILTINS_DENY - 禁止的内置函数列表
+ N8N_BLOCK_RUNNER_ENV_ACCESS - 是否阻止访问环境变量

4. 健康检查配置：

+ N8N_RUNNERS_HEALTH_CHECK_SERVER_ENABLED - 是否启用健康检查服务器
+ N8N_RUNNERS_HEALTH_CHECK_SERVER_HOST - 健康检查服务器主机
+ N8N_RUNNERS_HEALTH_CHECK_SERVER_PORT - 健康检查服务器端口

5. 日志配置：

+ N8N_RUNNERS_LAUNCHER_LOG_LEVEL - 日志级别
