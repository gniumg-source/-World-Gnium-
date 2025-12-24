#!/usr/bin/env bash
# Script para crear el repo en la cuenta gniumg-source y empujar el contenido.
# USO:
# 1) export GH_TOKEN="ghp_...."      # (o configure la CLI gh con gh auth login)
# 2) ./script/create_and_push.sh
#
# El token debe tener scope: repo (y workflow si quieres actualizar actions)
set -euo pipefail

REPO="world-gnium"
OWNER="gniumg-source"
FULL="${OWNER}/${REPO}"
COMMIT_MSG="chore: complete repo scaffold with starter app and automation"

# Inicializar git local si no existe
if [ ! -d .git ]; then
  git init
  git add .
  git commit -m "$COMMIT_MSG"
fi

# Preferir gh CLI si está autenticado
if command -v gh >/dev/null 2>&1; then
  echo "[info] gh CLI disponible. Intentando crear/actualizar repositorio usando gh..."
  if gh repo view "$FULL" >/dev/null 2>&1; then
    echo "[info] El repositorio $FULL ya existe en GitHub. Empujando cambios..."
    git remote remove origin 2>/dev/null || true
    git remote add origin "https://github.com/$FULL.git"
    git branch -M main
    git push -u origin main
    exit 0
  else
    echo "[info] Creando repositorio $FULL con gh..."
    gh repo create "$FULL" --public --source=. --remote=origin --push -y || true
    exit 0
  fi
fi

# Si no hay gh CLI, usar GH_TOKEN para crear via API
if [ -z "${GH_TOKEN:-}" ]; then
  echo "Error: ni la CLI 'gh' está disponible ni la variable GH_TOKEN está configurada."
  echo "Por favor instala la CLI 'gh' o exporta GH_TOKEN con un Personal Access Token."
  exit 1
fi

echo "[info] Usando GH_TOKEN para crear repo vía API GitHub..."
# Crear repo; si existe, lo ignoramos
HTTP_RESPONSE=$(curl -s -o /dev/stderr -w "%{http_code}" -H "Authorization: token $GH_TOKEN" -H "Accept: application/vnd.github+json" \
  -d "{\"name\":\"$REPO\",\"private\":false}" https://api.github.com/user/repos || true)

# Añadir remoto y empujar
git remote remove origin 2>/dev/null || true
git remote add origin "https://github.com/$FULL.git"
git branch -M main
git push -u origin main

echo "[done] Repositorio disponible: https://github.com/$FULL"
