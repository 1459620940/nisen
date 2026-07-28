<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个人科技博客 | Tech Space</title>
    <script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft Yahei", sans-serif;
        }
        :root {
            --neon-blue: #00e5ff;
            --neon-purple: #9d00ff;
            --dark-bg: #050812;
            --card-bg: rgba(16, 22, 36, 0.7);
            --text-color: #e6edf7;
        }
        body {
            background-color: var(--dark-bg);
            color: var(--text-color);
            overflow-x: hidden;
        }
        /* 粒子背景容器 */
        #particles-js {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            z-index: 1;
        }
        .container-wrap {
            position: relative;
            z-index: 2;
        }
        /* 导航栏 */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 22px 8%;
            backdrop-filter: blur(8px);
            border-bottom: 1px solid rgba(0, 229, 255, 0.2);
            position: sticky;
            top: 0;
        }
        .logo {
            font-size: 26px;
            font-weight: bold;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
            -webkit-background-clip: text;
            color: transparent;
        }
        .nav-links a {
            color: var(--text-color);
            text-decoration: none;
            margin-left: 32px;
            font-size: 16px;
            transition: 0.3s;
        }
        .nav-links a:hover {
            color: var(--neon-blue);
            text-shadow: 0 0 8px var(--neon-blue);
        }
        /* 首页横幅 */
        .hero {
            min-height: 90vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
        }
        .hero h1 {
            font-size: 48px;
            margin-bottom: 16px;
        }
        .hero h1 span {
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
            -webkit-background-clip: text;
            color: transparent;
        }
        .hero-desc {
            max-width: 700px;
            font-size: 18px;
            opacity: 0.85;
            line-height: 1.8;
            margin-bottom: 36px;
        }
        .tag-group {
            display: flex;
            gap: 14px;
            flex-wrap: wrap;
            justify-content: center;
            margin-bottom: 40px;
        }
        .tag {
            border: 1px solid var(--neon-blue);
            padding: 7px 16px;
            border-radius: 30px;
            font-size: 14px;
            color: var(--neon-blue);
            transition: .3s;
        }
        .tag:hover {
            background: rgba(0, 229, 255, 0.15);
            box-shadow: 0 0 12px #00e5ff44;
        }
        .btn {
            padding: 14px 34px;
            border: none;
            border-radius: 4px;
            font-size: 17px;
            cursor: pointer;
            background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
            color: #000;
            font-weight: bold;
            text-decoration: none;
            transition: 0.3s;
        }
        .btn:hover {
            box-shadow: 0 0 24px #00e5ff80;
            transform: translateY(-3px);
        }
        /* 通用区块 */
        section {
            padding: 90px 8%;
        }
        .section-title {
            text-align: center;
            font-size: 34px;
            margin-bottom: 60px;
        }
        .section-title span {
            border-bottom: 3px solid var(--neon-blue);
            padding-bottom: 8px;
        }
        /* 项目卡片 */
        .project-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 28px;
        }
        .card {
            background: var(--card-bg);
            border: 1px solid rgba(0, 229, 255, 0.18);
            border-radius: 12px;
            padding: 28px;
            transition: 0.35s;
        }
        .card:hover {
            border-color: var(--neon-blue);
            box-shadow: 0 0 22px rgba(0, 229, 255, 0.18);
            transform: translateY(-6px);
        }
        .card h3 {
            font-size: 22px;
            margin-bottom: 12px;
            color: var(--neon-blue);
        }
        .card p {
            opacity: 0.8;
            line-height: 1.7;
        }
        /* 博客文章区域 */
        .article-item {
            background: var(--card-bg);
            border-left: 4px solid var(--neon-purple);
            padding: 22px 26px;
            margin-bottom: 20px;
            border-radius: 0 8px 8px 0;
            transition: .3s;
        }
        .article-item:hover {
            background: rgba(26, 34, 54, 0.85);
        }
        .article-item h4 {
            font-size: 20px;
            margin-bottom: 8px;
        }
        .article-item a {
            color: inherit;
            text-decoration: none;
        }
        /* 底部 */
        footer {
            text-align: center;
            padding: 40px;
            border-top: 1px solid rgba(0, 229, 255, 0.2);
            opacity: 0.7;
        }
        /* 滚动动画 */
        .fade-in {
            opacity: 0;
            transform: translateY(30px);
            transition: all 0.7s ease;
        }
        .fade-in.active {
            opacity: 1;
            transform: translateY(0);
        }
        /* 移动端适配 */
        @media(max-width:768px){
            .nav-links {
                display: none;
            }
            .hero h1 {
                font-size: 34px;
            }
        }
    </style>
