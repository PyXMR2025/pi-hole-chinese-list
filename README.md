# pi-hole-chinese-list
适用于 Pi-hole 的中文广告/骚扰域名列表，基于 Easylist 等系列规则自动生成，每天 UTC 0 点（北京时间 8 点）自动更新。

## 仓库特点
- **自动更新**：每天 UTC 0:00 自动抓取最新规则并生成列表，无需手动维护  
- **精准过滤**：基于 Easylist 官方规则+中文特化规则，适配国内广告场景  
- **去重优化**：自动去重、过滤无效规则，仅保留 Pi-hole 可识别的纯域名格式  
- **完全开源**：基于开源规则构建，免费使用  

## 🔧 快速使用（Pi-hole 配置）

### 方法 1：通过 Pi-hole 网页界面添加（推荐）
1. 登录你的 Pi-hole 管理后台（默认地址：`http://你的Pi-holeIP/admin`）  
2. 点击左侧菜单 **Group Management** → **Adlists**  
3. 点击 **Add a new adlist**：  
   - **Address** 填写：`https://raw.githubusercontent.com/PyXMR2025/pi-hole-chinese-list/master/easylist.hosts`  
   - **Comment** 填写（可选）：`Pi-hole Chinese Ad List (Daily Update)`  
4. 点击 **Add** 保存  
5. 刷新 Pi-hole 重力列表（Gravity）：  
   - 网页端：点击左侧 **Tools** → **Gravity** → **Update Gravity**  
   - 终端端：执行 `pihole -g`

### 方法 2：通过终端命令添加
```bash
# 添加列表到 Pi-hole
pihole -a adlist https://raw.githubusercontent.com/PyXMR2025/pi-hole-chinese-list/master/easylist.hosts

# 刷新重力列表
pihole -g
```

## 📅 更新机制

### 自动更新时间
- 每日 **UTC 0:00**（北京时间 UTC+8 → **8:00**）自动执行更新  
- 可在仓库 **Actions** 页面查看更新记录  
- 支持手动触发更新（仓库维护者可通过 Actions 手动运行工作流）

### 数据源
列表基于以下开源规则文件构建（均为官方源）：
- Easylist 主规则：https://easylist.to/easylist/easylist.txt  
- Fanboy 骚扰规则：https://easylist.to/easylist/fanboy-annoyance.txt  
- Fanboy 社交广告规则：https://easylist.to/easylist/fanboy-social.txt  
- Easylist 中国特化规则：https://easylist-downloads.adblockplus.org/easylistchina.txt  
- 恶意域名规则：https://easylist-downloads.adblockplus.org/malwaredomains_full.txt  
- CJX 中文规则：https://raw.githubusercontent.com/cjx82630/cjxlist/master/cjxlist.txt  

### 规则处理逻辑
1. 抓取所有数据源文件并合并  
2. 自动去重（`sort -u`）  
3. 过滤仅保留 AdBlock 格式的域名规则（`||域名^` 格式）  
4. 移除无效字符（`|` / `^`），生成纯域名列表  
5. 输出最终文件 `easylist.hosts` 并推送到仓库  

## ❗ 注意事项
- Pi-hole 需确保能访问 GitHub Raw 地址（若网络受限，可自行克隆仓库后本地使用）  
- 列表仅过滤域名级广告
- 若出现误屏蔽，可在 Pi-hole 后台 **Whitelist** 中添加对应域名  

## 🙏 致谢
- **Easylist**：广告规则 
- **CJX List**：广告规则  
- **Pi-hole**：优秀的 DNS 级广告过滤工具  
- **GitHub Actions**：提供免费的自动更新能力  

## 📄 许可证
本仓库仅做规则整理与格式转换，原始规则遵循各自开源许可证，衍生列表仅供个人非商业使用。