---
layout:     post   
title:      "Aprenda a customizar mapas na sua aplicação Android com um pé nas costas"
subtitle:   "Esse artigo é uma transcrição de uma palestra que dei no GDG Cascavel e no GDG Pato Branco, adaptada na forma de artigo."
date:       2017-06-07 12:00:00
author:     "Wellington Mitrut"
tags:       Android, Design, Google Maps
comments:   true
header-img: "img/posts/other/map.png"
---

<blockquote>Esse artigo é uma transcrição de uma palestra que dei no GDG Cascavel e no GDG Pato Branco, adaptada na forma de artigo. Você tem total autorização para replicar. Seguem também os slides, link do github para você baixar e brincar um pouco, assim como link do hangout que fiz sobre o assunto. Agradecimentos especiais ao Walmyr Carvalho que foi com quem vi o assunto pela primeira vez e ao Everton Bortolini, amigo de longa data que contribui com curiosidades sobre cartografia.</blockquote>

<p>Mapas, acho que existem poucas pessoas senão nenhuma que não tenha tido contato com esse tipo de ‘tecnologia’. Segundo a wikipedia, um mapa é <i>“uma representação simbólica enfatizando as relações entre elementos de algum espaço, como objetos, regiões ou temas.”</i>, ou seja, um mapa é uma representação gráfica de uma região.</p>

<p>Segundo o Engenheiro Cartógrafo <a href="https://twitter.com/eTonBortolini" target="_blank">Everton Bortolini</a>, a <a href="http://icaci.org/mission/" target="_blank">ICACI</a> (International Cartography Association) tem as seguintes definições para mapas e cartografia :</p>

<h3>Mapa:</h3>

<blockquote>“Um mapa é uma representação simbolizada da realidade geográfica, representando características gerais ou características selecionadas, resultante do esforço criativo da execução de escolhas de seus autores, e é projetado para uso quando as relações espaciais são de relevância principal.”</blockquote>

<h3>Cartografia:</h3>

<blockquote>“A cartografia é a disciplina que trata da arte, ciência e tecnologia de fazer e usar mapas.”</blockquote>

<p>Um dos mapas mais antigos que se tem notícia, ainda segundo Bortolini, é o <a href="https://en.wikipedia.org/wiki/Bedolina_Map" target="_blank">Bedolina Map</a> que é um mapa feito numa pedra nos alpes italianos, sendo datado da idade do bronze. De lá para cá, a cartografia foi evoluindo e alcançando níveis altíssimos de precisão.</p>

<h3>Cartografia == UX</h3>
<p>Não é errado dizer que os primeiros UX designers foram os cartógrafos da idade média, eles tinham um trabalho hercúleo de pesquisa, cálculos, levantamento de dados e se ocorresse de criarem um design ruim ou que não entregasse aquilo que seus usuários pudessem entender… bem, seria uma User experience muitas vezes literalmente desastrosa.</p>

<figure style="text-align: center;">
    <img class="center" src="{{ site.baseurl }}/img/posts/other/mercator.png" style="margin: 0 auto;">
    <figcaption>Mercator, utilizando o Sketch ou o Figma da idade média.</figcaption>
</figure>


<p>Mas onde diretamente isto vem a ter uma intersecção com o nosso assunto de hoje? Bem, justamente a entrega de uma experiência decente com mapas em nossas aplicações pode se tornar o nosso diferencial.</p>

<p>É necessário se pensar além do branding quando vamos personalizar um mapa. Um mapa mal projetado, sem informações ou então com informações erradas pode custar muito para o seu usuário, as vezes <a href="http://g1.globo.com/rio-de-janeiro/noticia/2015/10/mulher-morre-apos-entrar-por-engano-em-comunidade-em-niteroi-rj.html" target="_blank" >mais do que você pode imaginar</a>.</p>

Então bora aprender como se personaliza um mapa no android de forma simples e sem precisar perder a dignidade?
As opções de personalização

<p style="margin: 0 auto;">&hellip;</p>



<p>Até pouco tempo atrás, personalizar os mapas no android demandava uma série de configurações, usar outras APIs externas, baixar libs e ficar um tempo considerável configurando. Ainda é possível utilizar alguns destes serviços e alguns deles realmente se destacaram, os principais você confere abaixo:<p>
<ul>
    <li><a href="https://here.com/en">Here Maps</a></li>
    <li><a href="https://www.mapbox.com/">Mapbox</a></li>
    <li><a href="https://www.openstreetmap.org/#map=5/51.500/-0.100">Open Street Maps</a></li>
    <li><a href="https://mapzen.com/">Mapzen</a></li>
</ul>

<p>Mas a principal opção de uso de mapas para android na maioria das aplicações ainda é a <a href="https://developers.google.com/maps/">Google Maps API.</a></p>
<p>Até pouco tempo atrás, todos os mapas que usavam exclusivamente a Google Maps API dependiam de algum serviço externo para que fossem personalizados, mas desde a versão da Google Play Services 9.6.0 é possível editar e personalizar os mapas de forma ‘nativa’, sem a necessidade de uma biblioteca externa.</p>

