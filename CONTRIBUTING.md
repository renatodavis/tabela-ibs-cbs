# Como Contribuir

Obrigado pelo interesse! Este repositório existe para ser um bem público — qualquer contador, desenvolvedor ou analista fiscal pode ajudar.

---

## O que mais precisa de ajuda agora

### 1. Manter o dataset atualizado

O CGIBS pode publicar novas resoluções adicionando ou alterando códigos a qualquer momento. Se você acompanha o Diário Oficial ou o portal SVRS, abra uma issue quando detectar uma mudança.

**Onde verificar:** Portal SVRS — https://dfe-portal.svrs.rs.gov.br/DFE/TabelaClassificacaoTributaria

### 2. Correção de descrições

Se você encontrar uma descrição errada ou desatualizada em relação à resolução do CGIBS vigente, abra uma issue ou PR com a correção e o link da resolução.

### 3. Tradução das descrições

Algumas descrições estão como transcrição literal do texto legal — pode ser útil manter um campo `descricao_resumida` mais amigável. Se quiser propor isso, abra uma issue primeiro para discutir o formato.

### 4. Melhorias na interface web

O `index.html` e o `learn.html` são autocontidos (sem dependências externas) para poder ser abertos diretamente do sistema de arquivos. Contribuições à UX são bem-vindas — mantenha essa característica.

---

## Como adicionar ou corrigir um registro

Edite o arquivo `data/cclassTrib.json`. O formato de cada entrada é:

```json
{ "codigo": "620001", "cst": "620", "descricao": "Descrição conforme publicação oficial" }
```

Regras:
- **`codigo`**: 6 dígitos, formato `CSTXXX` onde CST é o grupo (3 dígitos) e XXX é o sequencial dentro do grupo (001, 002, ...)
- **`cst`**: 3 dígitos, apenas o grupo
- **`descricao`**: copie da fonte oficial; não parafraseie
- Mantenha a ordem: agrupe por CST, dentro de cada grupo em ordem crescente de código
- Atualize o campo `meta.total_registros` e `meta.atualizado_em` após adicionar registros

Se for adicionar um grupo CST novo que ainda não existe em `grupos_cst`, adicione também sua entrada no array, com:

```json
{ "codigo": "999", "descricao": "Descrição do grupo", "cor": "#4f46e5" }
```

---

## Fluxo de Pull Request

1. Fork → crie branch com nome descritivo (`add-cst-620`, `fix-cst-200012`, `update-cst-200-resolucao-42`, etc.)
2. Edite `data/cclassTrib.json`
3. Atualize `meta.atualizado_em` com a data atual (formato `AAAA-MM-DD`)
4. Inclua na descrição do PR:
   - Fonte consultada (URL + data de acesso)
   - Número da resolução CGIBS, se aplicável
5. Abra o PR

---

## Critério de aceitação

- Dados devem ter origem verificável em fonte oficial (SVRS, CGIBS, portal NF-e, NT NF-e 2025.002 ou resolução CGIBS publicada)
- Código e CST devem coincidir com a publicação oficial
- Descrição deve ser fiel ao texto publicado (não é paráfrase)

PRs que alteram dados sem citar fonte serão solicitados a complementar antes do merge.

---

## Issues

Abra uma issue se:
- O CGIBS publicou uma resolução com códigos novos ou alterados
- Encontrou um código errado ou descrição desatualizada
- Quer propor melhoria de formato ou estrutura do JSON

---

## Não é escopo deste projeto

- Consultor de classificação (qual cClassTrib usar para meu produto): use o guia interativo `learn.html` ou consulte um contador
- API com autenticação, banco de dados ou SaaS: fork e construa o seu
- Dados de ICMS/ISS legados: este projeto cobre apenas IBS/CBS (reforma tributária LC 214/2025)
