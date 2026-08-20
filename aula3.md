# estrutura JSON e BSON

## JSON

formato universal de dados, possui tipos de dados mais limitados(string, number, boolean, array, Object, Null)

ocupa mais espaço e mais lento para analise computacional.

CHAVE - VALOR

## BSON

BINARIO json

# DOCUMENTOS EBUTIDOS VS REFERÊNCIAS

## referencias
OS DOCUMENTOS SÃO ARMAZENADOS EM COLEÇÕES SEPARADAS E CONECTADOS UTILIZANDO UM IDENTIFICADOR UNICO (ObjectIDs)

relação muitos pra muitos / dados compartilhados / documentos muito grande.

## Embutidos

os dados são armazenados diretamente, dentro de um unico documento, utilizando sub-documentos ou arrays.

relação 1-1 / 1 - poucos / dados sempre consultados juntos.

# foco principal do mongoDB

consultas frequentes - performace(latencia baixa) - menos Joins

## Denormalização

EX: 
{
    "pedido": 100,
    "cliente": {
        "id":1
        "nome": "João"
    }
}

