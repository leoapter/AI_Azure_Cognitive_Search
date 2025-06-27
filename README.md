
# 🧪 Laboratório Azure AI Search (Cognitive Search)

**Objetivo:** Usar AI Search para **indexar** e **consultar** dados com enriquecimento via skills cognitivas.

🔗 Baseado no laboratório oficial do Microsoft Learn:  
[https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html)

---

## 🔧 Pré-requisitos

- Conta Azure ativa (pode ser trial)
- Permissões para criar recursos (Resource Groups, Storage, AI Search)
- Acesso ao [portal Azure](https://portal.azure.com)

---

## 🛠️ Passo a passo

### 1. Criar Resource Group e Storage 👥

```bash
az group create -l brazilsouth -n rg-ai-search-lab

az storage account create \
  --name staisearchlab \
  --resource-group rg-ai-search-lab \
  --location brazilsouth \
  --sku Standard_LRS \
  --kind StorageV2
```

📥 Crie um container (ex: `docs`) no Storage para os dados.

---

### 2. Provisionar Azure AI Search

No portal do Azure:

1. Pesquise por **Azure AI Search** (ou Cognitive Search).
2. Selecione o plano **Free Tier** (ideal para testes).
3. Configure:
   - RG: `rg-ai-search-lab`
   - Região: Brasil Sul (ou a mais próxima)
   - Nome exclusivo (ex: `aisearchlab`)

---

### 3. Carregar os dados

Adicione arquivos (PDFs, imagens, textos) ao container `docs` no Blob Storage.

---

### 4. Criar um **Data Source**, **Skillset** e **Indexer**

No portal:

#### 🧩 Data Source
Configure para apontar para seu Storage Account e container.

#### 🧠 Skillset
Adicione habilidades cognitivas, como:

- OCR (Reconhecimento de texto em imagem)
- Extração de frases-chave (Key Phrases)
- Reconhecimento de Entidades (Named Entities)
- Análise de Imagem (Image Analysis)

> Essas skills usam o Cognitive Services (você pode usar uma key existente ou criar uma nova).

#### 🔁 Indexer
Crie o indexador que:

- Lê os dados do Data Source
- Aplica o Skillset
- Envia para um índice (index) de busca

---

### 5. Executar o Indexer

- Vá até o recurso de Indexer no portal
- Clique em **Run** para iniciar a indexação
- Verifique os logs e resultados no painel do Azure

---

### 6. Explorar o índice 🔍

- Acesse a aba **Search Explorer**
- Faça consultas simples, como:

```json
{
  "search": "*"
}
```

- Teste filtros e ordenações

---

### 7. (Opcional) Criar Knowledge Store 🧠

- Permite armazenar os dados enriquecidos como JSON, tabelas, etc.
- Ideal para análises avançadas fora do Search

---

### 8. (Opcional) Consultas via API ou SDK

```http
GET https://<SEU-NOME>.search.windows.net/indexes/<INDEX-NAME>/docs?api-version=2023-07-01&search=azure
```

Ou utilize SDKs oficiais:
- Python
- C#
- JavaScript
- Java

Mais detalhes na [documentação oficial](https://learn.microsoft.com/pt-br/azure/search/search-get-started-portal)

---

### 9. Limpeza dos Recursos ⚠️

Quando finalizar o laboratório:

```bash
az group delete -n rg-ai-search-lab --yes --no-wait
```

---

## 🎯 Dicas Finais

- Utilize o **Free Tier** sempre que possível para economizar créditos
- Combine várias skills cognitivas para resultados mais ricos
- Experimente carregar arquivos diferentes: imagens, PDFs, textos longos
- Teste também a **classificação semântica** (semantic ranking) se disponível

---

## 🧾 Resumo Visual

| Etapa       | Ação                                                             |
|-------------|------------------------------------------------------------------|
| 1️⃣ Pré     | Criar RG e Storage, carregar dados                              |
| 2️⃣ Setup   | Criar serviço do Azure AI Search (Free Tier)                   |
| 3️⃣ Pipelines | Definir Data Source, Skillset (OCR, NER, key phrases, imagem) |
| 4️⃣ Indexar | Executar indexer, revisar enriquecimento                        |
| 5️⃣ Buscar  | Usar Search Explorer, filtro, facet, semantic, API/SDK         |

---

## 📸 Capturas de Tela (Exemplo)

> Substitua os links pelas capturas do seu ambiente, se desejar.

![Azure Blob Storage com arquivos carregados](https://learn.microsoft.com/en-us/azure/search/media/search-blob-storage.png)

![Configuração do Skillset](https://learn.microsoft.com/en-us/azure/search/media/cognitive-search-skillset.png)

![Search Explorer com resultado](https://learn.microsoft.com/en-us/azure/search/media/search-explorer.png)

---

## 📚 Referências

- [Documentação Oficial do Azure Cognitive Search](https://learn.microsoft.com/pt-br/azure/search/)
- [Laboratório Microsoft Learn](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html)
- [Azure SDKs](https://learn.microsoft.com/pt-br/azure/search/search-get-started-sdk)

---

## 🎉 Conclusão

Esse laboratório permite construir um pipeline completo com:

✅ Ingestão de documentos  
✅ Enriquecimento com inteligência artificial  
✅ Indexação e busca inteligente via Azure Cognitive Search

---

> 💡 *Explore mais no Microsoft Learn: [Fundamentals of Knowledge Mining](https://learn.microsoft.com/en-us/training/modules/intro-to-azure-search/)*
