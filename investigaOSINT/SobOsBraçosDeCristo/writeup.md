# Writeup — CTF GEOINT/OSINT: "Sob os Braços de CRISTO"

![Certificado](./assets/certified.png) 

## Descrição do desafio

O desafio consistia em identificar a localização exata de uma fotografia relacionada a um evento de hacking/cybersecurity ocorrido no Rio de Janeiro.

As únicas informações iniciais disponíveis eram:

* a imagem havia sido tirada no RJ;
* o evento ocorreu em maio de 2025;
* o contexto estava relacionado à área de hacking/cybersecurity.

Formato da flag:

```text
FLAG{XXXXXXXXXXXX_XXXXX_XX_XXXXXXX}
```

---

# Objetivo

Descobrir o local exato relacionado à imagem utilizando técnicas de GEOINT/OSINT.

![IMAGEM](./assets/image(1).png)

---

# Análise inicial

A primeira abordagem foi baseada em correlação contextual.

Sabendo que:

* o evento era relacionado à segurança ofensiva/cybersecurity;
* aconteceu no Rio de Janeiro;
* ocorreu em maio de 2025;

foi realizada uma busca por eventos de segurança da informação realizados nesse período.

---

# Primeira hipótese

Durante a investigação, um dos primeiros resultados encontrados foi o evento:

```text
Security Leaders Rio de Janeiro 2025
```

realizado em:

```text
08/05/2025
```

A hipótese parecia plausível devido à proximidade temporal e ao contexto do desafio.

Além disso, um repositório público contendo eventos de infosec no Brasil ajudou na investigação:

```text
https://github.com/IncursioHack/Eventos-Infosec-Brasil
```

No entanto, ao analisar melhor:

* o formato da flag não correspondia;
* os nomes dos locais não encaixavam no padrão;
* a hipótese começou a perder força.

---

# Uso de Google Lens

Para aprofundar a investigação, foi utilizado:

* Google Lens;
* pesquisa reversa de imagem;
* comparação visual.

Essa etapa foi decisiva.

O Google Lens conseguiu identificar elementos compatíveis com:

```text
Universidade Veiga de Almeida
```

associados a conteúdos relacionados a eventos de hacking/cybersecurity.

---

# Engenharia reversa da flag

O ponto mais importante veio ao analisar o padrão da flag:

```text
FLAG{XXXXXXXXXXXX_XXXXX_XX_XXXXXXX}
```

Separando os blocos:

* 12 caracteres;
* 5 caracteres;
* 2 caracteres;
* 7 caracteres.

Ao comparar com:

```text
UNIVERSIDADE_VEIGA_DE_ALMEIDA
```

foi possível perceber:

* UNIVERSIDADE → 12 caracteres;
* VEIGA → 5 caracteres;
* DE → 2 caracteres;
* ALMEIDA → 7 caracteres.

O padrão encaixava perfeitamente.

---

# Flag correta

```text
FLAG{UNIVERSIDADE_VEIGA_DE_ALMEIDA}
```

---

# Técnicas utilizadas

Este desafio envolveu principalmente:

* GEOINT;
* OSINT;
* pesquisa contextual;
* correlação temporal;
* engenharia reversa de formato de flag;
* pesquisa reversa de imagem;
* validação visual.

---

# Dificuldades encontradas

Um detalhe interessante foi que nem todas as informações públicas indicavam claramente a realização do evento BSides naquele local.

Isso tornou a investigação mais confusa, porque:

* alguns resultados apontavam para outros eventos;
* havia múltiplos locais possíveis;
* o nome da instituição não parecia inicialmente a resposta mais óbvia.

A resolução acabou vindo da combinação entre:

* reconhecimento visual;
* análise do formato da flag;
* validação contextual.

---

# Lições aprendidas

Esse desafio reforça alguns pontos importantes em GEOINT/OSINT:

* nem sempre o evento é a resposta;
* muitas vezes o criador quer o nome do venue;
* o formato da flag pode revelar muito sobre a solução;
* ferramentas como Google Lens são extremamente úteis para validação;
* correlação contextual ajuda a reduzir o espaço de busca.

Além disso, o desafio mostrou a importância de não abandonar hipóteses iniciais cedo demais.

Mesmo antes da confirmação final, a investigação já havia passado pela universidade correta, mas o foco acabou sendo direcionado inicialmente para o nome do evento.

---

# Conclusão

Este foi um excelente desafio de GEOINT voltado para investigação contextual e reconhecimento de localização.

A resolução exigiu:

* análise investigativa;
* correlação de eventos;
* pesquisa reversa;
* reconhecimento de padrões;
* interpretação do formato da flag.

Mesmo sem coordenadas, metadados ou informações explícitas, foi possível identificar corretamente o local utilizando apenas fontes abertas e raciocínio analítico.
