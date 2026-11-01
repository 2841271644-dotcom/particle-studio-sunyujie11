# 粒子工坊 Particle Studio

一个无需构建步骤的静态网页原型。使用原生 HTML / CSS / JavaScript 和 Canvas 2D API，在浏览器本地运行。

## 本地预览

直接双击 `index.html`，或在目录中运行：

```bash
python3 -m http.server 8080
```

然后访问 `http://localhost:8080`。

## 部署到国内服务器

将整个目录中的 `index.html`、`style.css`、`app.js` 上传到网站根目录即可。无需 Node.js、数据库或第三方 CDN。

Nginx 示例：

```nginx
server {
    listen 80;
    server_name your-domain.example;
    root /var/www/particle-studio;
    index index.html;
    location / {
        try_files $uri $uri/ =404;
    }
    location ~* \.(js|css|png|jpg|webp|svg)$ {
        expires 7d;
        add_header Cache-Control "public";
    }
}
```

生产环境建议配置 HTTPS。中国大陆服务器通常还需要按服务商要求完成 ICP 备案。

## 当前版本功能

- 2D / 2.5D 景深模拟粒子
- 点、圆形、线性、锥形、球体发射形状
- 数量、速率、生命周期、随机、速度、重力、风力、旋转、湍流
- 颜色、尺寸、透明度、五种内置粒子形状
- 本地 PNG / WebP / JPG 自定义贴图
- 生命周期大小和透明度变化
- 十二组预设（新增粒子炸开、持续上升、飘落、喷射、环绕、扩散）
- Loop 循环播放开关，可按动画时长重复播放效果
- JSON 项目保存 / 导入（包含循环设置）
- WebM 录制、PNG 静帧和 PNG 序列帧下载

## V1.2 更新

- 新增 Loop 循环播放按钮，开启后按导出时长设置重复播放粒子效果。
- 新增六种常用预设：粒子炸开、粒子上升、粒子飘落、粒子喷射、粒子环绕、粒子扩散。
- 预设支持继续调整发射、运动、外观和生命周期参数。

## 已知限制

- 当前 2.5D 是 Canvas 上的景深与 Z 轴模拟，不是完整 3D 粒子引擎或 GPU 粒子系统。
- WebM 透明通道受浏览器 MediaRecorder 编码器支持情况影响。
- PNG 序列帧当前按帧下载，建议允许浏览器多文件下载；正式产品建议改为 ZIP 打包。
- GIF 和 MP4 编码暂未内置，正式上线时可集成经过本地化部署的编码器，避免依赖境外 CDN。
- 当前为单机本地项目，没有账号系统、云端项目保存或协作功能。


## V1.2 新增运动预设

在保留原有 12 个预设的基础上，新增 6 个仅调整运动参数的预设：空间随机漂浮、中心爆发扩散、缓慢向上漂浮、花瓣自由飘落、星点聚集游动、爱心缓慢漂浮。新增预设不覆盖用户当前的颜色、大小、透明度、形状、贴图和生命周期外观设置。
