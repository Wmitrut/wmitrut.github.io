---
layout:     post
title:      "Entendendo e usando CSS filters para replicar o Instagram - PARTE 1"
subtitle:   "Front-drops #s01e02 - Como usar CSS filters e imitar efeitos como do Instagram."
date:       2015-04-08 12:00:00
author:     "Wellington Mitrut"
tags:       HTML5, Javascript, front drops
comments:   true
header-img: "img/posts/front/01/head.jpg"
---

<p>Depois de uma boa demora, voltaremos com a série de dicas de front-end aqui no blog, tente acompanhar, toda quarta sai o post e tem muito mais novidades programadas pra você vindo por aí.</p>

<p>Para começar, hoje teremos a parte 1 deste texto sobre o instagram, contando a história e alguns conceitos sobre cores em computadores.</p>


<h2 class="section-heading">Um pouco de história...</h2>

<p>O <a target="_blank" href="http://instagram.com">Instagram</a>, para quem não conhece, é um serviço de compartilhamento de fotos / Rede social que é utilizada de forma exclusiva pelo celular criada por <a target="_blank" href="https://twitter.com/KEVIN">Kevin Systrom</a> e pelo brasileiro <a target="_blank" href="https://twitter.com/mikeyk">Mike Krieger</a>, esse aplicativo permite que seus usuários tirem fotos com seu aparelho móvel em estilo Polaroid, fotos quadradas, nas quais podem ser aplicados filtros vintage para dar um ar cult à estas fotos, podendo assim compartilha-las com os demais usuários, funcionando de forma similar ao Twitter onde você segue e é seguido por outras pessoas.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/front/02/instagraminterface.jpg">
<span class="caption text-muted">Interface do instagram.</span>

<p>Em 2012, o Facebook anunciou a aquisição do Instagram. O valor pago pela startup foi avaliado em US$ 1 bilhão. Desde então, ele vem sido implementado e melhorado, tendo ganhado uma lista enorme de novas funcionalidades e derivações:</p>

<ul>
  <li>Ganhou suporte para mensagens/fotos diretas no Android e iOS.</li>
  <li>Recebeu uma atualização grande no Android, que padronizou o visual com a versão do iOS e diminuiu drasticamente o “peso” do app.</li>
  <li>No iOS, o efeito “Lux” ganhou uma barra para controlar a intensidade.</li>
  <li>Lançou um novo app para iOS, o Hyperlapse.</li>
  <li>Passou a exibir anúncios nos EUA.</li>
  <li>Liberou a opção de editar legendas das fotos no Android e iOS.</li>
  <li>Lançou cinco novos filtros e suporte a vídeos em câmera lenta, para Android e iOS.</li>
  <li>Mudou a exibição dos vídeos, de apenas uma para mostrá-los em loop eterno.</li>
  <li>Acrescentou suporte a carrossel de imagens para anúncios.</li>
  <li>Lançou o Layout, app para criar colagens de fotos, para o iOS.</li>
</ul>

<p>Um exêmplo de foto do instagram é esta abaixo:</p>

<blockquote class="instagram-media" data-instgrm-captioned data-instgrm-version="4" style=" background:#FFF; border:0; border-radius:3px; box-shadow:0 0 1px 0 rgba(0,0,0,0.5),0 1px 10px 0 rgba(0,0,0,0.15); margin: 1px; max-width:658px; padding:0; width:99.375%; width:-webkit-calc(100% - 2px); width:calc(100% - 2px);"><div style="padding:8px;"> <div style=" background:#F8F8F8; line-height:0; margin-top:40px; padding:50% 0; text-align:center; width:100%;"> <div style=" background:url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACwAAAAsCAMAAAApWqozAAAAGFBMVEUiIiI9PT0eHh4gIB4hIBkcHBwcHBwcHBydr+JQAAAACHRSTlMABA4YHyQsM5jtaMwAAADfSURBVDjL7ZVBEgMhCAQBAf//42xcNbpAqakcM0ftUmFAAIBE81IqBJdS3lS6zs3bIpB9WED3YYXFPmHRfT8sgyrCP1x8uEUxLMzNWElFOYCV6mHWWwMzdPEKHlhLw7NWJqkHc4uIZphavDzA2JPzUDsBZziNae2S6owH8xPmX8G7zzgKEOPUoYHvGz1TBCxMkd3kwNVbU0gKHkx+iZILf77IofhrY1nYFnB/lQPb79drWOyJVa/DAvg9B/rLB4cC+Nqgdz/TvBbBnr6GBReqn/nRmDgaQEej7WhonozjF+Y2I/fZou/qAAAAAElFTkSuQmCC); display:block; height:44px; margin:0 auto -44px; position:relative; top:-22px; width:44px;"></div></div> <p style=" margin:8px 0 0 0; padding:0 4px;"> <a href="https://instagram.com/p/lAcPM8FfHv/" style=" color:#000; font-family:Arial,sans-serif; font-size:14px; font-style:normal; font-weight:normal; line-height:17px; text-decoration:none; word-wrap:break-word;" target="_top">Preguiça</a></p> <p style=" color:#c9c8cd; font-family:Arial,sans-serif; font-size:14px; line-height:17px; margin-bottom:0; margin-top:8px; overflow:hidden; padding:8px 0 7px; text-align:center; text-overflow:ellipsis; white-space:nowrap;">Uma foto publicada por Wellington Mitrut (@wmitrut) em <time style=" font-family:Arial,sans-serif; font-size:14px; line-height:17px;" datetime="2014-03-01T16:35:21+00:00">Mar 1, 2014 às 8:35 PST</time></p></div></blockquote>
<script async defer src="//platform.instagram.com/en_US/embeds.js"></script>