</head>
<body>
    <div id="particles-js"></div>
    <div class="container-wrap">
        <!-- 导航 -->
        <nav>
            <div class="logo">TechBlog</div>
            <div class="nav-links">
                <a href="#home">首页</a>
                <a href="#about">关于我</a>
                <a href="#project">项目</a>
                <a href="#blog">博客文章</a>
                <a href="#contact">联系</a>
            </div>
        </nav>

        <!-- 首页横幅 -->
        <section id="home" class="hero">
            <h1>你好，我是 <span>技术创作者</span></h1>
            <p class="hero-desc">
                专注编程开发｜无人机航拍｜视频剪辑｜副业实战探索<br>
                分享代码、项目思路、创业思考、摄影航拍经验，持续沉淀，长期成长
            </p>
            <div class="tag-group">
                <span class="tag">Python开发</span>
                <span class="tag">HTML/前端</span>
                <span class="tag">无人机应用</span>
                <span class="tag">AI工具</span>
                <span class="tag">短视频剪辑</span>
                <span class="tag">副业思维</span>
            </div>
            <a href="#project" class="btn">查看我的项目</a>
        </section>

        <!-- 关于我 -->
        <section id="about">
            <h2 class="section-title"><span>关于我</span></h2>
            <div class="card fade-in">
                <p style="font-size:17px;line-height:2;">
                    持续探索技术落地，喜欢用最小成本验证想法，拒绝盲目投入。
                    掌握前端开发、Python脚本、无人机航拍、AE/剪映视频制作；
                    长期研究小程序开发、自动化工具、各类副业商业模式。
                    <br><br>
                    信奉：体力劳动效率有上限，脑力+长期热爱才能越做越强。
                    本博客用来记录学习笔记、踩坑经验、项目复盘、技术干货。
                </p>
            </div>
        </section>

        <!-- 项目展示 -->
        <section id="project">
            <h2 class="section-title"><span>实战项目</span></h2>
            <div class="project-grid">
                <div class="card fade-in">
                    <h3>成绩管理小程序</h3>
                    <p>教师/家长双端系统，支持Excel导入导出、成绩统计、薄弱学科分析、数据可视化图表。</p>
                </div>
                <div class="card fade-in">
                    <h3>航拍影像后期工具集</h3>
                    <p>批量图片处理、视频自动剪辑脚本，无人机航拍素材自动化工作流方案。</p>
                </div>
                <div class="card fade-in">
                    <h3>自动化办公脚本</h3>
                    <p>Python编写批量处理工具，PDF操作、文件整理、数据自动汇总，提升办公效率。</p>
                </div>
            </div>
        </section>

        <!-- 博客文章 -->
        <section id="blog">
            <h2 class="section-title"><span>技术随笔</span></h2>
            <div class="article-list">
                <div class="article-item fade-in">
                    <a href="#">
                        <h4>新手做项目一定要记住：最小成本验证想法</h4>
                        <p>不要为幻想买单，先验证需求，再投入大量时间资金，聊聊踩过的坑</p>
                    </a>
                </div>
                <div class="article-item fade-in">
                    <a href="#">
                        <h4>Python自动化入门思路，零基础快速上手</h4>
                        <p>不用精通语法，先学会写能解决自己痛点的小工具</p>
                    </a>
                </div>
                <div class="article-item fade-in">
                    <a href="#">
                        <h4>无人机航拍避坑指南：拍摄、合规、后期全总结</h4>
                        <p>飞行规范、构图技巧、素材存储与调色方案分享</p>
                    </a>
                </div>
            </div>
        </section>

        <!-- 联系区域 -->
        <section id="contact">
            <h2 class="section-title"><span>联系方式</span></h2>
            <div class="card fade-in" style="text-align:center;max-width:600px;margin:0 auto;">
                <p style="font-size:18px;">技术交流、项目合作、学习探讨欢迎留言</p>
                <br>
                <p>你可以自行添加微信/邮箱地址到这里</p>
            </div>
        </section>

        <footer>
            © 2026 TechBlog | 科技风个人博客 · All Rights Reserved
        </footer>
    </div>

    <script>
        // 粒子背景配置
        particlesJS("particles-js", {
            particles: {
                number: { value: 80 },
                color: { value: "#00e5ff" },
                shape: { type: "circle" },
                opacity: { value: 0.25, random: true },
                size: { value: 3, random: true },
                line_linked: {
                    enable: true,
                    distance: 130,
                    color: "#00e5ff",
                    opacity: 0.18,
                    width: 1
                },
                move: { enable: true, speed: 1.2 }
            },
            interactivity: {
                events: {
                    onhover: { enable: true, mode: "grab" },
                    onclick: { enable: true, mode: "push" }
                }
            },
            retina_detect: true
        });

        // 滚动渐入动画
        const fadeElements = document.querySelectorAll('.fade-in');
        function checkScroll() {
            fadeElements.forEach(el => {
                const rect = el.getBoundingClientRect();
                if(rect.top < window.innerHeight - 100){
                    el.classList.add('active');
                }
            })
        }
        window.addEventListener('scroll', checkScroll);
        checkScroll();

        // 平滑滚动
        document.querySelectorAll('a[href^="#"]').forEach(a=>{
            a.onclick = function(e){
                e.preventDefault();
                document.querySelector(this.getAttribute('href')).scrollIntoView({behavior:'smooth'})
            }
        })
    </script>
</body>
</html>
