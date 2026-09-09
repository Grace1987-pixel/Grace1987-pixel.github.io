<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Kanyapak Jetanapiwat | Interactive 3D Portfolio Showcase</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;800&family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <style>
    :root {
      --primary: #ff4d8d;
      --primary-glow: rgba(255, 77, 141, 0.4);
      --secondary: #7000ff;
      --accent: #00f0ff;
      --bg-dark: #090912;
      --card-bg: rgba(20, 18, 38, 0.65);
      --card-border: rgba(255, 255, 255, 0.12);
      --text-main: #ffffff;
      --text-sub: #b3b3cb;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body, html {
      width: 100%;
      height: 100%;
      overflow: hidden;
      font-family: 'Prompt', 'Plus Jakarta Sans', sans-serif;
      background-color: var(--bg-dark);
      color: var(--text-main);
    }

    /* 3D WebGL Canvas */
    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1;
      pointer-events: none;
    }

    /* Custom Cursor */
    .custom-cursor {
      position: fixed;
      width: 20px;
      height: 20px;
      border: 2px solid var(--primary);
      border-radius: 50%;
      pointer-events: none;
      transform: translate(-50%, -50%);
      transition: width 0.2s, height 0.2s, background-color 0.2s;
      z-index: 9999;
      box-shadow: 0 0 15px var(--primary);
    }

    .custom-cursor-dot {
      position: fixed;
      width: 6px;
      height: 6px;
      background: var(--accent);
      border-radius: 50%;
      pointer-events: none;
      transform: translate(-50%, -50%);
      z-index: 10000;
    }

    /* UI Layout Containers */
    .main-wrapper {
      position: relative;
      z-index: 10;
      width: 100%;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      perspective: 1000px;
    }

    /* Ultra Glassmorphism Card */
    .hero-card {
      position: relative;
      width: 100%;
      max-width: 850px;
      background: var(--card-bg);
      backdrop-filter: blur(25px) saturate(180%);
      -webkit-backdrop-filter: blur(25px) saturate(180%);
      border: 1px solid var(--card-border);
      border-radius: 32px;
      padding: 45px 50px;
      box-shadow: 
        0 30px 60px rgba(0, 0, 0, 0.5),
        inset 0 1px 0 rgba(255, 255, 255, 0.2),
        0 0 40px rgba(112, 0, 255, 0.15);
      transform-style: preserve-3d;
      transition: transform 0.15s ease-out, box-shadow 0.3s ease;
      overflow: hidden;
    }

    /* Neon Decorative Line */
    .hero-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(90deg, var(--primary), var(--secondary), var(--accent));
      box-shadow: 0 0 15px var(--primary);
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 25px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
      padding-bottom: 20px;
    }

    .tag-group {
      display: flex;
      gap: 10px;
    }

    .badge {
      background: rgba(255, 77, 141, 0.12);
      border: 1px solid rgba(255, 77, 141, 0.3);
      color: #ff85b3;
      padding: 6px 14px;
      border-radius: 50px;
      font-size: 0.85rem;
      font-weight: 600;
      letter-spacing: 0.5px;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .badge-alt {
      background: rgba(0, 240, 255, 0.1);
      border: 1px solid rgba(0, 240, 255, 0.3);
      color: var(--accent);
    }

    .year-tag {
      font-family: 'Plus Jakarta Sans', sans-serif;
      font-weight: 800;
      color: rgba(255, 255, 255, 0.4);
      font-size: 1.2rem;
    }

    h1.name {
      font-size: 2.8rem;
      font-weight: 700;
      background: linear-gradient(135deg, #ffffff 30%, #ffb3d1 70%, var(--primary) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      margin-bottom: 8px;
      letter-spacing: -0.5px;
      text-shadow: 0 10px 20px rgba(0,0,0,0.2);
    }

    .faculty {
      font-size: 1.25rem;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 25px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .faculty span {
      color: var(--text-sub);
      font-size: 1rem;
    }

    /* Grid for Skills & Details */
    .details-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      margin-bottom: 30px;
    }

    .info-box {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.06);
      border-radius: 20px;
      padding: 20px;
      transition: background 0.3s, border-color 0.3s, transform 0.3s;
    }

    .info-box:hover {
      background: rgba(255, 255, 255, 0.06);
      border-color: rgba(255, 255, 255, 0.18);
      transform: translateY(-3px);
    }

    .info-box h3 {
      font-size: 0.95rem;
      color: var(--text-sub);
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 12px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .info-box .value {
      font-size: 1.4rem;
      font-weight: 600;
      color: #fff;
    }

    /* Skills Hex Pill Tags */
    .skills-container {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }

    .skill-card {
      background: linear-gradient(135deg, rgba(112, 0, 255, 0.2), rgba(255, 77, 141, 0.2));
      border: 1px solid rgba(255, 255, 255, 0.15);
      padding: 10px 18px;
      border-radius: 14px;
      font-size: 0.95rem;
      font-weight: 500;
      color: #fff;
      display: flex;
      align-items: center;
      gap: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    .skill-card:hover {
      transform: scale(1.06) translateY(-2px);
      border-color: var(--accent);
      box-shadow: 0 8px 20px rgba(0, 240, 255, 0.25);
    }

    .skill-icon {
      font-size: 1.2rem;
    }

    /* Control Panel / Interactive Options */
    .controls-bar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-top: 20px;
      border-top: 1px solid rgba(255, 255, 255, 0.08);
    }

    .btn-interactive {
      background: linear-gradient(135deg, var(--primary), var(--secondary));
      border: none;
      color: white;
      padding: 12px 28px;
      border-radius: 50px;
      font-family: 'Prompt', sans-serif;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      box-shadow: 0 10px 25px var(--primary-glow);
      transition: all 0.3s;
      display: inline-flex;
      align-items: center;
      gap: 8px;
      pointer-events: auto;
    }

    .btn-interactive:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 15px 35px rgba(255, 77, 141, 0.6);
    }

    .btn-interactive:active {
      transform: translateY(1px);
    }

    .mode-toggle {
      display: flex;
      gap: 8px;
      background: rgba(0, 0, 0, 0.4);
      padding: 5px;
      border-radius: 40px;
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .mode-btn {
      background: transparent;
      border: none;
      color: var(--text-sub);
      padding: 8px 16px;
      border-radius: 30px;
      cursor: pointer;
      font-size: 0.85rem;
      font-family: 'Prompt', sans-serif;
      transition: all 0.3s;
      pointer-events: auto;
    }

    .mode-btn.active {
      background: rgba(255, 255, 255, 0.15);
      color: #fff;
      font-weight: 600;
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      .hero-card {
        padding: 30px 25px;
      }
      h1.name {
        font-size: 2rem;
      }
      .details-grid {
        grid-template-columns: 1fr;
      }
      .controls-bar {
        flex-direction: column;
        gap: 15px;
      }
    }
  </style>
</head>
<body>

  <!-- Custom Cursor Elements -->
  <div class="custom-cursor" id="cursor"></div>
  <div class="custom-cursor-dot" id="cursor-dot"></div>

  <!-- 3D Canvas Background -->
  <div id="canvas-container"></div>

  <!-- Main Showcase Container -->
  <div class="main-wrapper">
    <div class="hero-card" id="card">
      
      <!-- Card Top Header -->
      <div class="card-header">
        <div class="tag-group">
          <span class="badge">🌸 Interactive 3D Showcase</span>
          <span class="badge badge-alt">🎮 Game Design Portfolio</span>
        </div>
        <span class="year-tag">2026</span>
      </div>

      <!-- Main Title Section -->
      <h1 class="name">กัญญาภัค เจตนาภิวัฒน์</h1>
      <div class="faculty">
        คณะสถาปัตยกรรมศาสตร์ <span>/ สาขาเกมแอนิเมชัน</span>
      </div>

      <!-- Core Details Grid -->
      <div class="details-grid">
        <div class="info-box">
          <h3>📌 สถานะปัจจุบัน</h3>
          <div class="value">นักศึกษาชั้นปีที่ 4</div>
        </div>
        <div class="info-box">
          <h3>🎂 อายุ</h3>
          <div class="value">21 ปี</div>
        </div>
      </div>

      <!-- Specialized Skills -->
      <div style="margin-bottom: 25px;">
        <h3 style="font-size: 0.95rem; color: var(--text-sub); text-transform: uppercase; letter-spacing: 1px; margin-bottom: 12px;">
          ✨ ความสามารถเฉพาะทาง (Specializations)
        </h3>
        <div class="skills-container">
          <div class="skill-card">
            <span class="skill-icon">🎨</span>
            <span>การวาดรูป & Digital Art</span>
          </div>
          <div class="skill-card">
            <span class="skill-icon">🗿</span>
            <span>การปั้น 3D โมเดล (3D Modeling)</span>
          </div>
          <div class="skill-card">
            <span class="skill-icon">🏔️</span>
            <span>การออกแบบฉากสิ่งแวดล้อม (Environment Design)</span>
          </div>
        </div>
      </div>

      <!-- Interactive Controls -->
      <div class="controls-bar">
        <button class="btn-interactive" id="burstBtn">
          <span>🌸 ปล่อยระเบิดพายุดอกไม้ 3D</span>
        </button>

        <div class="mode-toggle">
          <button class="mode-btn active" onclick="changeTheme('sakura')">Sakura Pink</button>
          <button class="mode-btn" onclick="changeTheme('cyber')">Cyber Neon</button>
          <button class="mode-btn" onclick="changeTheme('gold')">Golden Hour</button>
        </div>
      </div>

    </div>
  </div>

  <script>
    /* ==========================================
       1. Custom Cursor Dynamic Follower
       ========================================== */
    const cursor = document.getElementById('cursor');
    const cursorDot = document.getElementById('cursor-dot');
    let mouseX = window.innerWidth / 2;
    let mouseY = window.innerHeight / 2;
    let cursorX = mouseX, cursorY = mouseY;

    window.addEventListener('mousemove', (e) => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      cursorDot.style.left = `${mouseX}px`;
      cursorDot.style.top = `${mouseY}px`;
    });

    function animateCursor() {
      cursorX += (mouseX - cursorX) * 0.15;
      cursorY += (mouseY - cursorY) * 0.15;
      cursor.style.left = `${cursorX}px`;
      cursor.style.top = `${cursorY}px`;
      requestAnimationFrame(animateCursor);
    }
    animateCursor();

    /* ==========================================
       2. 3D Parallax Tilt Effect on Card
       ========================================== */
    const card = document.getElementById('card');
    window.addEventListener('mousemove', (e) => {
      const xAxis = (window.innerWidth / 2 - e.clientX) / 25;
      const yAxis = (window.innerHeight / 2 - e.clientY) / 25;
      card.style.transform = `rotateY(${xAxis}deg) rotateX(${yAxis}deg)`;
    });

    /* ==========================================
       3. THREE.JS 3D Floating Flower Particles System
       ========================================== */
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.z = 30;

    const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    container.appendChild(renderer.domElement);

    // Create Custom Procedural Petal/Flower Geometry
    function createPetalGeometry() {
      const shape = new THREE.Shape();
      shape.moveTo(0, 0);
      shape.bezierCurveTo(0.4, 0.8, 0.8, 1.5, 0, 2.2);
      shape.bezierCurveTo(-0.8, 1.5, -0.4, 0.8, 0, 0);

      const extrudeSettings = {
        steps: 1,
        depth: 0.08,
        bevelEnabled: true,
        bevelThickness: 0.04,
        bevelSize: 0.04,
        bevelSegments: 3
      };
      return new THREE.ExtrudeGeometry(shape, extrudeSettings);
    }

    const petalGeo = createPetalGeometry();
    
    // Theme Colors Definition
    const themes = {
      sakura: [0xff4d8d, 0xff99c2, 0xffccd5, 0x7000ff],
      cyber: [0x00f0ff, 0x7000ff, 0xff007f, 0x00ff88],
      gold: [0xffb700, 0xff8800, 0xffe600, 0xff4500]
    };

    let currentTheme = 'sakura';
    const flowerGroup = new THREE.Group();
    scene.add(flowerGroup);

    const petals = [];
    const particleCount = 120;

    function createFlowerMesh(colorHex) {
      const flower = new THREE.Group();
      const petalMat = new THREE.MeshPhongMaterial({
        color: colorHex,
        shininess: 80,
        side: THREE.DoubleSide,
        transparent: true,
        opacity: 0.85
      });

      // Assemble 5 petals into a 3D Flower
      for (let i = 0; i < 5; i++) {
        const petal = new THREE.Mesh(petalGeo, petalMat);
        petal.rotation.z = (i * Math.PI * 2) / 5;
        petal.rotation.x = 0.2;
        flower.add(petal);
      }

      // Flower Center Core
      const centerGeo = new THREE.SphereGeometry(0.25, 16, 16);
      const centerMat = new THREE.MeshBasicMaterial({ color: 0xffe600 });
      const center = new THREE.Mesh(centerGeo, centerMat);
      flower.add(center);

      return flower;
    }

    // Spawn 3D Flowers
    for (let i = 0; i < particleCount; i++) {
      const colors = themes[currentTheme];
      const selectedColor = colors[Math.floor(Math.random() * colors.length)];
      const flower = createFlowerMesh(selectedColor);

      flower.position.x = (Math.random() - 0.5) * 60;
      flower.position.y = (Math.random() - 0.5) * 60;
      flower.position.z = (Math.random() - 0.5) * 40;

      const scale = 0.4 + Math.random() * 0.7;
      flower.scale.set(scale, scale, scale);

      // Custom velocity & rotation properties
      flower.userData = {
        vy: 0.03 + Math.random() * 0.05,
        vx: (Math.random() - 0.5) * 0.02,
        rotX: (Math.random() - 0.5) * 0.03,
        rotY: (Math.random() - 0.5) * 0.03,
        rotZ: (Math.random() - 0.5) * 0.03,
        initialX: flower.position.x
      };

      petals.push(flower);
      flowerGroup.add(flower);
    }

    // Lights Setup
    const ambientLight = new THREE.AmbientLight(0xffffff, 0.8);
    scene.add(ambientLight);

    const dirLight1 = new THREE.DirectionalLight(0xff4d8d, 1.2);
    dirLight1.position.set(20, 30, 20);
    scene.add(dirLight1);

    const dirLight2 = new THREE.DirectionalLight(0x00f0ff, 0.8);
    dirLight2.position.set(-20, -20, 10);
    scene.add(dirLight2);

    // Animation Loop
    let clock = new THREE.Clock();

    function animate() {
      requestAnimationFrame(animate);
      const elapsedTime = clock.getElapsedTime();

      // Mouse subtle influence on global group rotation
      flowerGroup.rotation.y = (mouseX / window.innerWidth - 0.5) * 0.3;
      flowerGroup.rotation.x = (mouseY / window.innerHeight - 0.5) * 0.3;

      petals.forEach((flower) => {
        flower.position.y += flower.userData.vy;
        flower.position.x = flower.userData.initialX + Math.sin(elapsedTime + flower.position.y * 0.1) * 1.5;

        flower.rotation.x += flower.userData.rotX;
        flower.rotation.y += flower.userData.rotY;
        flower.rotation.z += flower.userData.rotZ;

        // Reset floating boundaries
        if (flower.position.y > 30) {
          flower.position.y = -30;
          flower.position.x = (Math.random() - 0.5) * 60;
          flower.userData.initialX = flower.position.x;
        }
      });

      renderer.render(scene, camera);
    }

    animate();

    // Window Resize Handler
    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    /* ==========================================
       4. Interactive Burst & Theme Switching
       ========================================== */
    document.getElementById('burstBtn').addEventListener('click', () => {
      petals.forEach(flower => {
        flower.position.x = (Math.random() - 0.5) * 10;
        flower.position.y = -10 + (Math.random() - 0.5) * 10;
        flower.position.z = (Math.random() - 0.5) * 10;

        flower.userData.vy = 0.15 + Math.random() * 0.15;
        flower.userData.vx = (Math.random() - 0.5) * 0.2;
      });

      setTimeout(() => {
        petals.forEach(flower => {
          flower.userData.vy = 0.03 + Math.random() * 0.05;
        });
      }, 2500);
    });

    function changeTheme(themeName) {
      currentTheme = themeName;
      
      // Update UI Buttons
      document.querySelectorAll('.mode-btn').forEach(btn => btn.classList.remove('active'));
      event.target.classList.add('active');

      const colors = themes[themeName];
      petals.forEach((flower, index) => {
        const color = colors[index % colors.length];
        flower.children.forEach(child => {
          if (child.material && child.material.color) {
            child.material.color.setHex(color);
          }
        });
      });
    }
  </script>
</body>
</html>
