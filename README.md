# ambicao

Plugin do Claude Code com a skill `/ambicao`: reescreve um braindump ou pedido num prompt mais ambicioso (altitude, profundidade, alcance, juiz externo) e para antes de executar.

## Instalar

```
/plugin marketplace add nmarcofernandess/ambicao
/plugin install ambicao@ambicao
```

Uso: `/ambicao:ambicao [braindump ou tarefa]` (ou `/ambicao`, se não houver conflito de nome).

## Claude Code na web

Declare o marketplace em `.claude/settings.json` do repositório de trabalho:

```json
{
  "extraKnownMarketplaces": {
    "ambicao": { "source": { "source": "github", "repo": "nmarcofernandess/ambicao" } }
  },
  "enabledPlugins": { "ambicao@ambicao": true }
}
```
