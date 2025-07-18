# 教务管理系统

一个基于Flask的完整教务管理系统，支持学生、教师和管理员三种角色，提供选课、成绩管理、课表查询等功能。

## 功能特色

### 学生功能
- 🎓 课程选择和退课
- 📅 个人课表查看
- 📊 成绩查询和GPA统计
- 🎯 培养计划查看
- 📝 课程评价

### 教师功能
- 📚 授课管理
- 👥 班级名单查看
- ✏️ 成绩录入
- 📈 教学统计
- 📋 学生表现跟踪

### 管理员功能
- 👨‍🎓 学生信息管理
- 👨‍🏫 教师信息管理
- 📖 课程和专业管理
- 🏢 教学资源管理
- 📊 统计报表

### 系统特性
- 🔍 全局智能搜索
- 📱 响应式设计
- 🔐 角色权限控制
- 🌐 多语言支持（中文）
- 📈 实时数据统计

## 技术栈

- **后端**: Flask, Flask-Login, Flask-SQLAlchemy
- **前端**: HTML5, CSS3, JavaScript (原生)
- **数据库**: PostgreSQL / GaussDB
- **样式**: 自定义CSS（现代化设计）

## 安装说明

### 1. 环境要求

- Python 3.8+
- PostgreSQL 12+ 或 GaussDB
- pip 包管理器

### 2. 克隆项目

```bash
git clone <repository-url>
cd DataBase
```

### 3. 安装依赖

```bash
pip install -r requirements.txt
```

### 4. 数据库配置

1. 创建PostgreSQL数据库：
```sql
CREATE DATABASE liyh_university_db;
```

2. 执行数据库初始化脚本：
```bash
psql -d liyh_university_db -f university_db_setup.sql
```

3. 配置数据库连接，编辑 `src/database.py` 文件中的数据库连接参数：
```python
DATABASE_CONFIG = {
    'host': 'localhost',
    'port': 5432,
    'database': 'liyh_university_db',
    'user': 'your_username',
    'password': 'your_password'
}
```

### 5. 运行应用

```bash
python run.py
```

应用将在 `http://localhost:5000` 启动。

## 使用说明

### 登录账号

系统支持三种角色的用户：

1. **学生账号**：使用学号作为用户名（如：2023001）
2. **教师账号**：使用工号作为用户名（如：T001）
3. **管理员账号**：使用管理员ID作为用户名（如：A001）

> 注：演示版本中，所有账号的密码可以是任意值

### 主要功能模块

#### 学生端
- 访问 `/course_selection` 进行选课
- 访问 `/timetable` 查看课表
- 访问 `/grade_report` 查看成绩
- 访问 `/search` 使用全局搜索

#### 教师端
- 访问 `/my_teaching` 查看授课信息
- 访问 `/grade_input` 录入成绩
- 访问 `/class_roster` 查看班级名单

#### 管理员端
- 访问 `/manage_students` 管理学生信息
- 访问 `/manage_courses` 管理课程信息
- 访问 `/system_settings` 进行系统设置

## 项目结构

```
DataBase/
├── src/                    # 源代码目录
│   ├── __init__.py        # Flask应用工厂
│   ├── main.py            # 主要路由
│   ├── auth.py            # 认证模块
│   ├── models.py          # 数据模型
│   ├── database.py        # 数据库连接
│   ├── static/            # 静态文件
│   │   ├── css/          # 样式文件
│   │   └── js/           # JavaScript文件
│   └── templates/         # HTML模板
│       ├── base.html      # 基础模板
│       ├── dashboard.html # 仪表盘
│       ├── login.html     # 登录页面
│       ├── search.html    # 搜索页面
│       ├── student/       # 学生页面
│       ├── instructor/    # 教师页面
│       └── admin/         # 管理员页面
├── run.py                 # 应用启动文件
├── university_db_setup.sql # 数据库初始化脚本
└── README.md             # 说明文档
```

## 数据库设计

系统使用标准化的数据库设计，包含以下主要表：

- **Liyh_Student**: 学生信息表
- **Liyh_Instructor**: 教师信息表
- **Liyh_Course**: 课程信息表
- **Liyh_Section**: 教学班表
- **Liyh_Takes**: 选课记录表
- **Liyh_Teaches**: 授课记录表
- **Liyh_Major**: 专业信息表
- **Liyh_Department**: 院系信息表

详细的数据库结构请参考 `university_db_setup.sql` 文件。

## API接口

系统提供RESTful API接口：

### 学生相关
- `GET /api/student/stats` - 获取学生统计数据
- `GET /api/student/my_courses` - 获取学生选课信息
- `POST /api/student/enroll` - 学生选课
- `POST /api/student/withdraw` - 学生退课

### 搜索相关
- `GET /api/search` - 全局搜索
- `GET /api/popular_terms` - 热门搜索词

### 管理员相关
- `GET /api/admin/students` - 获取学生列表
- `POST /api/admin/students` - 添加学生
- `PUT /api/admin/students/{id}` - 更新学生信息
- `DELETE /api/admin/students/{id}` - 删除学生

## 开发说明

### 添加新功能

1. 在 `src/main.py` 中添加新的路由
2. 在 `src/templates/` 中创建对应的HTML模板
3. 在 `src/static/` 中添加必要的CSS和JavaScript
4. 更新数据库模型（如需要）

### 样式定制

系统使用自定义CSS，主要样式文件位于 `src/static/css/`。可以通过修改CSS变量来快速定制主题色彩。

### 数据库扩展

如需添加新的数据表或字段，请：

1. 更新 `university_db_setup.sql` 脚本
2. 在 `src/database.py` 中添加相应的查询函数
3. 更新相关的API接口

## 部署说明

### 生产环境部署

1. 使用 `gunicorn` 作为WSGI服务器：
```bash
pip install gunicorn
gunicorn -w 4 -b 0.0.0.0:5000 run:app
```

2. 配置反向代理（如Nginx）
3. 设置环境变量：
```bash
export FLASK_ENV=production
export DATABASE_URL=postgresql://user:password@localhost/dbname
```

### Docker部署

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["gunicorn", "-w", "4", "-b", "0.0.0.0:5000", "run:app"]
```

## 贡献指南

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 许可证

本项目采用 MIT 许可证。详情请参阅 `LICENSE` 文件。

## 联系方式

如有问题或建议，请通过以下方式联系：

- 项目Issues: [GitHub Issues](https://github.com/your-repo/issues)
- 邮箱: your-email@example.com

## 更新日志

### v1.0.0 (2024-01-XX)
- 初始版本发布
- 完整的学生、教师、管理员功能
- 全局搜索功能
- 响应式设计

---

感谢使用教务管理系统！🎓 