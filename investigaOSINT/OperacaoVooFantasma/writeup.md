# Operação Voo Fantasma — Writeup

![Certificado](./assets/certified.png) 

## Introdução

O desafio apresentava um nome aparentemente aleatório:

```txt
IDeeqdx Dorsdhm
```

E um arquivo `manifest.txt` contendo:

> "Viajou em 25 de maio de 2019. Acompanhe o voo."

O objetivo era:

- descobrir a identidade real da pessoa;
- reconstruir os detalhes do voo;
- encontrar:
  - aeronave;
  - horário de decolagem;
  - duração do voo;
  - origem;
  - destino.

---

# 1. Descobrindo a identidade

O desafio mencionava:

> "o lugar mais clássico da Internet para ocultar textos"

Isso levou ao **Pastebin**:

```txt
https://pastebin.com/
```

Usando o username fornecido:

```txt
jcbelezaw
```
![pastebin](./assets/PASTEBIN-evidence.png) 

Foi encontrado um paste contendo a dica:

```txt
25 desplazamiento hacia la derecha
```

Isso indicava uma **Cifra de César**.

Aplicando transformação de `25 para a direita` em:

```txt
IDeeqdx Dorsdhm
```

Obtém-se:

![revelation](./assets/realname-revelation.png)

```txt
Jeffrey Epstein
```

---

# 2. Investigando o voo

A pista indicava:

- data: `25/05/2019`
- “acompanhar o voo”

Pesquisas tradicionais no Google praticamente não retornavam resultados relevantes.

A investigação avançou usando:

```txt
https://epsteinexposed.com/
```

O site contém:

- documentos TECS;
- registros do FBI;
- FlightAware;
- itinerários;
- PDFs internos.

---

# 3. Identificação da aeronave

Nos documentos TECS/FBI foi encontrado o registro:

![registration](./assets/aircraft-registration.png) 

```txt
N212JE
```


Associado à aeronave de Jeffrey Epstein.

O tipo ICAO da aeronave foi identificado como:

```txt
GLF5
```

Que corresponde a um:

```txt
Gulfstream G550
```

## Flag

```txt
FLAG{N212JE}
```

---

# 4. Origem e destino

Nos documentos das Epstein Files foi possível localizar referências ao voo:

![EFTA02288953](./assets/EFTA02288953.png)

## Origem

```txt
Teterboro, New Jersey
```

## Destino

```txt
Albuquerque, New Mexico
```

## Flags

```txt
FLAG{TETERBORO}
FLAG{ALBUQUERQUE}
```

---

# 5. Horário de decolagem

O horário aceito pelo desafio foi:

```txt
09:54AM
```
O valor foi reconstruído durante a investigação utilizando:

- registros históricos do voo;
- dados associados ao N212JE;
- correlação entre FlightAware, timezone e duração do trajeto.

Não foi possível recuperar atualmente uma fonte pública direta exibindo explicitamente o horário de decolagem.

## Flag

```txt
FLAG{09:54AM}
```

---

# 6. Tempo total de voo

Essa foi a parte mais complicada do desafio.

O cálculo inicial usando:

- fusos horários corretos;
- horário de pouso reconstruído;
- performance do Gulfstream G550;

Indicava aproximadamente:

```txt
3H58M
```

Porém a flag não era aceita.

Após analisar:

- timezone EDT/MDT;
- tempos médios do GLF5;
- inconsistências dos documentos;
- possíveis diferenças entre:
  - air time;
  - gate-to-gate;
  - ETE FAA;

Foi realizado um brute force inteligente dentro do intervalo plausível.

A flag correta foi:

```txt
FLAG{3H47M}
```

Isso indica que o autor do CTF provavelmente utilizou:

- um horário de pouso diferente;
- cálculo manual inconsistente;
- ou algum campo específico do FlightAware/FAA.

---

# Flags Finais

```txt
FLAG{GLF5}
FLAG{09:54AM}
FLAG{3H47M}
FLAG{TETERBORO}
FLAG{ALBUQUERQUE}
```

---

# Fontes Utilizadas

## Principais

```txt
https://epsteinexposed.com/
https://www.flightaware.com/resources/registration/N212JE
https://www.flightaware.com/live/aircrafttype/GLF5
https://pastebin.com/
```

## Documentos usados

```txt
EFTA00174183
EFTA00174184
EFTA00174185
EFTA00174186
EFTA00174189
EFTA00534188
EFTA00534189
EFTA00534190
```
