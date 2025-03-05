# teakai-shop
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Teakai PWP Viewer</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
        .container { max-width: 600px; margin: auto; }
        img, video { max-width: 100%; height: auto; margin-top: 10px; cursor: pointer; }
        .item { margin-top: 20px; border: 1px solid #ddd; padding: 10px; }
        .modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            max-width: 90%;
            max-height: 90%;
        }
        .close {
            position: absolute;
            top: 10px;
            right: 20px;
            font-size: 30px;
            color: white;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Danh sách sản phẩm</h1>
        <div id="itemList"></div>
    </div>
    
    <div id="modal" class="modal">
        <span class="close" onclick="closeModal()">&times;</span>
        <img id="modalImg" class="modal-content">
        <video id="modalVideo" class="modal-content" controls></video>
    </div>
    
    <script>
        function loadItems() {
            const itemList = document.getElementById('itemList');
            itemList.innerHTML = '';
            const items = JSON.parse(localStorage.getItem('items')) || [];
            items.forEach((item) => {
                const div = document.createElement('div');
                div.className = 'item';
                div.innerHTML = `<p>${item.description}</p>
                    ${item.type.startsWith('image') ? `<img src="${item.src}" onclick="openModal('${item.src}', 'image')" />` 
                    : `<video controls onclick="openModal('${item.src}', 'video')"><source src="${item.src}" type="${item.type}"></video>`}`;
                itemList.appendChild(div);
            });
        }
        
        function openModal(src, type) {
            const modal = document.getElementById('modal');
            const modalImg = document.getElementById('modalImg');
            const modalVideo = document.getElementById('modalVideo');
            
            if (type === 'image') {
                modalImg.src = src;
                modalImg.style.display = 'block';
                modalVideo.style.display = 'none';
            } else {
                modalVideo.src = src;
                modalVideo.style.display = 'block';
                modalImg.style.display = 'none';
            }
            
            modal.style.display = 'flex';
        }
        
        function closeModal() {
            document.getElementById('modal').style.display = 'none';
        }
        
        window.onload = loadItems;
    </script>
<p>Link truy cập trang người dùng: <a href="user.html" target="_blank">Xem sản phẩm</a></p>
</body>
</html>
