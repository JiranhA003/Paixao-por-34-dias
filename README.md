<!DOCTYPE html>
<html>
<head>
    <title>Do Paixão para a Minha Paixão - Sistema Inteligente</title>
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
            overflow-x: hidden;
            padding: 20px 15px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 100%;
            margin: 0 auto;
        }
        
        /* Título */
        .titulo {
            margin-bottom: 25px;
        }
        
        .titulo h1 {
            font-size: 2.2rem;
            font-weight: 700;
            background: linear-gradient(135deg, #ff6b6b 0%, #ee5a24 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        
        /* Progresso */
        .progresso {
            margin: 0 auto 30px;
            max-width: 500px;
        }
        
        .dia-numero {
            font-size: 4.5rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ffffff 0%, #cccccc 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin: 10px 0;
        }
        
        .porcentagem {
            font-size: 1.5rem;
            font-weight: 600;
            color: #ffd700;
            margin-bottom: 15px;
        }
        
        .barra-container {
            height: 8px;
            background: #222;
            border-radius: 4px;
            overflow: hidden;
            margin: 0 auto;
            width: 80%;
        }
        
        .barra {
            height: 100%;
            background: linear-gradient(90deg, #ff6b6b 0%, #ee5a24 100%);
            width: 0%;
            transition: width 0.8s ease;
        }
        
        /* Container do conteúdo */
        .conteudo-container {
            margin: 30px auto;
            max-width: 400px;
            width: 100%;
            background: #111;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            position: relative;
        }
        
        /* VÍDEO */
        video {
            width: 100%;
            height: auto;
            display: block;
            aspect-ratio: 9/16;
            object-fit: cover;
        }
        
        /* SLIDESHOW */
        .slideshow-container {
            width: 100%;
            height: 640px;
            position: relative;
            overflow: hidden;
            touch-action: none;
        }
        
        .slides-track {
            display: flex;
            width: 100%;
            height: 100%;
            transition: transform 0.3s ease-out;
            will-change: transform;
        }
        
        .slide {
            flex: 0 0 100%;
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        
        .image-container {
            width: 100%;
            height: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }
        
        .slide-image {
            max-width: 100%;
            max-height: 100%;
            object-fit: contain;
            display: block;
        }
        
        .slide-texto {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            text-align: center;
            background: linear-gradient(to top, rgba(0,0,0,0.9), transparent);
            padding: 25px 15px 15px;
        }
        
        .slide-titulo {
            font-size: 1.3rem;
            font-weight: 600;
            color: white;
            margin-bottom: 5px;
            text-shadow: 0 2px 4px rgba(0,0,0,0.5);
        }
        
        .slide-descricao {
            font-size: 0.9rem;
            color: rgba(255,255,255,0.9);
            text-shadow: 0 1px 2px rgba(0,0,0,0.5);
        }
        
        /* Controles */
        .slide-indicator {
            position: absolute;
            bottom: 90px;
            left: 0;
            right: 0;
            display: flex;
            justify-content: center;
            gap: 10px;
            z-index: 10;
        }
        
        .indicator-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: rgba(255,255,255,0.3);
            transition: all 0.3s;
            cursor: pointer;
        }
        
        .indicator-dot.active {
            background: #ff6b6b;
            transform: scale(1.3);
            box-shadow: 0 0 10px rgba(255, 107, 107, 0.5);
        }
        
        .slide-counter {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(0,0,0,0.7);
            color: white;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 600;
            z-index: 10;
            backdrop-filter: blur(5px);
        }
        
        .music-control {
            position: absolute;
            bottom: 20px;
            left: 20px;
            z-index: 10;
        }
        
        .music-btn {
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
        
        .music-btn.playing {
            background: rgba(255,107,107,0.8);
        }
        
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
        
        /* Info do tipo de conteúdo */
        .content-type-badge {
            position: absolute;
            top: 20px;
            left: 20px;
            background: rgba(0,0,0,0.7);
            color: #ff6b6b;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            z-index: 10;
            backdrop-filter: blur(5px);
            border: 1px solid #ff6b6b;
            text-transform: uppercase;
            letter-spacing: 1px;
        }
        
        /* Loaders */
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
        
        /* Contador */
        .contador {
            margin: 25px auto;
            padding: 15px;
            background: rgba(20, 20, 20, 0.8);
            border-radius: 12px;
            max-width: 300px;
        }
        
        .tempo {
            font-size: 2.5rem;
            font-weight: 700;
            font-family: 'Courier New', monospace;
            color: #ff6b6b;
            letter-spacing: 2px;
            text-shadow: 0 0 10px rgba(255, 107, 107, 0.3);
            margin-bottom: 8px;
        }
        
        .texto-contador {
            font-size: 1.1rem;
            color: #aaa;
            line-height: 1.3;
        }
        
        .concluido {
            color: #4CAF50;
            font-size: 1.8rem;
            padding: 20px;
            animation: pulse 2s infinite;
            margin-top: 20px;
        }
        
        @keyframes pulse {
            0% { opacity: 0.8; }
            50% { opacity: 1; }
            100% { opacity: 0.8; }
        }
        
        /* Glow effect */
        .glow {
            animation: glow 3s ease-in-out infinite alternate;
        }
        
        @keyframes glow {
            from { text-shadow: 0 0 10px rgba(238, 90, 36, 0.5); }
            to { text-shadow: 0 0 20px rgba(238, 90, 36, 0.8), 0 0 30px rgba(238, 90, 36, 0.4); }
        }
        
        /* Element spacing */
        .elemento {
            display: block;
            margin-bottom: 25px;
        }
        
        /* Responsividade */
        @media (max-width: 768px) {
            .conteudo-container {
                max-width: 320px;
            }
            
            .slideshow-container {
                height: 570px;
            }
            
            .titulo h1 {
                font-size: 1.8rem;
            }
        }
        
        @media (max-width: 480px) {
            .conteudo-container {
                max-width: 280px;
            }
            
            .slideshow-container {
                height: 500px;
            }
            
            .titulo h1 {
                font-size: 1.6rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- TÍTULO -->
        <div class="titulo elemento">
            <h1 class="glow">Do Paixão para a Minha Paixão</h1>
        </div>
        
        <!-- PROGRESSO -->
        <div class="progresso elemento">
            <div class="dia-numero" id="dia-numero">1</div>
            <div class="porcentagem" id="porcentagem">3%</div>
            <div class="barra-container">
                <div class="barra" id="barra"></div>
            </div>
        </div>
        
        <!-- CONTEÚDO -->
        <div class="conteudo-container elemento">
            <div class="video-loader" id="loader">
                <div class="loader-spinner"></div>
                <div>Carregando conteúdo...</div>
            </div>
            <div id="conteudo-placeholder"></div>
        </div>
        
        <!-- CONTADOR -->
        <div class="contador elemento" id="contador">
            <div class="tempo" id="tempo">23:45:12</div>
            <div class="texto-contador">Até o próximo conteúdo!</div>
        </div>
        
        <!-- CONCLUÍDO -->
        <div id="concluido" style="display: none;"></div>
    </div>

    <script>
        // 🔧 CONFIGURAÇÃO DO USUÁRIO 🔧
        // Substitua pelo SEU usuário e repositório do GitHub
        const USER = "SEU_USUARIO_GITHUB";
        const REPO = "SEU_REPOSITORIO";
        
        // URLs base para as pastas no GitHub
        const BASE_URL = `https://github.com/${USER}/${REPO}/raw/main/`;
        const VIDEOS_FOLDER = `${BASE_URL}videos/`;
        const IMAGES_FOLDER = `${BASE_URL}images/`;
        
        // Sistema de gerenciamento inteligente
        const ContentManager = {
            // Listas de conteúdo disponível
            availableVideos: [],
            availableImages: [],
            
            // Conteúdo já usado (para não repetir)
            usedVideos: new Set(),
            usedImages: new Set(),
            
            // Histórico de tipos de conteúdo
            contentHistory: [],
            
            // Configuração do algoritmo
            config: {
                // Peso para vídeos vs imagens (0.5 = 50% de chance para cada)
                videoWeight: 0.5,
                // Tamanho máximo do slideshow
                maxSlidesPerDay: 3,
                // Garantir que depois de X dias, o tipo se repita
                maxSameTypeStreak: 2
            },
            
            // Inicializar o gerenciador
            async initialize() {
                console.log("🚀 Iniciando gerenciador de conteúdo inteligente...");
                
                // Tentar carregar da localStorage primeiro
                this.loadFromStorage();
                
                // Se não tem conteúdo salvo, descobrir automaticamente
                if (this.availableVideos.length === 0 && this.availableImages.length === 0) {
                    await this.discoverContent();
                }
                
                console.log(`✅ Conteúdo disponível: ${this.availableVideos.length} vídeos, ${this.availableImages.length} imagens`);
            },
            
            // Descobrir conteúdo automaticamente das pastas
            async discoverContent() {
                console.log("🔍 Descobrindo conteúdo automaticamente...");
                
                // Em um cenário real, você faria requisições para listar arquivos
                // Como GitHub Raw não permite listagem, simulemos com nomes padrão
                
                // Vídeos: Video01.mp4, Video02.mp4, etc (até Video30.mp4)
                for (let i = 1; i <= 30; i++) {
                    const num = i.toString().padStart(2, '0');
                    this.availableVideos.push({
                        url: `${VIDEOS_FOLDER}Video${num}.mp4`,
                        name: `Video${num}.mp4`,
                        id: `video_${num}`,
                        type: 'video'
                    });
                }
                
                // Imagens: Image01.jpg, Image02.jpg, etc (até Image30.jpg)
                for (let i = 1; i <= 30; i++) {
                    const num = i.toString().padStart(2, '0');
                    this.availableImages.push({
                        url: `${IMAGES_FOLDER}Image${num}.jpg`,
                        name: `Image${num}.jpg`,
                        id: `image_${num}`,
                        type: 'image'
                    });
                }
                
                // Embaralhar as listas para aleatoriedade
                this.shuffleArray(this.availableVideos);
                this.shuffleArray(this.availableImages);
                
                this.saveToStorage();
            },
            
            // Escolher conteúdo para um dia específico
            getContentForDay(day) {
                console.log(`🎯 Escolhendo conteúdo para o Dia ${day}...`);
                
                // Verificar se já temos conteúdo para este dia
                const storedContent = this.getStoredContentForDay(day);
                if (storedContent) {
                    console.log(`📦 Usando conteúdo armazenado para Dia ${day}`);
                    return storedContent;
                }
                
                // Decidir o tipo de conteúdo (vídeo ou slideshow)
                let contentType = this.decideContentType(day);
                
                // Escolher conteúdo específico baseado no tipo
                let content;
                
                if (contentType === 'video') {
                    content = this.chooseVideo(day);
                } else {
                    content = this.chooseSlideshow(day);
                }
                
                // Armazenar no histórico
                this.contentHistory.push({
                    day: day,
                    type: contentType,
                    content: content
                });
                
                // Salvar escolha para este dia
                this.saveContentForDay(day, content);
                
                console.log(`✅ Escolhido para Dia ${day}: ${contentType === 'video' ? 'Vídeo' : 'Slideshow'}`);
                return content;
            },
            
            // Decidir o tipo de conteúdo (algoritmo inteligente)
            decideContentType(day) {
                // Verificar último tipo usado
                const lastTwoDays = this.contentHistory.slice(-2);
                const videoCount = lastTwoDays.filter(c => c.type === 'video').length;
                const imageCount = lastTwoDays.filter(c => c.type === 'slideshow').length;
                
                // Se já usou o mesmo tipo 2 dias seguidos, alternar
                if (videoCount >= this.config.maxSameTypeStreak && this.availableImages.length > this.usedImages.size) {
                    return 'slideshow';
                }
                if (imageCount >= this.config.maxSameTypeStreak && this.availableVideos.length > this.usedVideos.size) {
                    return 'video';
                }
                
                // Se um tipo está acabando, priorizar o outro
                const remainingVideos = this.availableVideos.length - this.usedVideos.size;
                const remainingImages = this.availableImages.length - this.usedImages.size;
                
                if (remainingVideos === 0) return 'slideshow';
                if (remainingImages === 0) return 'video';
                
                // Decisão aleatória com peso
                const random = Math.random();
                return random < this.config.videoWeight ? 'video' : 'slideshow';
            },
            
            // Escolher um vídeo
            chooseVideo(day) {
                // Filtrar vídeos não usados
                const unusedVideos = this.availableVideos.filter(v => !this.usedVideos.has(v.id));
                
                if (unusedVideos.length === 0) {
                    // Se todos os vídeos foram usados, resetar (opcional)
                    console.log("🔄 Todos os vídeos usados, recomeçando...");
                    this.usedVideos.clear();
                    return this.availableVideos[day % this.availableVideos.length];
                }
                
                // Escolher um vídeo aleatório não usado
                const chosenVideo = unusedVideos[Math.floor(Math.random() * unusedVideos.length)];
                
                // Marcar como usado
                this.usedVideos.add(chosenVideo.id);
                
                return {
                    type: 'video',
                    url: chosenVideo.url,
                    title: `Dia ${day} - Transformação`,
                    description: `Aula ${day} da sua jornada de 30 dias`,
                    id: chosenVideo.id
                };
            },
            
            // Escolher um slideshow
            chooseSlideshow(day) {
                // Número de slides para este slideshow (1-3)
                const numSlides = Math.min(this.config.maxSlidesPerDay, 
                    Math.max(1, Math.floor(Math.random() * 3) + 1));
                
                const slides = [];
                
                for (let i = 0; i < numSlides; i++) {
                    // Encontrar uma imagem não usada
                    const unusedImages = this.availableImages.filter(img => !this.usedImages.has(img.id));
                    
                    if (unusedImages.length === 0) {
                        // Se todas as imagens foram usadas
                        console.log("🔄 Todas as imagens usadas, recomeçando...");
                        this.usedImages.clear();
                        break;
                    }
                    
                    const chosenImage = unusedImages[Math.floor(Math.random() * unusedImages.length)];
                    this.usedImages.add(chosenImage.id);
                    
                    slides.push({
                        url: chosenImage.url,
                        title: `Dia ${day} - Momento ${i + 1}`,
                        description: `Inspiração para o seu dia ${day}`,
                        id: chosenImage.id
                    });
                }
                
                return {
                    type: 'slideshow',
                    slides: slides,
                    title: `Dia ${day} - Galeria de Inspiração`,
                    description: `${slides.length} momentos especiais para você`
                };
            },
            
            // Gerenciamento de storage
            saveContentForDay(day, content) {
                const key = `dia_${day}_content`;
                try {
                    localStorage.setItem(key, JSON.stringify(content));
                } catch (e) {
                    console.warn("Não foi possível salvar no localStorage", e);
                }
            },
            
            getStoredContentForDay(day) {
                const key = `dia_${day}_content`;
                try {
                    const stored = localStorage.getItem(key);
                    return stored ? JSON.parse(stored) : null;
                } catch (e) {
                    return null;
                }
            },
            
            saveToStorage() {
                try {
                    const data = {
                        videos: this.availableVideos,
                        images: this.availableImages,
                        usedVideos: Array.from(this.usedVideos),
                        usedImages: Array.from(this.usedImages),
                        history: this.contentHistory
                    };
                    localStorage.setItem('content_manager', JSON.stringify(data));
                } catch (e) {
                    console.warn("Erro ao salvar no localStorage", e);
                }
            },
            
            loadFromStorage() {
                try {
                    const data = JSON.parse(localStorage.getItem('content_manager'));
                    if (data) {
                        this.availableVideos = data.videos || [];
                        this.availableImages = data.images || [];
                        this.usedVideos = new Set(data.usedVideos || []);
                        this.usedImages = new Set(data.usedImages || []);
                        this.contentHistory = data.history || [];
                    }
                } catch (e) {
                    console.warn("Erro ao carregar do localStorage", e);
                }
            },
            
            // Utilitários
            shuffleArray(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
            },
            
            // Resetar para testes
            reset() {
                this.usedVideos.clear();
                this.usedImages.clear();
                this.contentHistory = [];
                localStorage.removeItem('content_manager');
                console.log("🔄 Gerenciador de conteúdo resetado");
            }
        };
        
        // ============================================================================
        // SISTEMA PRINCIPAL DA APLICAÇÃO
        // ============================================================================
        
        let slideshowState = {
            currentIndex: 0,
            isDragging: false,
            startX: 0,
            currentX: 0,
            track: null
        };
        
        // FUNÇÕES PRINCIPAIS
        async function iniciar() {
            console.log("🎬 Iniciando aplicação...");
            
            // Inicializar gerenciador de conteúdo
            await ContentManager.initialize();
            
            // Sistema de datas
            let inicio = localStorage.getItem('jornada_inicio');
            if (!inicio) {
                inicio = new Date().toISOString();
                localStorage.setItem('jornada_inicio', inicio);
                console.log(`📅 Data de início definida: ${inicio}`);
            }
            
            const dataInicio = new Date(inicio);
            const hoje = new Date();
            const diferenca = hoje - dataInicio;
            const diasPassados = Math.floor(diferenca / (1000 * 60 * 60 * 24));
            let dia = diasPassados + 1;
            
            if (dia > 30) dia = 30;
            if (dia < 1) dia = 1;
            
            console.log(`📊 Dia atual: ${dia} (${diasPassados} dias passados)`);
            
            atualizar(dia);
            verificarProximo(dia);
        }
        
        function atualizar(dia) {
            // Atualizar UI de progresso
            document.getElementById('dia-numero').textContent = dia;
            const porcentagem = (dia / 30) * 100;
            const porcentagemFormatada = Math.round(porcentagem);
            document.getElementById('porcentagem').textContent = porcentagemFormatada + '%';
            document.getElementById('barra').style.width = porcentagem + '%';
            
            // Carregar conteúdo inteligente
            carregarConteudoInteligente(dia);
            
            // Se concluiu
            if (dia >= 30) {
                document.getElementById('concluido').style.display = 'block';
                document.getElementById('concluido').innerHTML = '<div class="concluido">✓ Jornada Concluída</div>';
                document.getElementById('contador').style.display = 'none';
            }
        }
        
        async function carregarConteudoInteligente(dia) {
            const container = document.getElementById('conteudo-placeholder');
            const loader = document.getElementById('loader');
            
            // Mostrar loader
            container.innerHTML = '';
            loader.style.display = 'block';
            
            // Obter conteúdo do gerenciador inteligente
            const conteudo = ContentManager.getContentForDay(dia);
            
            // Criar conteúdo baseado no tipo
            let html = '';
            
            switch (conteudo.type) {
                case 'video':
                    html = criarVideoPlayer(conteudo.url, conteudo.title, conteudo.description, dia);
                    break;
                    
                case 'slideshow':
                    html = criarSlideshow(conteudo.slides, conteudo.title, conteudo.description, dia);
                    break;
                    
                default:
                    html = criarPlaceholder(dia);
                    break;
            }
            
            // Inserir no DOM
            container.innerHTML = html;
            loader.style.display = 'none';
            
            // Inicializar controles
            if (conteudo.type === 'video') {
                setTimeout(() => inicializarVideoPlayer(conteudo.url), 100);
            } else if (conteudo.type === 'slideshow') {
                setTimeout(() => inicializarSlideshow(conteudo.slides), 100);
            }
        }
        
        // FUNÇÕES DE CRIAÇÃO DE CONTEÚDO
        function criarVideoPlayer(url, titulo, descricao, dia) {
            return `
                <div class="content-type-badge">🎬 Vídeo</div>
                <div class="video-container" id="video-container">
                    <video id="video-player" playsinline autoplay muted loop>
                        <source src="${url}" type="video/mp4">
                        Seu navegador não suporta vídeos HTML5.
                    </video>
                    <div class="slide-texto">
                        <div class="slide-titulo">${titulo || `Dia ${dia} - Transformação`}</div>
                        <div class="slide-descricao">${descricao || `Aula ${dia} da sua jornada`}</div>
                    </div>
                    <div class="video-controls">
                        <button class="video-btn" id="play-btn">⏸</button>
                        <button class="video-btn" id="mute-btn">🔇</button>
                        <button class="video-btn" id="fullscreen-btn">⛶</button>
                    </div>
                </div>
            `;
        }
        
        function criarSlideshow(slides, titulo, descricao, dia) {
            return `
                <div class="content-type-badge">🖼️ Galeria</div>
                <div class="slideshow-container" id="slideshow-container">
                    <div class="slides-track" id="slides-track">
                        ${slides.map((slide, index) => `
                            <div class="slide">
                                <div class="image-container">
                                    <img src="${slide.url}" alt="${slide.title}" 
                                         class="slide-image" id="slide-img-${index}"
                                         onerror="this.onerror=null; this.src='data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMzAwIiBoZWlnaHQ9IjUwMCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48cmVjdCB3aWR0aD0iMzAwIiBoZWlnaHQ9IjUwMCIgZmlsbD0iIzFhMWExYSIvPjx0ZXh0IHg9IjE1MCIgeT0iMjUwIiBmb250LWZhbWlseT0iQXJpYWwiIGZvbnQtc2l6ZT0iMjAiIGZpbGw9IiNmZjZjNmMiIHRleHQtYW5jaG9yPSJtaWRkbGUiIGR5PSIuM2VtIj5JbWFnZW0gJHtpbmRleCsxfTwvdGV4dD48L3N2Zz4=';">
                                </div>
                                <div class="slide-texto">
                                    <div class="slide-titulo">${slide.title}</div>
                                    <div class="slide-descricao">${slide.description}</div>
                                </div>
                            </div>
                        `).join('')}
                    </div>
                    <div class="slide-counter" id="slide-counter">1/${slides.length}</div>
                    <div class="slide-indicator" id="slide-indicator">
                        ${slides.map((_, index) => `
                            <div class="indicator-dot" data-index="${index}"></div>
                        `).join('')}
                    </div>
                    <div class="instruction" id="instruction">← Arraste para trocar de foto →</div>
                </div>
            `;
        }
        
        function criarPlaceholder(dia) {
            return `
                <div style="aspect-ratio: 9/16; display: flex; align-items: center; justify-content: center; background: #1a1a1a; color: #666;">
                    <div style="text-align: center;">
                        <div style="font-size: 3rem; margin-bottom: 15px; color: #ff6b6b;">🎲</div>
                        <div style="font-size: 1.2rem; color: #fff;">Dia ${dia}</div>
                        <div style="font-size: 0.9rem; color: #888; margin-top: 10px;">Gerando conteúdo inteligente...</div>
                    </div>
                </div>
            `;
        }
        
        // INICIALIZAR VÍDEO PLAYER
        function inicializarVideoPlayer(url) {
            const video = document.getElementById('video-player');
            const playBtn = document.getElementById('play-btn');
            const muteBtn = document.getElementById('mute-btn');
            const fullscreenBtn = document.getElementById('fullscreen-btn');
            
            if (!video) return;
            
            video.addEventListener('loadeddata', function() {
                if (video.paused) {
                    playBtn.textContent = '▶';
                } else {
                    playBtn.textContent = '⏸';
                }
            });
            
            video.addEventListener('error', function(e) {
                console.error("Erro ao carregar vídeo:", url);
                playBtn.textContent = '❌';
                playBtn.style.background = 'rgba(255,0,0,0.7)';
            });
            
            // Controles
            playBtn.addEventListener('click', function() {
                if (video.paused) {
                    video.play();
                    playBtn.textContent = '⏸';
                } else {
                    video.pause();
                    playBtn.textContent = '▶';
                }
            });
            
            muteBtn.addEventListener('click', function() {
                video.muted = !video.muted;
                muteBtn.textContent = video.muted ? '🔇' : '🔊';
            });
            
            fullscreenBtn.addEventListener('click', function() {
                const container = document.getElementById('video-container');
                if (container.requestFullscreen) {
                    container.requestFullscreen();
                } else if (container.webkitRequestFullscreen) {
                    container.webkitRequestFullscreen();
                }
            });
            
            video.addEventListener('ended', function() {
                playBtn.textContent = '▶';
            });
        }
        
        // INICIALIZAR SLIDESHOW
        function inicializarSlideshow(slides) {
            const container = document.getElementById('slideshow-container');
            const track = document.getElementById('slides-track');
            const indicators = document.getElementById('slide-indicator');
            const instruction = document.getElementById('instruction');
            
            if (!track) return;
            
            slideshowState.track = track;
            track.style.width = `${slides.length * 100}%`;
            
            // Configurar indicadores
            document.querySelectorAll('.indicator-dot').forEach((dot, index) => {
                dot.classList.toggle('active', index === 0);
                dot.addEventListener('click', () => {
                    goToSlide(index);
                });
            });
            
            // Eventos de arraste
            container.addEventListener('mousedown', startDrag);
            container.addEventListener('mousemove', drag);
            container.addEventListener('mouseup', endDrag);
            container.addEventListener('mouseleave', endDrag);
            
            container.addEventListener('touchstart', startDragTouch, { passive: false });
            container.addEventListener('touchmove', dragTouch, { passive: false });
            container.addEventListener('touchend', endDrag);
            
            // Esconder instrução após 7 segundos
            setTimeout(() => {
                if (instruction) {
                    instruction.style.opacity = '0';
                    setTimeout(() => {
                        instruction.style.display = 'none';
                    }, 1000);
                }
            }, 7000);
            
            // Atualizar UI inicial
            atualizarSlideshowUI();
        }
        
        // Funções do slideshow (mantidas do código anterior)
        function startDrag(e) {
            slideshowState.isDragging = true;
            slideshowState.startX = e.clientX;
            slideshowState.currentX = slideshowState.startX;
            slideshowState.track.style.transition = 'none';
            e.preventDefault();
        }
        
        function drag(e) {
            if (!slideshowState.isDragging) return;
            slideshowState.currentX = e.clientX;
            const diff = slideshowState.currentX - slideshowState.startX;
            updateTrackPosition(diff);
        }
        
        function startDragTouch(e) {
            e.preventDefault();
            slideshowState.isDragging = true;
            slideshowState.startX = e.touches[0].clientX;
            slideshowState.currentX = slideshowState.startX;
            slideshowState.track.style.transition = 'none';
        }
        
        function dragTouch(e) {
            if (!slideshowState.isDragging) return;
            e.preventDefault();
            slideshowState.currentX = e.touches[0].clientX;
            const diff = slideshowState.currentX - slideshowState.startX;
            updateTrackPosition(diff);
        }
        
        function endDrag() {
            if (!slideshowState.isDragging) return;
            slideshowState.isDragging = false;
            slideshowState.track.style.transition = 'transform 0.3s ease-out';
            
            const diff = slideshowState.currentX - slideshowState.startX;
            const threshold = 50;
            
            if (diff > threshold && slideshowState.currentIndex > 0) {
                previousSlide();
            } else if (diff < -threshold && slideshowState.currentIndex < getSlideCount() - 1) {
                nextSlide();
            } else {
                goToSlide(slideshowState.currentIndex);
            }
        }
        
        function updateTrackPosition(diff) {
            const slideWidth = 100 / getSlideCount();
            const basePosition = -slideshowState.currentIndex * slideWidth;
            const dragOffset = (diff / window.innerWidth) * 100;
            slideshowState.track.style.transform = `translateX(${basePosition + dragOffset}%)`;
        }
        
        function getSlideCount() {
            return document.querySelectorAll('.slide').length;
        }
        
        function previousSlide() {
            if (slideshowState.currentIndex > 0) {
                slideshowState.currentIndex--;
                goToSlide(slideshowState.currentIndex);
            }
        }
        
        function nextSlide() {
            if (slideshowState.currentIndex < getSlideCount() - 1) {
                slideshowState.currentIndex++;
                goToSlide(slideshowState.currentIndex);
            }
        }
        
        function goToSlide(index) {
            slideshowState.currentIndex = index;
            const slideWidth = 100 / getSlideCount();
            slideshowState.track.style.transform = `translateX(-${slideshowState.currentIndex * slideWidth}%)`;
            atualizarSlideshowUI();
        }
        
        function atualizarSlideshowUI() {
            const total = getSlideCount();
            document.getElementById('slide-counter').textContent = 
                `${slideshowState.currentIndex + 1}/${total}`;
            
            document.querySelectorAll('.indicator-dot').forEach((dot, index) => {
                dot.classList.toggle('active', index === slideshowState.currentIndex);
            });
        }
        
        // CONTADOR DE TEMPO
        function verificarProximo(dia) {
            if (dia >= 30) return;
            
            const agora = new Date();
            const amanha = new Date();
            amanha.setDate(amanha.getDate() + 1);
            amanha.setHours(0, 0, 0, 0);
            
            function atualizarContador() {
                const agora = new Date();
                const restante = amanha - agora;
                
                if (restante <= 0) {
                    document.getElementById('tempo').textContent = '00:00:00';
                    document.getElementById('tempo').style.color = '#4CAF50';
                    return;
                }
                
                const horas = Math.floor(restante / (1000 * 60 * 60));
                const minutos = Math.floor((restante % (1000 * 60 * 60)) / (1000 * 60));
                const segundos = Math.floor((restante % (1000 * 60)) / 1000);
                
                document.getElementById('tempo').textContent = 
                    `${horas.toString().padStart(2, '0')}:${minutos.toString().padStart(2, '0')}:${segundos.toString().padStart(2, '0')}`;
            }
            
            atualizarContador();
            setInterval(atualizarContador, 1000);
        }
        
        // INICIAR APLICAÇÃO
        document.addEventListener('DOMContentLoaded', iniciar);
        
        // Botão de reset para testes (opcional - remover em produção)
        console.log("💡 Dica: Use ContentManager.reset() no console para resetar o conteúdo");
    </script>
</body>
</html>
