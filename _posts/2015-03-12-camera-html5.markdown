---
layout:     post
title:      "Manipulando câmera utilizando HTML5 e JS"
subtitle:   "Front-drops #s01e01 - Pequeno tutorial rápido de como usar html5 e javascript para tirar fotos."
date:       2015-03-12 12:00:00
author:     "Wellington Mitrut"
tags:       HTML5, Javascript, front drops
comments:   true
header-img: "img/posts/front/01/head.jpg"
---

<p>Olá pessoal, tudo certo? Tenho mudado mais de casa dos meus blogs que  de roupa não é mesmo? Acontece que 2014 foi um ano corrido e 2015 promete ser um ano de grandes realizações, o que aconteceu na real é que eu não encontrava nenhum lugar que realmente imprimisse minha personalidade e que tivesse uma forma objetiva de apresentar as coisas, o que agora parece acontecer aqui no nosso amigo <a href="http://github.com/">GitHub</a>.</p>

<p>Nada melhor para inaugurar a casa que o primeiro episódio do meu novo projeto, o Front-Drops, pequenas doses e tutorias de CSS, javascript, html5 e afins para você, de forma esporádica, aleatória e dependendo da minha boa vontade.</p>

<p>Então vamos começar! Sublime Text / Atom / VIM aberto? Então bora codar!</p>


<h2 class="section-heading">Pequenos conceitos.</h2>

<p>O HTML5 é fantástico. Mesmo sendo o "5" apenas uma marca, um conceito para servir como divisor de águas entre a Old-Web e a web modernosa. Falarei sobre HTML5 especificamente em um post futuro, mas o que posso adiantar é que como diz <a href="https://twitter.com/ebidel">Eric Bidelman</a> do Google:

<blockquote>"captura de áudio / e vídeo foram o "Santo Graal" de desenvolvimento web por um longo tempo.</blockquote>

Mas o jogo mudou, visto que agora, não precisamos mais de recursos externos como o finado Flash ou até mesmo o monstrinho Silverlight para manipulação de mídias via web.</p>

<p>Talvez não tenha caído ainda no gosto popular (ou tenha e eu to falando merda), mas o HTML5 trouxe uma possibilidade muito maior de acesso ao hardware do dispositivo que você está utilizando, seja fone ou notebook. Desde Geolocation (GPS), acelerômetro, WebGL (GPU), e áudio. exemplos perfeitos e que são ridiculamente poderosos, utilizando APIs JavaScript de alto nível, tirando todo proveito possível de recursos de hardware subjacentes do sistema.</p>

<p>Hoje trabalharemos em uma  destas novas APIs, a <i> navigator.getUserMedia()</i>, que permite que aplicativos da web terem acesso à câmera e o microfone de um usuário.</p>

<blockquote>Antes de mais nada, seria interessante, se você for fazer este tutorial, verificar se seu navegador possui suporte para esta API, caso ela não possua, lhe indico atualizar para um navegador moderno. Para verificar se seu navegador tem suporte, clique <a href="http://caniuse.com/#feat=stream">aqui</a>.</blockquote>

<h2 class="section-heading">Botando a mão na massa!</h2>

<p>Espero que você já tenha feito uma estrutura básica de html com body, head e tudo mais aí pra facilitar a sua vida, caso esteja procurando algo mais estruturado ou apenas com um pouco de preguiça, lhe recomendo o <a href="https://html5boilerplate.com/">HTML5 Boilerplate</a>, você vai ter uma boa estrutura básica e teremos como começar nosso micro-projeto aí seguindo as melhores práticas.</p>

<p>O que faremos hoje, é uma estrutura semelhante à foto abaixo, onde destaco a foto e a camera para que você entenda melhor, aquele bloco azul logo abaixo da camera é o botão que irá tirar a foto. Então, bora fazer!</p>

<a href="#">
    <img src="{{ site.baseurl }}/img/posts/front/01/exemplo1.png" alt="Post Sample Image">
</a>
<span class="caption text-muted">Sim, essa beleza (ou a completa falta dela) aí em cima sou eu.</span>

