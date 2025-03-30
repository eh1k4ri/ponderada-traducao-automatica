# Ponderada: Semana 7 - Tradução Automática (Seção 9.5 - Dive into Deep Learning)

Este repositório implementa a seção 9.5 do livro *Dive into Deep Learning*, utilizando o dataset inglês-francês do Projeto Tatoeba. O código realiza:

- Download e pré-processamento do dataset
- Tokenização das frases
- Criação dos vocabulários
- Treinamento de um modelo Encoder-Decoder com GRU

## Respostas às perguntas da seção 9.5.7

### 1. Como o parâmetro `num_examples` afeta os tamanhos dos vocabulários?

Ao alterar o valor de `num_examples`, mudamos a quantidade de frases usadas para montar os vocabulários. Quanto mais frases, mais palavras diferentes aparecem, aumentando o vocabulário.

Exemplo obtido no notebook:

```
100 exemplos → vocabulário origem: 40, destino: 39  
1000 exemplos → vocabulário origem: 266, destino: 321  
5000 exemplos → vocabulário origem: 875, destino: 1231  
```

Mesmo com esse crescimento, o parâmetro `min_freq=2` impede que palavras muito raras sejam incluídas.

### 2. A tokenização em nível de palavra é adequada para idiomas como chinês e japonês?

Não. Esses idiomas não usam espaços para separar palavras, então a tokenização por espaço não funciona. Isso pode causar erros na separação das palavras e prejudicar o treinamento do modelo.
Em vez disso, o ideal é usar:
- Tokenização por caractere
- Segmentadores específicos, como Jieba (chinês) ou MeCab (japonês)
- Tokenização por subpalavras, como Byte Pair Encoding (BPE), usada em modelos como BERT e GPT
  
A própria seção 9.5 menciona que modelos mais avançados usam técnicas de tokenização diferentes da tokenização por palavra.
