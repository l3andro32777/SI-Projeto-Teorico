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
O presente relatório irá ser abordada a `"Binary Reverse Engineering"`, um tipo de RE cujo objetivo é ficar o mais perto possível do código fonte de um binário ou programa, no caso de não existir acesso ao código-fonte do programa original, visto que não é Open Source.
Serão, também, abordadas aplicações de RE, um exemplo prático e um outro tema relacionado com `Warez Scene`, que utiliza estas técnicas para distribuir conteúdo gratuito, através da Internet.

## Objetivos

RE é uma área muito especializada e requer um `conhecimento consistente de programação e Assembly`.

Qualquer uma das seguintes aplicações de RE requer vasta experiência e, em alguns, é necessário ser um perito:
- Encontrar vulnerabilidades no intuito de melhorar a segurança do programa.
- Analisar malware em situações onde os antivírus não conseguem.
- Recriar funcionalidades ou o programa inteiro.
- Crackear as defesas de DRM para poder usar o programa sem pagar.
- Desenvolvimento de cheats/trainers para jogos.

Vamos falar principalmente dos pontos 1 e 4. Mas primeiro temos que perceber como é que funcionam os programas e como fazer engenharia reversa.

