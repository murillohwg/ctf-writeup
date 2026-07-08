# OSINT CTF Writeup — “A Ilha da Corrupção Vol. 08”

![Certificado](assets/certified.png)

## Descrição do Desafio

O desafio descreve um pequeno país afetado pela crise financeira de 2008, onde um político e sua esposa estavam ligados a uma empresa offshore associada a bancos falidos. Após a exposição no maior vazamento financeiro da história moderna, ocorreram protestos massivos e o político renunciou em menos de 48 horas.

Objetivo:

* Identificar a empresa offshore
* Nome completo da esposa
* Data de início e término da vinculação oficial

Formato das flags:

```
FLAG{XXXXXXX_XXX.}
FLAG{Xxxx_Xxxxxxxxx_Xxxxxxxxxx}
FLAG{DD-MM-AAAA_TO_DD-MM-AAAA}
```

***

## Estratégia de Resolução

### 1. Identificação do Evento

A pista mais importante foi:

> “11,5 milhões de documentos” “maior vazamento financeiro da história moderna”

Isso leva diretamente ao:

* **Panama Papers (2016)**

***

### 2. Identificação do Político

Buscando por:

* “político offshore 2008 crise financeira protestos panela”
* “prime minister resigned panama papers”

Chegamos a:

* **Sigmundur Davíð Gunnlaugsson** (ex-primeiro-ministro da Islândia)

![IMGA](assets/IMGA.png)

Confirmado por:

* Renúncia em 2016 após os Panama Papers
* Envolvimento com ativos ligados a bancos falidos

***

### 3. Identificação da Offshore

Pesquisando:

> “Sigmundur Gunnlaugsson offshore”

Resultado:

* **Wintris Inc.**

Empresa registrada nas Ilhas Virgens Britânicas.

***

### 4. Nome da Esposa

Pesquisando:

> “Sigmundur Gunnlaugsson wife”

Resultado:

* **Anna Sigurlaug Pálsdóttir**

***

### 5. Determinação da Data (Parte Crítica)

Inicialmente, foram testadas datas comuns:

* 06-12-2007 (incorporação)
* 31-12-2009 (transferência)

-> Todas falharam <- :(

***

## Investigação Avançada

Foi necessário recorrer a documentos originais dos Panama Papers:

* ICIJ
* DocumentCloud
* Süddeutsche Zeitung

No artigo oficial, foi encontrado:

> A empresa foi registrada no final de novembro de 2007 **mas retroativamente datada para outubro**

Versões diferentes apresentavam:

* 07 de outubro de 2007
* 09 de outubro de 2007

***

## Insight Final

O CTF utilizava a versão alemã do documento, que indicava:

> **9 de outubro de 2007**

![IMGB](assets/IMGB.png)

***

## Flags Finais

### Empresa Offshore

```
FLAG{WINTRIS_INC.}
```

### Nome da Esposa

```
FLAG{Anna_Sigurlaug_Palsdottir}
```

### Período de Vinculação

```
FLAG{09-10-2007_TO_31-12-2009}
```

***

## Lições Aprendidas

* Nem sempre a “resposta correta” é a mais divulgada
* Documentos originais são essenciais em OSINT
* Diferenças entre idiomas podem impactar diretamente a resposta
* Termos como _“backdated”_ são críticos
* CTFs frequentemente utilizam fontes específicas, não consenso geral

***

## Conclusão

Este desafio exigiu:

* Correlação de eventos históricos
* Pesquisa avançada
* Análise de documentos oficiais
* Atenção a inconsistências entre fontes

Um excelente exemplo de OSINT aplicado além do básico.
