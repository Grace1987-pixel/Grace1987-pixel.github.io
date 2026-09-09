<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Portfolio | กัญญาภัค เจตนาภิวัฒน์</title>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@700&family=Charm:wght@400;700&family=Sarabun:wght@300;400;600&display=swap" rel="stylesheet">
    <!-- Three.js Library -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    
    <style>
        :root {
            --bg-cream: #F7F3EC;
            --rococo-pink: #E8C5C8;
            --rococo-gold: #D4AF37;
            --gold-light: #F3E5AB;
            --dark-gold: #997A15;
            --oil-text: #2C221E;
            --soft-blue: #A2C4C9;
            --rose-accent: #C87D87;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Sarabun', sans-serif;
            background-color: var(--bg-cream);
            color: var(--oil-text);
            overflow-x: hidden;
        }

        /* Canvas Container */
        #canvas-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1;
            pointer-events: auto;
        }

        /* Overlay Layout */
        .ui-container {
            position: relative;
            z-index: 10;
            pointer-events: none;
            width: 100%;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 2rem;
        }

        .interactive {
            pointer-events: auto;
        }

        /* Header / Banner */
        header {
            text-align: center;
            padding: 1.5rem;
            background: rgba(253, 251, 247, 0.75);
            backdrop-filter: blur(8px);
            border: 2px solid var(--rococo-gold);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(153, 122, 21, 0.15), inset 0 0 15px rgba(212, 175, 55, 0.2);
            max-width: 800px;
            margin: 0 auto 2rem auto;
            position: relative;
        }

        header::before, header::after {
            content: "✦";
            font-size: 1.5rem;
            color: var(--rococo-gold);
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
        }

        header::before { left: 15px; }
        header::after { right: 15px; }

        h1.title-th {
            font-family: 'Charm', cursive;
            font-size: 2.8rem;
            font-weight: 700;
            color: var(--rose-accent);
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
            margin-bottom: 0.2rem;
        }

        p.subtitle {
            font-family: 'Cinzel Decorative', serif;
            font-size: 0.95rem;
            letter-spacing: 2px;
            color: var(--dark-gold);
            text-transform: uppercase;
        }

        /* Main Content Grid */
        .content-wrapper {
            display: grid;
            grid-template-columns: 320px 1fr;
            gap: 2rem;
            max-width: 1200px;
            margin: 0 auto;
            width: 100%;
            align-items: start;
        }

        /* Rococo Card Frame */
        .rococo-card {
            background: rgba(253, 251, 247, 0.85);
            backdrop-filter: blur(10px);
            border: 3px double var(--rococo-gold);
            border-radius: 12px;
            padding: 1.8rem;
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.08);
            position: relative;
        }

        .rococo-card::after {
            content: '';
            position: absolute;
            top: 4px; left: 4px; right: 4px; bottom: 4px;
            border: 1px solid var(--rococo-pink);
            border-radius: 8px;
            pointer-events: none;
        }

        /* Profile Details */
        .profile-card h2 {
            font-family: 'Charm', cursive;
            font-size: 1.8rem;
            color: var(--dark-gold);
            border-bottom: 2px dashed var(--rococo-pink);
            padding-bottom: 0.5rem;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        .info-list {
            list-style: none;
            display: flex;
            flex-direction: column;
            gap: 1rem;
        }

        .info-item {
            display: flex;
            flex-direction: column;
            gap: 0.2rem;
        }

        .info-label {
            font-size: 0.85rem;
            color: #7A685D;
            font-weight: 600;
            text-transform: uppercase;
        }

        .info-value {
            font-size: 1.05rem;
            color: var(--oil-text);
            font-weight: 400;
        }

        .badge {
            display: inline-block;
            background: linear-gradient(135deg, var(--rococo-pink), var(--soft-blue));
            color: white;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        /* Controls Instructions Overlay */
        .controls-hint {
            position: absolute;
            bottom: 2rem;
            right: 2rem;
            background: rgba(44, 34, 30, 0.75);
            color: var(--gold-light);
            padding: 0.8rem 1.2rem;
            border-radius: 30px;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            backdrop-filter: blur(5px);
            border: 1px solid var(--rococo-gold);
        }

        /* Footer */
        footer {
            text-align: center;
            padding: 1rem;
            font-size: 0.85rem;
            color: var(--dark-gold);
            margin-top: auto;
        }

        .gallery-tag {
            position: absolute;
            top: -15px;
            right: 20px;
            background: var(--rococo-gold);
            color: white;
            font-family: 'Cinzel Decorative', serif;
            font-size: 0.75rem;
            padding: 0.2rem 0.8rem;
            border-radius: 4px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.15);
        }

        @media (max-width: 850px) {
            .content-wrapper {
                grid-template-columns: 1fr;
            }
            h1.title-th {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>

    <!-- Three.js 3D Canvas -->
    <div id="canvas-container"></div>

    <!-- UI Overlay -->
    <div class="ui-container">
        <!-- Header -->
        <header class="interactive">
            <h1 class="title-th">กัญญาภัค เจตนาภิวัฒน์</h1>
            <p class="subtitle">Rococo & Oil Painting 3D Portfolio</p>
        </header>

        <!-- Main Content -->
        <div class="content-wrapper">
            <!-- Profile Info Panel -->
            <div class="rococo-card profile-card interactive">
                <span class="gallery-tag">ARTIST PROFILE</span>
                <h2><i data-lucide="palette"></i> ข้อมูลส่วนตัว</h2>
                <ul class="info-list">
                    <li class="info-item">
                        <span class="info-label">ชื่อ-นามสกุล</span>
                        <span class="info-value">กัญญาภัค เจตนาภิวัฒน์</span>
                    </li>
                    <li class="info-item">
                        <span class="info-label">อายุ</span>
                        <span class="info-value">21 ปี</span>
                    </li>
                    <li class="info-item">
                        <span class="info-label">การศึกษา</span>
                        <span class="info-value">ชั้นปีที่ 4 (Senior)</span>
                        <span class="info-value" style="font-size:0.95rem; color:#555;">คณะสถาปัตยกรรมศาสตร์</span>
                        <span class="info-value"><span class="badge">สาขาเกมและอนิเมชั่น</span></span>
                    </li>
                    <li class="info-item">
                        <span class="info-label">ความสามารถพิเศษ</span>
                        <span class="info-value">🎨 การวาดภาพดิจิทัล & สีน้ำมัน</span>
                        <span class="info-value">🖌️ ออกแบบตัวละครและฉาก (Concept Art)</span>
                        <span class="info-value">🏛️ 3D Modeling & Texturing Style Rococo</span>
                    </li>
                </ul>
            </div>
            
            <div></div>
        </div>

        <!-- Controls Hint -->
        <div class="controls-hint interactive">
            <i data-lucide="mouse-pointer"></i>
            <span>หมุนภาพ 3D: คลิกลากซ้าย | ย่อ-ขยาย: สกอร์ลเมาส์</span>
        </div>

        <!-- Footer -->
        <footer>
            <p>© 2026 Kanyapak Chettanapiwat • Rococo Digital Art Gallery</p>
        </footer>
    </div>

    <script>
        lucide.createIcons();

        const container = document.getElementById('canvas-container');
        
        const scene = new THREE.Scene();
        scene.background = new THREE.Color(0xF5F0E6);

        const camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.1, 1000);
        camera.position.set(0, 1.2, 6);

        const renderer = new THREE.WebGLRenderer({ antialias: true });
        renderer.setSize(window.innerWidth, window.innerHeight);
        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        renderer.toneMapping = THREE.ACESFilmicToneMapping;
        renderer.toneMappingExposure = 1.1;
        container.appendChild(renderer.domElement);

        const controls = new THREE.OrbitControls(camera, renderer.domElement);
        controls.enableDamping = true;
        controls.dampingFactor = 0.05;
        controls.maxPolarAngle = Math.PI / 2 + 0.1;
        controls.minDistance = 3;
        controls.maxDistance = 10;

        // --- Create Dynamic Watercolor Background Effect in 3D ---
        function generateWatercolorBgTexture() {
            const canvas = document.createElement('canvas');
            canvas.width = 1024;
            canvas.height = 1024;
            const ctx = canvas.getContext('2d');

            ctx.fillStyle = '#F5F0E6';
            ctx.fillRect(0, 0, 1024, 1024);

            const colors = [
                'rgba(232, 197, 200, 0.25)', 
                'rgba(162, 196, 201, 0.25)', 
                'rgba(243, 229, 171, 0.3)', 
                'rgba(200, 125, 135, 0.15)',
                'rgba(44, 55, 40, 0.12)'
            ];

            for (let i = 0; i < 150; i++) {
                const x = Math.random() * 1024;
                const y = Math.random() * 1024;
                const radius = Math.random() * 180 + 50;

                const grad = ctx.createRadialGradient(x, y, 5, x, y, radius);
                const color = colors[Math.floor(Math.random() * colors.length)];
                grad.addColorStop(0, color);
                grad.addColorStop(1, 'transparent');

                ctx.fillStyle = grad;
                ctx.beginPath();
                ctx.arc(x, y, radius, 0, Math.PI * 2);
                ctx.fill();
            }

            return new THREE.CanvasTexture(canvas);
        }

        // Add soft watercolor background plane
        const bgGeo = new THREE.PlaneGeometry(30, 20);
        const bgMat = new THREE.MeshBasicMaterial({
            map: generateWatercolorBgTexture(),
            depthWrite: false
        });
        const bgMesh = new THREE.Mesh(bgGeo, bgMat);
        bgMesh.position.set(0, 0, -8);
        scene.add(bgMesh);

        // --- Lighting ---
        const ambientLight = new THREE.AmbientLight(0xFFFFFF, 1.2);
        scene.add(ambientLight);

        const mainLight = new THREE.DirectionalLight(0xFFFAF0, 1.0);
        mainLight.position.set(5, 8, 5);
        scene.add(mainLight);

        // --- Load User Artwork into 3D Frame ---
        const textureLoader = new THREE.TextureLoader();
        
        // Base64 Image string directly embedded
        const artworkImageSrc = 'input_file_0.png'; 

        const galleryGroup = new THREE.Group();

        textureLoader.load(artworkImageSrc, (texture) => {
            texture.generateMipmaps = true;
            
            // Ornate Gold Frame Material
            const goldMaterial = new THREE.MeshStandardMaterial({
                color: 0xD4AF37,
                metalness: 0.8,
                roughness: 0.3
            });

            // Frame dimensions matching artwork ratio (~1.4:1)
            const artWidth = 3.5;
            const artHeight = 2.5;
            const frameThickness = 0.15;

            // Outer Frame
            const frameGeo = new THREE.BoxGeometry(artWidth + 0.3, artHeight + 0.3, frameThickness);
            const frameMesh = new THREE.Mesh(frameGeo, goldMaterial);
            galleryGroup.add(frameMesh);

            // Canvas Artwork Plane
            const artGeo = new THREE.PlaneGeometry(artWidth, artHeight);
            const artMat = new THREE.MeshStandardMaterial({
                map: texture,
                roughness: 0.4
            });
            const artMesh = new THREE.Mesh(artGeo, artMat);
            artMesh.position.z = frameThickness / 2 + 0.01;
            galleryGroup.add(artMesh);

            // Ornate Corner Details
            const cornerGeo = new THREE.TorusGeometry(0.15, 0.04, 16, 32);
            const corners = [
                [-(artWidth/2), (artHeight/2)],
                [(artWidth/2), (artHeight/2)],
                [-(artWidth/2), -(artHeight/2)],
                [(artWidth/2), -(artHeight/2)]
            ];

            corners.forEach(pos => {
                const corner = new THREE.Mesh(cornerGeo, goldMaterial);
                corner.position.set(pos[0], pos[1], frameThickness / 2 + 0.02);
                galleryGroup.add(corner);
            });
        });

        galleryGroup.position.set(1.2, 0.8, 0);
        scene.add(galleryGroup);

        // --- Wooden Easel Stand ---
        const woodMaterial = new THREE.MeshStandardMaterial({ color: 0x5C3A21, roughness: 0.8 });
        const easelGroup = new THREE.Group();
        const legGeo = new THREE.CylinderGeometry(0.04, 0.04, 4.2);

        const leftLeg = new THREE.Mesh(legGeo, woodMaterial);
        leftLeg.position.set(-1.0, -0.6, -0.2);
        leftLeg.rotation.z = -0.2;
        easelGroup.add(leftLeg);

        const rightLeg = new THREE.Mesh(legGeo, woodMaterial);
        rightLeg.position.set(1.0, -0.6, -0.2);
        rightLeg.rotation.z = 0.2;
        easelGroup.add(rightLeg);

        const backLeg = new THREE.Mesh(legGeo, woodMaterial);
        backLeg.position.set(0, -0.6, -1.2);
        backLeg.rotation.x = -0.3;
        easelGroup.add(backLeg);

        const shelfGeo = new THREE.BoxGeometry(3.6, 0.08, 0.3);
        const shelf = new THREE.Mesh(shelfGeo, woodMaterial);
        shelf.position.set(0, -0.6, 0.1);
        easelGroup.add(shelf);

        easelGroup.position.set(1.2, 0.8, 0);
        scene.add(easelGroup);

        // --- Animation Loop ---
        let clock = new THREE.Clock();

        function animate() {
            requestAnimationFrame(animate);

            const elapsedTime = clock.getElapsedTime();

            // Gentle floating movement for the artwork and easel
            galleryGroup.position.y = 0.8 + Math.sin(elapsedTime * 1.2) * 0.05;
            galleryGroup.rotation.y = Math.sin(elapsedTime * 0.6) * 0.04;
            
            easelGroup.position.y = 0.8 + Math.sin(elapsedTime * 1.2) * 0.05;
            easelGroup.rotation.y = Math.sin(elapsedTime * 0.6) * 0.04;

            controls.update();
            renderer.render(scene, camera);
        }

        animate();

        // Responsive Resize
        window.addEventListener('resize', () => {
            camera.aspect = window.innerWidth / window.innerHeight;
            camera.updateProjectionMatrix();
            renderer.setSize(window.innerWidth, window.innerHeight);
        });
    </script>
</body>
</html>