<p>Mas como é que o instagram altera as fotos e aplica estes filtros que tornam nossas fotos tão bonitas?</p>

<h2 class="section-heading">Pixels, binários e hexadecimais.</h2>

<p>Como sabemos, fotos são pixels na tela e pixels são, segundo a wikipedia:</p>

<blockquote>"o menor elemento num dispositivo de exibição (como por exemplo um monitor), ao qual é possível atribuir-se uma cor. De uma forma mais simples, um pixel é o menor ponto que forma uma imagem digital, sendo que o conjunto de milhares de pixels formam a imagem inteira."</blockquote>

<p>Ainda, segundo o site <a href="http://petapixel.com/2010/11/04/first-digital-photograph-ever-made/">Petapixel</a>, a primeira imagem digital veio a surgir em 1957, quando Russell Kirsch, inventor do scanner, reproduziu uma foto do seu filho de 3 meses em uma imagem digital de 176 x 176 pixels.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/front/02/firstdigitalimage.jpg">
<span class="caption text-muted">Primeira imagem digital, feita por Russell Kirsch em 1957.</span>

<p>No video abaixo, Kevin e o pessoal do Code.org explicam de forma detalhada como os pixels se apresentam na tela do computador e como os filtros do instagram funcionam na variação de uso de rgb:</p>

<iframe width="560" height="315" src="https://www.youtube.com/embed/15aqFQQVBWU" frameborder="0" allowfullscreen></iframe>

<h2 class="section-heading">RGB, RYB, CMYK...</h2>

<p>No vídeo, fica claro que para que o computador entenda o que é uma cor, é necessário que existam valores de três cores primárias, cuja variação dará origem à todas as outras cores do espectro visivel, essas cores são RED(R -  Vermelho), GREEN (G - Verde) e BLUE (B - Azul). RGB.</p>

<p>Alguns leitores podem achar que essa constatação de que as cores primarias são vermelho, verde e azul está um tanto quanto errada, mas não, temos vários padrões de cores, o padrão RYB (red, yellow, blue) é, na verdade, uma base de cores primárias subtrativas. Cores primárias subtrativas formam outras cores através da absorção de luz, como nos foi ensinado nas aulas de artes.</p>

<p>Por exemplo, se você mistura tintas amarela e azul, teremos uma cor verde mais escura, correto? Isto ocorre porque o novo pigmento absorve tanto as frequências amarela e azul - as frequências que sobram e são refletidas "causam" a sensação da cor verde. Assim sendo, quanto mais tinta você misturar, mais escuro o pigmento vai ficar, porque absorverá mais cores.</b>

<p>As telas de computadores e celulares, porém, não refletem luz - ao contrário, elas emitem luz. Neste caso, "misturar os pigmentos" implica na verdade em emitir luz em várias frequências. Isto significa que, quanto mais cores são emitidas, mais clara será a cor. Claro que a combinação não poderia ser a mesma das cores subtrativas - na verdade, é o processo contrário: As cores primárias aditivas mais usadas são as cores secundárias das cores subtrativas primárias mais comuns, e vice versa.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/front/02/rgb.png">
<span class="caption text-muted">Esquema de cores RGB.</span>


<p>Essa base é conhecida como CMYK (do inglês "Cyan, Magenta, Yellow and Key (preto)") e é extremamente importante em design e impressão. Se você olhar o cartucho de uma impressora a tinta, provavelmente verá estas quatro cores. (O preto vai junto porque, embora possa ser composto em teoria com as outras cores, é uma muito usada e compensa ser mandado à parte, além de facilitar o escurecimento dos outros tons. Também pode ocorrer de haver cartuchos de outras cores, dependendo dos usos da impressora.)</p>

<p>Foi um texto longo, mas extremamente importante para entender os conceitos dos CSS filters que aplicaremos com base nas cores RGB, recriando os efeitos do Instagram na semana que vem!</p>
