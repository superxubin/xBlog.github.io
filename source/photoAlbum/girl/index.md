---
title: 头像和手机壁纸
date: 2023-03-08 15:37:54
aside: false
top_img: https://images8.alphacoders.com/505/505616.png
---
  <style>
        #waterfall {
            width: 100%;
            min-height:400px;
            /* max-height:100%; */
            column-count: 5;
            column-gap: 20px;
            margin:0 auto;
        }
        .item {
            position: absolute;
            top: -9999px;
            opacity: 0;
            transition: opacity 5s ease;
            perspective: 1000px;
            cursor: pointer;
            transform: rotateY(0); /* 添加这行代码 */
        }
       
        .item.show {
            position: static;
            left: auto;
            opacity: 1;
        }
        .item img {
            width: 100%;
            height: auto;
            transition: transform 1s;
            transform-style: preserve-3d;
        }
        
        .item:hover img {
            transform: rotateY(180deg);

        }
       .back{
        height:80px;
        font-size:30px;
        cursor: pointer;
        padding:10px 0;
        margin-bottom: 10px;
         transition: 1s;
       }
        .back:hover{
        font-size:32px;
       }
        .pagination {
            margin-top: 20px;
            text-align: center;
        }
        .aColor{
             background-image: linear-gradient(to bottom,  #ffb3d1,#ff7ea6)!important;
            color: #ff6c9c !important;
            transform: translateY(2px) !important;
            box-shadow: none !important;
            }
        .aClick{
            margin:0 15px;
        }
        .pagination a  {
            display: inline-block;
            padding: 0px 12px;
            border-radius: 50%;
            color: #2d2e2f;
            outline: none;
            text-decoration: none;
            margin:0 8px;
            background-image: linear-gradient(to bottom, #ff6c9c, #ff4077);
            box-shadow: 0 2px 6px rgba(255, 64, 119, 0.5);
            color: #ff4077;
            font-size: 16px;
            font-weight: bold;
            text-align: center;
            text-decoration: none;
            transition: all 0.3s ease;
            cursor: pointer;
            }

            .pagination a:hover {
            color: #ff6c9c !important;
	        text-decoration: none !important;
            background-image: linear-gradient(to bottom, #ff4077, #ff6c9c);
            box-shadow: 0 4px 10px rgba(255, 64, 119, 0.5);
            }
         
        .loading {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.8); /* 半透明黑色背景 */
        display: flex;
        justify-content: center;
        align-items: center;
        z-index: 2; /* 将 loading 置于图片和蒙层之上 */
        }

        .loading::before {
        content: "";
        display: block;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        border: 4px solid #fff; /* 白色边框 */
        border-top-color: transparent; /* 透明边框 */
        animation: loading 1s ease-in-out infinite; /* 旋转动画 */

   
        }

        @keyframes loading {
        0% {
            transform: rotate(0);
        }
        100% {
            transform: rotate(360deg);
        }
        }

    </style>

<a class='back' onclick="back()">⬅ 返回图册</a> 
  <div id="waterfall"></div>
    <div class="pagination"></div>


 <script>


        var waterfall = document.getElementById('waterfall');
         var imgUrl = 'http://43.136.28.91:8899/imageFile/blog/';

    var images = [
            { url: imgUrl + 'avatar.jpg', alt: 'Image 1' },
            { url: imgUrl + '07753-2023021614112679faa40310b4813f72741f5a9521934bd5d3f132.jpg', alt: 'Image 2' },
            { url: imgUrl + '201608.jpg', alt: 'Image 2' },
            { url: imgUrl + '185460.jpg', alt: 'Image 3' },
            { url: imgUrl + '197924.jpg', alt: 'Image 4' },
            { url: imgUrl + '169312.jpg', alt: 'Image 6' },
            { url: imgUrl + '173273.jpg', alt: 'Image 7' },
            { url: imgUrl + '198378.jpg', alt: 'Image 8' },
            { url: imgUrl + '215137.jpg', alt: 'Image 9' },
            { url: imgUrl + '212134.jpg', alt: 'Image 10' },
            { url: imgUrl + '212136.jpg', alt: 'Image 10' },
            { url: imgUrl + '212132.jpg', alt: 'Image 10' },
            { url: imgUrl + '212131.jpg', alt: 'Image 10' },
            { url: imgUrl + '212138.jpg', alt: 'Image 10' },
            { url: imgUrl + '169310.jpg', alt: 'Image 10' },
            { url: imgUrl + '215131.jpg', alt: 'Image 10' },
            { url: imgUrl + '215133.jpg', alt: 'Image 10' },
            { url: imgUrl + '215134.jpg', alt: 'Image 10' },
            { url: imgUrl + '215135.jpg', alt: 'Image 10' },
            { url: imgUrl + '215157.jpg', alt: 'Image 10' },
            { url: imgUrl + '215136.jpg', alt: 'Image 10' },
            { url: imgUrl + '215170.jpg', alt: 'Image 10' },
            { url: imgUrl + '215422.jpg', alt: 'Image 10' },
             { url: imgUrl + '215423.jpg', alt: 'Image 10' },

            { url: 'https://s1.ax1x.com/2023/03/10/ppu9IFP.jpg', alt: 'Image 10' },
            // { url: imgUrl + '197924.jpg', alt: 'Image 10' },
            // { url: imgUrl + '197924.jpg', alt: 'Image 10' }
        ];
    function back(){
       history.back();
    }

    images.forEach((image, index) => {

            var group = document.createElement('div');
            group.classList.add('item');
            var loading = document.createElement('div');
            loading.classList.add('loading');

            waterfall.appendChild(group);


            var img = document.createElement('img');
            img.src = image.url;
            img.alt = image.alt;
            img.dataset.src = image.url;

            var lastChild = waterfall.lastChild;
            lastChild.appendChild(img);
            lastChild.appendChild(loading);

            
        });

        // 获取所有图片元素
        var items = document.querySelectorAll('.item');

        // 每页渲染的图片数量
        var pageSize = 20;

        // 计算总页数
        var pageCount = Math.ceil(items.length / pageSize);

        // 获取页码容器元素
        var pagination = document.querySelector('.pagination');

        // 生成页码
        for (let i = 1; i <= pageCount; i++) {
            var link = document.createElement('a');
            link.classList.add('aClick');
            link.textContent = i;
            link.dataset.page = i;
            pagination.appendChild(link);
        }

        // 默认显示第一页
        showPage(1);
              var aList = document.querySelectorAll('.aClick');
                 aList[0].classList.add('aColor');
        // 添加点击事件监听器
        pagination.addEventListener('click', e => {
            var aList = document.querySelectorAll('.aClick');
             aList.forEach(item => {
                item.classList.remove('aColor');
                });
            var link = e.target.closest('a');
            link.classList.add('aColor');
            if (link) {
                var page = parseInt(link.dataset.page);
                showPage(page);
            }
        });

        // 渲染指定页码的图片
        function showPage(page) {

            // 隐藏所有图片
            items.forEach(item => {
                item.classList.remove('show');
                item.style.opacity = 0;


            //图片懒加载
            var url = item.querySelector("img").dataset.src;;
            var imgEl = new Image();
            imgEl.src = url;
            imgEl.addEventListener("load", () => {
                item.classList.add("loaded");
                item.querySelector(".loading").style.display = "none"; /* 隐藏 loading 元素 */
            });
            });
            // 计算当前页显示的图片范围
            var startIndex = (page - 1) * pageSize;
            var endIndex = Math.min(startIndex + pageSize, items.length);
            // 显示对应页码的图片
            for (let i = startIndex; i < endIndex; i++) {
                items[i].style.display = 'inline-block';
                items[i].style.opacity = 1;
            }
            // 设置短暂延迟等待浏览器更新视图
            setTimeout(() => {
                // 将当前页码显示的图片元素显示出来
                for (let i = startIndex; i < endIndex; i++) {
                    items[i].classList.add('show');
                }
                // 将前一页码显示的图片元素隐藏起来
                for (let i = 0; i < startIndex; i++) {;
                    items[i].classList.remove('show');
                    items[i].style.opacity = 0;

                }
                for (let i = endIndex; i < items.length; i++) {
                    items[i].classList.remove('show');
                    items[i].style.opacity = 0;

                }
            }, 10);
        }


    </script>






