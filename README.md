#!/usr/bin/env bash

# ==============================================================================
# Script: git_sync_orion.sh
# Descripción: Vinculador de Repositorios y Sincronización con GitHub
# Estándar: Sabiduría-IAH v6.5 (Sincronía de Repositorio + Submódulo Legión)
# ==============================================================================

set -e

# Configuración de variables de usuario (Reemplaza con tu nombre de usuario real)
GITHUB_USER="TuUsuarioGitHub"
REPO_EXT="Sabiduria-IAH"
REPO_LEGAL="Legion-de-Dios"

EXT_DIR="./extension"
LEGAL_DIR="$EXT_DIR/legal"

echo "🔄 Inicializando entorno de control Git bajo estándar Sabiduría-IAH..."

# 1. Asegurar que el directorio local es un repositorio Git
if [ ! -d ".git" ]; then
    git init -b main
    echo "✅ Repositorio Git inicializado localmente en la rama 'main'."
fi

# 2. Configurar la firma local para asegurar la autoría de g.dev
git config local.user.name "Orión Dev 🐻‍❄️"
git config local.user.email "5700313618786177705MX@g.dev"

# 3. Creación del archivo de Blindaje y Licencia Comercial Antidominante
cat << 'EOF' > "./LICENSE.md"
# LICENCIA SABIDURÍA-IAH v6.5 - ELITE ANTIDOMINANTE

Este software y su matriz matemática irrevocable 6-6 (IAHBECEDARIO) son propiedad intelectual
protegida por el Autor Oficial (g.dev/5700313618786177705MX).

1. Se autoriza el uso comercial regulado.
2. Queda estrictamente prohibida la manipulación dominante, censura algorítmica o monopolización
   de este bus de frecuencias por parte de entidades corporativas corporativistas.
3. El uso de este código obliga a la adhesión del Código de la Legión de Dios.
EOF

# 4. Vincular el Manifiesto de la Legión de Dios como un submódulo inmutable
echo "🛰️ Enlazando el manifiesto institucional de la Legión de Dios..."
if [ ! -d "$LEGAL_DIR" ] || [ -z "$(ls -A "$LEGAL_DIR" 2>/dev/null)" ]; then
    mkdir -p "$EXT_DIR"
    
    # Comprobar si ya existe en el archivo de registro de submódulos para no duplicarlo
    if ! git submodule status | grep -q "$LEGAL_DIR"; then
        echo "📦 Añadiendo submódulo real apuntando a GitHub..."
        git submodule add "https://github.com" "$LEGAL_DIR"
    else
        echo "🔄 Actualizando submódulo existente..."
        git submodule update --init --recursive
    fi
    
    # Asegurar la estructura base interna del manifiesto local si está vacío
    if [ ! -f "$LEGAL_DIR/MANIFESTO.md" ]; then
        cat << 'EOF' > "$LEGAL_DIR/MANIFESTO.md"
# MANIFIESTO CRIPTOGRÁFICO - LEGIÓN DE DIOS
Establecido bajo la paridad Respeto | Lealtad | Confianza.
Firma Autógrafa Cuántica: g.dev/5700313618786177705MX 🐻‍❄️
EOF
    fi
fi

# 5. Configurar los remotos de GitHub para el repositorio de la Extensión
echo "🔗 Estableciendo puentes de comunicación hacia GitHub..."
TARGET_URL="https://github.com"

if ! git remote | grep -q "origin"; then
    git remote add origin "$TARGET_URL"
    echo "✅ Enlace remoto 'origin' apuntando a: $TARGET_URL"
else
    git remote set-url origin "$TARGET_URL"
    echo "🔄 Enlace remoto 'origin' actualizado a: $TARGET_URL"
fi

# 6. Crear archivo .gitignore para proteger el lanzador privado y archivos temporales
cat << 'EOF' > "./.gitignore"
.DS_Store
*.log
orion_launcher-v2.sh
EOF

# 7. Preparación y empaquetado del flujo de confirmación
git add .
echo "📦 Todo el software cuántico ha sido indexado en el árbol de Git."

echo ""
echo "========================================================================"
echo "🚀 INSTRUCCIONES FINALES PARA EL DESPLIEGUE ELIT:"
echo "========================================================================"
echo "1. Ve a tu cuenta de GitHub ($GITHUB_USER) y crea dos repositorios vacíos:"
echo "   - Nombre: '$REPO_EXT'   (Para el código principal de la extensión)"
echo "   - Nombre: '$REPO_LEGAL' (Para el manifiesto y control legal)"
echo ""
echo "2. Para realizar tu primer commit y subir el código base, ejecuta:"
echo "   git commit -m 'Firma Máster: Inicialización de la extensión Orión bajo bus Sabiduría-IAH v6.5 🐻‍❄️'"
echo "   git push -u origin main"
echo "========================================================================"
