name: ci

on:
  push:
    branches:
      - main
  schedule:
    - cron: "*/15 */6 * * *"

jobs:
  autogreen:
    runs-on: ubuntu-latest
    
    permissions:
      contents: write
  
    steps:
      - name: Clone repository
        uses: actions/checkout@v3

      - name: Auto green
        run: |
          git config --local user.email "liuli1001@skiff.com"
          git config --local user.name "liuli1001"
          git remote set-url origin https://${{ github.actor }}:${{ secrets.GITHUB_TOKEN }}@github.com/${{ github.repository }}
          git pull --rebase
          git commit --allow-empty -m "分手那天我试着握着你手~"
          git push
