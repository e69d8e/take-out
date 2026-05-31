# 苍穹外卖系统 (Sky Take Out)

一个基于 Spring Boot 的外卖点餐系统，包含管理端和用户端，支持微信小程序登录、菜品管理、订单处理、数据统计等功能。

## 🚀 技术栈

### 后端技术
- **核心框架**: Spring Boot 3.3.5
- **Java版本**: JDK 21
- **持久层**: MyBatis 3.0.3
- **数据库**: MySQL 8.0
- **缓存**: Redis
- **安全认证**: JWT (JSON Web Token)
- **文件存储**: 阿里云 OSS
- **支付集成**: 微信支付
- **实时通信**: WebSocket
- **API文档**: Knife4j (Swagger) 3.0.2
- **分页插件**: PageHelper 1.4.6
- **其他**: Lombok, FastJSON, AOP, Spring Cache

### 开发工具
- **构建工具**: Maven
- **IDE**: IntelliJ IDEA
- **版本控制**: Git

## 📁 项目结构

```
takeOut/
├── src/
│   ├── main/
│   │   ├── java/com/li/
│   │   │   ├── annotation/          # 自定义注解
│   │   │   ├── aspect/              # AOP切面
│   │   │   ├── common/              # 公共模块
│   │   │   │   ├── constant/        # 常量定义
│   │   │   │   ├── enumeration/     # 枚举类
│   │   │   │   ├── exception/       # 自定义异常
│   │   │   │   ├── json/            # JSON配置
│   │   │   │   ├── properties/      # 配置属性
│   │   │   │   ├── result/          # 返回结果封装
│   │   │   │   └── utils/           # 工具类
│   │   │   ├── config/              # 配置类
│   │   │   ├── controller/          # 控制器
│   │   │   │   ├── admin/           # 管理端接口
│   │   │   │   ├── user/            # 用户端接口
│   │   │   │   └── upload/          # 文件上传
│   │   │   ├── handler/             # 全局异常处理
│   │   │   ├── interceptor/         # 拦截器
│   │   │   ├── mapper/              # MyBatis Mapper接口
│   │   │   ├── pojo/                # 实体类
│   │   │   │   ├── dto/             # 数据传输对象
│   │   │   │   ├── entity/          # 数据库实体
│   │   │   │   └── vo/              # 视图对象
│   │   │   └── service/             # 业务逻辑层
│   │   │       └── impl/            # 服务实现类
│   │   └── resources/
│   │       ├── mapper/              # MyBatis XML映射文件
│   │       ├── application.yml      # 主配置文件
│   │       └── application-dev.yml  # 开发环境配置
│   └── test/                        # 测试代码
├── pom.xml                          # Maven配置
└── README.md                        # 项目说明
```

## ✨ 核心功能

### 管理端功能
1. **员工管理**
   - 员工登录/退出
   - 员工信息CRUD
   - 密码修改
   - 状态管理（启用/禁用）

2. **菜品管理**
   - 菜品分类管理
   - 菜品信息维护
   - 菜品口味管理
   - 菜品起售/停售
   - 批量删除

3. **套餐管理**
   - 套餐信息维护
   - 套餐菜品关联
   - 套餐起售/停售
   - 批量删除

4. **订单管理**
   - 订单查询与搜索
   - 订单状态管理（接单、拒单、派送、完成、取消）
   - 订单详情查看
   - 订单统计

5. **数据统计**
   - 今日运营数据
   - 营业额统计
   - 订单数量统计
   - 用户增长统计
   - 销量TOP10统计

6. **工作台**
   - 今日数据概览
   - 套餐总览
   - 菜品总览
   - 订单管理概览

### 用户端功能
1. **用户认证**
   - 微信小程序登录
   - JWT Token管理
   - 退出登录

2. **菜品浏览**
   - 菜品分类查看
   - 菜品详情
   - 套餐浏览

3. **购物车**
   - 添加商品
   - 修改数量
   - 清空购物车
   - 查看购物车列表

