SUBIR A REPOSITORIO

```
git init
```

```
git add .
```

```
git commit -m "comentario"
```

```
git branch -M main
```

```
git remote add origin enlace
```

```
git push -u origin main
```

SOLUCIÓN PULL REQUEST 
```
git checkout rama
```

```
git branch main rama -f
```

```
git checkout main
```

```
git push origin main -f
```

SOLUCIÓN DE ERRORES MASTER --> MAIN

```
git fetch origin main:tmp
```

```
git rebase tmp
```

```
git push -u origin main
```

