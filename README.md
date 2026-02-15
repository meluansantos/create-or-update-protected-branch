# Create or Update Protected Branch

GitHub Action para aplicar regras de proteção a branches automaticamente.

## Uso

```yaml
- uses: meluansantos/create-or-update-protected-branch@v2
  with:
    token: ${{ secrets.GITHUB_TOKEN }}
    repository: ${{ github.repository }}
    branch: main
    required_status_checks: |
      build
      test
      security-scan
    required_pull_request_reviews: true
    required_approving_review_count: 2
    enforce_admins: true
    require_signed_commits: true
```

## Inputs

| Input | Descrição | Obrigatório | Default |
| ----- | --------- | ----------- | ------- |
| `token` | GitHub token com permissões de admin | ✅ | - |
| `repository` | Repositório (owner/repo) | ✅ | - |
| `branch` | Branch a proteger | ✅ | `main` |
| `required_status_checks` | Status checks obrigatórios (um por linha) | ❌ | - |
| `required_pull_request_reviews` | Exigir PR reviews | ❌ | `false` |
| `required_approving_review_count` | Mínimo de aprovadores | ❌ | `1` |
| `enforce_admins` | Aplicar regras para admins | ❌ | `false` |
| `require_signed_commits` | Exigir commits assinados | ❌ | `false` |

## Permissões

O token precisa das seguintes permissões:
- `repo` (para repositórios privados)
- Ou `public_repo` (para repositórios públicos)

Para `enforce_admins: true`, o token precisa ser de um admin do repositório.

## Exemplo Completo

```yaml
name: Protect Main
on:
  schedule:
    - cron: '0 0 * * SUN'  # Todo domingo
  workflow_dispatch:       # Manual

jobs:
  protect:
    runs-on: ubuntu-latest
    steps:
      - uses: hardened-sh/create-or-update-protected-branch@v2
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          repository: ${{ github.repository }}
          branch: main
          required_status_checks: |
            build
            test
            security-scan
          required_pull_request_reviews: true
          required_approving_review_count: 2
          enforce_admins: true
          require_signed_commits: true
```

## Licença

MIT
