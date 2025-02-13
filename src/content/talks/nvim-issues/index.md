---
title: "Nvim 问题及解决方法"
description: "日常遇到过的 Nvim 问题及解决方法"
date: "2025-02-13"
lastUpdateDate: "2025-02-13"
tags:
  - neovim
---

## Neovide 无法通过 `<C-+>`, `<C-_>`, `<C-)>` 快捷键切换缩放比

手动为需要的模式配置快捷键触发相应动作来使 neovide 缩放比可以通过快捷键触发修改

```lua
if vim.g.neovide then
    vim.api.nvim_set_keymap("v", "<sc-c>", '"+y', { noremap = true })
    vim.api.nvim_set_keymap("n", "<sc-v>", 'l"+p', { noremap = true })
    vim.api.nvim_set_keymap("v", "<sc-v>", '"+P', { noremap = true })
    for _, mode in ipairs({ "c", "i" }) do
        vim.api.nvim_set_keymap(mode, "<S-C-V>", "<C-R>+", { noremap = true })
    end
    vim.api.nvim_set_keymap("t", "<sc-v>", '<C-\\><C-n>"+Pi', { noremap = true })

    local function increase_scale()
        vim.g.neovide_scale_factor = vim.g.neovide_scale_factor + 0.1
    end

    local function decrease_scale()
        vim.g.neovide_scale_factor = vim.g.neovide_scale_factor - 0.1
    end

    local function reset_scale()
        vim.g.neovide_scale_factor = 1.0
    end

    for _, mode in ipairs({ "v", "n", "c", "i", "t" }) do
        vim.keymap.set(mode, "<C-+>", increase_scale, { noremap = true })
        vim.keymap.set(mode, "<C-_>", decrease_scale, { noremap = true })
        vim.keymap.set(mode, "<C-)>", reset_scale, { noremap = true })
    end
end
```
