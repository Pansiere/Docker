# Meu Docker hub :D

## Dica 1 - Limpar o cache de build do Docker

Às vezes, mesmo removendo o container e o volume, o Docker ainda pode usar cache de build para etapas específicas. Você pode limpar completamente o cache de build usando o seguinte comando:

```BASH
docker builder prune --all --force
```

Este comando remove todos os build cache, forçando o Docker a reconstruir tudo desde o início na próxima vez que você construir as imagens.
