# **Captions with Intention**

Legendas Detalhadas em JSON para Automação no AE
## Visão Geral

Este projeto trabalha JSON detalhados do filme "Jurassic Park (1993)", estruturados para automação de animações no After Effects via ExtendScript (`.jsx`).

Os arquivos JSON incluem transcrições precisas, temporização exata por palavra (em frames absolutos), identificação de locutor por IDs de cor, pontuações de emoção/intensidade por palavra e anotações para Diálogo (`dia`), Efeitos Sonoros (`sfx`) e Música (`mus`).

## Principais Recursos dos Dados para Scripting

- **Temporização Absoluta por Palavra em Frames:** Cada palavra (`wds`) tem `in` e `out` (frame inicial e final exato, 23.976 fps). O preenchimento de lacunas garante temporização contínua.
- **IDs Hexadecimais de Cor por Locutor (`sid`):** Blocos de diálogo (`dia`) contêm `sid` (código de cor hexadecimal único) mapeado para nomes de personagens em `meta.char_colors`, para controle de cor no AE.
- **Pontuações de Emoção/Intensidade (`int`):** Cada palavra tem um valor `int` (1-11) para modular parâmetros de animação.
- **Anotações Estruturadas (`dia`, `sfx`, `mus`):** Blocos de legenda contêm _apenas uma_ dessas chaves, permitindo diferenciação de conteúdo e aplicação de estilos específicos.
- **Transcrição Completa (`txt`):** A chave `txt` em `dia`, `sfx` ou `mus` fornece o texto completo do bloco. `wds[].w` fornece o texto da palavra individual.

## Exemplo da Estrutura JSON

```json
{
  "tr": {
    "meta": {
      "fps": 23.976,
      "lang": "pt-BR",
      "qual": "Alta",
      "char_colors": { "#FFB482": "GRANT" }
    },
    "subs": [
      {
        "in": 2500, "out": 2550,
        "dia": {
          "sid": "#FFB482", "cty": "main01",
          "txt": "A vida encontrou um meio.",
          "wds": [
            { "w": "A", "in": 2500, "out": 2505, "int": 7 },
            { "w": "vida", "in": 2506, "out": 2515, "int": 7 },
            { "w": "encontrou", "in": 2516, "out": 2530, "int": 7 },
            { "w": "um", "in": 2531, "out": 2533, "int": 6 },
            { "w": "meio.", "in": 2534, "out": 2550, "int": 8 }
          ]
        }
      }
    ]
  }
}
```