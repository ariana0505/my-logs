21/09/26

# Objetivos de la clase 🎯

Instalar Claude Code y extensiones para nuestro editor.

---

## Ambientes

- Terminal
- Desktop
- Extensión en un IDE
- Slack
- Chrome Extension
- GitHub Actions

---

## Instalación de Claude Code

Vamos a usar la instalación de Claude Code en la terminal usando el siguiente comando de acuerdo con la plataforma.

### macOS/Linux

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### Windows (powershell)

```powershell
irm https://claude.ai/install.ps1 | iex
```

### Windows (CMD)

```batch
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

---

## En profundidad

### Sobre los ambientes

No todos los ambientes listados son lo mismo:

- **Terminal**: la forma principal, un CLI (interfaz de línea de comandos) que se instala una sola vez y funciona en cualquier proyecto.
- **Desktop**: una aplicación con interfaz gráfica para Mac o Windows.
- **Extensión en un IDE**: se integra dentro de editores como VS Code o JetBrains, mostrando los cambios directamente en el editor.
- **Slack, Chrome Extension, GitHub Actions**: formas de invocar Claude Code desde fuera de la terminal, útiles para automatizar tareas o revisar código sin salir de esas herramientas.

### Sobre los comandos de instalación

Los comandos de este archivo están fragmentados: en macOS/Linux y en PowerShell, el patrón real de instalación es descargar el script y ejecutarlo en un mismo paso encadenado, no dos comandos sueltos como aparecen aquí. La forma habitual sería algo del tipo:

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

```powershell
irm https://claude.ai/install.ps1 | iex
```

**Nota:** antes de ejecutar cualquiera de estos comandos conviene verificar la URL exacta y el script en la documentación oficial de Claude Code, ya que instalar así implica correr un script descargado de internet con permisos del sistema.
