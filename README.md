<!DOCTYPE html>
<html>
<head>
    <title>Paixão por 34 Dias - Reprodutor</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-user-select: none;
            user-select: none;
            -webkit-tap-highlight-color: transparent;
        }
        
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: #000000;
            color: #ffffff;
            text-align: center;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }
        
        .container {
            width: 100%;
            max-width: 400px;
        }
        
        /* Título */
        .titulo {
            margin-bottom: 20px;
        }
        
        .titulo h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Container do vídeo */
        .video-container {
            width: 100%;
            background: #111;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            position: relative;
            margin-bottom: 20px;
        }
        
        /* Vídeo */
        video {
            width: 100%;
            height: auto;
            display: block;
            aspect-ratio: 9/16;
            object-fit: cover;
        }
        
        /* Controles */
        .video-controls {
            position: absolute;
            bottom: 20px;
            left: 0;
            right: 0;
            display: flex;
            justify-content: center;
            gap: 15px;
            z-index: 10;
        }
        
        .video-btn {
            background: rgba(0,0,0,0.7);
            border: 2px solid #ff6b6b;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            color: white;
            font-size: 1.2rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s;
            backdrop-filter: blur(5px);
        }
        
        .video-btn:hover {
            background: rgba(255,107,107,0.8);
            transform: scale(1.1);
        }
        
        /* Info do vídeo */
        .video-info {
            background: rgba(20, 20, 20, 0.8);
            border-radius: 10px;
            padding: 15px;
            margin-top: 15px;
            border: 1px solid #333;
        }
        
        .video-titulo {
            font-size: 1.1rem;
            font-weight: 600;
            color: #ff6b6b;
            margin-bottom: 5px;
        }
        
        .video-descricao {
            font-size: 0.9rem;
            color: #aaa;
            line-height: 1.4;
        }
        
        /* Loader */
        .video-loader {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: #ff6b6b;
            font-size: 1rem;
            background: rgba(0,0,0,0.8);
            padding: 15px 25px;
            border-radius: 20px;
            z-index: 20;
            display: none;
            border: 2px solid #ff6b6b;
            text-align: center;
        }
        
        .loader-spinner {
            width: 30px;
            height: 30px;
            border: 3px solid rgba(255,107,107,0.3);
            border-top: 3px solid #ff6b6b;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 10px;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Status */
        .status {
            margin-top: 15px;
            padding: 10px;
            background: rgba(20, 20, 20, 0.5);
            border-radius: 8px;
            font-size: 0.9rem;
            color: #aaa;
        }
        
        /* Lista de vídeos */
        .lista-videos {
            margin-top: 20px;
            background: rgba(20, 20, 20, 0.8);
            border-radius: 10px;
            padding: 15px;
            border: 1px solid #333;
            max-height: 200px;
            overflow-y: auto;
        }
        
        .lista-titulo {
            font-size: 1rem;
            font-weight: 600;
            color: #ff6b6b;
            margin-bottom: 10px;
        }
        
        .video-item {
            padding: 8px;
            margin: 5px 0;
            background: rgba(40, 40, 40, 0.5);
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s;
            font-size: 0.85rem;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .video-item:hover {
            background: rgba(255, 107, 107, 0.2);
            transform: translateX(5px);
        }
        
        .video-item.ativo {
            background: rgba(255, 107, 107, 0.3);
            border-left: 3px solid #ff6b6b;
        }
        
        .video-numero {
            background: #ff6b6b;
            color: white;
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: bold;
        }
        
        /* Responsivo */
        @media (max-width: 768px) {
            .container {
                max-width: 320px;
            }
            
            .titulo h1 {
                font-size: 1.6rem;
            }
            
            .lista-videos {
                max-height: 150px;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                max-width: 280px;
            }
            
            .titulo h1 {
                font-size: 1.4rem;
            }
            
            .video-btn {
                width: 40px;
                height: 40px;
                font-size: 1.1rem;
            }
            
            .lista-videos {
                max-height: 120px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- TÍTULO -->
        <div class="titulo">
            <h1>Paixão por 34 Dias</h1>
            <div style="font-size: 0.9rem; color: #666; margin-top: 5px;">Reprodutor de Vídeos</div>
        </div>
        
        <!-- VÍDEO -->
        <div class="video-container">
            <div class="video-loader" id="loader">
                <div class="loader-spinner"></div>
                <div>Carregando vídeo...</div>
            </div>
            
            <video id="video-player" playsinline autoplay muted>
                <source src="" type="video/mp4" id="video-source">
                Seu navegador não suporta vídeos HTML5.
            </video>
            
            <div class="video-controls">
                <button class="video-btn" id="play-btn">⏸</button>
                <button class="video-btn" id="mute-btn">🔇</button>
                <button class="video-btn" id="fullscreen-btn">⛶</button>
            </div>
        </div>
        
        <!-- INFO DO VÍDEO -->
        <div class="video-info">
            <div class="video-titulo" id="video-title">Vídeo 01</div>
            <div class="video-descricao" id="video-description">Dia 1 da sua jornada</div>
        </div>
        
        <!-- LISTA DE VÍDEOS -->
        <div class="lista-videos">
            <div class="lista-titulo">🎬 Todos os Vídeos</div>
            <div id="video-list">
                <!-- Lista gerada por JavaScript -->
            </div>
        </div>
        
        <!-- STATUS -->
        <div class="status" id="status">
            Pronto para reproduzir
        </div>
    </div>

    <script>
        // 🔧 CONFIGURAÇÃO COM SEUS DADOS
        const USER = "JiranhA003";
        const REPO = "Paixão-por-34-dias";
        const BASE_URL = `https://github.com/${USER}/${REPO}/raw/main/videos/`;
        
        // Lista de vídeos disponíveis
        const VIDEOS = [];
        
        // Gerar automaticamente os 34 vídeos
        for (let i = 1; i <= 34; i++) {
            const numero = i.toString().padStart(2, '0');
            VIDEOS.push({
                url: `${BASE_URL}Video${numero}.mp4`,
                title: `Dia ${i} - Transformação`,
                description: `Aula ${i} da jornada de 34 dias`,
                numero: i
            });
        }
        
        // Elementos do DOM
        const videoPlayer = document.getElementById('video-player');
        const videoSource = document.getElementById('video-source');
        const loader = document.getElementById('loader');
        const playBtn = document.getElementById('play-btn');
        const muteBtn = document.getElementById('mute-btn');
        const fullscreenBtn = document.getElementById('fullscreen-btn');
        const videoTitle = document.getElementById('video-title');
        const videoDescription = document.getElementById('video-description');
        const statusDiv = document.getElementById('status');
        const videoList = document.getElementById('video-list');
        
        // Estado do player
        let currentVideoIndex = 0;
        let isPlaying = true;
        let isMuted = true;
        
        // Inicializar
        function iniciarPlayer() {
            console.log("🎬 Iniciando reprodutor de vídeo...");
            console.log(`👤 Usuário: ${USER}`);
            console.log(`📁 Repositório: ${REPO}`);
            console.log(`🎥 ${VIDEOS.length} vídeos configurados`);
            
            // Criar lista de vídeos
            criarListaVideos();
            
            // Carregar primeiro vídeo
            carregarVideo(currentVideoIndex);
            
            // Configurar eventos
            configurarEventos();
        }
        
        // Criar lista de vídeos clicáveis
        function criarListaVideos() {
            videoList.innerHTML = '';
            
            VIDEOS.forEach((video, index) => {
                const item = document.createElement('div');
                item.className = 'video-item';
                if (index === currentVideoIndex) {
                    item.classList.add('ativo');
                }
                
                item.innerHTML = `
                    <div class="video-numero">${video.numero}</div>
                    <div style="flex: 1; text-align: left;">
                        <div style="font-weight: 500; color: #fff;">${video.title}</div>
                        <div style="font-size: 0.75rem; color: #888;">${video.description}</div>
                    </div>
                `;
                
                item.addEventListener('click', () => {
                    carregarVideo(index);
                });
                
                videoList.appendChild(item);
            });
        }
        
        // Carregar vídeo específico
        function carregarVideo(index) {
            if (index < 0 || index >= VIDEOS.length) return;
            
            currentVideoIndex = index;
            const video = VIDEOS[index];
            
            console.log(`📺 Carregando: ${video.title}`);
            
            // Atualizar UI
            videoTitle.textContent = video.title;
            videoDescription.textContent = video.description;
            
            // Mostrar loader
            loader.style.display = 'block';
            statusDiv.textContent = `Carregando vídeo ${video.numero}...`;
            
            // Atualizar lista
            document.querySelectorAll('.video-item').forEach((item, i) => {
                if (i === index) {
                    item.classList.add('ativo');
                } else {
                    item.classList.remove('ativo');
                }
            });
            
            // Tentar carregar o vídeo
            videoSource.src = video.url;
            videoPlayer.load();
            
            // Forçar recarga
            videoPlayer.onloadeddata = function() {
                console.log(`✅ Vídeo ${video.numero} carregado com sucesso!`);
                loader.style.display = 'none';
                
                // Tentar reproduzir automaticamente
                videoPlayer.play().then(() => {
                    isPlaying = true;
                    playBtn.textContent = '⏸';
                    statusDiv.textContent = `Reproduzindo: ${video.title}`;
                }).catch(error => {
                    console.log("❌ Autoplay bloqueado:", error);
                    playBtn.textContent = '▶';
                    isPlaying = false;
                    statusDiv.textContent = `Vídeo ${video.numero} carregado - Clique em ▶`;
                });
            };
            
            videoPlayer.onerror = function(e) {
                console.error(`❌ Erro ao carregar vídeo ${video.numero}:`, e);
                loader.innerHTML = `
                    <div style="color: #ff6b6b; font-size: 2rem;">❌</div>
                    <div>Erro ao carregar vídeo ${video.numero}</div>
                    <div style="font-size: 0.8rem; margin-top: 10px; color: #ff6b6b;">
                        URL: ${video.url}
                    </div>
                `;
                statusDiv.innerHTML = `
                    <div style="color: #ff6b6b;">
                        ❌ Erro: Vídeo ${video.numero} não encontrado
                    </div>
                    <div style="font-size: 0.8rem; margin-top: 5px;">
                        Verifique se o arquivo existe no GitHub
                    </div>
                `;
            };
        }
        
        // Configurar eventos
        function configurarEventos() {
            // Controle de play/pause
            playBtn.addEventListener('click', function() {
                if (isPlaying) {
                    videoPlayer.pause();
                    playBtn.textContent = '▶';
                    isPlaying = false;
                    statusDiv.textContent = "Pausado";
                } else {
                    videoPlayer.play().then(() => {
                        playBtn.textContent = '⏸';
                        isPlaying = true;
                        statusDiv.textContent = `Reproduzindo: ${videoTitle.textContent}`;
                    }).catch(error => {
                        console.log("Erro ao reproduzir:", error);
                        statusDiv.textContent = "Erro ao reproduzir";
                    });
                }
            });
            
            // Controle de mudo
            muteBtn.addEventListener('click', function() {
                if (isMuted) {
                    videoPlayer.muted = false;
                    muteBtn.textContent = '🔊';
                    isMuted = false;
                    statusDiv.textContent = "Som ativado";
                } else {
                    videoPlayer.muted = true;
                    muteBtn.textContent = '🔇';
                    isMuted = true;
                    statusDiv.textContent = "Som desativado";
                }
            });
            
            // Tela cheia
            fullscreenBtn.addEventListener('click', function() {
                const container = document.querySelector('.video-container');
                
                if (!document.fullscreenElement) {
                    if (container.requestFullscreen) {
                        container.requestFullscreen();
                    } else if (container.webkitRequestFullscreen) {
                        container.webkitRequestFullscreen();
                    } else if (container.msRequestFullscreen) {
                        container.msRequestFullscreen();
                    }
                    statusDiv.textContent = "Tela cheia ativada";
                } else {
                    if (document.exitFullscreen) {
                        document.exitFullscreen();
                    } else if (document.webkitExitFullscreen) {
                        document.webkitExitFullscreen();
                    } else if (document.msExitFullscreen) {
                        document.msExitFullscreen();
                    }
                    statusDiv.textContent = "Tela cheia desativada";
                }
            });
            
            // Quando o vídeo terminar
            videoPlayer.addEventListener('ended', function() {
                playBtn.textContent = '⏭️';
                isPlaying = false;
                statusDiv.textContent = "Vídeo finalizado";
                
                // Ir para o próximo vídeo após 2 segundos
                setTimeout(() => {
                    const nextIndex = (currentVideoIndex + 1) % VIDEOS.length;
                    carregarVideo(nextIndex);
                }, 2000);
            });
            
            // Eventos de teclado
            document.addEventListener('keydown', function(e) {
                switch(e.key) {
                    case ' ':
                    case 'Spacebar':
                        e.preventDefault();
                        playBtn.click();
                        break;
                    case 'm':
                    case 'M':
                        e.preventDefault();
                        muteBtn.click();
                        break;
                    case 'f':
                    case 'F':
                        e.preventDefault();
                        fullscreenBtn.click();
                        break;
                    case 'ArrowLeft':
                        e.preventDefault();
                        if (e.ctrlKey || e.metaKey) {
                            // Ctrl+← = vídeo anterior
                            const prevIndex = (currentVideoIndex - 1 + VIDEOS.length) % VIDEOS.length;
                            carregarVideo(prevIndex);
                        } else {
                            // ← = retroceder 10s
                            videoPlayer.currentTime -= 10;
                            statusDiv.textContent = "Retrocedeu 10 segundos";
                        }
                        break;
                    case 'ArrowRight':
                        e.preventDefault();
                        if (e.ctrlKey || e.metaKey) {
                            // Ctrl+→ = próximo vídeo
                            const nextIndex = (currentVideoIndex + 1) % VIDEOS.length;
                            carregarVideo(nextIndex);
                        } else {
                            // → = avançar 10s
                            videoPlayer.currentTime += 10;
                            statusDiv.textContent = "Avançou 10 segundos";
                        }
                        break;
                    case 'ArrowUp':
                        e.preventDefault();
                        const prevIndex = (currentVideoIndex - 1 + VIDEOS.length) % VIDEOS.length;
                        carregarVideo(prevIndex);
                        break;
                    case 'ArrowDown':
                        e.preventDefault();
                        const nextIndex = (currentVideoIndex + 1) % VIDEOS.length;
                        carregarVideo(nextIndex);
                        break;
                }
            });
        }
        
        // Testar URLs
        function testarURLs() {
            statusDiv.innerHTML = `
                <div>🔍 Testando conexão com GitHub...</div>
                <div style="font-size: 0.8rem; color: #888; margin-top: 5px;">
                    Usuário: ${USER} | Repo: ${REPO}
                </div>
            `;
            
            // Testar primeiro vídeo
            fetch(VIDEOS[0].url)
                .then(response => {
                    if (response.ok) {
                        statusDiv.innerHTML = `
                            <div style="color: #4CAF50;">✅ Conexão estabelecida!</div>
                            <div style="font-size: 0.8rem; color: #888; margin-top: 5px;">
                                ${VIDEOS.length} vídeos disponíveis
                            </div>
                        `;
                    } else {
                        statusDiv.innerHTML = `
                            <div style="color: #ff6b6b;">⚠️ Repositório encontrado, mas vídeo não</div>
                            <div style="font-size: 0.8rem; margin-top: 5px;">
                                Crie a pasta <strong>videos/</strong> com Video01.mp4, etc.
                            </div>
                        `;
                    }
                })
                .catch(error => {
                    statusDiv.innerHTML = `
                        <div style="color: #ff6b6b;">❌ Erro de conexão</div>
                        <div style="font-size: 0.8rem; margin-top: 5px;">
                            Verifique: https://github.com/${USER}/${REPO}
                        </div>
                    `;
                });
        }
        
        // Iniciar quando a página carregar
        document.addEventListener('DOMContentLoaded', function() {
            iniciarPlayer();
            // Testar conexão após 2 segundos
            setTimeout(testarURLs, 2000);
        });
        
        // Comandos do console
        console.log("🎮 Comandos disponíveis:");
        console.log("• Espaço = Play/Pause");
        console.log("• M = Mudo/Desmudo");
        console.log("• F = Tela cheia");
        console.log("• Setas = Avançar/Retroceder 10s");
        console.log("• Ctrl+Setas ou ↑↓ = Trocar vídeo");
        console.log("• currentVideoIndex = Ver vídeo atual");
        console.log("• carregarVideo(n) = Ir para vídeo n (0-33)");
    </script>
</body>
</html>
