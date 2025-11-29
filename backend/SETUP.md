# Setup Guide / 设置指南

## Python 3.13.9 Virtual Environment / Python 3.13.9 虚拟环境

### Why pip3.13 can't be used directly / 为什么不能直接使用 pip3.13

Homebrew 安装的 Python 3.13 是"外部管理"的（PEP 668），这是为了保护系统 Python 不被破坏。**必须使用虚拟环境**来安装包。

### Current Setup / 当前设置

✅ Python 3.13.9 已通过 Homebrew 安装  
✅ 虚拟环境已创建在 `venv/` 目录  
✅ 核心包已安装：
- FastAPI 0.118.3
- Uvicorn 0.38.0
- Pydantic 2.12.5
- Google ADK 1.19.0

### Usage / 使用方法

1. **激活虚拟环境 / Activate virtual environment:**
   ```bash
   source venv/bin/activate
   ```

2. **运行应用 / Run application:**
   ```bash
   python main.py
   ```

3. **安装额外依赖 / Install additional dependencies:**
   ```bash
   pip install <package-name>
   ```

4. **退出虚拟环境 / Deactivate virtual environment:**
   ```bash
   deactivate
   ```

### Notes / 注意事项

- 始终在虚拟环境中工作 / Always work within the virtual environment
- `google-adk` 可能需要额外的依赖，当实际使用时 pip 会自动安装 / `google-adk` may need additional dependencies that will be installed automatically when used
- 如果遇到依赖冲突，可以尝试：`pip install --upgrade google-adk` / If you encounter dependency conflicts, try: `pip install --upgrade google-adk`

