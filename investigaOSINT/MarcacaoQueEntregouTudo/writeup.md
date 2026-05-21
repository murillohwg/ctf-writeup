# Writeup — CTF OSINT/GEOINT: "A Marcação que Entregou Tudo"

![Certificado](./assets/certified.png) 

## Descrição do desafio

> “Uma das regras de ouro do OSINT não é só o que você posta… é o que postam sobre você.
> Muita gente acredita que está segura porque não compartilha nada nas redes sociais.
> Mas esquece de um detalhe crítico: amigos, familiares e conhecidos podem postar fotos, marcar pessoas e revelar pistas sem perceber.
>
> Foi exatamente isso que aconteceu.
>
> Um suspeito procurado pela polícia da Espanha entrou discretamente no Brasil. Ele não publicou nada. Nenhum story. Nenhuma localização.
>
> Mas alguém próximo cometeu um erro: postou uma foto em uma rede social e o marcou.
>
> Agora sua missão como investigador é rastrear essa pista.
>
> Sabemos apenas que a imagem foi feita em São Paulo, dentro de um parque.”

Formato da flag:

```text
FLAG{XXXXXX_XXXXX_XXXXX}
```

---

# Objetivo

Identificar o local exato onde a fotografia foi tirada utilizando técnicas de GEOINT/OSINT.
![image](./assets/image.png) 
fotografia

---

# Análise inicial da imagem

Ao observar a imagem, alguns elementos chamam atenção imediatamente:

* Um grande rio/canal atravessando a cena;
* Uma via expressa ao lado do rio;
* Área extremamente arborizada;
* Estruturas urbanas densas ao fundo;
* Uma roda-gigante visível na parte inferior da imagem;
* A fotografia aparentemente foi tirada de dentro da própria roda-gigante.

Além disso, o desafio já informava que o local ficava em São Paulo e dentro de um parque.

---

# Primeira hipótese

A combinação:

* rio/canal;
* grandes avenidas;
* área verde extensa;
* paisagem urbana de São Paulo;

levou rapidamente à hipótese de que a imagem havia sido feita próxima às marginais da cidade.

Em São Paulo, poucos locais combinam:

* parque;
* rio;
* pista expressa;
* vista elevada.

Isso reduziu drasticamente o espaço de busca.

---

# Investigação GEOINT

A estratégia utilizada foi simples e eficiente:

1. Procurar parques localizados próximos às marginais de São Paulo;
2. Comparar a geometria do rio;
3. Observar a disposição das vias;
4. Procurar estruturas semelhantes à roda-gigante.

Durante essa etapa, um detalhe extremamente importante ajudou:

A imagem mostra claramente uma roda-gigante branca.

Isso praticamente elimina vários parques da cidade.

---

# Identificação da roda-gigante

Pesquisando por:

```text
roda gigante são paulo marginal parque
```

foi possível encontrar a roda-gigante localizada no Parque Cândido Portinari, ao lado do Parque Villa-Lobos.

A estrutura corresponde exatamente à imagem:

* cabine branca;
* estrutura metálica;
* vista para o Rio Pinheiros;
* Marginal Pinheiros ao lado;
* vegetação extensa;
* skyline compatível.

---

# Confirmação visual

A confirmação veio comparando:

* direção do rio;
* disposição das pistas;
* prédios ao fundo;
* área arborizada;
* posição relativa da marginal;
* altura da roda-gigante.

Tudo correspondia perfeitamente.

Além disso, o círculo roxo na imagem parece destacar justamente uma região do horizonte, provavelmente usada pelo criador do desafio para dificultar levemente a identificação.

Mesmo assim, os elementos estruturais do ambiente já eram suficientes.

---

# Local identificado
```

próximo ao:

```text
Parque Villa-Lobos
```

em São Paulo.

---

# Técnica OSINT/GEOINT utilizada

Este desafio envolveu principalmente:

* GEOINT visual;
* reconhecimento de padrões urbanos;
* análise de infraestrutura;
* correlação geográfica;
* redução do espaço de busca;
* validação visual com imagens públicas.

---

# Lição do desafio

O ponto central do desafio é demonstrar que:

> Mesmo que uma pessoa não publique nada diretamente, terceiros podem expor sua localização involuntariamente.

Uma única foto contendo:

* paisagem;
* estruturas urbanas;
* elementos arquitetônicos;
* vias;
* vegetação;

já pode ser suficiente para localizar alguém.

---

# Flag

```text
FLAG{PARQUE_VILLA_LOBOS}
```

---

# Conclusão

Esse foi um desafio clássico de GEOINT baseado em reconhecimento visual.

A resolução foi possível principalmente pela combinação entre:

* conhecimento urbano;
* observação de padrões;
* eliminação de hipóteses;
* correlação entre parque + marginal + roda-gigante.

Mesmo sem metadados, coordenadas ou informações explícitas, a imagem continha pistas suficientes para identificar o local exato.
