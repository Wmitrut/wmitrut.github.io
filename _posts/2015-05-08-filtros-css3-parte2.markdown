---
layout:     post
title:      "Entendendo e usando CSS filters para replicar o Instagram - PARTE 2"
subtitle:   "Front-drops #s01e03 - Como usar CSS filters e imitar efeitos como do Instagram.(continuação)"
date:       2015-05-08 12:00:00
author:     "Wellington Mitrut"
tags:       HTML5, Javascript, front drops
comments:   true
header-img: "img/post-bg-03.jpg"
---

<p>Olá, como prometido, o post hoje é mais prático e mostra uma aplicação do css filter tentando replicar os filtros do instagram.</p>

<p>Criei então, uma página de demonstração, a FILTRAGRAM, que você pode clonar do nosso repositório do <a target="_blank" href="https://github.com/Wmitrut/css-filter-example">GitHub</a> e fazer o que bem quiser com ele.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/front/03/filtragram.jpg">
<span class="caption text-muted">Interface do Filtragram.</span>

<p>Alguns filtros ficaram bons, outros ruins, isso tudo depende da imagem que você está aplicando, pois isto varia conforme os níveis de saturação original de cada imagem, no caso do celular, é a definição que manda na qualidade e na saturação da sua imagem.</p>

<p>Para facilitar o processo de estruturação do HTML e CSS, usei o <a target="_blank" href="http://getbootstrap.com/">Twitter Bootstrap</a>, o que me garantiu também uma interface, apesar de bem simples, responsiva e bem fácil de prototipar, deixando com que eu me preocupasse apenas com os filtros em si, fazendo com que todo o trabalho 'chato' ficasse por conta do framework.</p>

<img class="center" src="{{ site.baseurl }}/img/posts/front/03/responsive.jpg">
<span class="caption text-muted">Filtragram no celular.</span>

<p>Outra parte 'chata' do desenvolvimento ficou por conta do <a target="_blank" href="https://middlemanapp.com/">Middleman</a>, um gerador de páginas estáticas feito em Ruby derivado do Sinatra, onde toda parte de gerência de bibliotecas e assets ficou por conta dele.</p>


<p>Para rodar o projeto, você precisará executar os seguintes passos:</p>
   <p> <pre>
   <br>
    - Instalar/ter instalado Ruby 1.9.3 ou superior
    <br>
    - gem install middleman
    <br>
    - gem install bundler
   <br>
    - entrar no diretório onde clonou o repositório
   <br>
    - bundle install
    <br>
    - middleman server
    <br>
    - no seu navegador acesse: http://localhost:4567
    </pre>
</p>
<p>Pronto, agora desfrute como bem entender do projeto, estudando e alterando os filtros, explorando cada um deles, qualquer coisa, antes de alterar diretamente no código, você pode usar o Chrome DevTools para testar em realtime no seu navegador.</p>

<p><i>"Mas Mitrut, eu não sei usar o Chrome DevTools, como que eu faço?"</i> ora meu caro, mas isso é muito fácil, no canal do Youtube do Google Developers, o nosso amigo <a target="_blank" href=" https://twitter.com/zenorocha">Zeno Rocha</a> fez uma série EXATAMENTE sobre isso, que você pode conferir abaixo:</p>

<iframe width="560" height="315" src="https://www.youtube.com/embed/XUgfwYzv-WQ?list=PLOU2XLYxmsILUKyjDYUVYLeq7yyTxM_3d" frameborder="0" allowfullscreen></iframe>

<p>Gostou desta série sobre manipulação de imagens com html5 e css3? Quer aprender mais sobre isto? Então não perca mais tempo! Estamos oferendo um workshop introdutório sobre FRONT-END WEBDESIGN no dia 06/06/2015 na Invent.to Coworking. São apenas 20 vagas! Quer garantir a sua?<a target="_blank" href="http://wmitrut.github.io/workshops/"> Acesse aqui e saiba como!</a> Faremos tudo de uma maneira lúdica e inovadora, instigando o uso de criatividade para criar uma página simples para internet.</p>

<p>Aproveito também para deixar mais duas novidades aqui, a primeira delas é a nossa <a target="_blank" href="http://wmitrut.github.io/newsletter/">newsletter</a>, a qual faremos uma curadoria com o melhor conteúdo sobre webdesign e front end e lhe enviaremos periodicamente. Pode ficar tranquilo, nós odiamos spam, ela será cheia de conteúdo de primeira e não vamos abarrotar sua caixa de entrada com conteúdo inutil.</p>

<p>A segunda novidade é que, apartir da proxima semana, começarei a escrever sobre uma tecnologia front-end mantida pelo Google que estou simpatizando muito! <a target="_blank" href="https://angularjs.org/">O AngularJS</a>. Falou pessoal, até a próxima!</p>