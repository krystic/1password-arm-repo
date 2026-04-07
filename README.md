# 1Password ARM64 APT Repository

自动构建的 1Password Linux ARM64 版本 APT 软件源。

## 使用方法

```bash
# 添加 GPG 密钥
curl -fsSL https://1password.repo.ice2coder.com/public.key | sudo gpg --dearmor -o /usr/share/keyrings/1password-arm.gpg

# 添加软件源
echo "deb [arch=arm64 signed-by=/usr/share/keyrings/1password-arm.gpg] https://1password.repo.ice2coder.com stable main" | sudo tee /etc/apt/sources.list.d/1password-arm.list

# 安装
sudo apt update && sudo apt install 1password
```

## 工作原理

- **自动构建**：GitHub Actions 每天检查 [1Password 官方](https://downloads.1password.com/linux/tar/stable/aarch64/1password-latest.tar.gz) 是否有新版本
- **打包发布**：自动将 tar.gz 打包为 .deb 并发布到 GitHub Releases
- **APT 仓库**：通过 Cloudflare Pages 托管仓库索引，.deb 文件通过 302 重定向到 GitHub Releases

## 为什么需要这个？

1Password 官方不提供 ARM64 架构的 APT 源，只提供 tar.gz 格式。本项目自动将其转换为标准 APT 源，方便在 ARM64 设备（如树莓派、Apple Silicon 虚拟机等）上安装和更新。

## 许可证

本仓库仅提供自动化打包脚本，1Password 软件本身的版权归 [1Password](https://1password.com/) 所有。
