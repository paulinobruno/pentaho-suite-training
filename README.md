# ETL

## Configurando o servidor

Variável de ambiente `KETTLE_HOME` é o diretório onde deve estar os arquivos `kettle.properties` e `repositories.xml`.

## Database Lookup

Faz N queries por valor. Simula um JOIN com outra fonte de dados.
O problema: faz N queries. Dependendo do volume de linhas, vale à pena fazer cache dos valores.

## Pegando propriedades da JVM

A notação de substituição de variáveis `${variavel}` considera todas as variáveis da plataforma Pentaho.

Para ter acesso aos valores de propriedades da JVM (exemplo: `System.getProperties("java.io.tmpdir")`) pode-se utilizar a seguinte notação: `%%java.io.tmpdir%%`.

## Dimension Lookup / Update

Aplica o conceito de Slowly Changing Dimension Type 2, onde se versiona os registros.
É sempre necessário ter, além de todos os atributos da dimensão, 3 campos auxiliares para o controle de versionamento:

- número da versão;
- data início;
- data fim.

No caso dos campos data, é importante determinar valores de ano mínimo e máximo (para que o Pentaho já alimente a data início com 1/jan do ano mínimo e a data término com 31/dez do ano máximo).

Na situação em que precisa inserir registros (não somente atualizar), o Pentaho gerencia a relação de Insert / Update com o devido versionamento.

**Importante**: há um [bug](https://jira.pentaho.com/browse/PDI-2292) no Data Integration. O workaround conhecido é inserir um registro com chave técnica (PK da dimensão) `0` (zero).
