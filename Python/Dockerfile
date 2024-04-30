# 使用多阶段构建
# 第一阶段：构建阶段
FROM python:3.11.9-slim-bullseye as builder

# 设置工作目录
WORKDIR /usr/src/app

# 安装依赖
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# 拷贝源代码到镜像
COPY . .

# 第二阶段：运行阶段
FROM python:3.11.9-slim-bullseye

# 创建非root用户
RUN useradd -m app
USER app

# 设置工作目录
WORKDIR /usr/src/app

# 从构建阶段拷贝已安装依赖和源码
COPY --from=builder /usr/src/app .

# 暴露端口
EXPOSE 8000

# 环境变量
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# 定义运行时命令
CMD ["python", "app.py"]