4. **订单管理**
   - 提交订单
   - 微信支付
   - 订单查询
   - 取消订单
   - 订单催单

5. **地址管理**
   - 收货地址CRUD
   - 默认地址设置

## 🛠️ 环境要求

- **JDK**: 21 或更高版本
- **Maven**: 3.6 或更高版本
- **MySQL**: 8.0 或更高版本
- **Redis**: 6.0 或更高版本
- **Node.js**: 16 或更高版本（用于前端）

## 📦 安装与运行

### 1. 克隆项目
```bash
git clone <repository-url>
cd take-out
```

### 2. 数据库配置
1. 创建数据库：
```sql
CREATE DATABASE sky_take_out DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

2. 导入数据库脚本（需要手动创建表结构）

3. 修改数据库配置：
编辑 `src/main/resources/application-dev.yml`，配置数据库连接信息：
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/sky_take_out?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8&useSSL=false&allowPublicKeyRetrieval=true
    username: your_username
    password: your_password
```

### 3. Redis配置
确保Redis服务已启动，配置Redis连接信息：
```yaml
spring:
  data:
    redis:
      host: localhost
      port: 6379
      password: your_redis_password
```

### 4. 第三方服务配置
配置以下服务（在环境变量或配置文件中）：

**阿里云OSS**（文件存储）：
```yaml
sky:
  alioss:
    access-key-id: your_access_key_id
    access-key-secret: your_access_key_secret
    bucket-name: your_bucket_name
    endpoint: your_endpoint
```

**微信小程序**（用户登录）：
```yaml
sky:
  wechat:
    app-id: your_app_id
    secret: your_secret
```

**JWT配置**：
```yaml
sky:
  jwt:
    admin-secret-key: your_admin_secret_key
    admin-token-name: adminToken
    admin-ttl: 8640000
    user-secret-key: your_user_secret_key
    user-token-name: token
    user-ttl: 8640000
```

### 5. 运行项目
```bash
# 进入项目目录
cd takeOut

# 使用Maven运行
mvn spring-boot:run

# 或者打包后运行
mvn clean package
java -jar target/takeOut-0.0.1-SNAPSHOT.jar
```

### 6. 访问应用
- **管理端API**: http://localhost:8080/admin/
- **用户端API**: http://localhost:8080/user/
- **API文档**: http://localhost:8080/doc.html (Knife4j)

## 📚 API接口说明

### 管理端接口 (`/admin/`)

#### 员工管理
- `POST /admin/employee/login` - 员工登录
- `GET /admin/employee/logout` - 员工退出
- `POST /admin/employee` - 新增员工
- `GET /admin/employee/page` - 分页查询员工
- `GET /admin/employee/{id}` - 根据ID查询员工
- `PUT /admin/employee/status/{status}` - 修改员工状态
- `PUT /admin/employee/password` - 修改密码
- `PUT /admin/employee` - 编辑员工信息

#### 菜品管理
- `POST /admin/dish` - 新增菜品
- `GET /admin/dish/{id}` - 根据ID查询菜品
- `GET /admin/dish/list/{categoryId}` - 根据分类查询菜品
- `GET /admin/dish/page` - 分页查询菜品
- `POST /admin/dish/status/{status}` - 菜品起售/停售
- `PUT /admin/dish` - 修改菜品
- `DELETE /admin/dish` - 批量删除菜品

#### 套餐管理
- `POST /admin/setmeal` - 新增套餐
- `GET /admin/setmeal/{id}` - 根据ID查询套餐
- `GET /admin/setmeal/page` - 分页查询套餐
- `POST /admin/setmeal/status/{status}` - 套餐起售/停售
- `PUT /admin/setmeal` - 修改套餐
- `DELETE /admin/setmeal` - 批量删除套餐

#### 订单管理
- `GET /admin/order/conditionSearch` - 订单搜索
- `GET /admin/order/details/{id}` - 订单详情
- `GET /admin/order/statistics` - 订单统计
- `PUT /admin/order/confirm` - 接单
- `PUT /admin/order/rejection` - 拒单
- `PUT /admin/order/delivery/{id}` - 派送订单
- `PUT /admin/order/cancel` - 取消订单
- `PUT /admin/order/complete/{id}` - 完成订单