<p>Bom, a única ajuda externa que você vai precisar é talvez o <a href="https://mapstyle.withgoogle.com/">Google Maps Styling Wizard</a>. A não ser que você seja muito bom em criar JSON.</p>

<h2>Criando a nossa aplicação</h2>

<blockquote>Caso você não queira passar por tudo isso, você pode clonar um projeto demo que fiz lá no meu <a href="https://github.com/Wmitrut/custommapsgdgcascavel">Github</a>, os passos são praticamentes os mesmos.</blockquote>

<h3>1 — Crie um projeto novo no Android Studio com o template de mapas</h3>

<img class="center" src="{{ site.baseurl }}/img/posts/maps/newactivity.png" style="margin: 0 auto;">

<h3>2 — Abra o Google Maps Styling Wizard e personalize o mapa</h3>

<p>É sério, existem algumas opções prontas de mapas customizados, mas eu te indico entrar nele e começar a explorar, você consegue desde aplicar a densidade de informações até mesmo personalizar a cor de elementos de interesse deste mapa.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/maps/wizard.png" style="margin: 0 auto;">

<h3>3 — Baixe o arquivo JSON do Wizard e reserve na geladeira.</h3>

<p>O arquivo em média terá uns 5kb e aproximadamente 300 linhas, dependendo de como você personalizar.</p>

<h3>4 — Configure a sua chave de API no AndroidManifest.xml</h3>

<p>Sim, apesar de gerar um aplicativo preparado para receber dados do Google Maps a nossa parte a gente tem que fazer, ir lá no <a href="https://console.developers.google.com/?pli=1">Google Developers Console</a>, e requisitar a chave de API do Google Maps. Isto feito, é só colocar no AndroidManifest.xml e seguir o baile.</p>

<h2>Personalizando o nosso mapa com o tema criado</h2>

<p>Agora vem a parte legal e extremamente simples da nossa implementação. É onde a nossa aplicação deixará de ter a cara de Google Maps e passará a ter o estilo que criamos lá no wizard anteriormente.</p>

<h3>1 — Primeiro de tudo, crie uma pasta raw</h3>
<p>Lá dentro de sua pasta res crie uma nova pasta vazia chamada <code>raw</code>. Dentro desta pasta raw coloque o arquivo JSON que você personalizou e baixou no Map Wizard.</p>

<p>A estrutura vai ficar mais ou menos como esta</p>
<img class="center" src="{{ site.baseurl }}/img/posts/maps/pastas.png" style="margin: 0 auto;">

<h3>2 — Sete a sua view na activity de forma correta</h3>
<p>É importante que a sua view esteja corretamente setada tanto no .java (ou Kotlin) quanto no seu arquivo de layout XML.
No java você seta assim:</p>

<script src="https://gist.github.com/Wmitrut/83bd9a52de47456f983b1558b43e9977.js"></script>

<p>E no XML:</p>

<script src="https://gist.github.com/Wmitrut/37a978834aba9c01d01163f091c614c1.js"></script>

<h3>3 — Sete as coordenadas do seu ponto e chame o estilo do mapa</h3>
<p>Neste caso, eu criei os dados de forma fixa. Setei as coordenadas de Cascavel — PR e deixei num zoom de câmera do mapa que desse para visualizar até mesmo as BRs que cercam a cidade.
No caso, ficou assim:</p>

<code>LatLng cascavel = new LatLng(-24.952327, -53.461767);</code>
<p>E no java:</p>

<script src="https://gist.github.com/Wmitrut/b5232e2b6521d6c86b661cc7179ff193.js"></script>

<p>Note o primeiramente que a API do maps provê uma classe chamada <code>onMapReady()</code>, no caso, ela irá executar o código assim que o mapa estiver carregado em nossa view.</p>

<p>Para carregar o estilo eu abri um try-catch onde seto a situação de aplicação do estilo. No caso, se o estilo for carregado, eu apenas seto ele no meu mapa, senão, eu informo o erro que ocorreu no console. As configurações e chamadas seguintes são relativas ao que já falamos de ponto no mapa e zoom.</p>s

<h3>4 — Rode a aplicação</h3>
<p>Se tudo ocorrer bem, pronto — você tem uma aplicação demonstrativa com um mapa personalizada, agora você pode agregar mais valor ainda ao seu aplicativo com um mapa que possua a sua branding e um design único como os grandes players. Se você baixar o projeto do GitHub ele vai resultar em algo mais ou menos assim:</p>
<img class="center" src="{{ site.baseurl }}/img/posts/maps/device.jpeg" style="margin: 0 auto;">

<p>Caso você se interesse, este post é também uma palestra que fiz, os slides podem ser vistos abaixo:</p>

<script async class="speakerdeck-embed" data-id="bf05988c341347e18503b04c39380828" data-ratio="1.77777777777778" src="//speakerdeck.com/assets/embed.js"></script>

E um hangout que fizemos com o #GDGPATOBRANCO no dia 16 de Março de 2017 pode ser conferido aqui:

<iframe width="560" height="315" src="http://www.youtube.com/embed/https://youtu.be/-ey-iOdTX58?" frameborder="0" allowfullscreen></iframe>

