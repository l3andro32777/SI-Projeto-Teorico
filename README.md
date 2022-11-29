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

![Processo de Engenharia Reversa](https://cdn.discordapp.com/attachments/855373378717351936/1047283111953702962/Processo.png)

Grande parte dos computadores - mais concretamente, os CPUs -, hoje em dia, utilizam `arquitetura x86-64`. Para um programa correr, é necessário que este seja compilado, previamente. O `código-fonte` é introduzido num `compilador` (o mais comum é o GNU C Compiler - GCC) e, em seguida, traduzido para `código-máquina`, que o computador entende e consegue executar.

Indo pelo `processo inverso`, é necessário compreender `Assembly`, que pode não ser uma tarefa fácil. É uma linguagem intermédia (entre código-máquina e código-fonte). Cada arquitetura, linguagem de programação e compilador possuem `diferentes formas de gerar código-máquina`, o que significa que o código em Assembly também apresentará diferenças.

No processo RE, normalmente, `uma pessoa não compreende o código-máquina`. Para isso, é necessária a posse de um *`Dissassembler`*, que mostra o código Assembly equivalente, sendo o `ponto de partida` para a compreensão do programa em causa.
Em seguida, podem ser utilizados um `Descompilador` e outras ferramentas, que permitem a geração de `pseudocódigo`. Decompiladores são muito poderosos, pois utilizam técnicas avançadas de `deobfuscação` e heurísticas para `gerar (pseudo)código de alto nível`.

