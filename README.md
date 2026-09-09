<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Floating Flowers Background Effect</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Sukhumvit Set', sans-serif, Arial;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #fff0f5 0%, #ffe4e1 100%);
      overflow: hidden;
      position: relative;
    }

    /* เนื้อหาหลักด้านหน้า */
    .content-card {
      position: relative;
      z-index: 10; /* อยู่ด้านหน้าดอกไม้ */
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(8px);
      padding: 40px 60px;
      border-radius: 20px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
      text-align: center;
      max-width: 500px;
    }

    .content-card h1 {
      color: #d87093;
      margin-bottom: 15px;
    }

    .content-card p {
      color: #666;
      line-height: 1.6;
    }

    /* คอนเทนเนอร์ดอกไม้ด้านหลัง */
    .flower-background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none; /* ป้องกันการคลิกทับเนื้อหา */
      z-index: 1; /* อยู่หลัง content-card */
      overflow: hidden;
    }

    /* สไตล์และอนิเมชันของดอกไม้ */
    .floating-flower {
      position: absolute;
      bottom: -80px;
      font-size: 2rem;
      user-select: none;
      animation: floatUp linear infinite;
      opacity: 0.7;
    }

    @keyframes floatUp {
      0% {
        transform: translateY(0) rotate(0deg) scale(0.8);
        opacity: 0;
      }
      10% {
        opacity: 0.8;
      }
      90% {
        opacity: 0.8;
      }
      100% {
        transform: translateY(-110vh) rotate(360deg) scale(1.2);
        opacity: 0;
      }
    }
  </style>
</head>
<body>

  <!-- พื้นหลังดอกไม้ลอย -->
  <div class="flower-background" id="flowerContainer"></div>

  <!-- เนื้อหาหลัก -->
  <div class="content-card">
    <h1>ข้อความอยู่ด้านหน้า</h1>
    <p>ดอกไม้จะลอยไปมาจากด้านล่างขึ้นด้านบนอยู่ทางด้านหลังของการ์ดนี้อย่างสวยงามและเป็นธรรมชาติ</p>
  </div>

  <script>
    const container = document.getElementById('flowerContainer');
    const flowerIcons = ['🌸', '🌺', '🌼', '🌷', '🌹', '🌻', '✨'];
    const flowerCount = 25; // จำนวนดอกไม้ลอย

    for (let i = 0; i < flowerCount; i++) {
      const flower = document.createElement('span');
      flower.classList.add('floating-flower');
      
      // สุ่มสัญลักษณ์ดอกไม้
      flower.innerText = flowerIcons[Math.floor(Math.random() * flowerIcons.length)];
      
      // สุ่มตำแหน่งเริ่มต้น horizontal (0% - 100%)
      flower.style.left = `${Math.random() * 100}%`;
      
      // สุ่มขนาดดอกไม้
      const size = 1.2 + Math.random() * 1.8;
      flower.style.fontSize = `${size}rem`;
      
      // สุ่มระยะเวลาการลอย (6 ถึง 15 วินาที)
      const duration = 6 + Math.random() * 9;
      flower.style.animationDuration = `${duration}s`;
      
      // สุ่มเวลาดีเลย์เริ่มต้น
      flower.style.animationDelay = `${Math.random() * 8}s`;

      container.appendChild(flower);
    }
  </script>

</body>
</html>
