### Symmetric Base Converter — Conversor de Bases Simétricas

#### Visão geral
Aplicação web simples para converter entre:
- Ternário balanceado (Base 3) usando os símbolos `+`, `0`, `-` (trits)
- Nonário simétrico (Base 9) usando os símbolos `W X Y Z 0 1 2 3 4`

A conversão é direta porque `9 = 3²`: cada par de trits (2 dígitos em base 3 balanceada) corresponde exatamente a um dígito em base 9 simétrica. É análogo ao agrupamento de 4 bits em um dígito hexadecimal (`2⁴ = 16`).

#### Demonstração
Site Online: https://randintn.github.io/SymmetricBaseConverterNonary/?lang=en

Abra o arquivo `index.html` em um navegador moderno. Não há dependências locais: todo o estilo é via Tailwind CDN e o conteúdo explicativo usa KaTeX (CDN) para fórmulas.

- Alternância de idioma: botão no topo alterna entre PT-BR e EN.
- Validação de entrada: aceita apenas os símbolos permitidos em cada base.
- Conversão em tempo real: altera qualquer lado e o outro é atualizado automaticamente; o valor decimal (base 10) é mostrado.

---

### Alfabetos e valores
- Ternário balanceado (base 3): `+` = +1, `0` = 0, `-` = −1.
- Nonário simétrico (base 9):
    - `4` = +4, `3` = +3, `2` = +2, `1` = +1, `0` = 0
    - `Z` = −1, `Y` = −2, `X` = −3, `W` = −4

#### Tabela de mapeamento (2 trits ↔ 1 dígito nonário)
```
Ternário  →  Valor  →  Nonário
  ++      →   +4    →   4
  +0      →   +3    →   3
  +-      →   +2    →   2
  0+      →   +1    →   1
  00      →    0    →   0
  0-      →   −1    →   Z
  -+      →   −2    →   Y
  -0      →   −3    →   X
  --      →   −4    →   W
```

---

### Como funciona a conversão
Como `9 = 3²`, agrupamos trits de 2 em 2 (da direita para a esquerda) e mapeamos cada par para um dígito nonário usando a tabela acima. O processo é reversível 1:1.

#### Regras práticas
- Ao converter de ternário balanceado (B3) para nonário simétrico (B9):
    1. Da direita para a esquerda, agrupe os trits em pares. Se houver quantidade ímpar, adicione um `0` à esquerda para completar o primeiro par.
    2. Para cada par, substitua pelo correspondente dígito em B9.

- Ao converter de nonário simétrico (B9) para ternário balanceado (B3):
    1. Substitua cada dígito B9 pelo par de trits correspondente.
    2. Remova zeros à esquerda que não alterem o valor, se desejar.

- Valor decimal (B10):
    - Para B3 balanceado, considere `+ = +1`, `0 = 0`, `- = −1` e use pesos `3⁰, 3¹, 3², ...` da direita para a esquerda.
    - Para B9 simétrico, use pesos `9⁰, 9¹, 9², ...` com os valores simétricos de cada dígito.

---

### Exemplos
- B3 → B9: `++ 00` → `4 0` → `40` (B9)
- B9 → B3: `WZ` → `--` `0-` → `--0-` (B3)
- B3 (ímpar de trits): `+-0` → complete à esquerda: `0 +- 0` → pares: `0+` `-0` → `1 X` → `1X` (B9)

> Observação: os espaços acima são apenas para ilustrar o agrupamento; no app, digite sem espaços.

---

### Uso
1. Abra `index.html` no navegador.
2. Digite no campo “Ternário Balanceado (trits)” usando somente `+ - 0`.
3. Ou digite em “Nonário Simétrico” usando somente `W X Y Z 0 1 2 3 4`.
4. O outro campo será atualizado automaticamente e o valor decimal (base 10) é exibido.
5. Use o botão “EN/PT” no cabeçalho para alternar o idioma da interface e da explicação.

---

### Sobre a implementação
- UI: Tailwind CSS via CDN; layout responsivo com grid.
- I18n: objeto `translations` em JavaScript injeta textos e conteúdos explicativos (PT e EN), inclusive fórmulas renderizadas por KaTeX.
- Lógica de conversão: mapeamento direto entre pares de trits e dígitos nonários, com validação de caracteres e sincronização bilateral dos campos.

---

### Estrutura do projeto
```
.
├─ index.html   # App completo (UI, lógica, i18n, explicações)
├─ README.md    # Este documento
└─ SymmetricBaseConverterNonary.iml
```

---

### Limitações e notas
- Espaços e letras minúsculas no campo nonário são normalizados (o app converte para maiúsculas e ignora espaços não permitidos) — conforme implementação da UI.
- Ao agrupar trits, o preenchimento com `0` à esquerda é apenas para completar pares e não altera o valor representado.

---

### Créditos
- Projeto: “Symmetric Base Converter — Balanced Ternary ⇄ Symmetric Nonary”.
- Fontes e libs: Tailwind CSS (CDN), KaTeX (CDN), Google Fonts (Inter).

### Licença
Não especificada neste repositório.

---

#### English summary
Balanced Ternary (Base 3, symbols `+ 0 -`) ⇄ Symmetric Nonary (Base 9, symbols `W X Y Z 0 1 2 3 4`). Since `9 = 3²`, group two trits into one base‑9 digit using the mapping table above. Open `index.html` to use the converter with live updates, validation, and language toggle (PT/EN).