<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Do Paixão para a Minha Paixão</title>

    <!-- ========================== -->
    <!--  VERSÃO LIMITADA E LIMPADA  -->
    <!--  Tudo organizado, sem scripts duplicados. -->
    <!-- ========================== -->
    <style>
        *{box-sizing:border-box;margin:0;padding:0}
        html,body{height:100%}
        body{
            font-family:Inter,Arial,sans-serif;background:#000;color:#fff;display:flex;align-items:flex-start;justify-content:center;padding:20px;min-height:100vh
        }
        .container{width:100%;max-width:420px}
        .titulo h1{font-size:2rem;background:linear-gradient(135deg,#ff6b6b,#ee5a24);-webkit-background-clip:text;-webkit-text-fill-color:transparent;text-align:center;margin-bottom:20px}
        .progresso{text-align:center;margin-bottom:18px}
        .dia-numero{font-size:3.5rem;font-weight:800}
        .barra-container{width:80%;margin:10px auto;height:8px;background:#222;border-radius:6px;overflow:hidden}
        .barra{height:100%;width:0;background:linear-gradient(90deg,#ff6b6b,#ee5a24);transition:width .6s}
        .conteudo-container{margin:18px auto;background:#111;border-radius:12px;overflow:hidden;box-shadow:0 0 20px rgba(0,0,0,.4)}
        .iframe-wrap{position:relative;padding-top:133.33%;width:100%}
        .iframe-wrap iframe{position:absolute;left:0;top:0;width:100%;height:100%;border:0}
        .liberar-wrap{text-align:center;margin:14px 0}
        .btn-primary{background:#ff6b6b;color:#fff;padding:12px 18px;border-radius:10px;text-decoration:none;display:inline-block}
        .contador{padding:12px;text-align:center;background:#111;border-radius:10px;margin-top:10px}
        .tempo{font-size:1.6rem;color:#ff6b6b;font-weight:700}
        .meta{font-size:.92rem;color:#ccc;margin-top:6px}
        @media(min-width:700px){body{padding:40px}}
    </style>
</head>
<body>
    <div class="container">
        <div class="titulo"><h1>Do Paixão para a Minha Paixão</h1></div>

        <div class="progresso">
            <div id="dia-numero" class="dia-numero">1</div>
            <div class="barra-container"><div id="barra" class="barra"></div></div>
        </div>

        <div id="conteudo" class="conteudo-container" aria-live="polite"></div>

        <div id="liberar" class="liberar-wrap" style="display:none">
            <a id="liberar-link" class="btn-primary" href="#">Ir para o site principal</a>
        </div>

        <div class="contador">
            <div id="tempo" class="tempo">00:00:00</div>
            <div class="meta">Até o próximo conteúdo</div>
        </div>
    </div>

    <script>
    (function(){
        'use strict';

        // ---------- CONFIGURAÇÃO (edite aqui) ----------
        const USER = 'SEU_USUARIO_GITHUB';
        const REPO = 'SEU_REPOSITORIO';
        // Se você usar Kinescope, aqui o iframe padrão (substitua pelo seu).
        const DEFAULT_KINESCOPE_IFRAME = 'https://kinescope.io/embed/fFQj6uS7LPKfJnCbUd7Hwm';
        // Tempo mínimo para liberar o botão (em segundos). Usado quando não é possível detectar fim do vídeo.
        const FALLBACK_UNLOCK_SECONDS = 20;
        // ------------------------------------------------

        const RAW = `https://raw.githubusercontent.com/${USER}/${REPO}/main/`;
        const VIDEOS = RAW + 'videos/';
        const IMAGES = RAW + 'images/';

        // Função utilitária: formata tempo HH:MM:SS
        function formatHHMMSS(totalMs){
            if(totalMs <= 0) return '00:00:00';
            const s = Math.floor(totalMs/1000);
            const hh = String(Math.floor(s/3600)).padStart(2,'0');
            const mm = String(Math.floor((s%3600)/60)).padStart(2,'0');
            const ss = String(s%60).padStart(2,'0');
            return `${hh}:${mm}:${ss}`;
        }

        // Inicia: garante início_jornada
        function ensureStart(){
            let inicio = localStorage.getItem('inicio_jornada');
            if(!inicio){
                inicio = new Date().toISOString();
                localStorage.setItem('inicio_jornada', inicio);
            }
            return new Date(inicio);
        }

        // Calcula dia atual (1..30)
        function obterDiaAtual(){
            const inicio = ensureStart();
            const diffMs = Date.now() - inicio.getTime();
            const dia = Math.min(30, Math.floor(diffMs / (1000*60*60*24)) + 1);
            return dia;
        }

        // Próximo desbloqueio baseado no início + dia*24h
        function proximoDesbloqueio(dia){
            const inicio = new Date(localStorage.getItem('inicio_jornada'));
            // desbloqueio do dia = inicio + dia*24h (dia indexado a 1)
            const unlock = new Date(inicio.getTime() + dia * 24 * 60 * 60 * 1000);
            return unlock;
        }

        // Atualiza barra e número
        function atualizarProgresso(dia){
            const pct = Math.round((dia/30)*100);
            document.getElementById('dia-numero').textContent = dia;
            document.getElementById('barra').style.width = pct + '%';
        }

        // Carrega conteúdo (usa iframe Kinescope por dia se fornecido)
        // Você pode personalizar a lista KINESCOPE_IFRAMES com 30 entradas.
        const KINESCOPE_IFRAMES = (function(){
            // exemplo: return [ 'https://kinescope.io/embed/UID1', 'https://kinescope.io/embed/UID2', ... ];
            return [];
        })();

        function iframeForDay(dia){
            if(KINESCOPE_IFRAMES && KINESCOPE_IFRAMES.length >= dia && KINESCOPE_IFRAMES[dia-1]){
                return KINESCOPE_IFRAMES[dia-1];
            }
            return DEFAULT_KINESCOPE_IFRAME; // fallback
        }

        function carregarConteudo(dia){
            const wrap = document.getElementById('conteudo');
            wrap.innerHTML = '';

            // sempre usar vídeo (por pedido)
            const iframeUrl = iframeForDay(dia);
            const html = `<div class="iframe-wrap" aria-hidden="false"><iframe src="${iframeUrl}" allow="autoplay; fullscreen; picture-in-picture; encrypted-media; clipboard-write" loading="lazy" ></iframe></div>`;
            wrap.innerHTML = html;

            // preparar liberação do botão: tentaremos usar flag persistente para não reiniciar contador de liberação
            const unlockKey = `liberado_dia_${dia}`;
            if(localStorage.getItem(unlockKey) === 'true'){
                showLiberar();
            } else {
                startUnlockTimer(dia, unlockKey);
            }
        }

        // Mostra botão liberar
        function showLiberar(){
            const lib = document.getElementById('liberar');
            lib.style.display = 'block';
        }

        // Timer fallback para liberar (quando não podemos detectar fim do iframe)
        function startUnlockTimer(dia, unlockKey){
            // Se já tiver sido liberado no mesmo dia, mostra
            if(localStorage.getItem(unlockKey) === 'true'){
                showLiberar();
                return;
            }

            // calculamos tempo restante até próximo desbloqueio (apenas para UI do contador)
            const unlockAt = proximoDesbloqueio(dia);
            const now = Date.now();
            const remainingMs = unlockAt.getTime() - now;

            // Se o desbloqueio natural já passou, liberar imediatamente
            if(remainingMs <= 0){
                localStorage.setItem(unlockKey,'true');
                showLiberar();
                return;
            }

            // Fallback: liberar após FALLBACK_UNLOCK_SECONDS (persistente por dia)
            const fallbackMs = FALLBACK_UNLOCK_SECONDS * 1000;
            const timerMs = Math.min(remainingMs, fallbackMs);

            setTimeout(()=>{
                localStorage.setItem(unlockKey,'true');
                showLiberar();
            }, timerMs);
        }

        // Contador mostrando tempo até próximo desbloqueio
        function iniciarContador(dia){
            const el = document.getElementById('tempo');
            function tick(){
                const unlockAt = proximoDesbloqueio(dia);
                const remain = unlockAt.getTime() - Date.now();
                el.textContent = formatHHMMSS(remain);
            }
            tick();
            setInterval(tick,1000);
        }

        // Inicialização
        function init(){
            const dia = obterDiaAtual();
            atualizarProgresso(dia);
            carregarConteudo(dia);
            iniciarContador(dia);

            // configurar link do botão liberar (alterar href caso queira)
            const liberarLink = document.getElementById('liberar-link');
            liberarLink.href = 'https://seusite.com';
            liberarLink.addEventListener('click', function(){
                // aqui você pode registrar evento, analytics, etc.
            });
        }

        // Run
        document.addEventListener('DOMContentLoaded', init);

    })();
    </script>
</body>
</html>
