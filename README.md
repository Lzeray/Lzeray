name: Update Streak Stats
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      - uses: DenverCoder1/github-readme-streak-stats@v1
        with:
          options: user=${{ github.repository_owner }}&theme=radical
          path: profile/streak.svg
      - name: Commit
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add profile/streak.svg
          git commit -m "Update streak" || exit 0
          git push