#### 数据统计
- `GET /admin/report/turnoverStatistics` - 营业额统计
- `GET /admin/report/ordersStatistics` - 订单统计
- `GET /admin/report/userStatistics` - 用户统计
- `GET /admin/report/top10` - 销量TOP10

#### 工作台
- `GET /admin/workspace/businessData` - 今日运营数据
- `GET /admin/workspace/overviewSetmeals` - 套餐总览
- `GET /admin/workspace/overviewDishes` - 菜品总览
- `GET /admin/workspace/overviewOrders` - 订单管理数据

### 用户端接口 (`/user/`)

#### 用户认证
- `POST /user/user/login` - 微信登录
- `POST /user/user/logout` - 退出登录

#### 菜品浏览
- `GET /user/meal/list` - 菜品列表
- `GET /user/meal/{id}` - 菜品详情

#### 购物车
- `POST /user/shoppingCart/add` - 添加到购物车
- `GET /user/shoppingCart/list` - 查看购物车
- `POST /user/shoppingCart/sub` - 删除购物车商品
- `DELETE /user/shoppingCart/clean` - 清空购物车

#### 订单管理
- `POST /user/order/submit` - 提交订单
- `PUT /user/order/payment` - 订单支付
- `GET /user/order/orderDetail/{id}` - 订单详情
- `GET /user/order/historyOrders` - 历史订单
- `PUT /user/order/cancel` - 取消订单
- `GET /user/order/reminder/{id}` - 用户催单

#### 地址管理
- `POST /user/addressBook` - 新增地址
- `GET /user/addressBook/list` - 地址列表
- `GET /user/addressBook/{id}` - 地址详情
- `PUT /user/addressBook` - 修改地址
- `DELETE /user/addressBook/{id}` - 删除地址
- `PUT /user/addressBook/default` - 设置默认地址
- `GET /user/addressBook/default` - 获取默认地址

## 🔧 配置说明

### 环境变量配置
项目支持通过环境变量配置敏感信息，推荐使用以下方式：

1. **数据库密码**: `PASSWORD`
2. **Redis密码**: `PASSWORD`
3. **阿里云OSS**: `OSS_ACCESS_KEY_ID`, `OSS_ACCESS_KEY_SECRET`
4. **微信小程序**: `WECHAT_APP_ID`, `WECHAT_SECRET`

### 配置文件
- `application.yml` - 主配置文件
- `application-dev.yml` - 开发环境配置
- `application-prod.yml` - 生产环境配置（需创建）

## 🧪 测试

### 单元测试
```bash
mvn test
```

### API测试
使用Knife4j进行API测试：
1. 启动项目
2. 访问 http://localhost:8080/doc.html
3. 在线调试API接口

## 📝 开发规范

### 代码规范
- 遵循阿里巴巴Java开发手册
- 使用Lombok简化代码
- 统一异常处理
- 统一返回结果封装

### 数据库规范
- 表名使用下划线命名
- 字段名使用下划线命名
- 必须包含创建时间和更新时间字段
- 逻辑删除使用status字段

### API规范
- RESTful风格
- 统一响应格式
- 合理的HTTP状态码使用

## 🚨 注意事项

1. **安全性**
   - 生产环境必须修改默认密码
   - JWT密钥必须使用强密码
   - 敏感信息使用环境变量配置

2. **性能优化**
   - 启用Redis缓存
   - 合理使用数据库索引
   - 大数据量查询使用分页

3. **部署建议**
   - 使用Nginx反向代理
   - 配置HTTPS
   - 定期备份数据库
   - 监控系统日志

## 🤝 贡献指南

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 创建 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 📞 联系方式

- 项目维护者: [Your Name]
- 邮箱: [your-email@example.com]
- 项目链接: [项目仓库地址]

## 🙏 致谢

感谢所有为这个项目做出贡献的开发者！

---

**最后更新**: 2026年5月31日