<p>A idéia deste tutorial surgiu da minha experiência com captura de imagens para webcam como desejado para um projeto do qual faço parte, o <a href="https://www.academi.as/">Academi.as</a>, um software gestor de academias, e o <i>product owner</i> queria que no ato do cadastro de um novo aluno, o dono da academia pudesse tirar uma foto do respectivo aluno.</p>

<p>Porém, os exêmplos que encontrei de captura de imagens, ou eram muito vagos, ou iam muito além do que eu precisava, que era a pura captura, após várias tentativas, decidi mesclar os dois melhores que eu achei, o do <a href=" http://davidwalsh.name/browser-camera">David Walsh</a> da Mozilla e do anteriormente citado <a href=" http://www.html5rocks.com/en/tutorials/getusermedia/intro/">Eric Bidelman</a>, no HTML5ROCKS (ambos os blogs recomendadíssimos, por sinal) .</p>

<p>Primeiro, criamos uma div que englobará nossos três elementos, o vídeo, que estará pegando o streamming da câmera, o canvas, que irá receber nossa imagem capturada e o input button, que irá disparar o evento de captura do script.</p>

    <div class="camera_snap">
        <video autoplay id="vid"></video>
        <canvas id="canvas" width="640" height="480"></canvas>
            <br />
        <input type="button" class="snapbutton"
        onclick="snapshot()"/>
    </div>

<p>Para estilizar, podemos colocar o seguinte código CSS:</p>

    video#vid,canvas#canvas {
        width: 300px;
        height:225px;
        border: 3px solid #d3d3d3;
    }
    video#vid{
        border: 3px solid #d3d3d3;
    }
    canvas#canvas {
        border: 3px solid #d3d3d3;
    }
    .camera_snap>input[type="button"] {
        border: none;
        padding: 1%;
        width: 37px;
        color: #fff;
        transition: 0.1s all;
    }
    .camera_snap>input[type="button"]:active{
        opacity:0.4;
        width:30px;
        background-size: cover;
        -moz-background-size: cover;
    }

<p>Logo abaixo do nosso input, dentro da div que engloba todos os elementos, podemos abrir nosso bloco de javascript, colocando o seguinte bloco de script:</p>

    <script type="text/javascript">
        var video = document.querySelector("#vid");
        var canvas = document.querySelector('#canvas');
        var ctx = canvas.getContext('2d');
        var localMediaStream = null;

<p>Adicionamos também, um gatilho de mensagem para o console, caso dê tudo errado:</p>

    var onCameraFail = function(e) {
        console.log('Não funcionou ://// .', e);
    };

<p>No bloco abaixo, inicializamos a função <i>snapshot</i> de captura da nossa câmera, que irá por sua vez usar a getUserMedia de vários motores de renderização, webkit (para Chrome e Safari), Gecko (para firefox) e também irá operar nas últimas versões do Internet (câncer) Explorer.</p>

    function snapshot() {
        if (localMediaStream) {
            ctx.drawImage(video, 0, 0);
        }
    }
    navigator.getUserMedia = navigator.getUserMedia
    || navigator.webkitGetUserMedia
    || navigator.mozGetUserMedia
    || navigator.msGetUserMedia;
    window.URL = window.URL || window.webkitURL;
    navigator.getUserMedia({
        video : true
        }, function(stream) {
            video.src = window.URL.createObjectURL(stream);
            localMediaStream = stream;
            }, onCameraFail);

<p>Caso nosso querido script esteja de acordo e nossa cãmera esteja habilitada, é esperado que ela mostre sua com o streamming da câmera no local onde você definiu a tag vídeo, ao você clicar no botão de captura, ele irá jogar a imagem capturada no canvas. Agora é só salvar e correr pro abraço, sua câmera com HTML5 e JS está funcionando :D</p>

<p>Em breve farei um tutorial sobre css filters, tentado clonar alguns dos efeitos do Instagram, mas isto tudo vai depender do feedback de vocês.</p>

<p>Gostou do tutorial? Alguma dúvida? Comente abaixo, diga o que achou e compartilhe, caso encontre um erro, também manda que corrigimos assim que possível, obrigado :D</p>
