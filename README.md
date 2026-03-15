# Virus-

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LOVE_LETTER_FOR_YOU.txt.html</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }
        .heart {
            position: absolute;
            color: #ff4d4d;
            font-size: 2rem;
            pointer-events: none;
            z-index: 50;
            animation: float linear forwards;
        }
        .glitch {
            text-shadow: 2px 0 #ff00c1, -2px 0 #00fff9;
            animation: glitch-anim 0.2s infinite;
        }
        @keyframes glitch-anim {
            0% { transform: translate(0); }
            20% { transform: translate(-2px, 2px); }
            40% { transform: translate(-2px, -2px); }
            60% { transform: translate(2px, 2px); }
            80% { transform: translate(2px, -2px); }
            100% { transform: translate(0); }
        }
        #terminal {
            font-family: 'Courier New', Courier, monospace;
        }
        .scanline {
            width: 100%;
            height: 2px;
            background: rgba(255, 0, 0, 0.1);
            position: absolute;
            top: 0;
            left: 0;
            pointer-events: none;
            animation: scan 4s linear infinite;
        }
        @keyframes scan {
            0% { top: 0; }
            100% { top: 100%; }
        }
    </style>
</head>
<body class="bg-black text-red-500 min-h-screen flex flex-col items-center justify-center overflow-hidden selection:bg-red-900 selection:text-white">
    <div class="scanline"></div>

    <!-- Initial "Email" Interface -->
    <div id="email-view" class="bg-zinc-900 p-8 rounded-lg border border-red-500 shadow-2xl max-w-md w-full mx-4 transition-all duration-500 z-10">
        <div class="flex items-center gap-2 mb-4 border-b border-red-800 pb-2">
            <div class="w-3 h-3 rounded-full bg-red-500"></div>
            <h1 class="text-xl font-bold">1 New Urgent Message</h1>
        </div>
        <div class="space-y-2 mb-6 text-zinc-300">
            <p><span class="text-red-500 font-bold">From:</span> internal_system_service@vault.mail</p>
            <p><span class="text-red-500 font-bold">Subject:</span> [ENCRYPTED] LOVE-LETTER-FOR-YOU</p>
            <p class="italic text-sm mt-4 text-zinc-500">"This message contains a protected attachment. Click below to decrypt and view."</p>
        </div>
        <button id="open-btn" class="w-full bg-red-600 hover:bg-red-700 text-white font-bold py-4 rounded shadow-lg shadow-red-900/50 transition-all uppercase tracking-widest animate-pulse active:scale-95">
            Decrypt Attachment
        </button>
    </div>

    <!-- "Infection" Simulation -->
    <div id="virus-view" class="hidden fixed inset-0 flex flex-col items-center justify-center bg-black p-4">
        <div id="terminal" class="w-full max-w-3xl p-8 bg-black/80 border border-red-900 rounded shadow-inner text-sm md:text-base overflow-y-auto max-h-screen">
            <!-- Content added via JS -->
        </div>
    </div>

    <script>
        const emailView = document.getElementById('email-view');
        const virusView = document.getElementById('virus-view');
        const openBtn = document.getElementById('open-btn');
        const terminal = document.getElementById('terminal');

        // Gather real browser data to "scare" the user
        const userData = {
            platform: navigator.platform,
            agent: navigator.userAgent.split(')')[0] + ')',
            cores: navigator.hardwareConcurrency || 'Unknown',
            screen: `${window.screen.width}x${window.screen.height}`,
            lang: navigator.language,
            time: new Date().toLocaleString()
        };

        const logs = [
            "> INITIALIZING ILOVEYOU.vbs.exe...",
            "> BYPASSING SYSTEM PERMISSIONS...",
            "> ESCALATING PRIVILEGES: [ADMIN]",
            "> ACCESSING LOCAL HARD DRIVE (C:/)...",
            "> [!] FIREWALL BREACHED SUCCESSFULLY.",
            "> GATHERING TARGET SPECIFICATIONS...",
            `> TARGET_OS: ${userData.platform}`,
            `> TARGET_HARDWARE: ${userData.cores} CPU CORES DETECTED`,
            `> DISPLAY_RESOLUTION: ${userData.screen}`,
            `> SYSTEM_TIME: ${userData.time}`,
            `> BROWSER_FINGERPRINT: ${userData.agent}`,
            "> LOCATING PRIVATE_PHOTOS & CHATS...",
            "> PACKAGING SENSITIVE DATA...",
            "> UPLOADING TO REMOTE SERVER [45.128.2.1]...",
            "> OVERWRITING SYSTEM_FILES...",
            "> ILOVEYOU PROTOCOL: 100% COMPLETE."
        ];

        function createHeart() {
            const heart = document.createElement('div');
            heart.innerHTML = '❤️';
            heart.className = 'heart';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 2 + 1) + 's';
            heart.style.fontSize = (Math.random() * 30 + 10) + 'px';
            document.body.appendChild(heart);
            
            setTimeout(() => heart.remove(), 3000);
        }

        async function runSimulation() {
            emailView.classList.add('opacity-0', 'scale-110', 'rotate-12');
            setTimeout(() => {
                emailView.style.display = 'none';
                virusView.classList.remove('hidden');
                startTerminal();
            }, 500);
        }

        async function startTerminal() {
            for (let i = 0; i < logs.length; i++) {
                const p = document.createElement('p');
                p.className = 'mb-1 leading-relaxed opacity-0 transition-opacity duration-100';
                terminal.appendChild(p);
                
                terminal.scrollTop = terminal.scrollHeight;
                
                for (let char of logs[i]) {
                    p.innerHTML += char;
                    p.classList.remove('opacity-0');
                    await new Promise(r => setTimeout(r, 15));
                }
                
                if (logs[i].includes('!') || logs[i].includes('SENSITIVE')) {
                    p.classList.add('text-red-400', 'font-bold', 'glitch');
                }
                if (logs[i].includes('TARGET_') || logs[i].includes('SYSTEM_')) {
                    p.classList.add('text-green-400');
                }
                
                await new Promise(r => setTimeout(r, 250));
            }

            // Start the heart storm
            const heartInterval = setInterval(createHeart, 80);
            
            // Final Scare Message (Reboot button removed)
            const finalMsg = document.createElement('div');
            finalMsg.className = 'mt-12 text-center p-6 border-4 border-double border-red-600 bg-red-950/20';
            finalMsg.innerHTML = `
                <h2 class="text-5xl font-black text-white uppercase tracking-tighter glitch mb-2">YOU'VE BEEN INFECTED!</h2>
                <p class="text-red-400 text-xl font-bold italic mb-6">"All your files belong to me now... and so does your heart."</p>
                <p class="text-zinc-600 text-xs mb-8">Data wipe in progress: 34%... 56%... 89%...</p>
                
                <div class="flex flex-col gap-4">
                    <p class="text-white text-sm animate-pulse">SYSTEM CRITICAL ERROR: RECOVERY UNAVAILABLE</p>
                    <p class="text-[10px] text-zinc-700 uppercase tracking-[0.2em]">Just kidding, stay safe! :)</p>
                </div>
            `;
            terminal.appendChild(finalMsg);
            terminal.scrollTop = terminal.scrollHeight;
        }

        openBtn.addEventListener('click', runSimulation);
    </script>
</body>
</html>
