name: Metrics
on:
  schedule: [{cron: "0 0,12 * * *"}]
  workflow_dispatch:
  push: {branches: ["master", "main"]}
jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      # 🟢 第一步：在 GitHub 宿主机上十秒钟内强行安装中文字体包与核心字体
      - name: Install Chinese Fonts and Emoji Support
        run: |
          sudo apt-get update
          sudo apt-get install -y fonts-noto-cjk fonts-noto-color-emoji ttf-mscorefonts-installer

      # 🟢 第二步：调用 Docker 镜像，并把宿主机的字体目录直接挂载（共享）进容器内部
      - name: Generate Custom Metrics via Docker Container
        uses: docker://ghcr.io/lowlighter/metrics:master
        with:
          # 💡 核心破局点：使用 entrypoint 强行调用核心脚本，同时自动继承宿主机的字体环境
          entrypoint: node
          args: /metrics/source/app/action/index.mjs
        env:
          GITHUB_TOKEN: ${{ secrets.METRICS_TOKEN }}
          TOKEN: ${{ secrets.METRICS_TOKEN }}
          INPUT_TOKEN: ${{ secrets.METRICS_TOKEN }}
          
          USER: jax2730
          TEMPLATE: classic
          BASE: header, metadata
          CONFIG_TIMEZONE: Asia/Shanghai
          PLUGINS_ERRORS_FATAL: "no"

          # 🟢 1. 3D 立体贡献日历
          PLUGIN_ISOCALENDAR: "yes"
          PLUGIN_ISOCALENDAR_DURATION: full-year

          # 🟢 2. 技术栈与编程语言详细分析
          PLUGIN_LANGUAGES: "yes"
          PLUGIN_LANGUAGES_ANALYSIS_TIMEOUT: "15"
          PLUGIN_LANGUAGES_CATEGORIES: markup, programming
          PLUGIN_LANGUAGES_COLORS: github
          PLUGIN_LANGUAGES_LIMIT: "8"
          PLUGIN_LANGUAGES_SECTIONS: most-used
          PLUGIN_LANGUAGES_THRESHOLD: "0%"

          # 🟢 3. 星标与高光项目展示
          PLUGIN_STARS: "yes"
          PLUGIN_STARS_LIMIT: "4"

          # 🟢 4. 编码作息习惯分析
          PLUGIN_HABITS: "yes"
          PLUGIN_HABITS_FROM: "200"
          PLUGIN_HABITS_DAYS: "14"
          PLUGIN_HABITS_FACTS: "yes"
          PLUGIN_HABITS_CHARTS: "yes"

          CONFIG_TWEMOJI: "no"
          CONFIG_PADDING: 0, 5 + 11%
