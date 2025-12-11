<!DOCTYPE html>
<html>
<head>
    <title>Paixão por 34 Dias - Dia 19</title>
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
        
        /* Cabeçalho com data */
        .cabecalho {
            margin-bottom: 25px;
        }
        
        .data-atual {
            font-size: 0.9rem;
            color: #ff6b6b;
            margin-bottom: 5px;
            font-weight: 500;
        }
        
        .titulo h1 {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        .subtitulo {
            font-size: 0.9rem;
            color: #666;
            margin-top: 5px;
        }
        
        /* Progresso */
        .progresso {
            margin: 0 auto 25px;
            background: rgba(20, 20, 20, 0.8);
            padding: 15px;
            border-radius: 10px;
            border: 1px solid #333;
        }
        
        .dia-numero {
            font-size: 3.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ffffff 0%, #cccccc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin: 5px 0;
        }
        
        .porcentagem {
            font-size: 1.3rem;
            font-weight: 600;
            color: #ffd700;
            margin-bottom: 10px;
        }
        
        .barra-container {
            height: 6px;
            background: #222;
            border-radius: 3px;
            overflow: hidden;
            margin: 0 auto;
            width: 80%;
        }
        
        .barra {
            height: 100%;
            background: linear-gradient(90deg, #ff6b6b 0%, #ee5a24 100%);
            width: 56%; /* 19/34 = ~56% */
            transition: width 0.8s ease;
        }
        
        .info-progresso {
            font-size: 0.8rem;
            color: #aaa;
            margin-top: 8px;
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
        
        /* Lista de vídeos (escondida por padrão) */
        .lista-videos {
            margin-top: 20px;
            background: rgba(20, 20, 20, 0.8);
            border-radius: 10px;
            padding: 15px;
            border: 1px solid #333;
            max-height: 150px;
            overflow-y: auto;
            display: none; /* Escondido inicialmente */
        }
        
        .lista-titulo {
            font-size: 1rem;
            font-weight: 600;
            color: #ff6b6b;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .toggle-lista {
            background: transparent;
            border: none;
            color: #ff6b6b;
            cursor: pointer;
            font-size: 0.9rem;
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
        
        /* Botão para ver todos os vídeos */
        .ver-todos-btn {
            background: rgba(255, 107, 107, 0.2);
            border: 1px solid #ff6b6b;
            color: #ff6b6b;
            padding: 10px 20px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 0.9rem;
            margin-top: 15px;
            transition: all 0.3s;
        }
        
        .ver-todos-btn:hover {
            background: rgba(255, 107, 107, 0.4);
            transform: translateY(-2px);
        }
        
        /* Responsivo */
        @media (max-width: 768px) {
            .container {
                max-width: 320px;
            }
            
            .titulo h1 {
                font-size: 1.6rem;
            }
            
            .dia-numero {
                font-size: 3rem;
            }
            
            .lista-videos {
                max-height: 120px;
            }
        }
        
        @media (max-width: 480px) {
            .container {
                max-width: 280px;
            }
            
            .titulo h1 {
                font-size: 1.4rem;
            }
            
            .dia-numero {
                font-size: 2.5rem;
            }
            
            .video-btn {
                width: 40px;
                height: 40px;
                font-size: 1.1rem;
            }
            
            .lista-videos {
                max-height: 100px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- CABEÇALHO COM DATA -->
        <div class="cabecalho">
            <div class="data-atual" id="data-atual">19 de Dezembro de 2024</div>
            <div class="titulo">
                <h1>Paixão por 34 Dias</h1>
                <div class="subtitulo">Transformação Diária</div>
            </div>
        </div>
        
        <!-- PROGRESSO -->
        <div class="progresso">
            <div class="dia-numero" id="dia-numero">19</div>
            <div class="porcentagem" id="porcentagem">56%</div>
            <div class="barra-container">
                <div class="barra" id="barra"></div>
            </div>
            <div class="info-progresso">Dia 19 de 34 • Mais 15 dias para concluir</div>
        </div>
        
        <!-- VÍDEO -->
        <div class="video-container">
            <div class="video-loader" id="loader">
                <div class="loader-spinner"></div>
                <div>Carregando vídeo do Dia 19...</div>
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
            <div class="video-titulo" id="video-title">Dia 19 - Transformação</div>
            <div class="video-descricao" id="video-description">Aula 19 da sua jornada de 34 dias. Continue firme!</div>
        </div>
        
        <!-- BOTÃO PARA VER TODOS -->
        <button class="ver-todos-btn" id="ver-todos-btn">
            📋 Ver todos os vídeos (1-34)
        </button>
        
        <!-- LISTA DE VÍDEOS (ESCONDIDA) -->
        <div class="lista-videos" id="lista-videos">
            <div class="lista-titulo">
                <span>🎬 Todos os Vídeos</span>
                <button class="toggle-lista" id="fechar-lista">✕ Fechar</button>
            </div>
            <div id="video-list">
                <!-- Lista gerada por JavaScript -->
            </div>
        </div>
        
        <!-- STATUS -->
        <div class="status" id="status">
            Carregando conteúdo do Dia 19...
        </div>
    </div>

    <script>
        // 🔧 CONFIGURAÇÃO COM SEUS DADOS
        const USER = "JiranhA003";
        const REPO = "Paixão-por-34-dias";
        const BASE_URL = `https://github.com/${USER}/${REPO}/raw/main/videos/`;
        
        // CONFIGURAÇÃO DA JORNADA
        const DIA_ATUAL = 19; // ⭐ DIA FIXO 19 ⭐
        const TOTAL_DIAS = 34;
        
        // Lista de vídeos disponíveis
        const VIDEOS = [];
        
        // Gerar automaticamente os 34 vídeos
        for (let i = 1; i <= TOTAL_DIAS; i++) {
            const numero = i.toString().padStart(2, '0');
            VIDEOS.push({
                url: `${BASE_URL}Video${numero}.mp4`,
                title: `Dia ${i} - Transformação`,
                description: i === DIA_ATUAL ? 
                    `Aula ${i} - Você está aqui!` :
                    `Aula ${i} da jornada de ${TOTAL_DIAS} dias`,
                numero: i,
                isCurrentDay: i === DIA_ATUAL
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
        const listaVideos = document.getElementById('lista-videos');
        const verTodosBtn = document.getElementById('ver-todos-btn');
        const fecharLista = document.getElementById('fechar-lista');
        const diaNumero = document.getElementById('dia-numero');
        const porcentagem = document.getElementById('porcentagem');
        const barra = document.getElementById('barra');
        const dataAtual = document.getElementById('data-atual');
        
        // Estado do player
        let currentVideoIndex = DIA_ATUAL - 1; // Começa no dia 19
        let isPlaying = true;
        let isMuted = true;
        
        // Atualizar data atual
        function atualizarDataAtual() {
            const hoje = new Date();
            // Começando em 1º de dezembro, dia 19 seria 19 de dezembro
            const dataInicio = new Date('2024-12-01');
            const dataDiaAtual = new Date(dataInicio);
            dataDiaAtual.setDate(dataInicio.getDate() + (DIA_ATUAL - 1));
            
            const options = { day: 'numeric', month: 'long', year: 'numeric' };
            const dataFormatada = dataDiaAtual.toLocaleDateString('pt-BR', options);
            dataAtual.textContent = dataFormatada;
        }
        
        // Calcular progresso
        function atualizarProgresso() {
            const percentual = (DIA_ATUAL / TOTAL_DIAS) * 100;
            const percentualArredondado = Math.round(percentual);
            
            diaNumero.textContent = DIA_ATUAL;
            porcentagem.textContent = `${percentualArredondado}%`;
            barra.style.width = `${percentual}%`;
            
            console.log(`📊 Progresso: Dia ${DIA_ATUAL}/${TOTAL_DIAS} (${percentualArredondado}%)`);
        }
        
        // Inicializar
        function iniciarPlayer() {
            console.log("🎬 Iniciando reprodutor de vídeo...");
            console.log(`👤 Usuário: ${USER}`);
            console.log(`📁 Repositório: ${REPO}`);
            console.log(`📅 Dia atual: ${DIA_ATUAL}/${TOTAL_DIAS}`);
            console.log(`🎥 ${VIDEOS.length} vídeos configurados`);
            
            // Atualizar interface
            atualizarDataAtual();
            atualizarProgresso();
            
            // Criar lista de vídeos
            criarListaVideos();
            
            // Carregar vídeo do dia 19
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
                if (video.isCurrentDay) {
                    item.classList.add('ativo');
                }
                
                item.innerHTML = `
                    <div class="video-numero">${video.numero}</div>
                    <div style="flex: 1; text-align: left;">
                        <div style="font-weight: 500; color: ${video.isCurrentDay ? '#ff6b6b' : '#fff'};">${video.title}</div>
                        <div style="font-size: 0.75rem; color: #888;">${video.description}</div>
                    </div>
                    ${video.isCurrentDay ? '<div style="color: #ff6b6b; font-size: 1.2rem;">▶</div>' : ''}
                `;
                
                item.addEventListener('click', () => {
                    carregarVideo(index);
                    // Não fecha a lista, só atualiza o vídeo
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
                        Verifique se o arquivo "Video${video.numero.toString().padStart(2, '0')}.mp4" existe no GitHub
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
                playBtn.textContent = '🔄';
                isPlaying = false;
                statusDiv.textContent = "Vídeo finalizado";
                
                // Se for o dia 19, sugerir dia 20
                if (currentVideoIndex === DIA_ATUAL - 1) {
                    setTimeout(() => {
                        statusDiv.innerHTML = `
                            <div>🎯 Vídeo do Dia ${DIA_ATUAL} concluído!</div>
                            <div style="font-size: 0.8rem; color: #4CAF50; margin-top: 5px;">
                                Amanhã: Dia ${DIA_ATUAL + 1}
                            </div>
                        `;
                    }, 1000);
                }
            });
            
            // Mostrar/ocultar lista de vídeos
            verTodosBtn.addEventListener('click', function() {
                listaVideos.style.display = 'block';
                verTodosBtn.style.display = 'none';
                statusDiv.textContent = "Selecione um vídeo da lista";
            });
            
            fecharLista.addEventListener('click', function() {
                listaVideos.style.display = 'none';
                verTodosBtn.style.display = 'block';
                statusDiv.textContent = `Reproduzindo: ${videoTitle.textContent}`;
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
                    case 'l':
                    case 'L':
                        e.preventDefault();
                        if (listaVideos.style.display === 'block') {
                            fecharLista.click();
                        } else {
                            verTodosBtn.click();
                        }
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
                }
            });
        }
        
        // Testar URLs
        function testarURLs() {
            statusDiv.innerHTML = `
                <div>🔍 Testando conexão com GitHub...</div>
                <div style="font-size: 0.8rem; color: #888; margin-top: 5px;">
                    Buscando Video19.mp4...
                </div>
            `;
            
            // Testar vídeo do dia 19
            const video19URL = VIDEOS[DIA_ATUAL - 1].url;
            fetch(video19URL)
                .then(response => {
                    if (response.ok) {
                        statusDiv.innerHTML = `
                            <div style="color: #4CAF50;">✅ Vídeo do Dia 19 encontrado!</div>
                            <div style="font-size: 0.8rem; color: #888; margin-top: 5px;">
                                ${VIDEOS.length} vídeos disponíveis
                            </div>
                        `;
                    } else {
                        statusDiv.innerHTML = `
                            <div style="color: #ff6b6b;">⚠️ Video19.mp4 não encontrado</div>
                            <div style="font-size: 0.8rem; margin-top: 5px;">
                                Crie o arquivo: <strong>videos/Video19.mp4</strong> no GitHub
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
        console.log("• L = Mostrar/ocultar lista");
        console.log("• Setas = Avançar/Retroceder 10s");
        console.log("• Ctrl+Setas = Trocar vídeo");
        console.log(`• Dia atual fixo: ${DIA_ATUAL}`);
    </script>
</body>
</html>
