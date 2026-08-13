# tabela-ibs-cbs

**Tabela aberta de Códigos de Classificação Tributária do IBS e CBS (cClassTrib)**

> Dados machine-readable da Reforma Tributária Brasileira (LC 214/2025) — para contadores, analistas fiscais e desenvolvedores.

[![Licença: CC0](https://img.shields.io/badge/licen%C3%A7a-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/deed.pt)
[![Dados: SVRS/SEFAZ](https://img.shields.io/badge/fonte-SVRS%2FSEFAZ-blue)](https://dfe-portal.svrs.rs.gov.br/DFE/TabelaClassificacaoTributaria)
[![Status](https://img.shields.io/badge/status-parcial%20(118%2F200%2B%20registros)-orange)](#status-dos-dados)

---

## O que é

O **cClassTrib** é um campo de 6 dígitos obrigatório na NF-e (e demais DFe) a partir de **03/08/2026** para empresas não optantes pelo Simples Nacional.

Ele especifica exatamente qual regime de IBS/CBS se aplica a cada item da nota:

```
200003  →  CST 200 (alíquota reduzida) — Cesta Básica Nacional, Anexo I
```

Sem este código correto, a nota pode ser recusada pela SEFAZ ou gerar autuações por classificação incorreta.

**O problema**: não existe uma fonte aberta, machine-readable e atualizada desta tabela. Os dados estão disponíveis no portal do SVRS, mas somente via interface web ou exportação CSV/Excel sem metadados.

**A solução deste repositório**: manter o dataset em JSON estruturado, versionado, com metadados de origem — para que qualquer sistema possa consumir sem depender de scraping ou compra de licença.

---

## Uso rápido

### Consulta via browser (zero instalação)

Abra o arquivo `index.html` diretamente no browser. Ele carrega os dados localmente sem precisar de servidor.

Se preferir uma versão hospedada: `https://renatodavis.github.io/tabela-ibs-cbs`

### Como dado (JSON)

```json
// data/cclassTrib.json — estrutura
{
  "meta": {
    "versao": "1.0.0",
    "atualizado_em": "2026-08-12",
    "total_registros": 118
  },
  "grupos_cst": [
    { "codigo": "000", "descricao": "Tributação integral pelo IBS e CBS", "cor": "#2563eb" }
  ],
  "cclassTrib": [
    { "codigo": "000001", "cst": "000", "descricao": "Situações tributadas integralmente pelo IBS e CBS" },
    { "codigo": "200003", "cst": "200", "descricao": "Vendas de produtos destinados à alimentação humana (Cesta Básica Nacional — Anexo I)" }
  ]
}
```

### Via curl

```bash
curl https://raw.githubusercontent.com/renatodavis/tabela-ibs-cbs/main/data/cclassTrib.json
```

### Via JavaScript

```js
const res = await fetch('https://raw.githubusercontent.com/renatodavis/tabela-ibs-cbs/main/data/cclassTrib.json');
const tabela = await res.json();

// Buscar código específico
const codigo = tabela.cclassTrib.find(r => r.codigo === '200003');
```

---

## Status dos dados

| Grupo CST | Descrição | Registros | Status |
|-----------|-----------|-----------|--------|
| 000 | Tributação integral | 5 | ✅ Completo |
| 010 | Alíquotas uniformes — financeiro | 2 | ✅ Completo |
| 011 | Alíquotas uniformes reduzidas | 5 | ✅ Completo |
| 200 | Alíquota reduzida | 54 | ✅ Completo |
| 220 | Alíquota fixa — RET/parcelamento | 3 | ✅ Completo |
| 221 | Alíquota proporcional fixa | 4 | ✅ Completo |
| 222 | Redução de base — transporte intl | 1 | ✅ Completo |
| 400 | Isenção — transporte público | 2 | ✅ Completo |
| 410 | Imunidade / Não-incidência | 38 | ✅ Completo |
| 510 | Diferimento — energia elétrica | 1 | ✅ Completo |
| 515 | Diferimento — insumos agropecuários | 1 | ✅ Completo |
| 550 | Suspensão | 2 | ⚠️ Parcial |
| 620 | Tributação monofásica — combustíveis | 0 | ❌ Pendente |
| 800–830 | Transferências e ajustes | 0 | ❌ Pendente |

**Total atual: 118 de ~200+ registros**

Veja como contribuir com os grupos faltantes em [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Fonte oficial

Os dados são derivados da tabela publicada pelo **Comitê Gestor do IBS (CGIBS)** e disponibilizada via:

- Portal SVRS/SEFAZ: https://dfe-portal.svrs.rs.gov.br/DFE/TabelaClassificacaoTributaria
- Portal NF-e: https://www.nfe.fazenda.gov.br/
- LC 214/2025: https://www.planalto.gov.br/ccivil_03/leis/lcp/lcp214.htm
- NT NF-e 2025.002 (especificação técnica do campo cClassTrib)

---

## Licença

**CC0 1.0 Universal** — domínio público.

Os dados são derivados de atos normativos públicos do governo brasileiro. Este repositório os organiza e estrutura para uso técnico. Sem restrições de uso comercial, acadêmico ou pessoal.

---

## Como contribuir

Veja [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Aviso

Este repositório **não presta consultoria fiscal**. Sempre confirme a classificação com um contador ou advogado tributarista antes de emitir notas fiscais. A tabela pode estar parcial ou desatualizada — verifique sempre com as fontes oficiais citadas acima.
