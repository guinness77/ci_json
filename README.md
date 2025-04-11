# **Captions with Intention**

Legendas Detalhadas em JSON para Automação no AE

## Visão Geral

Este repositório contém arquivos de legenda em JSON altamente detalhados, derivados do áudio do filme "Jurassic Park (1993)". Os dados são estruturados especificamente para facilitar a automação de animações, tipografia cinética e visualizações de dados dentro do Adobe After Effects, utilizando ExtendScript (`.jsx`) ou outros métodos de scripting.

Os arquivos JSON contêm transcrições precisas, temporização exata por palavra (em frames absolutos), identificação de locutor via IDs de cor únicos, pontuações de emoção/intensidade por palavra e anotações distintas para Diálogo (`dia`), Efeitos Sonoros (`sfx`) e Música (`mus`).

## Principais Recursos dos Dados para Scripting

*   **Temporização Absoluta por Palavra em Frames:** Cada objeto de palavra (item no array `wds`) possui chaves `in` e `out` representando o **frame exato de início e fim** (inteiro, baseado em 23.976 fps). O **preenchimento estrito de lacunas** garante temporização contínua dentro de cada bloco `wds`, ideal para criação de keyframes sem interrupções.
*   **IDs Hexadecimais de Cor por Locutor (`sid`):** Cada bloco de diálogo (`dia`) contém uma chave `sid` com um código de cor hexadecimal único atribuído ao locutor. Isso pode controlar diretamente propriedades de cor em camadas do AE. O objeto `meta.char_colors` mapeia esses códigos hex para os nomes dos personagens.
*   **Pontuações de Emoção/Intensidade (`int`):** Cada objeto de palavra possui um valor `int` (escala 1-11) representando a intensidade/emoção do áudio. Estes dados podem ser usados para modular parâmetros de animação como escala, opacidade, intensidade de efeitos, etc.
*   **Anotações Estruturadas (`dia`, `sfx`, `mus`):** Cada bloco de legenda (item `subs`) contém *apenas uma* dessas chaves, permitindo que os scripts diferenciem facilmente os tipos de conteúdo e apliquem estilos ou presets de animação específicos.
*   **Transcrição Completa (`txt`):** A chave `txt` dentro de cada bloco `dia`, `sfx` ou `mus` fornece o texto completo do bloco. O `wds[].w` fornece o texto da palavra individual.

## Exemplo da Estrutura JSON

```json
{
  "tr": {
    "meta": {
      "fps": 23.976,
      "lang": "pt-BR", // Exemplo: Pode ser 'en' se a transcrição for original
      "qual": "Alta",
      "char_colors": {
        "#FFB482": "GRANT", // Mapeamento Exemplo
        // ... outros personagens
      }
    },
    "subs": [
      {
        "in": 2500,  // Frame de início do bloco
        "out": 2550, // Frame de fim do bloco
        "dia": {
          "sid": "#FFB482", // ID Hex do Locutor para cor
          "cty": "main01",  // Categoria do Personagem
          "txt": "A vida encontrou um meio.", // Exemplo traduzido
          "wds": [ // Array de palavras
            { "w": "A",     "in": 2500, "out": 2505, "int": 7 }, // Dados da Palavra
            { "w": "vida",  "in": 2506, "out": 2515, "int": 7 }, // Nota: 'in' segue 'out' anterior + 1 (gap preenchido)
            { "w": "encontrou", "in": 2516, "out": 2530, "int": 7 },
            { "w": "um",    "in": 2531, "out": 2533, "int": 6 },
            { "w": "meio.", "in": 2534, "out": 2550, "int": 8 } // Pontuação anexada
          ]
        }
      },
      // ... outros blocos de legenda (dia, sfx, ou mus)
    ]
  }
}
