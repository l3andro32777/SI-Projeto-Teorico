a
# Reverse Engineering - Projeto Teórico

## Unidade Curricular

Segurança Informática

## Alunos

Leandro Francisco - 202001310

Daniel Lachkeev - 201801899

## Ano Letivo

2022/2023

## Introdução

*`Reverse Engineering`* ou `RE` é um método utilizado para compreender `o modo como um sistema fechado ou desconhecido realiza uma determinada tarefa` - o mesmo pode ser aplicado a dispositivos, software ou processos.
Essencialmente, é um processo de abertura e “dissecação” de um sistema, que permite descobrir como o mesmo funciona, com o objetivo de o `copiar e/ou melhorar`.
De um modo geral, “Reverse Engineering” permite `aquisição de conhecimento` que, dependendo da tecnologia em causa, tem a capacidade de auxiliar na recuperação de sistemas obsoletos, analisar a segurança de um sistema ou, simplesmente, compreender como algo funciona.
O presente relatório irá ser abordada a *`Binary Reverse Engineering`*, um tipo de RE cujo objetivo é ficar o mais perto possível do código fonte de um binário ou programa, no caso de não existir acesso ao código-fonte do programa original, visto que não é Open Source.
Serão, também, abordadas aplicações de RE, um exemplo prático e um outro tema relacionado com `Warez Scene`, que utiliza estas técnicas para distribuir conteúdo gratuito, através da Internet.

## Objetivos

RE é uma área muito especializada e requer um `conhecimento vasto de programação e Assembly`.

Qualquer uma das seguintes aplicações de RE requer vasta experiência e, em algumas, é necessário ser um perito:
- 1 - Encontrar vulnerabilidades, no intuito de melhorar a segurança de um programa;
- 2 - Analisar *malware*, quando antivírus não possuem essa capacidade;
- 3 - Recriar funcionalidades de um programa ou o próprio;
- 4 - Crackear as defesas de DRM, para poder usar um programa, sem pagar pelo mesmo;
- 5 - Desenvolvimento de *cheats/trainers* para jogos.

Os pontos 1 e 4 serão os principais a serem abordados.

## Assembly x86-64

