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

RE é uma área muito especializada e requer um `conhecimento consistente de programação e Assembly`.

Qualquer uma das seguintes aplicações de RE requer vasta experiência e, em algumas, é necessário ser um perito:
- 1 - Encontrar vulnerabilidades, no intuito de melhorar a segurança de um programa;
- 2 - Analisar *malware*, quando antivírus não possuem essa capacidade;
- 3 - Recriar funcionalidades de um programa ou o próprio;
- 4 - Crackear as defesas de DRM, para poder usar um programa, sem pagar pelo mesmo;
- 5 - Desenvolvimento de *cheats/trainers* para jogos.

Os pontos 1 e 4 serão os principais a serem abordados.

## Assembly x86-64

![Processo de Engenharia Reversa](/Imagens/Processo.png)

Grande parte dos computadores (mais concretamente os CPUs) hoje em dia usam a arquitetura x86-64. Para um programa correr é necessário primeiro que este programa seja compilado. O código fonte é introduzido num compilador, o mais comum é o GNU C Compiler (gcc), e de seguida traduzido para código máquina que o computador entende e consegue executar.

Se pretendemos ir pelo processo inverso temos que compreender Assembly (não é uma tarefa fácil!). É uma linguagem intermédia entre código máquina e código fonte. Cada arquitetura, linguagem de programação e compilador tem maneiras diferentes de gerar código máquina que por sua vez também vai ter código Assembly diferente.

No processo RE, um humano normal não consegue perceber código máquina. 
Para isso temos em primeiro lugar um dissassembler que mostra o código Assembly equivalente e dá o ponto de partida para a compreensão do programa.
Em seguida podemos usar um decompilador e outras ferramentas que permitem a geração de pseudocódigo. Decompiladores são muito poderosos porque usam técnicas avançadas de deobfuscação e heurísticas para gerar (pseudo)código de alto nível, mas não são obrigatórios para o processo. 

