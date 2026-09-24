# 学术主页模板改版设计 (Classic Academic)

日期：2026-09-25
状态：已获用户批准

## 目标

将 https://henry0132.github.io 从当前的单栏顶部布局改为 Classic Academic（Jon Barron 风格）双栏布局，并新增 NeurIPS 2026 论文。URL 保持不变。

## 布局

- 桌面端：两栏。左侧栏约占 30%（内容居中），右侧主栏约占 70%。侧栏在页面滚动时保持固定（`position: sticky`）。
- 移动端（视口 ≤ 768px）：退化为单栏，侧栏内容置顶堆叠。
- 页脚：`Last updated: September 2026`。

## 左侧栏内容

- 照片 `photo.jpg`（圆形裁切，`onerror` 时隐藏）
- 姓名：Hengrui Zhang
- 身份：Ph.D. Student @ China University of Mining and Technology（链接 https://www.cumt.edu.cn/）
- 邮箱：hengruizhang@cumt.edu.cn / hengruizhang0132@gmail.com
- 链接：GitHub (https://github.com/Henry0132)、Google Scholar (https://scholar.google.com.hk/citations?user=PFxa-9YAAAAJ&hl=zh-CN)

## 主栏内容（按顺序）

### 1. About

I am a first-year Ph.D. student at the School of Information and Control Engineering, China University of Mining and Technology (CUMT), born on March 2, 2001. My research focuses on offline reinforcement learning, goal-conditioned reinforcement learning, and generative models. I am advised by Prof. Xuesong Wang.

链接：CUMT (https://www.cumt.edu.cn/)、Prof. Xuesong Wang (https://siee.cumt.edu.cn/info/1012/1025.htm)

### 2. Research Interests

- Offline Reinforcement Learning
- Goal-Conditioned Reinforcement Learning
- Generative Models

### 3. News（新增）

- `[2026] One paper accepted at NeurIPS 2026 as Poster.`（具体的月份待用户确认后填写）

### 4. Publications（6 篇，按此顺序，作者本人加粗）

1. **Diffusion Subgoal Planning for Long-Horizon Offline Goal-Conditioned Reinforcement Learning**（新增）
   - Hengrui Zhang, Yuhu Cheng, C. L. Philip Chen, Xuesong Wang
   - NeurIPS 2026 (Poster)
2. Return-Critic: Bridging Goal Discrepancy for Efficient Visual Reinforcement Learning
   - Ruyi Lu, Xuesong Wang, Hengrui Zhang, Yuhu Cheng
   - ICML 2026
3. PCDT: Pessimistic Critic Decision Transformer for Offline Reinforcement Learning
   - Xuesong Wang, Hengrui Zhang, Jiazhi Zhang, C. L. Philip Chen, Yuhu Cheng
   - IEEE Transactions on Systems, Man, and Cybernetics: Systems, 2025, 55(10): 7247–7258
   - DOI: https://doi.org/10.1109/TSMC.2025.3583392
4. Visual Reinforcement Learning Based on Multiview Optimization Aggregation
   - Xuesong Wang, Ruyi Lu, Hengrui Zhang, Yuhu Cheng
   - IEEE Transactions on Cognitive and Developmental Systems, 2025, 17(4): 1011–1021
   - DOI: https://doi.org/10.1109/TCDS.2025.3540115
5. Diffusion Policy Distillation for Offline Reinforcement Learning
   - Jiazhi Zhang, Yuhu Cheng, C. L. Philip Chen, Hengrui Zhang, Xuesong Wang
   - Neural Networks, 2025, 190: 107694
   - DOI: https://doi.org/10.1016/j.neunet.2025.107694
6. Offline Reinforcement Learning Based on Advantage-Constrained Diffusion Policy
   - Xuesong Wang, Hengrui Zhang, Jiazhi Zhang, Yuhu Cheng
   - Control and Decision, 2025, 40(06): 1903–1912
   - DOI: https://doi.org/10.13195/j.kzyjc.2024.0618

### 5. Education

- Ph.D. in Control Science and Engineering — China University of Mining and Technology, 2025 — Present
- M.Sc. in Control Science and Engineering — China University of Mining and Technology, 2023 — 2025
- B.Sc. in Internet of Things Engineering — Yancheng Institute of Technology (https://www.ycit.edu.cn/en/), 2019 — 2023

### 6. Honors & Awards（按学位分组）

Ph.D.:
- First-Class Entrance Scholarship

M.Sc.:
- Second-Class Entrance Scholarship
- Second-Class Academic Scholarship

B.Sc.:
- National Scholarship
- National Endeavor Scholarship
- Yancheng "Yellow Sea Pearl" Scholarship
- First-Class Academic Scholarship ×8
- National Second Prize, 17th "Challenge Cup"
- National Third Prize, China College Student Computer Design Competition
- National Second Prize, China College Student Computer Design Competition (Preliminary)

## 技术方案

- 纯 HTML + CSS，无 JavaScript 依赖、无构建步骤
- 重写 `index.html` 与 `style.css`，复用现有 `photo.jpg`
- 部署方式：推送到已有仓库 `Henry0132.github.io` 的 `main` 分支，GitHub Pages 自动部署，URL 不变
- 兼容现有 `.gitignore`（含 `.superpowers/`）

## 验收标准

- [ ] 上述全部内容均出现在页面上（不丢失任何原有信息）
- [ ] 桌面端双栏、侧栏 sticky；移动端单栏
- [ ] 所有链接（CUMT、导师、YCIT、GitHub、Scholar、5 个 DOI）可点击且指向正确
- [ ] 推送后 https://henry0132.github.io 正常显示新模板
