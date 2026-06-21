# O Poder de IA e do Python na Coleta e Tratamento de Dados Judiciais
---
## Agenda
- Transcrição de audiências judiciais
- Análise de dados da API do DataJud
---
## Transcrição de audiências judiciais
- Por que automatizar a transcrição?
- Pipeline com FFmpeg + Word Online + Chat de IA
---
### FFmpeg
- Baixar e instalar a versão portátil
- Mover a pasta para local de preferência
- Editar Path (variáveis de ambiente) apontando para o executável da pasta "bin"
- Testar
---
### Comandos úteis
- De "asf" para "mp4":
`ffmpeg -i arquivo_original.asf arquivo_modificado.mp4`
- De "asf" para "mp3":
`ffmpeg -i arquivo_original.asf -vn arquivo_modificado.mp3`
- Segmentando os primeiros 10 minutos de um vídeo:
`ffmpeg -i arquivo_original.asf -t 00:10:00 parte_1.asf`
- Segmentando dos 10 aos 20 minutos de um vídeo:
`ffmpeg -i arquivo_original.asf -ss 00:10:00 -t 00:20:00 parte_2.asf`
- [Cheat Sheet](docs\ffmpeg_cheat_sheet.pdf)
---
### Word online
- Arquivos suportados: `.wav`, `.mp4`, `.m4a`, `.mp3`
- Identificação/edição dos palestrantes
- Opções de carimbo e data/hora
- Vínculo com o arquivo original (parsta `Meus Arquivos\Arquivos Transcritos`)
- Solução alternativa: **Whisper** (modelo local)
---
### Passo final: ajustes com IA
**Exemplo de prompt**
```markdown

# Tarefa

Transcreva o(s) depoimentos(s) fornecidos abaixo em forma discursiva e direta, ou seja, transforme-os em narrativas, uma para cada depoente.

# Formato de saída esperado

**Exemplo**
A vítima Maria da Silva contou que, em novembro de 2020, deixou o carro no estacionamento do réu. Acordaram que ele o venderia por 60 mil. O acusado avisou que vendeu o carro para Renata. Ela ficou com o carro mesmo não tendo transferido o carro para ela. Ela não pagou em dezembro, nem em janeiro, apesar de conversarem. Acordaram datas e ele não cumpriu. Ficou com o recibo. Consultando o carro, viu que ele estava alienado. Eles conseguiram fazer o financiamento, sem que o depoente tivesse assinado. O réu chegou a pagar 10 mil reais. Em fevereiro, arrumou um advogado, fez uma notificação e entrou com ação. O contrato era bem claro: vender o carro do depoente e entregar o valor. Por isso se sentiu lesada.   
**Fim do Exemplo**

# Instruções especiais
- Proceda assim com todos os depoimentos contidos na transcrição.
- Não omita informações. Escreva tudo o que foi dito. 
- Omita, porém, as perguntas do juiz, do promotor e do advogado, deixando as respostas fluidas e na forma de depoimento contínuo, como no exemplo. 
```
---
## Análise de dados da API do DataJud
### Visão geral
- O que é uma API?
- A API do CNJ: 
  - metadados e movimentações dos processos judiciais não gravados de sigilo. 
  - Consultas com **Elasticsearch** (motor de busca orientado a JSON)
---
### Busca com Elasticsearch
- Blocos: `size`, `query` e `search` (opicionais)
```markdown
{
  "size": 10,
  "query": {
    "bool": {
      "must": [
        { "match": { "nome_do_campo_1": "valor_procurado" } },
        { "match": { "nome_do_campo_2": "outro_valor" } }
      ]
    }
  },
  "sort": [
    { "campo_data": { "order": "desc" } }
  ]
}
```

- [Cheat Sheet](docs\datajud_cheat_sheet.pdf)

---
## Referências
- [API pública do Datajud](https://www.cnj.jus.br/sistemas/datajud/api-publica/)
- [Blog](https://jespimentel.blogspot.com/2025/11/ffmpeg-para-manipulacao-de-arquivos-de.html)
- [Brazilvisible.org](https://brazilvisible.org/docs/apis/poder-judiciario-cnj/datajud/)
- **Pimentel**, José Eduardo de Souza. [Por que promotores de justiça deveriam conhecer o Python?](https://medium.com/@pimentel.jes/por-que-promotores-de-justi%C3%A7a-deveriam-conhecer-o-python-26c9c7860f43)
- [Colab da transcrição]()
- [Colab da API do Datajud]()
