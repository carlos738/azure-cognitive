# azure-cognitive
O Azure Cognitive Search é um serviço de pesquisa na nuvem da Microsoft que permite indexar, pesquisar e analisar dados de forma eficiente. Ele é usado para criar buscas sofisticadas em grandes volumes de informações, como documentos, bancos de dados e até mesmo conteúdos estruturados e não estruturados.
Como utilizar o Azure Cognitive Search:

    Criar um serviço de pesquisa: No portal do Azure, você pode provisionar um serviço de pesquisa e definir sua capacidade com base no tamanho e na complexidade dos seus dados.

    Criar um índice: O índice é onde os dados serão armazenados e organizados para pesquisa. Você define os campos do índice, como nome, categoria, data de criação, etc.

    Carregar e indexar os dados: Os dados podem ser carregados de diversas fontes, como SQL, Blob Storage ou Cosmos DB, e são processados para que possam ser pesquisados rapidamente.

    Executar consultas: Com a API de pesquisa, você pode realizar buscas utilizando filtros, ranking de relevância e até mesmo pesquisas baseadas em inteligência artificial, como análise de texto e sinônimos.
    
    
    
    1- Criando um serviço de pesquisa

Antes de qualquer coisa, você precisa provisionar um serviço no Portal do Azure:

Acesse o portal do Azure.
     Pesquise por Azure Cognitive Search e clique em Criar.

    Escolha o nível de serviço (gratuito para testes ou escalável para produção).

    Defina um nome e uma região para seu serviço.

    Após a criação, anote a Chave de Administração e o URL do serviço.

2 - Criando um índice de pesquisa

O índice define como os dados serão armazenados e pesquisados. Um exemplo de índice para um catálogo de livros poderia ser:

{
  "name": "books-index",
  "fields": [
    {"name": "id", "type": "Edm.String", "key": true},
    {"name": "title", "type": "Edm.String", "searchable": true},
    {"name": "author", "type": "Edm.String", "searchable": true},
    {"name": "description", "type": "Edm.String", "searchable": true},
    {"name": "price", "type": "Edm.Double", "filterable": true, "sortable": true}
  ]
}
3 - Indexando os dados

Agora, precisamos alimentar esse índice com informações. Se seus dados estiverem em um banco SQL, você pode usar um Indexer para automatizar o processo. Exemplo de indexação via API REST:

POST https://<seu-servico>.search.windows.net/indexes/books-index/docs?api-version=2023-10-01
Content-Type: application/json
api-key: <sua-chave>

{
  "value": [
    {"id": "1", "title": "Dom Quixote", "author": "Miguel de Cervantes", "description": "Clássico espanhol", "price": 25.99},
    {"id": "2", "title": "1984", "author": "George Orwell", "description": "Distopia política", "price": 19.90}
  ]
}

4 - Consultando os dados

Agora podemos executar pesquisas nesse índice. Exemplo de consulta via API REST:
GET https://<seu-servico>.search.windows.net/indexes/books-index/docs?search=Orwell&api-version=2023-10-01
api-key: <sua-chave>

Esse comando retorna todos os livros que mencionam "Orwell" no título ou descrição!

5 - Melhorando a experiência de busca

Para refinar os resultados, podemos: ✅ Adicionar sinônimos, para considerar termos semelhantes (Exemplo: “romance” ↔ “ficção”). ✅ Relevância personalizada, ordenando por campos importantes como popularidade. ✅ Busca semântica, que interpreta contexto e intenção das pesquisas.

# obs : usei algumas imagens da internet para ilustrar alguns serviços do azure cognitive e da azure.
# material do site oficial da azure.
