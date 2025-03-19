name: Update README

on:
  schedule:
    - cron: "0 */12 * * *"  # Runs every 12 hours
  workflow_dispatch:  # Allows manual trigger

jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Generate New README
        run: |
          echo "# Hi there! 👋" > README.md
          echo "" >> README.md
          echo "Welcome to my profile. Here are my latest updates:" >> README.md
          echo "" >> README.md
          
          # GitHub Stats
          echo "## 📊 GitHub Stats" >> README.md
          echo "![](https://github-readme-stats.vercel.app/api?username=${{ github.repository_owner }}&show_icons=true&theme=dark)" >> README.md
          echo "" >> README.md
          
          # Recent Contributions
          echo "## 🔥 Recent GitHub Contributions" >> README.md
          echo "![](https://github-readme-streak-stats.herokuapp.com/?user=${{ github.repository_owner }}&theme=dark)" >> README.md
          echo "" >> README.md
          
          # Last Updated
          echo "_Last updated: $(date +"%Y-%m-%d %H:%M:%S")_" >> README.md

      - name: Commit and Push Changes
        run: |
          git config --global user.name "github-actions[bot]"
          git config --global user.email "github-actions[bot]@users.noreply.github.com"
          git add README.md
          git commit -m "Updated README with latest stats" || exit 0
          git push
