### Symmetric Base Converter — Balanced Ternary ⇄ Symmetric Nonary

#### Overview
A simple web app to convert between:
- Balanced Ternary (Base 3) using symbols `+`, `0`, `-` (trits)
- Symmetric Nonary (Base 9) using symbols `W X Y Z 0 1 2 3 4`

The conversion is straightforward because `9 = 3²`: every pair of trits (two digits in balanced base 3) maps exactly to one digit in symmetric base 9. It is analogous to grouping 4 bits into one hexadecimal digit (`2⁴ = 16`).

#### Demo
Live Demo at: https://randintn.github.io/SymmetricBaseConverterNonary/?lang=en

Open `index.html` in any modern browser. No local dependencies: styling is via Tailwind CDN, and explanatory content uses KaTeX (CDN) for formulas.

- Language toggle: header button switches between EN and PT-BR.
- Input validation: only the allowed symbols for each base are accepted.
- Live conversion: edit either side and the other updates automatically; the decimal (base 10) value is displayed.

---

### Alphabets and values
- Balanced ternary (base 3): `+` = +1, `0` = 0, `-` = −1.
- Symmetric nonary (base 9):
    - `4` = +4, `3` = +3, `2` = +2, `1` = +1, `0` = 0
    - `Z` = −1, `Y` = −2, `X` = −3, `W` = −4

#### Mapping table (2 trits ↔ 1 nonary digit)
```
Ternary  →  Value  →  Nonary
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

### How the conversion works
Since `9 = 3²`, group trits in pairs (right to left) and map each pair to a nonary digit using the table above. The process is reversible 1:1.

#### Practical rules
- Balanced Ternary (B3) → Symmetric Nonary (B9):
    1. From right to left, group trits in pairs. If there is an odd count, prepend a `0` to complete the leftmost pair.
    2. Replace each pair with the corresponding B9 digit.

- Symmetric Nonary (B9) → Balanced Ternary (B3):
    1. Replace each B9 digit with its corresponding pair of trits.
    2. Remove non‑significant leading zeros if desired.

- Decimal value (B10):
    - For balanced B3, treat `+ = +1`, `0 = 0`, `- = −1` with weights `3⁰, 3¹, 3², ...` from right to left.
    - For symmetric B9, use weights `9⁰, 9¹, 9², ...` with the signed value of each digit.

---

### Examples
- B3 → B9: `++ 00` → `4 0` → `40` (B9)
- B9 → B3: `WZ` → `--` `0-` → `--0-` (B3)
- B3 (odd trit count): `+-0` → pad left: `0 +- 0` → pairs: `0+` `-0` → `1 X` → `1X` (B9)

> Note: spaces above are just to illustrate grouping; type without spaces in the app.

---

### Usage
1. Open `index.html` in the browser.
2. Type in “Balanced Ternary (trits)” using only `+ - 0`.
3. Or type in “Symmetric Nonary” using only `W X Y Z 0 1 2 3 4`.
4. The other field updates automatically and the decimal value (base 10) is shown.
5. Use the header button to toggle EN/PT.

---

### Implementation notes
- UI: Tailwind CSS via CDN; responsive layout with grid.
- I18n: a `translations` object in JavaScript injects UI texts and explanatory content (EN and PT), including formulas rendered with KaTeX.
- Conversion logic: direct mapping between trit pairs and nonary digits, with character validation and two‑way field synchronization.

---

### Project structure
```
.
├─ index.html   # Full app (UI, logic, i18n, explanations)
├─ README.md    # This document
└─ SymmetricBaseConverterNonary.iml
```

---

### Limitations and notes
- Spaces and lowercase letters in the nonary field are normalized (the app uppercases and filters invalid chars) — per UI implementation.
- Left‑padding with `0` when grouping trits only completes pairs and does not change the represented value.

---

### Credits
- Project: “Symmetric Base Converter — Balanced Ternary ⇄ Symmetric Nonary”.
- Libraries: Tailwind CSS (CDN), KaTeX (CDN), Google Fonts (Inter).

### License
MIT LICENSE Robson Cassiano

Live Long and Prosper 🖖🏻

---

### Conversor de Bases Simétricas — Ternário Balanceado ⇄ Nonário Simétrico

#### Visão geral
Aplicação web simples para converter entre:
- Ternário balanceado (Base 3) usando os símbolos `+`, `0`, `-` (trits)
- Nonário simétrico (Base 9) usando os símbolos `W X Y Z 0 1 2 3 4`

A conversão é direta porque `9 = 3²`: cada par de trits (2 dígitos em base 3 balanceada) corresponde exatamente a um dígito em base 9 simétrica. É análogo ao agrupamento de 4 bits em um dígito hexadecimal (`2⁴ = 16`).

#### Demonstração

Aqui: https://randintn.github.io/SymmetricBaseConverterNonary/?lang=pt

Abra o arquivo `index.html` em um navegador moderno. Não há dependências locais: todo o estilo é via Tailwind CDN e o conteúdo explicativo usa KaTeX (CDN) para fórmulas.

- Alternância de idioma: botão no topo alterna entre EN e PT-BR.
- Validação de entrada: aceita apenas os símbolos permitidos em cada base.
- Conversão em tempo real: altere qualquer lado e o outro é atualizado automaticamente; o valor decimal (base 10) é mostrado.

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
- Ternário Balanceado (B3) → Nonário Simétrico (B9):
    1. Da direita para a esquerda, agrupe os trits em pares. Se houver quantidade ímpar, adicione um `0` à esquerda para completar o primeiro par.
    2. Para cada par, substitua pelo dígito correspondente em B9.

- Nonário Simétrico (B9) → Ternário Balanceado (B3):
    1. Substitua cada dígito B9 pelo par de trits correspondente.
    2. Remova zeros à esquerda que não alterem o valor, se desejar.

- Valor decimal (B10):
    - Para B3 balanceado, considere `+ = +1`, `0 = 0`, `- = −1` e use pesos `3⁰, 3¹, 3², ...` da direita para a esquerda.
    - Para B9 simétrico, use pesos `9⁰, 9¹, 9², ...` com o valor simétrico de cada dígito.

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
5. Use o botão do cabeçalho para alternar EN/PT.

---

### Sobre a implementação
- UI: Tailwind CSS via CDN; layout responsivo com grid.
- I18n: objeto `translations` em JavaScript injeta textos e conteúdos explicativos (EN e PT), inclusive fórmulas renderizadas por KaTeX.
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
- Espaços e letras minúsculas no campo nonário são normalizados (o app converte para maiúsculas e filtra caracteres inválidos) — conforme implementação da UI.
- Ao agrupar trits, o preenchimento com `0` à esquerda é apenas para completar pares e não altera o valor representado.

---

### Créditos
- Projeto: “Symmetric Base Converter — Balanced Ternary ⇄ Symmetric Nonary”.
- Fontes e libs: Tailwind CSS (CDN), KaTeX (CDN), Google Fonts (Inter).

### Licença
MIT LICENSE
Vida Longa e Próspera 🖖🏻