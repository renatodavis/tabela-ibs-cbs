# Como Contribuir

Obrigado pelo interesse! Este repositório existe para ser um bem público — qualquer contador, desenvolvedor ou analista fiscal pode ajudar.

---

## O que mais precisa de ajuda agora

### 1. Grupos CST pendentes

Os grupos a seguir ainda não têm registros no dataset:

| Grupo | Descrição |
|-------|-----------|
| **620** | Tributação monofásica — combustíveis e biocombustíveis |
| **800** | Transferência de crédito |
| **810** | Estorno de crédito |
| **811** | Estorno de crédito — variantes |
| **820** | Ajuste de débito |
| **830** | Ajuste de crédito |

**Onde encontrar:** Portal SVRS — https://dfe-portal.svrs.rs.gov.br/DFE/TabelaClassificacaoTributaria  
Filtrar pelo CST desejado e exportar. Os campos que precisamos: Código (6 dígitos), CST (3 dígitos), Descrição.

### 2. Grupo 550 incompleto

O grupo 550 (Suspensão) tem mais registros além dos 2 já cadastrados. Verificar e completar.

### 3. Correção de descrições

Se você encontrar uma descrição errada ou desatualizada em relação à resolução do CGIBS vigente, abra uma issue ou PR com a correção e o link da resolução.

### 4. Atualização pós-resolução CGIBS

O CGIBS pode publicar novas resoluções adicionando ou alterando códigos. Se você acompanha o Diário Oficial, abra uma issue quando detectar uma mudança.

---

## Como adicionar um registro

Edite o arquivo `data/cclassTrib.json`. O formato de cada entrada é:

```json
{ "codigo": "620001", "cst": "620", "descricao": "Descrição conforme publicação oficial" }
```

Regras:
- **`codigo`**: 6 dígitos, formato `CSTXXX` onde CST é o grupo (3 dígitos) e XXX é o sequencial dentro do grupo (001, 002, ...)
- **`cst`**: 3 dígitos, apenas o grupo
- **`descricao`**: copie da fonte oficial; não parafraseie
- Mantenha a ordem: agrupe por CST, dentro de cada grupo em ordem crescente de código
- Atualize o campo `meta.total_registros` após adicionar registros

Se for adicionar um grupo CST novo que ainda não existe em `grupos_cst`, adicione também sua entrada no array, com:

```json
{ "codigo": "620", "descricao": "Tributação monofásica — combustíveis e biocombustíveis", "cor": "#4f46e5" }
```

---

## Fluxo de Pull Request

1. Fork → crie branch com nome descritivo (`add-cst-620`, `fix-cst-200012`, etc.)
2. Edite `data/cclassTrib.json`
3. Atualize `meta.atualizado_em` com a data atual (formato `AAAA-MM-DD`)
4. Inclua na descrição do PR:
   - Fonte consultada (URL + data de acesso)
   - Trecho ou número da resolução CGIBS, se aplicável
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
- Encontrou um código errado
- O CGIBS publicou uma resolução com códigos novos
- Tem dúvida sobre a classificação de alguma operação (para compartilhar com a comunidade, não para obter assessoria jurídica)

---

## Código da aplicação web (`index.html`)

Contribuições à interface também são bem-vindas. O arquivo é intencionalmente autocontido (sem dependências externas) para poder ser aberto diretamente do sistema de arquivos. Mantenha essa característica.

---

## Não é escopo deste projeto

- Consultor de classificação (qual cClassTrib usar para meu produto): use um contador
- API com autenticação, banco de dados ou SaaS: fork e construa o seu
- Dados de ICMS/ISS legados: este projeto cobre apenas IBS/CBS (reforma tributária LC 214/2025)
