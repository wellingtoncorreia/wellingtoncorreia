name: Generate snake animation

on:
  schedule: # execute every 12 hours
    - cron: "0 */12 * * *" # Ajustado para executar a cada 12 horas de forma correta

  workflow_dispatch:

  push:
    branches:
    - master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: Checkout the repository
        uses: actions/checkout@v3

      - name: generate snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: wellingtoncorreia # Substituído pelo seu nome de usuário
          outputs: dist/snake.svg?palette=github-dark

      - name: push snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