![Processo de Engenharia Reversa](https://cdn.discordapp.com/attachments/855373378717351936/1047283111953702962/Processo.png)

Grande parte dos computadores - mais concretamente, os CPUs -, hoje em dia, utilizam `arquitetura x86-64`. Para um programa correr, é necessário que este seja compilado, previamente. O `código-fonte` é introduzido num `compilador` (o mais comum é o GNU C Compiler - GCC) e, em seguida, traduzido para `código-máquina`, que o computador entende e consegue executar.

Indo pelo `processo inverso`, é necessário compreender `Assembly`, que pode não ser uma tarefa fácil. É uma linguagem intermédia (entre código-máquina e código-fonte). Cada arquitetura, linguagem de programação e compilador possuem `diferentes formas de gerar código-máquina`, o que significa que o código em Assembly também apresentará diferenças.

Em RE, normalmente, `código-máquina não é compreendido`. Para isso, é necessária a posse de um *`Dissassembler`*, que mostra o código Assembly equivalente, sendo o `ponto de partida` para a compreensão do programa em causa.
Em seguida, podem ser utilizados um `Descompilador` e outras ferramentas, que permitem a geração de `pseudocódigo`. Decompiladores são muito poderosos, pois utilizam técnicas avançadas de `deobfuscação` e heurísticas para `gerar (pseudo)código de alto nível`.

![Processo de Engenharia Reversa](https://cdn.discordapp.com/attachments/855373378717351936/1047267281840902174/image.png)


## Ferramentas

### IDA Pro

Certamente é o software mais completo, e definitivamente “industry standard”. Tem um excelente suporte de plugins e a geração de pseudocódigo é a melhor. A IDA tem uma versão gratuita mas é bastante limitada porque só trabalha com x86 (32 bits) e x86-64 e apenas vem com um decompilador para 64 bits. Ou seja, se pretendemos trabalhar com outras arquiteturas temos que ir por outras opções, pois a versão Pro custa 2000€ e cada decompilador extra são no mínimo 2765€! [Fonte](https://www.hex-rays.com/cgi-bin/quote.cgi/products)
Isto cria uma imagem engraçada, pois originalmente a pessoa que crackeou IDA Pro para os outros puderem piratear deve tê-lo feito com o próprio IDA Pro.  

### Radare2

É um programa de linha de comandos mais indicado para RE de menor escala. Tem um grande fator de personalização e usa os decompiladores de Ghidra. Para certas tarefas e casos específicos, radare2 é o melhor.

### Ghidra

Ghidra é um competidor recente ao IDA Pro que foi lançado em 2019 e foi desenvolvido pela NSA dos Estados Unidos. É gratuito e open source e tem o melhor suporte de decompiladores e do API. Ghidra pretende destacar-se pois oferece colaboração integrada em projetos de RE. Em suma, tem muito potencial para crescimento com o suporte da comunidade.

## Demonstração Prática
Vamos agora fazer um simples desafio ou CTF que se designa por “crackme”. Isto são programas especialmente feitos para testar as capacidades de RE. O objetivo do crackme é perceber como o programa funciona para podermos inserir a palavra passe certa sem termos isso guardado em texto em algum lado. No final inserimos a passe certa para confirmar que completamos o desafio.
Vou pegar num exemplo básico para vermos como se faz.

O nome deste programa é “keyg3nme” e vamos resolver em Linux. Resolução deste crackme foi tirada deste [link](https://medium.com/@Asm0d3us/1-crackmes-one-beginner-friendly-reversing-challenges-6df94ea6b29d).

Comecemos por executar o comando file para determinar o tipo de ficheiro.

![](https://miro.medium.com/max/720/1*eKVYyzX9PVD4f6QtMaMqnQ.png)

Podemos então ver que keyg3nme é um binário executável de Linux. Adicionamos permissões de execução caso não haja.

$ chmod +x keyg3nme

Agora executamos o programa

![](https://miro.medium.com/max/720/1*VxWW2xVIes4OBFYY3yCbjw.png)

Como podemos ver, não sabemos o que introduzir, e ataques de brute force não parecem fazer sentido aqui (para além de não ser o objetivo). 

Executamos o comando strings para achar o texto claro existente no programa que poderá dar algumas dicas ou uma chave hardcoded. 
![](https://miro.medium.com/max/720/1*kMSfVijiOhLlIujAM2RUkg.png)

- Enter your key :
- Good job mate, now go keygen me - aparece quando a passe estiver certa
- nope - aparece quando falha a passe
Como podemos observar, não há nada mais além disso que nos ajude. Portanto só nos resta usar ferramentas dedicadas. Aqui usamos Ghidra, que para a dificuldade deste desafio, é um pouco overkill. Vamos abrir e analisar o programa. Selecionamos a função main do lado esquerdo do menu.

![](https://miro.medium.com/max/640/1*IAtGAjAyU0mRUSlEYZPdrg.png)

E aqui temos pseudocódigo gerado. Tem aspeto muito sujo porque os nomes e tipos das variáveis não são os convencionais. Mas lendo com calma conseguimos chegar que local_14 é a chave que inserimos porque está no scanf. iVar1 é o resultado da validação da chave usando a função validate_key. Portanto só nos resta ver essa função.

![](https://miro.medium.com/max/598/1*ypSPaH2Rje3nI15hh0e58Q.png)

Nota-se que a função no fundo verifica se a chave é um múltiplo de 1223 usando o módulo operador. Portanto inserindo 1223, por exemplo, vai resolver o desafio.

![](https://miro.medium.com/max/720/1*JBfIi2iIdHI6xz6bwBmfiw.png)

Cá está e está concluído o desafio! Com este exemplo simples claramente vemos a vulnerabilidade mas esta metodologia aplica-se independentemente da escala.

## DRM e Cracking

Uma consequência da existência de ferramentas de RE é a possibilidade de circum navegar as proteções de conteúdos com direitos de autor, DRM para eventualmente virem parar nos sites de torrent e de vídeos online. Isto aplica-se mais a software pago como Photoshop e videojogos.
Remover proteções DRM (especialmente de jogos com Denuvo) é uma das tarefas mais difíceis de RE. Atualmente existe só uma pessoa no mundo capaz de tirar este DRM da versão mais recente de Denuvo e é [EMPRESS](https://www.wired.com/story/empress-drm-cracking-denuvo-video-game-piracy/).

## Warez Scene

Esta é uma rede subterrânea onde os maiores crackers partilham o conteúdo pirateado. Qualquer filme, série, anime, videojogo que seja pago ou tenha proteção DRM tem alta chance de se originar daqui. 
Indivíduous ou equipas “na cena” compram o conteúdo que pretendem crackear e retiram as proteções. Ao lançar o conteúdo no que se designa por “Scene Release”, os autores deste lançamento costumam lançar um gráfico de arte em ASCII através de ficheiros .nfo onde podem fazer comentários, recrutar. Ganham crédito por estes lançamentos.

![](https://defacto2.net/images/uuid/original/54acf284-7df8-4764-b5ba-00b80f534c26.png)

Através desses créditos, eles adquirem conteúdo pirateado proveniente de outros grupos e assim há uma economia interna baseada em meritocracia. 
Claro que na vida real temos conteúdo pirateado facilmente disponível até que chegue. Isto porque há crackers que não estão nessa rede. E também há pessoas que estão em Warez que se aproveitam deste conteúdo para lançar publicamente em torrents, P2P (peer-to-peer). 
Warez Scene é um grande “rabbit hole” e eu só passei pela superfície do iceberg.
Este [post](https://reddit.com/r/CrackWatch/comments/92uz49/the_warez_scene_how_it_works/) explica com enorme detalhe o que é.

## Conclusão

Aprendemos o que é código Assembly e como podemos usar, para que serve engenharia reversa e as suas aplicações tal como um exemplo prático. Vimos também um efeito curioso que começou a desenvolver há mais de 20 anos a propagação de conteúdo pirateado e como relativamente escondido são as pessoas por detrás.

