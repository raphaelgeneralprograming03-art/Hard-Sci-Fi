
<html lang="en" class="dark">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quantum Vacuum & Relativistic Ship Simulation</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        cyber: {
                            cyan: '#00f0ff',
                            gold: '#ffd700',
                            magenta: '#ff007f',
                            dark: '#030712',
                            panel: '#0b0f19'
                        }
                    }
                }
            }
        }
    </script>
    <!-- Google Fonts: Orbitron & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Orbitron:wght@400;600;800;900&display=swap" rel="stylesheet">
    <!-- FontAwesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #030712;
            color: #f3f4f6;
            overflow-x: hidden;
        }
        .font-orbitron {
            font-family: 'Orbitron', sans-serif;
        }
        .glass-panel {
            background: rgba(11, 15, 25, 0.85);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(0, 240, 255, 0.15);
            box-shadow: 0 0 25px rgba(0, 0, 0, 0.5), inset 0 0 15px rgba(0, 240, 255, 0.03);
        }
        .glow-text-cyan {
            text-shadow: 0 0 10px rgba(0, 240, 255, 0.6);
        }
        .glow-text-gold {
            text-shadow: 0 0 10px rgba(255, 215, 0, 0.6);
        }
        .glow-text-magenta {
            text-shadow: 0 0 10px rgba(255, 0, 127, 0.6);
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #030712;
        }
        ::-webkit-scrollbar-thumb {
            background: #1f2937;
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #374151;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col">

    <!-- Top Navigation Header -->
    <header class="glass-panel border-b border-cyan-500/20 px-6 py-4 flex flex-wrap justify-between items-center z-20">
        <div class="flex items-center space-x-3">
            <div class="w-10 h-10 rounded-lg bg-cyan-500/10 border border-cyan-400/40 flex items-center justify-center text-cyan-400">
                <i class="fa-solid fa-atom text-xl animate-spin" style="animation-duration: 10s;"></i>
            </div>
            <div>
                <h1 class="font-orbitron font-extrabold text-xl tracking-wider text-white glow-text-cyan">CHRONOS-V</h1>
                <p class="text-xs text-cyan-400/70 tracking-widest uppercase">Quantum Vacuum Extraction & Frame-Dragging Engine</p>
            </div>
        </div>
        <div class="flex items-center space-x-4 mt-3 md:mt-0">
            <button id="info-btn" class="px-4 py-2 rounded-lg bg-slate-800/80 hover:bg-slate-700 border border-cyan-500/30 text-cyan-300 text-sm font-orbitron transition flex items-center space-x-2">
                <i class="fa-solid fa-book-atlas"></i>
                <span>Physics Codex</span>
            </button>
            <div class="flex items-center space-x-2 bg-slate-900/90 border border-slate-700 px-3 py-1.5 rounded-lg">
                <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
                <span class="text-xs font-orbitron text-slate-300">SYSTEM: ONLINE</span>
            </div>
        </div>
    </header>

    <!-- Main Grid Container -->
    <div class="flex-1 grid grid-cols-1 lg:grid-cols-12 gap-4 p-4 max-w-[1800px] w-full mx-auto">

        <!-- Simulation Canvas Panel (Cols 1-8) -->
        <div class="lg:col-span-8 glass-panel rounded-2xl p-4 flex flex-col relative overflow-hidden min-h-[500px] lg:min-h-[700px]">
            <div class="flex justify-between items-center mb-3 z-10">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-satellite text-cyan-400"></i>
                    <h2 class="font-orbitron font-semibold text-sm tracking-wider text-cyan-300">SPACETIME & ORBITAL TELEMETRY</h2>
                </div>
                <div class="flex items-center space-x-2">
                    <button id="pause-btn" class="px-3 py-1 bg-cyan-950/60 hover:bg-cyan-900/80 border border-cyan-500/40 text-cyan-300 rounded text-xs font-orbitron transition">
                        <i class="fa-solid fa-pause mr-1"></i> Pause
                    </button>
                    <button id="reset-btn" class="px-3 py-1 bg-slate-800 hover:bg-slate-700 border border-slate-600 text-slate-300 rounded text-xs font-orbitron transition">
                        <i class="fa-solid fa-rotate-right mr-1"></i> Reset
                    </button>
                </div>
            </div>

            <!-- Canvas Wrapper -->
            <div class="flex-1 relative rounded-xl overflow-hidden border border-cyan-500/10 bg-black/40 flex items-center justify-center">
                <canvas id="simCanvas" class="w-full h-full block cursor-crosshair"></canvas>
                <!-- Overlay Legends -->
                <div class="absolute bottom-3 left-3 pointer-events-none bg-slate-950/80 backdrop-blur-md p-3 rounded-xl border border-slate-800 text-xs space-y-1 text-slate-300">
                    <div class="flex items-center space-x-2">
                        <span class="w-3 h-3 rounded-full bg-cyan-400 inline-block shadow-[0_0_8px_#00f0ff]"></span>
                        <span>Relativistic Ship ($v \to c$)</span>
                    </div>
                    <div class="flex items-center space-x-2">
                        <span class="w-3 h-3 rounded-full bg-magenta-500 inline-block shadow-[0_0_8px_#ff007f]" style="background-color: #ff007f;"></span>
                        <span>Synchrotron Radiation Loss</span>
                    </div>
                    <div class="flex items-center space-x-2">
                        <span class="w-3 h-3 rounded-full bg-amber-400 inline-block shadow-[0_0_8px_#ffd700]"></span>
                        <span>MHD Harvested Vacuum Energy</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- Telemetry & Controls Panel (Cols 9-12) -->
        <div class="lg:col-span-4 flex flex-col space-y-4">
            
            <!-- HUD Readouts Card -->
            <div class="glass-panel rounded-2xl p-4 space-y-4">
                <h3 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-400 flex items-center space-x-2">
                    <i class="fa-solid fa-gauge-high"></i>
                    <span>RELATIVISTIC METRICS</span>
                </h3>

                <div class="grid grid-cols-2 gap-3">
                    <div class="bg-slate-950/60 p-3 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">VELOCITY ($v/c$)</div>
                        <div id="val-vc" class="text-lg font-orbitron font-bold text-cyan-300 glow-text-cyan">0.950c</div>
                    </div>
                    <div class="bg-slate-950/60 p-3 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">LORENTZ FACTOR ($\gamma$)</div>
                        <div id="val-gamma" class="text-lg font-orbitron font-bold text-cyan-300">3.20</div>
                    </div>
                    <div class="bg-slate-950/60 p-3 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">UNRUH TEMP ($T_U$)</div>
                        <div id="val-temp" class="text-base font-orbitron font-bold text-amber-300 glow-text-gold">1.42 MK</div>
                    </div>
                    <div class="bg-slate-950/60 p-3 rounded-xl border border-cyan-500/10">
                        <div class="text-[10px] text-slate-400 font-orbitron">CENTRIPETAL ACCEL</div>
                        <div id="val-accel" class="text-base font-orbitron font-bold text-magenta-400 glow-text-magenta">4.8e17 $g$</div>
                    </div>
                </div>

                <!-- Energy Balance Meter -->
                <div class="bg-slate-950/80 p-3.5 rounded-xl border border-slate-800 space-y-2">
                    <div class="flex justify-between items-center text-xs font-orbitron">
                        <span class="text-slate-300">POWER BALANCE</span>
                        <span id="net-power-label" class="text-emerald-400 font-bold">+142.8 TW</span>
                    </div>
                    <div class="space-y-1.5 text-[11px]">
                        <div class="flex justify-between text-slate-400">
                            <span>MHD Harvested Vacuum:</span>
                            <span id="harvest-power" class="text-amber-300 font-orbitron">320.5 TW</span>
                        </div>
                        <div class="flex justify-between text-slate-400">
                            <span>Synchrotron Radiation Loss:</span>
                            <span id="sync-loss" class="text-magenta-400 font-orbitron">177.7 TW</span>
                        </div>
                    </div>
                    <div class="w-full bg-slate-800 h-2 rounded-full overflow-hidden flex">
                        <div id="bar-harvest" class="bg-amber-400 h-full transition-all duration-200" style="width: 64%;"></div>
                        <div id="bar-loss" class="bg-magenta-500 h-full transition-all duration-200" style="width: 36%;"></div>
                    </div>
                </div>
            </div>

            <!-- Interactive Controls Card -->
            <div class="glass-panel rounded-2xl p-4 space-y-4">
                <h3 class="font-orbitron font-semibold text-xs tracking-wider text-cyan-400 flex items-center space-x-2">
                    <i class="fa-solid fa-sliders"></i>
                    <span>SIMULATION PARAMETERS</span>
                </h3>

                <!-- Velocity Slider -->
                <div class="space-y-1.5">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">Orbit Velocity ($v/c$)</span>
                        <span id="slider-vc-val" class="text-cyan-400 font-bold">0.950c</span>
                    </div>
                    <input id="range-vc" type="range" min="0.100" max="0.999" step="0.001" value="0.950" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-cyan-400">
                    <div class="flex justify-between text-[10px] text-slate-500 font-orbitron">
                        <span>0.1c (Sub-relativistic)</span>
                        <span>0.999c (Ultra-relativistic)</span>
                    </div>
                </div>

                <!-- MHD Field Strength Slider -->
                <div class="space-y-1.5">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">MHD Capture Efficiency</span>
                        <span id="slider-mhd-val" class="text-amber-400 font-bold">85%</span>
                    </div>
                    <input id="range-mhd" type="range" min="10" max="100" step="1" value="85" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-amber-400">
                </div>

                <!-- Spacetime Shear Slider -->
                <div class="space-y-1.5">
                    <div class="flex justify-between text-xs font-orbitron">
                        <span class="text-slate-300">Spacetime Shear (Lense-Thirring)</span>
                        <span id="slider-shear-val" class="text-magenta-400 font-bold">7.5 TΩ</span>
                    </div>
                    <input id="range-shear" type="range" min="1.0" max="15.0" step="0.1" value="7.5" 
                           class="w-full h-2 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-magenta-500">
                </div>

                <!-- Quick Presets -->
                <div class="pt-2 border-t border-slate-800/80">
                    <div class="text-[10px] text-slate-400 font-orbitron mb-2">OPERATIONAL PRESETS</div>
                    <div class="grid grid-cols-3 gap-2">
                        <button id="preset-stable" class="px-2 py-1.5 rounded bg-slate-800 hover:bg-slate-700 border border-slate-700 text-cyan-300 text-[10px] font-orbitron transition">Stable Net+</button>
                        <button id="preset-unruh" class="px-2 py-1.5 rounded bg-slate-800 hover:bg-slate-700 border border-slate-700 text-amber-300 text-[10px] font-orbitron transition">Max Unruh</button>
                        <button id="preset-overload" class="px-2 py-1.5 rounded bg-slate-800 hover:bg-slate-700 border border-slate-700 text-magenta-400 text-[10px] font-orbitron transition">Sync Overload</button>
                    </div>
                </div>
            </div>

        </div>

    </div>

    <!-- Physics Codex Modal -->
    <div id="info-modal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md hidden p-4">
        <div class="glass-panel rounded-2xl max-w-2xl w-full p-6 space-y-4 max-h-[85vh] overflow-y-auto border border-cyan-500/40 relative">
            <div class="flex justify-between items-center border-b border-cyan-500/20 pb-3">
                <div class="flex items-center space-x-2 text-cyan-400 font-orbitron font-bold text-lg">
                    <i class="fa-solid fa-book-atlas"></i>
                    <span>QUANTUM VACUUM PHYSICS CODEX</span>
                </div>
                <button id="close-modal" class="text-slate-400 hover:text-white text-xl p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            
            <div class="space-y-4 text-sm text-slate-300 leading-relaxed">
                <div>
                    <h4 class="font-orbitron font-bold text-cyan-300 mb-1">1. The Dynamic Effect (Unruh & Synchrotron Radiation)</h4>
                    <p>According to special relativity, an object with mass can approach arbitrarily close to light speed ($v \to c$). When forced into rapid circular motion at relativistic velocities, the centripetal acceleration is monumental. Through the <strong>Unruh Effect</strong>, an accelerating observer perceives the quantum vacuum not as empty space, but as a thermal bath filled with real particles (photons and quanta). However, accelerated charges or energy packets experience <strong>Synchrotron Radiation</strong> losses, radiating energy violently outward like a cosmic radiator.</p>
                </div>

                <div>
                    <h4 class="font-orbitron font-bold text-amber-300 mb-1">2. Spacetime Shear & Lense-Thirring Frame-Dragging</h4>
                    <p>To overcome pure radiative loss and extract usable energy, the ship does not merely coast in empty space. It generates a localized rotating mass-energy field that creates a severe spacetime shear (the <strong>Lense-Thirring effect</strong>). The ship acts like a blender agitator stirring the metric tensor fabric of spacetime. This violent quantum-scale churning excites vacuum fluctuations, converting virtual particle-antiparticle pairs into real energetic particles before they annihilate.</p>
                </div>

                <div>
                    <h4 class="font-orbitron font-bold text-magenta-400 mb-1">3. MHD Reactor Energy Harvesting</h4>
                    <p>The onboard Magnetohydrodynamic (MHD) reactor captures the high-energy plasma stream generated by the vacuum excitation zone. By balancing the <strong>MHD Capture Efficiency</strong> against the exponential <strong>Synchrotron Radiation Loss</strong> ($\propto \gamma^4 a_c^2$), the system achieves a positive Net Power Balance, sustaining warp-drive level energy extraction.</p>
                </div>
            </div>

            <div class="pt-4 border-t border-slate-800 flex justify-end">
                <button id="close-modal-btn" class="px-5 py-2 bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-orbitron font-bold rounded-lg text-xs transition">
                    Acknowledge & Return
                </button>
            </div>
        </div>
    </div>

    <!-- Simulation & Animation Engine -->
    <script>
        window.addEventListener('DOMContentLoaded', () => {
            const canvas = document.getElementById('simCanvas');
            const ctx = canvas.getContext('2d');

            // UI Elements
            const vcSlider = document.getElementById('range-vc');
            const vcValLabel = document.getElementById('slider-vc-val');
            const vcReadout = document.getElementById('val-vc');
            const gammaReadout = document.getElementById('val-gamma');
            const tempReadout = document.getElementById('val-temp');
            const accelReadout = document.getElementById('val-accel');

            const mhdSlider = document.getElementById('range-mhd');
            const mhdValLabel = document.getElementById('slider-mhd-val');
            const shearSlider = document.getElementById('range-shear');
            const shearValLabel = document.getElementById('slider-shear-val');

            const harvestPowerEl = document.getElementById('harvest-power');
            const syncLossEl = document.getElementById('sync-loss');
            const netPowerLabel = document.getElementById('net-power-label');
            const barHarvest = document.getElementById('bar-harvest');
            const barLoss = document.getElementById('bar-loss');

            const pauseBtn = document.getElementById('pause-btn');
            const resetBtn = document.getElementById('reset-btn');
            const infoBtn = document.getElementById('info-btn');
            const infoModal = document.getElementById('info-modal');
            const closeModal = document.getElementById('close-modal');
            const closeModalBtn = document.getElementById('close-modal-btn');

            const presetStable = document.getElementById('preset-stable');
            const presetUnruh = document.getElementById('preset-unruh');
            const presetOverload = document.getElementById('preset-overload');

            // Simulation State
            let isPaused = false;
            let time = 0;
            let shipAngle = 0;
            
            // Parameters
            let vc = parseFloat(vcSlider.value);
            let mhdEfficiency = parseFloat(mhdSlider.value) / 100;
            let shearIntensity = parseFloat(shearSlider.value);

            // Particle arrays
            const vacuumParticles = [];
            const synchrotronSparks = [];
            const mhdStreams = [];
            const numVacuumParticles = 120;

            // Resize Canvas to Container
            function resizeCanvas() {
                const rect = canvas.parentElement.getBoundingClientRect();
                canvas.width = rect.width * window.devicePixelRatio;
                canvas.height = rect.height * window.devicePixelRatio;
                ctx.scale(window.devicePixelRatio, window.devicePixelRatio);
            }
            window.addEventListener('resize', resizeCanvas);
            resizeCanvas();

            // Initialize Vacuum Quantum Fluctuations
            for (let i = 0; i < numVacuumParticles; i++) {
                vacuumParticles.push({
                    x: (Math.random() - 0.5) * 800,
                    y: (Math.random() - 0.5) * 800,
                    vx: (Math.random() - 0.5) * 0.5,
                    vy: (Math.random() - 0.5) * 0.5,
                    life: Math.random() * 100,
                    maxLife: 100 + Math.random() * 100,
                    excited: false
                });
            }

            // Event Listeners for UI
            vcSlider.addEventListener('input', (e) => {
                vc = parseFloat(e.target.value);
                vcValLabel.textContent = vc.toFixed(3) + 'c';
            });

            mhdSlider.addEventListener('input', (e) => {
                mhdEfficiency = parseFloat(e.target.value) / 100;
                mhdValLabel.textContent = e.target.value + '%';
            });

            shearSlider.addEventListener('input', (e) => {
                shearIntensity = parseFloat(e.target.value);
                shearValLabel.textContent = shearIntensity.toFixed(1) + ' TΩ';
            });

            pauseBtn.addEventListener('click', () => {
                isPaused = !isPaused;
                pauseBtn.innerHTML = isPaused ? '<i class="fa-solid fa-play mr-1"></i> Resume' : '<i class="fa-solid fa-pause mr-1"></i> Pause';
            });

            resetBtn.addEventListener('click', () => {
                vc = 0.950;
                vcSlider.value = vc;
                vcValLabel.textContent = '0.950c';
                mhdEfficiency = 0.85;
                mhdSlider.value = 85;
                mhdValLabel.textContent = '85%';
                shearIntensity = 7.5;
                shearSlider.value = 7.5;
                shearValLabel.textContent = '7.5 TΩ';
                time = 0;
            });

            // Presets
            presetStable.addEventListener('click', () => {
                vc = 0.850; vcSlider.value = vc; vcValLabel.textContent = '0.850c';
                mhdEfficiency = 0.95; mhdSlider.value = 95; mhdValLabel.textContent = '95%';
                shearIntensity = 5.0; shearSlider.value = 5.0; shearValLabel.textContent = '5.0 TΩ';
            });

            presetUnruh.addEventListener('click', () => {
                vc = 0.985; vcSlider.value = vc; vcValLabel.textContent = '0.985c';
                mhdEfficiency = 0.70; mhdSlider.value = 70; mhdValLabel.textContent = '70%';
                shearIntensity = 12.0; shearSlider.value = 12.0; shearValLabel.textContent = '12.0 TΩ';
            });

            presetOverload.addEventListener('click', () => {
                vc = 0.999; vcSlider.value = vc; vcValLabel.textContent = '0.999c';
                mhdEfficiency = 0.50; mhdSlider.value = 50; mhdValLabel.textContent = '50%';
                shearIntensity = 15.0; shearSlider.value = 15.0; shearValLabel.textContent = '15.0 TΩ';
            });

            // Modal Controls
            infoBtn.addEventListener('click', () => infoModal.classList.remove('hidden'));
            closeModal.addEventListener('click', () => infoModal.classList.add('hidden'));
            closeModalBtn.addEventListener('click', () => infoModal.classList.add('hidden'));

            function updatePhysicsAndHUD() {
                // Lorentz factor gamma = 1 / sqrt(1 - v^2/c^2)
                const gamma = 1.0 / Math.sqrt(Math.max(0.0001, 1.0 - (vc * vc)));
                
                // Orbital radius (logical pixels)
                const R = 150;
                // Centripetal acceleration scales with gamma^2 * v^2 / R
                const accel = (gamma * gamma * vc * vc * 5000) / R;
                
                // Unruh Temperature proportional to acceleration
                const unruhTemp = accel * 2.95e-14; // in MK (Mega Kelvin)

                // Energy equations (arbitrary scifi scales scaled for visual dynamic)
                const syncLoss = Math.pow(gamma, 3.2) * (vc * 45) * (shearIntensity * 0.4);
                const harvestPower = syncLoss * mhdEfficiency * (shearIntensity * 0.22) * (1.1 + vc);
                const netPower = harvestPower - syncLoss;

                // Update HUD Text
                vcReadout.textContent = vc.toFixed(3) + 'c';
                gammaReadout.textContent = gamma.toFixed(2);
                tempReadout.textContent = unruhTemp > 1000 ? (unruhTemp / 1000).toFixed(2) + ' GK' : unruhTemp.toFixed(1) + ' MK';
                accelReadout.textContent = (accel / 1e15).toFixed(1) + 'e15 g';

                harvestPowerEl.textContent = harvestPower.toFixed(1) + ' TW';
                syncLossEl.textContent = syncLoss.toFixed(1) + ' TW';
                
                netPowerLabel.textContent = (netPower >= 0 ? '+' : '') + netPower.toFixed(1) + ' TW';
                netPowerLabel.className = netPower >= 0 ? 'text-emerald-400 font-bold font-orbitron' : 'text-rose-500 font-bold font-orbitron';

                const totalEnergy = harvestPower + syncLoss;
                const harvestPct = Math.min(100, Math.max(0, (harvestPower / totalEnergy) * 100));
                const lossPct = 100 - harvestPct;
                barHarvest.style.width = harvestPct + '%';
                barLoss.style.width = lossPct + '%';

                return { gamma, R, accel, netPower };
            }

            // Main Animation Loop
            function animate() {
                const width = canvas.parentElement.clientWidth;
                const height = canvas.parentElement.clientHeight;

                ctx.clearRect(0, 0, width, height);

                const centerX = width / 2;
                const centerY = height / 2;

                const physics = updatePhysicsAndHUD();
                const gamma = physics.gamma;
                const R = physics.R;

                if (!isPaused) {
                    // Angular speed proportional to relativistic velocity
                    shipAngle += (vc * 0.04);
                }

                // 1. Render Spacetime Vortex & Lense-Thirring Grid
                ctx.save();
                ctx.translate(centerX, centerY);
                
                const gridSpacing = 40;
                const maxRadius = Math.max(width, height);
                
                ctx.lineWidth = 1;
                for (let r = gridSpacing; r < maxRadius; r += gridSpacing) {
                    ctx.beginPath();
                    // Warp grid based on shear intensity and time (frame dragging vortex effect)
                    const warpFactor = (shearIntensity * 50) / (r + 50);
                    for (let a = 0; a < Math.PI * 2; a += 0.1) {
                        const twistedA = a + Math.sin(a * 4 - time * 0.05) * warpFactor * 0.1;
                        const currR = r + Math.sin(time * 0.03 + r * 0.05) * (shearIntensity * 2);
                        const gx = Math.cos(twistedA) * currR;
                        const gy = Math.sin(twistedA) * currR;
                        if (a === 0) ctx.moveTo(gx, gy);
                        else ctx.lineTo(gx, gy);
                    }
                    ctx.closePath();
                    ctx.strokeStyle = `rgba(0, 240, 255, ${Math.max(0.03, 0.12 - (r / maxRadius) * 0.08)})`;
                    ctx.stroke();
                }

                // Central Quantum Singularity / Vortex Core
                const coreGradient = ctx.createRadialGradient(0, 0, 5, 0, 0, 60);
                coreGradient.addColorStop(0, 'rgba(0, 240, 255, 0.8)');
                coreGradient.addColorStop(0.4, 'rgba(255, 0, 127, 0.3)');
                coreGradient.addColorStop(1, 'transparent');
                ctx.fillStyle = coreGradient;
                ctx.beginPath();
                ctx.arc(0, 0, 60, 0, Math.PI * 2);
                ctx.fill();

                // 2. Render Quantum Vacuum Fluctuations & Real Particle Excitation
                vacuumParticles.forEach(p => {
                    if (!isPaused) {
                        p.x += p.vx;
                        p.y += p.vy;
                        p.life++;
                        if (p.life > p.maxLife || Math.abs(p.x) > width / 2 || Math.abs(p.y) > height / 2) {
                            p.x = (Math.random() - 0.5) * width * 0.8;
                            p.y = (Math.random() - 0.5) * height * 0.8;
                            p.life = 0;
                            p.excited = false;
                        }
                    }

                    // Check distance to ship orbit
                    const dx = p.x - Math.cos(shipAngle) * R;
                    const dy = p.y - Math.sin(shipAngle) * R;
                    const distToShip = Math.sqrt(dx * dx + dy * dy);

                    if (distToShip < 60) {
                        p.excited = true;
                    }

                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.excited ? 2.5 : 1.2, 0, Math.PI * 2);
                    ctx.fillStyle = p.excited ? 'rgba(255, 215, 0, 0.9)' : 'rgba(0, 240, 255, 0.3)';
                    ctx.shadowColor = p.excited ? '#ffd700' : '#00f0ff';
                    ctx.shadowBlur = p.excited ? 8 : 2;
                    ctx.fill();
                    ctx.shadowBlur = 0;
                });

                // 3. Calculate Ship Position
                const shipX = Math.cos(shipAngle) * R;
                const shipY = Math.sin(shipAngle) * R;

                // Emit synchrotron radiation sparks outward from ship
                if (!isPaused && Math.random() < 0.6) {
                    const ejectAngle = shipAngle + Math.PI / 2 + (Math.random() - 0.5) * 0.5;
                    synchrotronSparks.push({
                        x: shipX,
                        y: shipY,
                        vx: Math.cos(ejectAngle) * (4 + vc * 6),
                        vy: Math.sin(ejectAngle) * (4 + vc * 6),
                        life: 0,
                        maxLife: 30 + Math.random() * 20
                    });
                }

                // Render Synchrotron Radiation Trail / Sparks
                for (let i = synchrotronSparks.length - 1; i >= 0; i--) {
                    const s = synchrotronSparks[i];
                    if (!isPaused) {
                        s.x += s.vx;
                        s.y += s.vy;
                        s.life++;
                    }
                    const alpha = 1.0 - (s.life / s.maxLife);
                    ctx.beginPath();
                    ctx.arc(s.x, s.y, 2, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(255, 0, 127, ${alpha})`;
                    ctx.shadowColor = '#ff007f';
                    ctx.shadowBlur = 6;
                    ctx.fill();
                    ctx.shadowBlur = 0;

                    if (s.life >= s.maxLife) {
                        synchrotronSparks.splice(i, 1);
                    }
                }

                // Render MHD Energy Extraction Beams connecting Ship to Core
                ctx.beginPath();
                ctx.moveTo(0, 0);
                ctx.lineTo(shipX, shipY);
                ctx.strokeStyle = 'rgba(255, 215, 0, 0.4)';
                ctx.lineWidth = 2;
                ctx.setLineDash([4, 4]);
                ctx.stroke();
                ctx.setLineDash([]);

                // Render Relativistic Ship
                ctx.save();
                ctx.translate(shipX, shipY);
                ctx.rotate(shipAngle + Math.PI / 2);

                // Ship Glow Aura
                const shipGlow = ctx.createRadialGradient(0, 0, 0, 0, 0, 25);
                shipGlow.addColorStop(0, 'rgba(0, 240, 255, 0.8)');
                shipGlow.addColorStop(1, 'transparent');
                ctx.fillStyle = shipGlow;
                ctx.beginPath();
                ctx.arc(0, 0, 25, 0, Math.PI * 2);
                ctx.fill();

                // Ship Hull (Sci-fi Triangle / Dart)
                ctx.beginPath();
                ctx.moveTo(0, -14);
                ctx.lineTo(8, 10);
                ctx.lineTo(0, 6);
                ctx.lineTo(-8, 10);
                ctx.closePath();
                ctx.fillStyle = '#ffffff';
                ctx.shadowColor = '#00f0ff';
                ctx.shadowBlur = 12;
                ctx.fill();
                ctx.shadowBlur = 0;

                // Ion Thruster Plume
                ctx.beginPath();
                ctx.moveTo(-4, 10);
                ctx.lineTo(0, 22 + vc * 10);
                ctx.lineTo(4, 10);
                ctx.closePath();
                ctx.fillStyle = '#00f0ff';
                ctx.fill();

                ctx.restore();
                ctx.restore();

                time += 1;
                requestAnimationFrame(animate);
            }

            requestAnimationFrame(animate);
        });
    </script>
</body>
</html>
