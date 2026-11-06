<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Hugo Studio — Interactive 3D Experience</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/vanilla-tilt/1.8.0/vanilla-tilt.min.js"></script>
  <style>
    body {
      background-color: #f8fafc;
      color: #0f172a;
      font-family: system-ui, -apple-system, sans-serif;
      overflow-x: hidden;
    }
    #canvas-container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 0;
      pointer-events: none;
    }
    .glass-card {
      background: rgba(255, 255, 255, 0.75);
      backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.8);
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.04);
      transform-style: preserve-3d;
    }
    .gradient-text {
      background: linear-gradient(135deg, #3b82f6 0%, #8b5cf6 50%, #ec4899 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
  </style>
</head>
<body class="relative min-h-screen">

  <!-- 3D Canvas Background -->
  <div id="canvas-container"></div>

  <!-- Content Wrapper -->
  <main class="relative z-10 max-w-5xl mx-auto px-6 py-16 space-y-24">

    <!-- Hero Section -->
    <section class="text-center space-y-6 pt-12">
      <span class="inline-block px-4 py-1.5 rounded-full text-xs font-semibold tracking-wider text-blue-600 bg-blue-50 border border-blue-200 uppercase">
        Independent Digital Design & Software Studio · Saigon
      </span>
      <h1 class="text-6xl md:text-8xl font-black tracking-tight leading-none">
        Hugo <span class="gradient-text">Studio</span>
      </h1>
      <p class="text-xl md:text-2xl text-slate-600 font-medium max-w-2xl mx-auto">
        "Purposeful design. Clean code delivered."
      </p>
    </section>

    <!-- Community Ecosystem Section -->
    <section class="space-y-8">
      <h2 class="text-3xl font-bold text-center">Community Ecosystem & Live Projects</h2>
      <div class="grid md:grid-cols-2 gap-8">
        
        <!-- Hugo Edu+ -->
        <div class="glass-card rounded-3xl p-8 space-y-6 transition-all duration-300 hover:shadow-2xl" data-tilt data-tilt-max="10" data-tilt-speed="400">
          <div class="w-14 h-14 rounded-2xl bg-blue-500/10 flex items-center justify-center text-blue-600 font-bold text-2xl">
            🎓
          </div>
          <div>
            <h3 class="text-2xl font-bold">Hugo Edu+</h3>
            <p class="text-sm font-medium text-blue-600">Free Interactive Coding & Quirky UI</p>
          </div>
          <p class="text-slate-600 text-sm leading-relaxed">
            An open-access interactive platform created for learning programming through engaging visual modules and dynamic user interfaces.
          </p>
          <a href="https://education.hugowishpax.studio" target="_blank" class="sound-btn inline-flex items-center gap-2 px-6 py-3 rounded-xl bg-blue-600 text-white font-semibold text-sm hover:bg-blue-700 transition">
            Launch Education App ↗
          </a>
        </div>

        <!-- Hugo QR -->
        <div class="glass-card rounded-3xl p-8 space-y-6 transition-all duration-300 hover:shadow-2xl" data-tilt data-tilt-max="10" data-tilt-speed="400">
          <div class="w-14 h-14 rounded-2xl bg-pink-500/10 flex items-center justify-center text-pink-600 font-bold text-2xl">
            📱
          </div>
          <div>
            <h3 class="text-2xl font-bold">Hugo QR</h3>
            <p class="text-sm font-medium text-pink-600">Custom QR Engine & Developer API</p>
          </div>
          <p class="text-slate-600 text-sm leading-relaxed">
            A fast visual generator for custom QR codes with real-time design tuning and integrated REST APIs for seamless application embedding.
          </p>
          <a href="https://qr.hugowishpax.studio" target="_blank" class="sound-btn inline-flex items-center gap-2 px-6 py-3 rounded-xl bg-pink-600 text-white font-semibold text-sm hover:bg-pink-700 transition">
            Launch QR Engine ↗
          </a>
        </div>

      </div>
    </section>

    <!-- Design Philosophy Grid -->
    <section class="glass-card rounded-3xl p-10 space-y-6 text-center">
      <h2 class="text-2xl font-bold">Design Philosophy & Principles</h2>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-sm font-medium text-slate-700">
        <div class="p-4 rounded-xl bg-white/50 border border-slate-100">💡 Good ideas outlive trends</div>
        <div class="p-4 rounded-xl bg-white/50 border border-slate-100">🎧 Design starts by listening</div>
        <div class="p-4 rounded-xl bg-white/50 border border-slate-100">📐 Every pixel has a reason</div>
        <div class="p-4 rounded-xl bg-white/50 border border-slate-100">💬 Colors are emotions</div>
      </div>
    </section>

  </main>

  <script>
    // --- 1. THREE.JS 3D BACKGROUND SCENE ---
    const container = document.getElementById('canvas-container');
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });

    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    container.appendChild(renderer.domElement);

    // Create Floating 3D Shapes
    const geometry = new THREE.TorusKnotGeometry(1.2, 0.35, 128, 32);
    const material = new THREE.MeshPhysicalMaterial({
      color: 0x3b82f6,
      roughness: 0.2,
      metalness: 0.1,
      transmission: 0.6,
      thickness: 1.2,
      clearcoat: 1.0
    });
    const torus = new THREE.Mesh(geometry, material);
    scene.add(torus);

    // Lights
    const light1 = new THREE.PointLight(0xec4899, 2, 100);
    light1.position.set(5, 5, 5);
    scene.add(light1);

    const light2 = new THREE.PointLight(0x8b5cf6, 2, 100);
    light2.position.set(-5, -5, 5);
    scene.add(light2);

    const ambientLight = new THREE.AmbientLight(0xffffff, 1.5);
    scene.add(ambientLight);

    camera.position.z = 5;

    // Mouse Physics & Rotation
    let mouseX = 0, mouseY = 0;
    window.addEventListener('mousemove', (e) => {
      mouseX = (e.clientX / window.innerWidth - 0.5) * 2;
      mouseY = -(e.clientY / window.innerHeight - 0.5) * 2;
    });

    function animate() {
      requestAnimationFrame(animate);
      torus.rotation.x += 0.005;
      torus.rotation.y += 0.008;
      
      // Dynamic mouse response
      torus.position.x += (mouseX * 1.5 - torus.position.x) * 0.05;
      torus.position.y += (mouseY * 1.5 - torus.position.y) * 0.05;

      renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
      camera.aspect = window.innerWidth / window.innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(window.innerWidth, window.innerHeight);
    });

    // --- 2. WEB AUDIO SOUND EFFECTS ---
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    
    function playSound(type) {
      if (audioCtx.state === 'suspended') audioCtx.resume();
      const osc = audioCtx.createOscillator();
      const gain = audioCtx.createGain();
      osc.connect(gain);
      gain.connect(audioCtx.destination);

      if (type === 'hover') {
        osc.type = 'sine';
        osc.frequency.setValueAtTime(400, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(800, audioCtx.currentTime + 0.05);
        gain.gain.setValueAtTime(0.03, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.05);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.05);
      } else {
        osc.type = 'triangle';
        osc.frequency.setValueAtTime(520, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(260, audioCtx.currentTime + 0.1);
        gain.gain.setValueAtTime(0.08, audioCtx.currentTime);
        gain.gain.exponentialRampToValueAtTime(0.001, audioCtx.currentTime + 0.1);
        osc.start();
        osc.stop(audioCtx.currentTime + 0.1);
      }
    }

    document.querySelectorAll('.glass-card, .sound-btn').forEach(el => {
      el.addEventListener('mouseenter', () => playSound('hover'));
      el.addEventListener('click', () => playSound('click'));
    });
  </script>
</body>
</html>
