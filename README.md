<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>กัญญาภัค เจตนาภิวัฒน์ - Profile</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Sukhumvit Set', 'Prompt', sans-serif, Arial;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #fff0f5 0%, #ffe4e1 100%);
      overflow: hidden;
      position: relative;
    }

    /* การ์ดเนื้อหาหลักด้านหน้า */
    .profile-card {
      position: relative;
      z-index: 10; /* อยู่ด้านหน้าดอกไม้ */
      background: rgba(255, 255, 255, 0.88);
      backdrop-filter: blur(10px);
      padding: 40px;
      border-radius: 24px;
      box-shadow: 0 12px 35px rgba(216, 112, 147, 0.15);
      text-align: center;
      max-width: 520px;
      width: 90%;
      border: 1px solid rgba(255, 255, 255, 0.6);
    }

    .profile-card h1 {
      color: #d87093;
      font-size: 1.8rem;
      margin-bottom: 8px;
    }

    .profile-card .subtitle {
      color: #8b5a2b;
      font-weight: 600;
      font-size: 1.05rem;
      margin-bottom: 20px;
      background: #fff5f8;
      display: inline-block;
      padding: 6px 16px;
      border-radius: 20px;
    }

    .profile-card .info-list {
      text-align: left;
      color: #555;
      line-height: 1.8;
      margin-bottom: 20px;
      background: rgba(255, 255, 255, 0.6);
      padding: 20px;
      border-radius: 16px;
    }

    .profile-card .info-list p {
      margin-bottom: 8px;
    }

    .profile-card .info-list p:last-child {
      margin-bottom: 0;
    }

    .profile-card .skills-title {
      font-weight: bold;
      color: #c71585;
      margin-top: 10px;
    }

    /* คอนเทนเนอร์ดอกไม้ด้านหลัง */
    .flower-background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none; /* ป้องกันการคลิกทับเนื้อหา */
      z-index: 1; /* อยู่หลัง profile-card */
      overflow: hidden;
    }

    /* สไตล์และอนิเมชันของดอกไม้ */
    .floating-flower {
      position: absolute;
      bottom: -80px;
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
        opacity: 0.85;
      }
      90% {
        opacity: 0.85;
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
  <div class="profile-card">
    <h1>กัญญาภัค เจตนาภิวัฒน์</h1>
    <div class="subtitle">คณะสถาปัตยกรรมศาสตร์ สาขาเกมแอนิเมชัน</div>

    <div class="info-list">
      <p><strong>อายุ:</strong> 21 ปี</p>
      <p><strong>การศึกษา:</strong> กำลังศึกษาอยู่ชั้นปีที่ 4</p>
      <p class="skills-title">ความสามารถพิเศษ:</p>
      <p>• การวาดรูป</p>
      <p>• การปั้น 3D โมเดล</p>
      <p>• การออกแบบฉากสิ่งแวดล้อม (Environment Design)</p>
    </div>
  </div>

  <script>
    const container = document.getElementById('flowerContainer');
    const flowerIcons = ['🌸', '🌺', '🌼', '🌷', '🌹', '🌻', '✨', '🌿'];
    const flowerCount = 30; // จำนวนดอกไม้ที่ลอยอยู่ด้านหลัง

    for (let i = 0; i < flowerCount; i++) {
      const flower = document.createElement('span');
      flower.classList.add('floating-flower');
      
      // สุ่มสัญลักษณ์ดอกไม้
      flower.innerText = flowerIcons[Math.floor(Math.random() * flowerIcons.length)];
      
      // สุ่มตำแหน่งเริ่มต้นตามแนวนอน (0% - 100%)
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
