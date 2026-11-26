# Rust Vision Lab

Computer Vision Studio: uma plataforma desktop para experimentar e visualizar algoritmos clássicos de visão computacional, com o motor de processamento implementado em Rust.

O projeto serve como laboratório prático para estudar os fundamentos matemáticos e computacionais da visão computacional: processamento espacial e de frequência, detecção de bordas, extração de características, segmentação, transformações geométricas, análise de formas e reconhecimento de padrões.

## Funcionalidades previstas

- Pipelines configuráveis, encadeando operações em sequência
- Visualização de resultados intermediários de cada etapa
- Comparação lado a lado de resultados
- Parâmetros de cada operação editáveis pela interface

## Estrutura do projeto

```
rust-vision-lab/
├── Cargo.toml          # workspace
├── crates/
│   ├── vision-core/    # tipos base (Image) e trait Operation
│   ├── vision-ops/     # algoritmos clássicos, organizados por tema
│   └── vision-pipeline/# encadeamento, execução e cache de estágios
├── src-tauri/          # casca Tauri (comandos que chamam o pipeline)
└── ui/                 # interface React/TypeScript
```

### Algoritmos (`vision-ops`)

```
vision-ops/src/
├── spatial/        # convolução, gaussiano, média, mediana
├── frequency/      # FFT 2D (rustfft), filtros passa-baixa e passa-alta
├── edges/          # Sobel, Prewitt, Laplaciano, Canny
├── geometry/       # rotação, escala, translação, afim, perspectiva
├── segmentation/   # limiarização (Otsu), crescimento de regiões, watershed
├── morphology/     # erosão, dilatação, abertura, fechamento
├── features/       # Harris, histogramas, HOG
└── shape/          # contornos e momentos (com nalgebra quando útil)
```

Cada módulo corresponde a um tema do estudo. Os laços por linha ou por pixel usam `rayon` apenas depois que a versão sequencial estiver correta, para permitir comparação entre as duas.

## Stack

- **Rust**: `image`, `ndarray`, `rustfft`, `rayon`, `nalgebra`
- **Desktop**: Tauri
- **Front-end**: React + TypeScript
- **Opcional**: `wgpu` para aceleração

## Como executar

> Em construção. Os comandos serão documentados conforme cada etapa for concluída.

Pré-requisitos previstos:
- Rust (toolchain estável)
- Node.js e npm (para o front-end)
- Dependências de sistema do Tauri

## Roteiro

1. Tipo `Image` e conversões de entrada e saída, com testes de ida e volta
2. Convolução genérica e filtro gaussiano, validados contra referências conhecidas
3. Sobel e Canny
4. Pipeline linear com captura de estágios intermediários
5. Limiarização, morfologia e FFT
6. Binário de linha de comando que executa um pipeline a partir de JSON
7. Casca Tauri e interface React

## Licença

A definir.