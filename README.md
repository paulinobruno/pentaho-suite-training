## Configurando o servidor

Variável de ambiente `KETTLE_HOME` é o diretório onde deve estar os arquivos `kettle.properties` e `repositories.xml`.

## Database Lookup

Faz N queries por valor. Simula um JOIN com outra fonte de dados.
O problema: faz N queries. Dependendo do volume de linhas, vale à pena fazer cache dos valores.

## Pegando propriedades da JVM

A notação de substituição de variáveis `${variavel}` considera todas as variáveis da plataforma Pentaho.

Para ter acesso aos valores de propriedades da JVM (exemplo: `System.getProperties("java.io.tmpdir")`) pode-se utilizar a seguinte notação: `%%java.io.tmpdir%%`.