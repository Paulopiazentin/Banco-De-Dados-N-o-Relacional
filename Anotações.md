# Banco de Dados Key-Value (Chave-Valor)

É o tipo mais simples de banco de dados NoSQL. Ele armazena dados como pares de chave e valor, parecido com um dicionário ou um mapa hash gigante.

## Como funciona

### Cada item tem:

Chave: um identificador único (string, número, etc.) usado para buscar o dado
Valor: o dado em si, que pode ser qualquer coisa — texto, número, JSON, objeto binário, lista, etc.

## Exemplo simples:

chave: "usuario:1001"     valor: {"nome": "Ana", "email": "ana@email.com"}
chave: "sessao:xyz789"    valor: {"user_id": 1001, "expira": "2026-08-13"}
chave: "carrinho:1001"    valor: ["produto_A", "produto_B"]
## Características principais
Sem esquema fixo (schema-less): o valor pode ter qualquer formato, não precisa seguir uma estrutura de tabela com colunas definidas

Acesso muito rápido: como a busca é feita diretamente pela chave (geralmente via hash table), operações de leitura e escrita são extremamente rápidas — O(1) na maioria dos casos

Sem relacionamentos: não existe conceito de JOIN entre tabelas como em bancos relacionais. Cada par chave-valor é independente
Alta escalabilidade horizontal: é fácil distribuir os dados entre vários servidores (sharding), já que não há relações complexas para manter

# Quando usar
Cache de dados (sessões de usuário, resultados de consultas frequentes)
Carrinhos de compra
Configurações de aplicações
Filas de mensagens simples
Perfis de usuário quando não há necessidade de consultas complexas
# Quando NÃO é ideal
Quando você precisa fazer buscas complexas por atributos dentro do valor (ex: "todos os usuários com idade > 30")
Quando há muitos relacionamentos entre entidades diferentes
Quando você precisa de transações complexas envolvendo múltiplos registros
# Exemplos de bancos key-value
Banco	Uso típico
Redis	Cache, filas, dados em memória (muito rápido)
Amazon DynamoDB	Aplicações escaláveis na AWS
Riak	Alta disponibilidade e tolerância a falhas
etcd	Configuração distribuída (usado no Kubernetes)
Memcached	Cache simples em memória
# Comparando com um banco relacional

Em um banco relacional (SQL), você teria uma tabela usuarios com colunas fixas (id, nome, email) e faria consultas com WHERE, JOIN, etc.

Em um key-value, você simplesmente pede o valor associado à chave "usuario:1001" e recebe o objeto inteiro de volta — sem consultas SQL, sem JOINs, só busca direta.

# Banco de Dados de Documentos

## Como funciona

Os dados são armazenados como documentos (geralmente JSON, BSON ou XML), agrupados em coleções (equivalente a "tabelas" no mundo relacional, mas sem esquema fixo).

## json
{
  "_id": "usr_1001",
  "nome": "Ana",
  "email": "ana@email.com",
  "enderecos": [
    {"tipo": "casa", "cidade": "São Paulo"},
    {"tipo": "trabalho", "cidade": "Marília"}
  ],
  "preferencias": {
    "notificacoes": true,
    "tema": "escuro"
  }
}

Note que endereços e preferências estão aninhados dentro do mesmo documento — em um banco relacional, isso normalmente exigiria tabelas separadas com chaves estrangeiras.

# Dados semi-estruturados

Diferente do modelo relacional (schema rígido) e do key-value (sem estrutura interna visível), o documento tem estrutura, mas ela pode variar entre documentos da mesma coleção. Dois usuários podem ter campos diferentes sem quebrar nada.

Estruturas aninhadas e mapeamento com código

Esse é um dos maiores atrativos: um documento JSON mapeia quase diretamente para um objeto em linguagens como JavaScript, Python ou Java. Você não precisa "desmontar" o objeto em várias tabelas relacionadas — ele já vem pronto para uso na aplicação.

# Vantagens (detalhando as suas)
Estrutura flexível: adicionar um novo campo não exige alterar o esquema de toda a coleção (sem ALTER TABLE)
Consultas poderosas: apesar de não ter JOINs tradicionais, permite filtrar, indexar e agregar por campos internos do documento, inclusive dentro de arrays e objetos aninhados
Fácil integração com APIs: como APIs REST geralmente trocam JSON, o dado sai do banco e vai para a API (e vice-versa) quase sem transformação
Evolução do esquema (schema evolution): útil quando os requisitos do produto mudam com frequência, comum em startups e MVPs
# Desvantagens (para equilibrar)
Redundância de dados: como não há normalização forte, o mesmo dado pode se repetir em vários documentos
Consistência mais fraca em relacionamentos: se um dado repetido muda, é preciso atualizar em vários lugares (ou usar referências manuais)
Transações complexas envolvendo múltiplos documentos podem ser mais custosas que em um banco relacional tradicional
# Exemplos de bancos (com contexto)
Banco	Característica principal
MongoDB	Mais popular; usa BSON; ótimo suporte a agregações
CouchDB	Foco em replicação e sincronização (bom para apps offline-first)
CosmosDB	Serviço da Microsoft Azure, multi-modelo (documentos, grafos, key-value)
Firestore	Do Google, muito usado em apps mobile/web em tempo real
# Comparando com Key-Value (do seu material anterior)
	Key-Value	Documentos
Valor	Opaco (o banco não "enxerga" o conteúdo)	Estruturado (o banco entende os campos internos)
Consultas	Só pela chave	Pode filtrar por qualquer campo interno
Exemplo	Redis, DynamoDB	MongoDB, CouchDB

# banco de dados em grafos 

??
# banco de dados em colunas
