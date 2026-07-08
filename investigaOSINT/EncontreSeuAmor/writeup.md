# writeup

## Writeup — CTF OSINT: “Encontre seu amor”

>

![Certificado](assets/certified.png)

### Descrição do desafio

O desafio apresentava um suposto site de relacionamentos que voltou a circular em fóruns e redes sociais.

![imagesCTF](assets/imagemCTF.png)

A missão era identificar:

* o nic-hdl-br do domínio;
* o nome do criador do site;
* a data em que o site apareceu pela primeira vez na internet.

Formato das flags:

```
FLAG{XXXXX}
FLAG{XXXXXXX_XXXXXXX_XXXXX}
FLAG{XX/XX/XXXX}
```

***

## Objetivo

Realizar uma investigação OSINT utilizando:

* WHOIS;
* Registro.br;
* Wayback Machine;
* análise de histórico do domínio.

***

## Etapa 1 — Investigação WHOIS

A primeira etapa consistiu em consultar os registros públicos do domínio:

```
amorespossiveis.com.br
```

A consulta WHOIS revelou informações importantes:

![WHOIS](assets/REGISTROBR.png)

```
Titular: Gabriel Machado Badan
Contato: GMB31
Criado: 08/11/2005
```

Com isso, foi possível identificar rapidamente:

### nic-hdl-br

```
FLAG{GMB31}
```

### Nome do criador

```
FLAG{GABRIEL_MACHADO_BADAN}
```

***

## Etapa 2 — Data de primeira aparição do site

A terceira flag exigia descobrir:

> “o dia, o mês e o ano em que o site apareceu pela primeira vez na internet”

Inicialmente, a hipótese mais óbvia foi utilizar a data de criação do domínio:

```
08/11/2005
```

Porém, a flag estava incorreta.

Isso indicava que o desafio não queria a criação do domínio, mas sim:

* a primeira vez que o site realmente ficou acessível;
* ou a primeira captura pública do site.

***

## Investigação no Wayback Machine

A próxima etapa foi utilizar o:

```
Wayback Machine
```

Pesquisando:

```
amorespossiveis.com.br
```

![Wayback-machine](assets/PesquisandoPossivelDATA.png)

foi possível visualizar o histórico arquivado do domínio.

Ao navegar até 2005, apareceu o primeiro snapshot disponível:

```
09/11/2005 - 14:36:56
```

Essa captura mostrava a página inicial hospedada no provedor:

![DATA](assets/PossivelDATA.png)

```
Iphotel Hospedagem Profissional
```

com a mensagem:

![confirmacao](assets/ConfimacaoDeDEPLOY.png)

```
“Seu site já está ativo”
```

Isso confirmou que:

* o domínio havia sido criado em 08/11/2005;
* o site efetivamente apareceu online em 09/11/2005.

***

## Flag final

```
FLAG{09/11/2005}
```

***

## Flags completas

### nic-hdl-br

```
FLAG{GMB31}
```

### Nome do criador

```
FLAG{GABRIEL_MACHADO_BADAN}
```

### Primeira aparição do site

```
FLAG{09/11/2005}
```

***

## Técnicas utilizadas

Este desafio envolveu:

* WHOIS;
* Registro.br;
* investigação de domínio;
* análise histórica de sites;
* Wayback Machine;
* validação temporal;
* OSINT raiz.

***

## Lições aprendidas

O desafio mostrou uma diferença importante entre:

* criação de domínio;
* e primeira aparição pública de um site.

Embora o domínio tenha sido registrado em:

```
08/11/2005
```

isso não significa que o site já estava acessível naquele momento.

A validação correta veio através da primeira captura pública arquivada pelo Wayback Machine.

***

## Conclusão

Esse foi um ótimo desafio introdutório de OSINT voltado para:

* investigação de domínios;
* análise de registros públicos;
* pesquisa histórica;
* correlação temporal.

Mesmo sendo um desafio simples, ele reforça conceitos fundamentais utilizados frequentemente em investigações reais:

* identificação de responsáveis;
* rastreamento histórico;
* análise de infraestrutura;
* validação de presença digital.
