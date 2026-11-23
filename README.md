<div align="center">
  <h1>Привет! Я Василиса👋</h1>
  <h3>Frontend / Backend / Fullstack разработчик</h3>
</div>

---

### 👨‍💻 Обо мне
- 🔭 Сейчас работаю над **[Разработкой сайтов и игр]**
- 🌱 Изучаю **TypeScript, Git и GitHub, Linux и работу с терминалом**

[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/ilsved)
[![VK](https://img.shields.io/badge/VK-4C75A3?style=for-the-badge&logo=vk&logoColor=white)](https://vk.com/id756701331)

name: Generate snake animation

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - uses: actions/checkout@v4

      - name: generate snake animation
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: push to output branch
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: output
          force: true
          directory: dist
