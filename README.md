


# Leitor Inteligente de PDFs com IA Multimodal

Este projeto implementa um pipeline RAG (Retrieval-Augmented Generation) multimodal capaz de responder perguntas sobre o conteúdo de documentos PDF, combinando extração de texto, descrição automática de imagens e busca semântica.
Código desenvolvido para explicar RAG para alunos da oficina "Fluxos Inteligentes: Construindo Sistemas Multiagentes com LangChain e LangGraph" para o evento Elas@Conectam


## 🔍 Como Funciona (Visão Geral)

1. **Upload**: usuário envia o PDF via interface do Colab.
2. **Extração**: texto e imagens são extraídos de cada página.
3. **Descrição de Imagens**: cada imagem é codificada em Base64 e enviada ao Gemini para gerar descrição.
4. **Indexação**: textos e descrições são transformados em vetores semânticos com MiniLM e indexados com FAISS.
5. **Pipeline RAG**:

   * **retrieve**: busca os 7 documentos (texto ou descrição) mais relevantes à pergunta.
   * **generate**: compõe o prompt com contexto e envia ao Gemini para resposta.
6. **Exibição**: resposta textual + imagens relevantes.


## 🚀 Funcionalidades

* **Extração de texto** de cada página do PDF usando PyMuPDF.
* **Extração e salvamento de imagens** embutidas no PDF.
* **Geração automática de descrições** para cada imagem via modelo Gemini (Google Generative AI).
* **Indexação semântica** de todos os trechos (texto e descrições) com FAISS.
* **Arquitetura RAG** modular usando LangGraph: etapas de *retrieve* (busca de contexto) e *generate* (geração de resposta).
* **Interação interativa**: o usuário envia uma pergunta e recebe resposta contextualizada + exibição das imagens relevantes.

## 📦 Pré-requisitos

* Python 3.8 ou superior
* Conta e chave de API do Google Cloud com acesso ao modelo Gemini
* Google Colab (recomendado) ou ambiente local com Jupyter

## 🛠️ Instalação

1. Clone este repositório:

   ```bash
   git clone https://github.com/seu-usuario/leitor-pdf-multimodal.git
   cd leitor-pdf-multimodal
   ```

2. Instale as dependências:

   ```bash
   pip install -U langgraph langchain langchain-google-genai langchain_community faiss-cpu pdf2image PyMuPDF
   ```

3. Defina sua chave de API do Google:

   * Exporte como variável de ambiente:

     ```bash
     export GOOGLE_API_KEY="SUACHAVE"
     ```
   * Ou, ao executar no Colab, insira quando solicitado.

## 📄 Uso

1. Abra o notebook `notebook.ipynb` no Colab ou Jupyter.
2. Execute todas as células sequencialmente:

   * Instalação de pacotes
   * Configuração da chave de API
   * Upload do PDF
   * Extração de texto e imagens
   * Indexação e construção do grafo RAG
   * Loop de perguntas
3. Quando solicitado, digite sua pergunta sobre o PDF e pressione **Enter**.
4. A resposta gerada será exibida junto com miniaturas das imagens que deram suporte à resposta.

## 🗂️ Estrutura do Projeto

```
leitor-pdf-multimodal/
├── notebook.ipynb       # Notebook principal de execução
├── pdf_images/         # Imagens extraídas do PDF
├── README.md           # Documentação do projeto
└── requirements.txt    # Dependências do projeto
```

## 📄 Licença

Este projeto está licenciado sob a [MIT License](LICENSE).
