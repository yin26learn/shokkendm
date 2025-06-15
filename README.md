<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>右下角浮動目錄示例</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .main-content {
            max-width: 800px;
            margin: 0 auto;
            padding: 40px 20px;
            background: rgba(255, 255, 255, 0.95);
            margin-top: 20px;
            margin-bottom: 20px;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
        }

        h1, h2, h3 {
            margin: 30px 0 20px 0;
            color: #2c3e50;
        }

        h1 {
            font-size: 2.5em;
            text-align: center;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        h2 {
            font-size: 2em;
            border-left: 4px solid #667eea;
            padding-left: 15px;
        }

        h3 {
            font-size: 1.5em;
            color: #34495e;
        }

        p {
            margin-bottom: 15px;
            text-align: justify;
        }

        /* 浮動目錄樣式 */
        .floating-toc {
            position: fixed;
            bottom: 30px;
            right: 30px;
            width: 60px;
            height: 60px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: 1000;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow: hidden;
        }

        .floating-toc:hover {
            transform: scale(1.1);
            box-shadow: 0 15px 40px rgba(102, 126, 234, 0.4);
        }

        .toc-icon {
            width: 24px;
            height: 24px;
            fill: white;
            transition: transform 0.3s ease;
        }

        .floating-toc.expanded .toc-icon {
            transform: rotate(180deg);
        }

        .toc-menu {
            position: absolute;
            bottom: 80px;
            right: 0;
            min-width: 300px;
            max-height: 400px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.2);
            opacity: 0;
            visibility: hidden;
            transform: translateY(20px) scale(0.9);
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            overflow-y: auto;
        }

        .floating-toc.expanded .toc-menu {
            opacity: 1;
            visibility: visible;
            transform: translateY(0) scale(1);
        }

        .toc-title {
            font-size: 1.2em;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 15px;
            text-align: center;
            border-bottom: 2px solid #667eea;
            padding-bottom: 10px;
        }

        .toc-list {
            list-style: none;
        }

        .toc-item {
            margin-bottom: 8px;
        }

        .toc-link {
            display: block;
            color: #555;
            text-decoration: none;
            padding: 8px 12px;
            border-radius: 8px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .toc-link::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(102, 126, 234, 0.1), transparent);
            transition: left 0.5s ease;
        }

        .toc-link:hover {
            color: #667eea;
            background: rgba(102, 126, 234, 0.1);
            transform: translateX(5px);
        }

        .toc-link:hover::before {
            left: 100%;
        }

        .toc-link.active {
            color: #667eea;
            background: rgba(102, 126, 234, 0.15);
            font-weight: bold;
        }

        .toc-h2 {
            font-weight: bold;
            border-left: 3px solid #667eea;
            padding-left: 15px;
        }

        .toc-h3 {
            padding-left: 30px;
            font-size: 0.9em;
            color: #666;
        }

        /* 自定義滾動條 */
        .toc-menu::-webkit-scrollbar {
            width: 6px;
        }

        .toc-menu::-webkit-scrollbar-track {
            background: rgba(0, 0, 0, 0.1);
            border-radius: 3px;
        }

        .toc-menu::-webkit-scrollbar-thumb {
            background: linear-gradient(45deg, #667eea, #764ba2);
            border-radius: 3px;
        }

        /* 響應式設計 */
        @media (max-width: 768px) {
            .floating-toc {
                bottom: 20px;
                right: 20px;
                width: 50px;
                height: 50px;
            }

            .toc-menu {
                min-width: 280px;
                max-width: calc(100vw - 40px);
            }
        }

        /* 平滑滾動 */
        html {
            scroll-behavior: smooth;
        }
    </style>
</head>
<body>
    <!-- 主要內容 -->
    <div class="main-content">
        <h1 id="title">網頁右下角目錄示例</h1>
        
        <h2 id="section1">第一章：簡介</h2>
        <p>這是一個展示右下角浮動目錄功能的示例頁面。目錄會自動檢測頁面中的標題，並提供快速導航功能。</p>
        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</p>
        
        <h3 id="subsection1-1">1.1 功能特色</h3>
        <p>這個目錄具有現代化的設計，包含漸變背景、毛玻璃效果、平滑動畫等視覺特效。</p>
        <p>Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        
        <h3 id="subsection1-2">1.2 使用方法</h3>
        <p>點擊右下角的圓形按鈕即可展開目錄，再次點擊可收合。點擊目錄項目可快速跳轉到對應章節。</p>
        
        <h2 id="section2">第二章：技術實現</h2>
        <p>這個目錄使用純 HTML、CSS 和 JavaScript 實現，具有良好的響應式設計和用戶體驗。</p>
        <p>Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo.</p>
        
        <h3 id="subsection2-1">2.1 CSS 動畫</h3>
        <p>使用 CSS3 的 transform 和 transition 屬性實現平滑的展開收合動畫。</p>
        <p>Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt.</p>
        
        <h3 id="subsection2-2">2.2 JavaScript 互動</h3>
        <p>JavaScript 負責處理點擊事件、滾動監聽和活動項目的高亮顯示。</p>
        <p>Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem.</p>
        
        <h2 id="section3">第三章：自定義選項</h2>
        <p>您可以根據需要調整目錄的樣式、位置和行為。</p>
        <p>Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur?</p>
        
        <h3 id="subsection3-1">3.1 樣式自定義</h3>
        <p>可以修改 CSS 變數來改變顏色、大小、動畫效果等。</p>
        
        <h3 id="subsection3-2">3.2 功能擴展</h3>
        <p>可以添加更多功能，如進度指示器、書籤功能等。</p>
        
        <h2 id="section4">第四章：總結</h2>
        <p>這個右下角浮動目錄提供了優秀的用戶體驗，適合用於長篇文檔或部落格文章。</p>
        <p>Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur?</p>
    </div>

    <!-- 浮動目錄 -->
    <div class="floating-toc" id="floatingToc">
        <svg class="toc-icon" viewBox="0 0 24 24">
            <path d="M3,9H17V7H3V9M3,13H17V11H3V13M3,17H17V15H3V17M19,17H21V15H19V17M19,7V9H21V7H19M19,13H21V11H19V13Z"/>
        </svg>
        
        <div class="toc-menu" id="tocMenu">
            <div class="toc-title">目錄</div>
            <ul class="toc-list" id="tocList">
                <!-- 目錄項目將由 JavaScript 動態生成 -->
            </ul>
        </div>
    </div>

    <script>
        class FloatingTOC {
            constructor() {
                this.tocButton = document.getElementById('floatingToc');
                this.tocList = document.getElementById('tocList');
                this.isExpanded = false;
                this.headings = [];
                this.activeHeading = null;
                
                this.init();
            }
            
            init() {
                this.generateTOC();
                this.bindEvents();
                this.observeHeadings();
            }
            
            generateTOC() {
                // 查找所有標題元素
                const headings = document.querySelectorAll('h1, h2, h3, h4, h5, h6');
                this.headings = Array.from(headings);
                
                // 清空現有目錄
                this.tocList.innerHTML = '';
                
                // 生成目錄項目
                this.headings.forEach((heading, index) => {
                    // 為沒有 ID 的標題生成 ID
                    if (!heading.id) {
                        heading.id = `heading-${index}`;
                    }
                    
                    const li = document.createElement('li');
                    li.className = 'toc-item';
                    
                    const a = document.createElement('a');
                    a.href = `#${heading.id}`;
                    a.textContent = heading.textContent;
                    a.className = `toc-link toc-${heading.tagName.toLowerCase()}`;
                    
                    // 添加點擊事件
                    a.addEventListener('click', (e) => {
                        e.preventDefault();
                        this.scrollToHeading(heading);
                        this.toggleTOC();
                    });
                    
                    li.appendChild(a);
                    this.tocList.appendChild(li);
                });
            }
            
            bindEvents() {
                // 切換目錄顯示/隱藏
                this.tocButton.addEventListener('click', (e) => {
                    if (!e.target.closest('.toc-menu')) {
                        this.toggleTOC();
                    }
                });
                
                // 點擊其他地方關閉目錄
                document.addEventListener('click', (e) => {
                    if (!e.target.closest('.floating-toc') && this.isExpanded) {
                        this.toggleTOC();
                    }
                });
                
                // 滾動時更新活動項目
                window.addEventListener('scroll', () => {
                    this.updateActiveHeading();
                });
            }
            
            toggleTOC() {
                this.isExpanded = !this.isExpanded;
                this.tocButton.classList.toggle('expanded', this.isExpanded);
            }
            
            scrollToHeading(heading) {
                const offsetTop = heading.offsetTop - 80; // 預留一些空間
                window.scrollTo({
                    top: offsetTop,
                    behavior: 'smooth'
                });
            }
            
            observeHeadings() {
                // 使用 Intersection Observer 監聽標題元素
                const observer = new IntersectionObserver((entries) => {
                    entries.forEach(entry => {
                        if (entry.isIntersecting) {
                            this.setActiveHeading(entry.target);
                        }
                    });
                }, {
                    rootMargin: '-20% 0px -80% 0px'
                });
                
                this.headings.forEach(heading => {
                    observer.observe(heading);
                });
            }
            
            setActiveHeading(heading) {
                // 移除之前的活動狀態
                const prevActive = this.tocList.querySelector('.toc-link.active');
                if (prevActive) {
                    prevActive.classList.remove('active');
                }
                
                // 添加新的活動狀態
                const currentLink = this.tocList.querySelector(`[href="#${heading.id}"]`);
                if (currentLink) {
                    currentLink.classList.add('active');
                    this.activeHeading = heading;
                }
            }
            
            updateActiveHeading() {
                // 簡單的滾動位置檢測
                let current = null;
                this.headings.forEach(heading => {
                    const rect = heading.getBoundingClientRect();
                    if (rect.top <= 100) {
                        current = heading;
                    }
                });
                
                if (current && current !== this.activeHeading) {
                    this.setActiveHeading(current);
                }
            }
        }
        
        // 初始化浮動目錄
        document.addEventListener('DOMContentLoaded', () => {
            new FloatingTOC();
        });
    </script>
</body>
</html>
