🩸 Blood Donation NoSQL Intelligence
Este repositório apresenta a aplicação de inteligência de dados e processamento NoSQL para um sistema de hemocentro. O projeto demonstra proficiência em operações de CRUD e no uso do Aggregation Framework do MongoDB para extração de KPIs.

🚀 Tecnologias e Competências
Banco de Dados: MongoDB (NoSQL).

Ferramenta: MongoDB Compass (Interface Gráfica).

Data Analysis: Construção de pipelines de agregação, extração de métricas e auditoria de dados.

Formação: Desenvolvido durante a graduação em Sistemas para Internet no IFES.

🛠️ Gestão de Registros (CRUD no Compass)
Exemplos de manipulação direta de documentos para manutenção da base de doadores.

Inserção de Novo Doador e Doação
JSON
// Documento inserido na coleção 'doador'
{
  "idDoador": 101,
  "nomDoador": "Brayan Costa Santos",
  "tipoSangueDoador": "A+",
  "tiposLancheDoador": ["Salmão", "Arroz integral", "Fruta"],
  "enderecoDoador": [{
    "dscLogradouroDoador": "Av tomé de souza, 101",
    "dscCidadeDoador": "Linhares",
    "dscUFDoador": "ES"
  }]
}
🔍 Pipelines de Agregação (Stages)
Abaixo estão os pipelines construídos no Aggregation Tab do Compass para gerar relatórios de Business Intelligence.

1. Relatório de Doações Pós-2020 (Join & Sort)
$lookup: Une a coleção doador com doacao pelo campo idDoador.

$unwind: Desconstrói o array de doações para análise individual.

$match: Filtra apenas doações com data superior a 01/01/2020.

$sort: Ordena os resultados pela data de forma decrescente.

2. Volume Total por Tipo Sanguíneo
Este pipeline calcula o volume acumulado de sangue coletado por categoria:

JSON
// Stage: $group
{
  "_id": "$indTipoSangDoador",
  "totalSangue": { "$sum": "$doacoes.qtdSangueDoada" }
}
3. Média de Doação por Estado (UF)
Análise geográfica para identificar o engajamento médio por região:

JSON
// Stage: $group
{
  "_id": "$enderecoDoador.dscUFDoador",
  "mediaSangue": { "$avg": "$doacoes.qtdSangueDoada" }
}
💡 Notas Técnicas de Auditoria
Validação de Filtros: Identifiquei que certos filtros combinados (como múltiplos lanches e doações simultâneas) resultavam em documentos vazios, validando a necessidade de uma base de dados populada com critérios específicos de negócio.

Tratamento de Datas: No Compass, utilizei a conversão para objetos de data para garantir que filtros por anos específicos (ex: 2021) fossem processados com precisão.

Operadores Avançados: Uso estratégico de $exists e $size para auditar campos opcionais e inconsistências de cadastro.

Projeto desenvolvido por Brayan Costa Santos
Analista de Dados em formação - IFES.

