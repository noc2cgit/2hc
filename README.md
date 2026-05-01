# 2hc — yum/dnf repository

Repositorio publico de RPMs do **2hc** (HealthCheck NOC para Oracle Linux),
binario diagnostico modular para servidores de banco de dados Oracle em
Oracle Linux 7, 8, 9 e 10.

> Este repositorio so hospeda os pacotes `.rpm` publicados.
> O codigo-fonte esta em [`ulissesb2com/healthcheck_noc`](https://github.com/ulissesb2com/healthcheck_noc) (privado).
> Os pacotes sao gerados automaticamente pelo workflow GitHub Actions
> daquele repositorio a cada tag `v*` e publicados na branch `gh-pages`
> deste repo.

## Instalacao em Oracle Linux 7/8/9/10

```bash
sudo dnf install -y https://noc2cgit.github.io/2hc/repo/2hc-release-latest.noarch.rpm
sudo dnf install -y 2hc

2hc -v          # imprime a versao instalada
2hc --noc       # gera relatorio NOC
```

A primeira linha adiciona `/etc/yum.repos.d/2hc.repo` apontando para
este repositorio. A segunda instala o pacote `2hc` propriamente dito.

O auto-update diario (`2hc-autoupdate.timer`) e ativado automaticamente
na primeira instalacao — atualiza apenas o pacote `2hc`.

## Verificacao manual

```bash
curl -sI https://noc2cgit.github.io/2hc/repo/2hc-release-latest.noarch.rpm
# HTTP/2 200 = repositorio servindo

curl -s https://noc2cgit.github.io/2hc/repo/repodata/repomd.xml | head
```

## Estrutura

A branch `gh-pages` contem:

```
repo/
|-- repodata/                       # metadata gerada por createrepo_c
|-- 2hc-8.X.Y-1.noarch.rpm          # pacote principal
|-- 2hc-release-1-1.noarch.rpm      # bootstrap repo
`-- 2hc-release-latest.noarch.rpm   # alias do release mais recente
```

A branch `main` (este README) e fachada — o conteudo servido pelo
GitHub Pages vem de `gh-pages`.

## Documentacao

- Codigo-fonte: [ulissesb2com/healthcheck_noc](https://github.com/ulissesb2com/healthcheck_noc)
- Instalacao detalhada: [Documentation/INSTALL.md](https://github.com/ulissesb2com/healthcheck_noc/blob/homolog/Documentation/INSTALL.md)
- Release pipeline: [Documentation/RELEASE.md](https://github.com/ulissesb2com/healthcheck_noc/blob/homolog/Documentation/RELEASE.md)

## Recursos do 2hc

- Governanca contextual de tablespaces (10 criterios + 3 dimensoes)
- Forecast de exaustao FS/ASM com janela longa preferida (90d)
- Deteccao de conflito de janelas RMAN x datapump
- Cruzamento top-consumo x logs de backup
- Suporte a Standby (DataGuard) e Grid Infrastructure (+ASM)
- Relatorio formatado para uso em NOC + saida JSON opcional
