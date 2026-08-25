name: generate contribution animations

on:
  schedule:
    - cron: "0 0 * * *"   # roda todo dia à meia-noite (UTC)
  workflow_dispatch:        # permite rodar manualmente pelo botão "Run workflow"
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 20
    steps:
      # 1) Gera a animação da Snake (cobrinha)
      - name: generate snake animation
        uses: Platane/snk@v3
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      # 2) Gera a animação do Pac-Man
      - name: generate pacman animation
        uses: abozanona/pacman-contribution-graph@main
        with:
          github_user_name: ${{ github.repository_owner }}
          games: 'pacman'

      # 3) Junta tudo e publica na branch "output"
      - name: push SVGs to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
