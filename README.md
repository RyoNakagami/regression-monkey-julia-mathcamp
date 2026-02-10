



## Juliaの初期設定

```bash
julia --project=$(git rev-parse --show-toplevel) -e 'using Pkg; Pkg.activate("."); Pkg.instantiate()'
```

```bash
julia --project=. -e 'using IJulia; installkernel("Julia (Book)", "--project=@.")'
```

## Quarto Publish

運用としては `main` ブランチの内容をlocalでレンダリングし，それをGitHub Pagesにデプロイする流れを想定しています．
ただし，`gh-pages` ブランチは `.pre-commit-config.yaml` は存在しないため，pre-commitのhookが働かず，以下のようなエラーが発生します:

```bash
branch 'gh-pages' set up to track 'origin/gh-pages'.
HEAD is now at 4d5b51a Built site for gh-pages
No .pre-commit-config.yaml file was found
- To temporarily silence this, run `PRE_COMMIT_ALLOW_NO_CONFIG=1 git ...`
- To permanently silence this, install pre-commit with the --allow-missing-config option
- To uninstall pre-commit run `pre-commit uninstall`
fatal: '.quarto/quarto-publish-worktree-21440733a1c14bff' contains modified or untracked files, use --force to delete it
```

それに対処するため，以下のような実行を想定しています

```bash
PRE_COMMIT_ALLOW_NO_CONFIG=1 quarto publish gh-pages
```

**&#9654;&nbsp; スクリプトversion**

```bash
bash publish-quarto-book.sh
```

## References

- [Quarto Publishing with GitHub Pages](https://quarto.org/docs/publishing/github-pages.html)
