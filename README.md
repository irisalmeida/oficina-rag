# Leitor Inteligente de PDFs

> Código desenvolvido para explicar RAG para alunos da oficina **"Fluxos Inteligentes: Construindo Sistemas Multiagentes com LangChain e LangGraph"** no evento **Elas\@Conectam**.

Este repositório apresenta um pipeline RAG (Retrieval-Augmented Generation) multimodal, ideal para quem deseja entender e aplicar fluxos de processamento de documentos que combinam texto e imagens .

---

## 📋 Sumário

* [Funcionalidades](#funcionalidades)
* [Motivação e Contexto](#motivação-e-contexto)
* [Pré-requisitos](#pré-requisitos)
* [Instalação](#instalação)
* [Estrutura do Projeto](#estrutura-do-projeto)
* [Como Usar](#como-usar)
* [Arquitetura](#arquitetura)
* [Exemplo de Execução](#exemplo-de-execução)
* [Contribuição](#contribuição)
* [Licença](#licença)

---

## 🚀 Funcionalidades

* **Extração de Texto**: captura todo o conteúdo textual de cada página do PDF.
* **Detecção e Salvamento de Imagens**: extrai e armazena todas as imagens embutidas.
* **Geração de Descrições Visuais**: usa o modelo **Gemini-2.0-Flash** para criar descrições detalhadas de cada imagem.
* **Indexação Semântica**: converte textos e descrições em vetores usando **MiniLM** e armazena em **FAISS**.
* **Pipeline RAG Modular**: separa claramente as etapas de *retrieve* (busca de contexto) e *generate* (resposta), orquestrado por **LangGraph**.
* **Interação em Tempo Real**: usuário faz perguntas sobre o PDF e recebe respostas contextuais, com as imagens relevantes exibidas.

---

## 🎓 Motivação e Contexto

Durante o evento Elas\@Conectam, a oficina **Fluxos Inteligentes** introduziu conceitos de sistemas multiagentes, RAG e arquiteturas de busca aumentada por recuperação. Este código serve como exemplo prático para demonstrar:

1. Como combinar LLMs multimodais (texto + imagem) em um único fluxo.
2. A modularidade de pipelines com **LangChain** e **LangGraph**.
3. A construção de um sistema didático que lê, entende e responde perguntas sobre PDFs.

---

## 🔧 Pré-requisitos

* **Python 3.8+**
* Conta e **API Key** do Google Cloud com acesso ao modelo Gemini
* Ambiente Jupyter ou **Google Colab** (recomendado)

---

## 🛠️ Instalação

1. Clone o repositório:

   ```bash
   git clone https://github.com/seu-usuario/leitor-pdf-multimodal.git
   cd leitor-pdf-multimodal
   ```
2. Instale as dependências:

   ```bash
   pip install -U langgraph langchain langchain-google-genai langchain_community faiss-cpu pdf2image PyMuPDF
   ```
3. Defina a API Key do Google:

   ```bash
   export GOOGLE_API_KEY="SUA_CHAVE_AQUI"
   ```

   > Se usar Colab, a célula de configuração solicitará a chave interativamente.

---

## 📂 Estrutura do Projeto

```plain
leitor-pdf-multimodal/
├── notebook.ipynb       # Notebook com todo o pipeline e comentários
├── pdf_images/          # Diretório onde as imagens são extraídas
├── README.md            # Documentação deste projeto
└── requirements.txt     # Lista de dependências pinadas
```

---

## 📝 Como Usar

1. Abra `notebook.ipynb` no Colab ou Jupyter.
2. Execute as células na ordem:

   * Instalação de pacotes
   * Configuração da API Key
   * Upload do PDF
   * Extração de texto e imagens
   * Geração de descrições
   * Indexação semântica
   * Construção e visualização do grafo RAG
   * Loop de perguntas
3. Quando solicitado, digite sua pergunta sobre o PDF e confira:

   * **Resposta textual** baseada no contexto extraído.
   * **Imagens relevantes** exibidas abaixo da resposta.

---

## 🏗️ Arquitetura do Pipeline

1. **Input**: usuário faz upload de um PDF.
2. **Extração**:

   * Texto (PyMuPDF → `Document`).
   * Imagens (PyMuPDF → arquivos PNG).
3. **Visão Computacional**:

   * Envio de cada imagem ao Gemini para descrição detalhada.
   * Criação de `Document` para cada descrição.
4. **Indexação Semântica**:

   * Gerar embeddings (MiniLM).
   * Construir índice FAISS.
5. **RAG** (LangGraph):

   * **retrieve**: busca os documentos mais similares.
   * **generate**: gera resposta com o contexto reunido.
6. **Output**: exibição da resposta + imagens usadas.

---

## 🖼️ Exemplo de Execução

> **Pergunta:** "Quais são os principais benefícios apresentados no capítulo 2?"

**Resposta:**

> Os benefícios descritos incluem X, Y e Z...

**Imagens relevantes:**
![Imagem 1](pdf_images/page_1_img_0.png)

---

## 📄 Licença

Este projeto está sob a [MIT License](LICENSE).
