---
title: "开发工具_线框图本地绘制工具"
published: 2026-06-16
pinned: true
description: "AI辅助开发工具"
tags: ["示例", "AI工具"]
category: "开发工具"
author: "AllenW"
draft: false
---

## 线框图本地绘制工具

![图片说明]()

现在的线框图软件有以下几个需要解决的问题：
1.正版软件需要购买；
2.线框软件主要服务于前端的开发，所以很多功能齐全但策划能用到的功能不多，主要是以展示为主；
3.线框软件很多功能需要安装插件或者第三方库，不然没法直接调用；
4.不够轻量，换设备时需要重新下载。
根据以上的问题，用AI工具设计了一个本地的html工具进行线框图设计

```yaml
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Markdown 博客可视化编辑器模板</title>
  <style>
    :root {
      --bg: #f4efe6;
      --panel: #fffaf2;
      --panel-2: #f2e6d7;
      --paper: #fffdf8;
      --ink: #201915;
      --muted: #7b7065;
      --line: #d8c8b6;
      --accent: #6d3f2a;
      --accent-2: #9b6a46;
      --ok: #2e6b46;
      --danger: #9b2e24;
      --radius: 14px;
      --shadow: 0 16px 42px rgba(45, 33, 22, .13);
      font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif;
    }
    * { box-sizing: border-box; }
    body {
      margin: 0;
      color: var(--ink);
      background:
        radial-gradient(circle at 12% 0%, rgba(155,106,70,.18), transparent 26%),
        radial-gradient(circle at 88% 12%, rgba(109,63,42,.10), transparent 24%),
        linear-gradient(180deg, #fbf7ef 0%, var(--bg) 100%);
      min-height: 100vh;
    }
    header.app-header {
      position: sticky;
      top: 0;
      z-index: 20;
      backdrop-filter: blur(14px);
      background: rgba(255,250,242,.9);
      border-bottom: 1px solid var(--line);
    }
    .topbar {
      max-width: 1540px;
      margin: 0 auto;
      padding: 13px 18px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }
    .brand { display: flex; flex-direction: column; gap: 2px; }
    .brand strong { font-size: 18px; letter-spacing: .04em; }
    .brand span { color: var(--muted); font-size: 12px; }
    .actions { display: flex; flex-wrap: wrap; gap: 8px; align-items: center; justify-content: flex-end; }
    button, .file-btn, select, input, textarea {
      font: inherit;
    }
    button, .file-btn {
      border: 1px solid var(--line);
      background: #fffdf8;
      color: var(--ink);
      padding: 8px 11px;
      border-radius: 10px;
      cursor: pointer;
      font-size: 13px;
      line-height: 1;
      transition: transform .08s ease, background .16s ease, border .16s ease;
      user-select: none;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }
    button:hover, .file-btn:hover { background: #f6eadb; border-color: #c5ad96; }
    button:active, .file-btn:active { transform: translateY(1px); }
    button.primary { background: var(--accent); color: #fffaf1; border-color: var(--accent); }
    button.primary:hover { background: #5a3424; }
    button.danger { color: var(--danger); }
    button.ok { color: var(--ok); }
    button.small { padding: 6px 8px; font-size: 12px; border-radius: 8px; }
    input[type="file"] { display: none; }
    .status { min-height: 18px; color: var(--ok); font-size: 12px; margin-left: 4px; }

    main {
      max-width: 1540px;
      margin: 0 auto;
      padding: 18px;
      display: grid;
      grid-template-columns: minmax(440px, 560px) minmax(620px, 1fr);
      gap: 18px;
      align-items: start;
    }
    .column { display: grid; gap: 14px; }
    .card {
      background: var(--panel);
      border: 1px solid var(--line);
      border-radius: var(--radius);
      box-shadow: var(--shadow);
      overflow: hidden;
    }
    .card-head {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      padding: 12px 14px;
      border-bottom: 1px solid var(--line);
      background: #f8efe2;
    }
    .card-head h2, .card-head h3 { margin: 0; font-size: 15px; letter-spacing: .03em; }
    .card-body { padding: 14px; display: grid; gap: 12px; }
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
    .grid-3 { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 10px; }
    .inline-grid { display: grid; grid-template-columns: 140px 1fr; gap: 10px; align-items: start; }
    .inline-grid-3 { display: grid; grid-template-columns: 130px 1fr 1fr; gap: 10px; align-items: start; }
    label { display: grid; gap: 5px; font-size: 12px; color: var(--muted); }
    label.inline { display: inline-flex; align-items: center; gap: 6px; color: var(--ink); }
    input, textarea, select {
      width: 100%;
      border: 1px solid var(--line);
      border-radius: 10px;
      background: #fffdf8;
      color: var(--ink);
      padding: 9px 10px;
      outline: none;
      font-size: 13px;
    }
    input:focus, textarea:focus, select:focus { border-color: var(--accent-2); box-shadow: 0 0 0 3px rgba(155,106,70,.12); }
    textarea { min-height: 92px; resize: vertical; line-height: 1.55; }
    .checkbox-row { display: flex; gap: 14px; flex-wrap: wrap; align-items: center; }
    .toolbar { display: flex; gap: 8px; align-items: center; }
    .toolbar select { min-width: 138px; }
    .dim { color: var(--muted); font-size: 12px; line-height: 1.65; }
    .tip {
      padding: 10px 12px;
      border: 1px dashed var(--line);
      border-radius: 12px;
      background: #fbf4ea;
      color: var(--muted);
      font-size: 12px;
      line-height: 1.65;
    }

    .blocks { display: grid; gap: 12px; }
    .block {
      border: 1px solid var(--line);
      border-radius: 12px;
      background: #fffdf8;
      overflow: hidden;
    }
    .block-title {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      padding: 9px 10px;
      border-bottom: 1px solid var(--line);
      background: #f8efe2;
    }
    .block-title strong { font-size: 13px; }
    .block-actions { display: flex; gap: 6px; flex-wrap: wrap; justify-content: flex-end; }
    .block-fields { padding: 11px; display: grid; gap: 10px; }
    .example-box {
      display: grid;
      gap: 7px;
      background: #fbf4ea;
      border: 1px dashed var(--line);
      border-radius: 12px;
      padding: 10px;
    }
    .example-box code { font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; font-size: 12px; word-break: break-all; }

    .preview-wrap { height: calc(100vh - 112px); min-height: 680px; display: flex; flex-direction: column; }
    .preview-tabs { display: flex; gap: 6px; flex-wrap: wrap; justify-content: flex-end; }
    .preview-tabs button.active { background: var(--accent); color: #fffaf1; border-color: var(--accent); }
    .preview-pane, .md-output {
      overflow: auto;
      flex: 1;
      background: #ede4d8;
      padding: 18px;
    }
    .md-output {
      background: #fffdf8;
      white-space: pre;
      font-size: 13px;
      line-height: 1.5;
      font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, "Liberation Mono", monospace;
    }
    .hidden { display: none !important; }

    /* 模拟网页预览 */
    .mock-browser {
      max-width: 980px;
      margin: 0 auto;
      background: #fffdf8;
      border: 1px solid #d1c2b1;
      border-radius: 18px;
      overflow: hidden;
      box-shadow: 0 18px 58px rgba(24,18,14,.16);
    }
    .browser-bar {
      height: 42px;
      background: #efe4d6;
      border-bottom: 1px solid var(--line);
      display: flex;
      align-items: center;
      gap: 9px;
      padding: 0 14px;
    }
    .dot { width: 11px; height: 11px; border-radius: 50%; background: #b89b82; opacity: .8; }
    .urlbar { flex: 1; height: 24px; border-radius: 99px; background: #fffaf2; border: 1px solid #dac8b7; color: var(--muted); font-size: 12px; display: flex; align-items: center; padding: 0 12px; overflow: hidden; }
    .site-shell { background: #fffdf8; color: #2a211c; }
    .site-nav {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      align-items: center;
      padding: 18px 28px;
      border-bottom: 1px solid #eadfd2;
      background: rgba(255,253,248,.96);
    }
    .site-logo { font-weight: 800; letter-spacing: .08em; }
    .site-menu { display: flex; gap: 14px; color: #7c6f63; font-size: 13px; }
    .article-hero {
      padding: 42px 32px 30px;
      background:
        linear-gradient(135deg, rgba(109,63,42,.12), rgba(255,253,248,.2)),
        radial-gradient(circle at 82% 20%, rgba(155,106,70,.14), transparent 32%);
      border-bottom: 1px solid #eadfd2;
    }
    .hero-inner { max-width: 780px; margin: 0 auto; }
    .category-pill { display: inline-flex; padding: 5px 10px; border-radius: 99px; border: 1px solid #d8c8b6; color: #6d3f2a; font-size: 12px; background: #fffaf2; }
    .article-hero h1 { margin: 14px 0 10px; font-size: clamp(30px, 5vw, 48px); line-height: 1.12; letter-spacing: -.03em; }
    .article-desc { color: #74675c; line-height: 1.8; margin: 0 0 14px; font-size: 15px; }
    .article-meta { color: #8a7d72; font-size: 12px; display: flex; flex-wrap: wrap; gap: 8px 14px; }
    .cover-image { width: 100%; margin-top: 20px; border-radius: 16px; border: 1px solid #d9caba; display: block; max-height: 360px; object-fit: cover; }
    .article-layout { display: grid; grid-template-columns: 210px minmax(0, 1fr); gap: 24px; max-width: 920px; margin: 0 auto; padding: 28px 28px 54px; }
    .toc-card {
      position: sticky;
      top: 80px;
      align-self: start;
      border: 1px solid #eadfd2;
      border-radius: 14px;
      background: #fffaf2;
      padding: 14px;
      font-size: 13px;
      color: #75685e;
      max-height: 70vh;
      overflow: auto;
    }
    .toc-card strong { color: #342720; display: block; margin-bottom: 8px; }
    .toc-card a { display: block; color: #75685e; text-decoration: none; padding: 5px 0; border-bottom: 1px dashed rgba(216,200,182,.75); }
    .toc-card a:hover { color: var(--accent); }
    .blog-article { min-width: 0; }
    .blog-article h1, .blog-article h2, .blog-article h3, .blog-article h4 { line-height: 1.28; margin: 1.28em 0 .62em; }
    .blog-article h1 { font-size: 2.05rem; border-bottom: 2px solid #e4d7ca; padding-bottom: .35em; }
    .blog-article h2 { font-size: 1.55rem; border-left: 5px solid #9b6a46; padding-left: .6em; }
    .blog-article h3 { font-size: 1.24rem; }
    .blog-article p, .blog-article li, .blog-article blockquote { line-height: 1.88; }
    .blog-article p { margin: 1em 0; }
    .blog-article a { color: #6d3f2a; }
    .blog-article img { max-width: 100%; border-radius: 14px; border: 1px solid #e0d2c4; display: block; margin: 16px auto; }
    .blog-article blockquote { margin: 16px 0; padding: 10px 16px; border-left: 4px solid #9b6a46; background: #fbf4ea; color: #463a31; }
    .blog-article code { background: #f1e6d8; border: 1px solid #e3d3c0; border-radius: 5px; padding: 1px 5px; font-size: .92em; }
    .blog-article pre { background: #201915; color: #fff4e8; border-radius: 14px; padding: 16px; overflow: auto; }
    .blog-article pre code { background: transparent; border: 0; color: inherit; padding: 0; }
    .blog-article table { border-collapse: collapse; width: 100%; margin: 16px 0; overflow: hidden; border-radius: 10px; }
    .blog-article th, .blog-article td { border: 1px solid #d8c8b6; padding: 9px 11px; }
    .blog-article th { background: #f4e8d8; }
    .blog-article hr { border: 0; border-top: 1px solid #dfd1c3; margin: 28px 0; }
    .blog-article iframe, .blog-article video { width: 100%; max-width: 100%; border: 1px solid #d8c8b6; border-radius: 14px; background: #000; display: block; margin: 16px 0; aspect-ratio: 16 / 9; }
    .frontmatter-box { max-width: 900px; margin: 0 auto 16px; color: var(--muted); border: 1px dashed var(--line); border-radius: 12px; padding: 12px; background: #fbf4ea; white-space: pre-wrap; font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; }

    .modal { position: fixed; inset: 0; background: rgba(31,26,23,.45); display: none; z-index: 60; align-items: center; justify-content: center; padding: 16px; }
    .modal.show { display: flex; }
    .modal-panel { width: min(820px, 100%); max-height: 88vh; overflow: auto; background: var(--panel); border-radius: 16px; border: 1px solid var(--line); box-shadow: 0 20px 70px rgba(0,0,0,.22); }
    .modal-panel .card-head { position: sticky; top: 0; z-index: 1; }
    .help-list { margin: 0; padding-left: 20px; line-height: 1.85; }

    @media (max-width: 1100px) {
      main { grid-template-columns: 1fr; }
      .preview-wrap { height: auto; min-height: 620px; }
      .grid-2, .grid-3, .inline-grid, .inline-grid-3 { grid-template-columns: 1fr; }
    }
    @media (max-width: 760px) {
      .topbar { align-items: flex-start; flex-direction: column; }
      main { padding: 12px; }
      .article-layout { grid-template-columns: 1fr; padding: 20px; }
      .toc-card { position: static; }
      .site-menu { display: none; }
      .article-hero { padding: 28px 20px 22px; }
    }
  </style>
</head>
<body>
  <header class="app-header">
    <div class="topbar">
      <div class="brand">
        <strong>Markdown 博客可视化编辑器</strong>
        <span>填写表单 → 实时模拟网页预览 → 导出 .md，可直接粘贴 iframe 视频代码</span>
      </div>
      <div class="actions">
        <label class="file-btn" for="importMd">导入 .md</label>
        <input id="importMd" type="file" accept=".md,.markdown,text/markdown,text/plain" />
        <button id="btnSave" class="ok">保存草稿</button>
        <button id="btnExample">载入视频示例</button>
        <button id="btnCopy">复制 Markdown</button>
        <button id="btnExportHtml">导出预览 HTML</button>
        <button id="btnExport" class="primary">导出 .md</button>
        <button id="btnHelp">规则</button>
        <button id="btnClear" class="danger">清空</button>
        <span id="status" class="status"></span>
      </div>
    </div>
  </header>

  <main>
    <section class="column">
      <div class="card">
        <div class="card-head"><h2>文章元信息</h2></div>
        <div class="card-body">
          <div class="grid-2">
            <label>标题 title<input id="title" data-meta="title" placeholder="文章标题" /></label>
            <label>发布时间 published<input id="published" data-meta="published" type="date" /></label>
          </div>
          <label>描述 description<textarea id="description" data-meta="description" placeholder="文章摘要，会显示在模拟网页预览的标题下方"></textarea></label>
          <div class="grid-2">
            <label>标签 tags，英文逗号分隔<input id="tags" data-meta="tags" placeholder="示例, 视频, Firefly" /></label>
            <label>分类 category<input id="category" data-meta="category" placeholder="文章示例" /></label>
          </div>
          <div class="grid-2">
            <label>作者 author<input id="author" data-meta="author" placeholder="作者名，可空" /></label>
            <label>授权 licenseName<input id="licenseName" data-meta="licenseName" placeholder="未授权，可空" /></label>
          </div>
          <div class="grid-2">
            <label>来源 sourceLink<input id="sourceLink" data-meta="sourceLink" placeholder="https://...，可空" /></label>
            <label>封面图 cover，可空<input id="cover" data-meta="cover" placeholder="https://... 或 /images/cover.webp" /></label>
          </div>
          <div class="checkbox-row">
            <label class="inline"><input id="pinned" data-meta="pinned" type="checkbox" /> 置顶 pinned</label>
            <label class="inline"><input id="draft" data-meta="draft" type="checkbox" /> 草稿 draft</label>
            <label class="inline"><input id="toc" type="checkbox" checked /> 预览中显示目录</label>
          </div>
          <div class="tip">导出的文件会保持博客常见的 <code>---</code> Front Matter。视频模块可以选择 YouTube、Bilibili、HTML5 video，也可以直接粘贴平台给出的完整 <code>&lt;iframe&gt;</code> 代码。</div>
        </div>
      </div>

      <div class="card">
        <div class="card-head">
          <h2>正文模块</h2>
          <div class="toolbar">
            <select id="blockType">
              <option value="heading">标题</option>
              <option value="paragraph">段落</option>
              <option value="quote">引用</option>
              <option value="ul">无序列表</option>
              <option value="ol">有序列表</option>
              <option value="image">图片</option>
              <option value="video">视频</option>
              <option value="link">链接</option>
              <option value="table">表格</option>
              <option value="code">代码块</option>
              <option value="hr">分割线</option>
              <option value="raw">原始 Markdown/HTML</option>
            </select>
            <button id="btnAddBlock" class="primary">添加模块</button>
          </div>
        </div>
        <div class="card-body">
          <div id="blocks" class="blocks"></div>
        </div>
      </div>
    </section>

    <section class="column">
      <div class="card preview-wrap">
        <div class="card-head">
          <h2>实时结果</h2>
          <div class="preview-tabs">
            <button id="tabPage" class="active">网页模拟预览</button>
            <button id="tabArticle">正文预览</button>
            <button id="tabMarkdown">Markdown 源码</button>
          </div>
        </div>
        <div id="pagePreview" class="preview-pane"></div>
        <div id="articlePreview" class="preview-pane hidden"></div>
        <pre id="mdOutput" class="md-output hidden"></pre>
      </div>
    </section>
  </main>

  <div id="helpModal" class="modal" role="dialog" aria-modal="true">
    <div class="modal-panel">
      <div class="card-head">
        <h3>编辑器导出规则</h3>
        <button id="btnCloseHelp">关闭</button>
      </div>
      <div class="card-body">
        <p class="dim">本模板默认适配 Markdown/GFM 博客。视频不是 Markdown 原生能力，因此按你给出的方式导出为 HTML iframe 或 video 标签。</p>
        <ul class="help-list">
          <li>元信息会导出到文件最前方的 <code>---</code> 包裹区域。</li>
          <li>标题使用 <code>#</code> 到 <code>######</code> 的 atx 写法。</li>
          <li>图片使用 <code>![替代文本](URL "标题")</code>。本地图片可转 Base64，但正式发布更建议使用图床/CDN/相对路径。</li>
          <li>视频：粘贴完整 iframe 时会原样导出；YouTube/Bilibili 模式会自动生成 iframe。</li>
          <li>Bilibili 的 <code>//player.bilibili.com</code> 在本地 file:// 预览里可能不稳定，因此自动生成模式默认导出 <code>https://player.bilibili.com</code>。</li>
          <li>原始模块适合粘贴复杂 Markdown、锚点、HTML、第三方嵌入代码。</li>
          <li>导入 .md 时会解析 Front Matter，正文作为一个“原始 Markdown/HTML”模块导入，避免破坏原文。</li>
        </ul>
      </div>
    </div>
  </div>

<script>
(() => {
  const $ = (sel, root = document) => root.querySelector(sel);
  const $$ = (sel, root = document) => Array.from(root.querySelectorAll(sel));
  const STORAGE_KEY = 'markdown_blog_editor_template_v2';

  const labels = {
    heading: '标题', paragraph: '段落', quote: '引用', ul: '无序列表', ol: '有序列表', image: '图片',
    video: '视频', link: '链接', table: '表格', code: '代码块', hr: '分割线', raw: '原始 Markdown/HTML'
  };

  const defaultMeta = () => ({
    title: '在文章中嵌入视频',
    published: '1970-01-01',
    pinned: false,
    description: '这篇文章演示如何在博客文章中嵌入视频。',
    tags: '示例, 视频, Firefly',
    category: '文章示例',
    licenseName: '',
    author: '',
    sourceLink: '',
    cover: '',
    draft: false
  });

  const state = { meta: defaultMeta(), toc: true, blocks: [] };

  function uid() { return 'b' + Math.random().toString(36).slice(2, 9); }
  function escapeHtml(s = '') {
    return String(s).replace(/[&<>"]/g, m => ({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;'}[m]));
  }
  function escapeAttr(s = '') { return escapeHtml(s).replace(/'/g, '&#39;'); }
  function escapeYamlString(s = '') {
    const v = String(s ?? '').replace(/\\/g, '\\\\').replace(/"/g, '\\"');
    return `"${v}"`;
  }
  function showStatus(text, ms = 1800) {
    $('#status').textContent = text;
    if (ms) setTimeout(() => { if ($('#status').textContent === text) $('#status').textContent = ''; }, ms);
  }
  function slugify(text = '') {
    const s = String(text).trim().toLowerCase().replace(/[\s_]+/g, '-').replace(/[^a-z0-9\-\u4e00-\u9fa5]/g, '').replace(/-+/g, '-');
    return s || 'section';
  }

  function defaultBlock(type) {
    const base = { id: uid(), type };
    switch (type) {
      case 'heading': return { ...base, level: 2, text: '新的标题', anchor: '' };
      case 'paragraph': return { ...base, text: '这里填写正文段落。' };
      case 'quote': return { ...base, text: '这里填写引用内容。' };
      case 'ul': return { ...base, items: '第一项\n第二项\n第三项' };
      case 'ol': return { ...base, items: '第一步\n第二步\n第三步' };
      case 'image': return { ...base, alt: '图片说明', url: '', title: '' };
      case 'video': return { ...base, provider: 'embed', source: '', title: '视频', width: '100%', height: '468', page: 1, autoplay: false, poster: '' };
      case 'link': return { ...base, text: '链接文本', url: 'https://example.com', title: '' };
      case 'table': return { ...base, headers: '项目,说明,状态', align: 'left,left,center', rows: '标题,使用 # 到 ######,可用\n图片,使用 Markdown 图片语法,可用' };
      case 'code': return { ...base, lang: 'yaml', code: '---\ntitle: 示例文章\npublished: 2023-10-19\n---' };
      case 'hr': return { ...base };
      case 'raw': return { ...base, text: '<!-- 这里可以粘贴原始 Markdown 或 HTML -->' };
      default: return { ...base, text: '' };
    }
  }

  function hydrateMetaInputs() {
    Object.keys(state.meta).forEach(k => {
      const el = $(`[data-meta="${k}"]`);
      if (!el) return;
      if (el.type === 'checkbox') el.checked = Boolean(state.meta[k]);
      else el.value = state.meta[k] ?? '';
    });
    $('#toc').checked = state.toc !== false;
  }

  function readMetaInputs() {
    $$('[data-meta]').forEach(el => {
      state.meta[el.dataset.meta] = el.type === 'checkbox' ? el.checked : el.value;
    });
    state.toc = $('#toc').checked;
  }

  function renderBlocks() {
    const root = $('#blocks');
    root.innerHTML = '';
    state.blocks.forEach((block, index) => root.appendChild(renderBlock(block, index)));
  }

  function renderBlock(block, index) {
    const el = document.createElement('div');
    el.className = 'block';
    el.dataset.id = block.id;
    el.innerHTML = `
      <div class="block-title">
        <strong>${index + 1}. ${labels[block.type] || block.type}</strong>
        <div class="block-actions">
          <button class="small" data-act="up">上移</button>
          <button class="small" data-act="down">下移</button>
          <button class="small" data-act="dup">复制</button>
          <button class="small danger" data-act="del">删除</button>
        </div>
      </div>
      <div class="block-fields">${fieldsHtml(block)}</div>
    `;
    el.addEventListener('input', e => updateBlockFromField(block.id, e.target));
    el.addEventListener('change', async e => {
      if (e.target.type === 'file' && e.target.files && e.target.files[0]) {
        const target = state.blocks.find(b => b.id === block.id);
        if (target && target.type === 'image') {
          target.url = await fileToDataUrl(e.target.files[0]);
          renderBlocks();
          updateOutput();
          showStatus('本地图片已写入 URL 字段');
        }
      } else {
        updateBlockFromField(block.id, e.target);
        if (block.type === 'video') renderBlocks();
      }
    });
    el.addEventListener('click', e => {
      const act = e.target.dataset.act;
      if (!act) return;
      const i = state.blocks.findIndex(b => b.id === block.id);
      if (i < 0) return;
      if (act === 'up' && i > 0) [state.blocks[i - 1], state.blocks[i]] = [state.blocks[i], state.blocks[i - 1]];
      if (act === 'down' && i < state.blocks.length - 1) [state.blocks[i + 1], state.blocks[i]] = [state.blocks[i], state.blocks[i + 1]];
      if (act === 'dup') state.blocks.splice(i + 1, 0, { ...JSON.parse(JSON.stringify(state.blocks[i])), id: uid() });
      if (act === 'del') state.blocks.splice(i, 1);
      renderBlocks();
      updateOutput();
    });
    return el;
  }

  function fieldsHtml(b) {
    switch (b.type) {
      case 'heading': return `
        <div class="inline-grid-3">
          <label>级别
            <select data-field="level">
              ${[1,2,3,4,5,6].map(n => `<option value="${n}" ${Number(b.level)===n?'selected':''}>H${n}</option>`).join('')}
            </select>
          </label>
          <label>标题文本<input data-field="text" value="${escapeAttr(b.text)}" /></label>
          <label>锚点 id，可空<input data-field="anchor" value="${escapeAttr(b.anchor)}" placeholder="不填则按标题自动生成" /></label>
        </div>`;
      case 'paragraph': return `<label>段落内容<textarea data-field="text">${escapeHtml(b.text)}</textarea></label>`;
      case 'quote': return `<label>引用内容<textarea data-field="text">${escapeHtml(b.text)}</textarea></label>`;
      case 'ul': return `<label>列表项：一行一项<textarea data-field="items">${escapeHtml(b.items)}</textarea></label>`;
      case 'ol': return `<label>列表项：一行一项<textarea data-field="items">${escapeHtml(b.items)}</textarea></label>`;
      case 'image': return `
        <div class="inline-grid-3">
          <label>替代文本 alt<input data-field="alt" value="${escapeAttr(b.alt)}" /></label>
          <label>图片 URL/路径<input data-field="url" value="${escapeAttr(b.url)}" placeholder="https://... 或 /images/a.webp" /></label>
          <label>可选标题 title<input data-field="title" value="${escapeAttr(b.title)}" /></label>
        </div>
        <div class="inline-grid">
          <label>导入本地图片<input data-field="localImage" type="file" accept="image/*" /></label>
          <p class="dim">本地图片会转成 Base64 写入 Markdown。正式发布更建议先上传到图床/CDN，再填写 URL。</p>
        </div>`;
      case 'video': return videoFieldsHtml(b);
      case 'link': return `
        <div class="inline-grid-3">
          <label>文本<input data-field="text" value="${escapeAttr(b.text)}" /></label>
          <label>URL<input data-field="url" value="${escapeAttr(b.url)}" /></label>
          <label>可选标题<input data-field="title" value="${escapeAttr(b.title)}" /></label>
        </div>`;
      case 'table': return `
        <label>表头：用英文逗号分隔<input data-field="headers" value="${escapeAttr(b.headers)}" /></label>
        <label>对齐：left, center, right，对应每列<input data-field="align" value="${escapeAttr(b.align)}" /></label>
        <label>数据行：每行一行，列用英文逗号分隔<textarea data-field="rows">${escapeHtml(b.rows)}</textarea></label>`;
      case 'code': return `
        <label>语言标识，可空<input data-field="lang" value="${escapeAttr(b.lang)}" placeholder="yaml / javascript / python ..." /></label>
        <label>代码<textarea data-field="code" style="min-height:160px">${escapeHtml(b.code)}</textarea></label>`;
      case 'hr': return `<p class="dim">该模块会导出为一条 Markdown 分割线：<code>---</code></p>`;
      case 'raw': return `<label>原始 Markdown/HTML<textarea data-field="text" style="min-height:220px">${escapeHtml(b.text)}</textarea></label>`;
      default: return `<label>内容<textarea data-field="text">${escapeHtml(b.text || '')}</textarea></label>`;
    }
  }

  function videoFieldsHtml(b) {
    const provider = b.provider || (b.mode === 'video' ? 'video' : 'embed');
    const sourceLabel = provider === 'embed' ? '完整 iframe / video 嵌入代码' : provider === 'youtube' ? 'YouTube 链接 / embed 链接 / 视频 ID' : provider === 'bilibili' ? 'Bilibili 链接 / iframe src / BV 号' : '视频文件 URL';
    const placeholder = provider === 'embed'
      ? '<iframe width="100%" height="468" src="https://www.youtube.com/embed/..." allowfullscreen></iframe>'
      : provider === 'youtube'
        ? 'https://www.youtube.com/watch?v=5gIf0_xpFPI 或 5gIf0_xpFPI'
        : provider === 'bilibili'
          ? 'BV1fK4y1s7Qf 或 https://www.bilibili.com/video/BV1fK4y1s7Qf/'
          : 'https://example.com/video.mp4';
    return `
      <div class="inline-grid-3">
        <label>视频来源
          <select data-field="provider">
            <option value="embed" ${provider==='embed'?'selected':''}>粘贴 iframe 代码</option>
            <option value="youtube" ${provider==='youtube'?'selected':''}>YouTube</option>
            <option value="bilibili" ${provider==='bilibili'?'selected':''}>Bilibili</option>
            <option value="video" ${provider==='video'?'selected':''}>HTML5 video</option>
          </select>
        </label>
        <label>标题 title<input data-field="title" value="${escapeAttr(b.title)}" /></label>
        <label>高度 height<input data-field="height" value="${escapeAttr(b.height || '468')}" /></label>
      </div>
      <label>${sourceLabel}<textarea data-field="source" style="min-height:120px" placeholder='${escapeAttr(placeholder)}'>${escapeHtml(b.source || b.embedCode || b.url || '')}</textarea></label>
      <div class="inline-grid-3">
        <label>宽度 width<input data-field="width" value="${escapeAttr(b.width || '100%')}" /></label>
        <label>Bilibili 分 P<input data-field="page" value="${escapeAttr(b.page || 1)}" /></label>
        <label>video 封面 poster<input data-field="poster" value="${escapeAttr(b.poster || '')}" /></label>
      </div>
      <div class="checkbox-row">
        <label class="inline"><input data-field="autoplay" type="checkbox" ${b.autoplay ? 'checked' : ''} /> 自动播放 autoplay，默认关闭</label>
      </div>
      <div class="example-box">
        <span class="dim">可直接粘贴你给出的代码，例如：</span>
        <code>&lt;iframe width="100%" height="468" src="https://www.youtube.com/embed/5gIf0_xpFPI?si=N1WTorLKL0uwLsU_" title="YouTube video player" frameborder="0" allowfullscreen&gt;&lt;/iframe&gt;</code>
        <code>&lt;iframe width="100%" height="468" src="//player.bilibili.com/player.html?bvid=BV1fK4y1s7Qf&amp;p=1&amp;autoplay=0" allowfullscreen="true"&gt;&lt;/iframe&gt;</code>
      </div>`;
  }

  function updateBlockFromField(id, el) {
    if (!el.dataset.field || el.type === 'file') return;
    const block = state.blocks.find(b => b.id === id);
    if (!block) return;
    let val = el.type === 'checkbox' ? el.checked : el.value;
    if (el.dataset.field === 'level') val = Number(val);
    if (el.dataset.field === 'page') val = Number(val) || 1;
    block[el.dataset.field] = val;
    updateOutput();
  }

  function frontMatter() {
    readMetaInputs();
    const tags = state.meta.tags ? state.meta.tags.split(',').map(t => t.trim()).filter(Boolean) : [];
    const lines = [
      '---',
      `title: ${escapeYamlString(state.meta.title)}`,
      `published: ${state.meta.published || new Date().toISOString().slice(0, 10)}`,
      `pinned: ${Boolean(state.meta.pinned)}`,
      `description: ${escapeYamlString(state.meta.description)}`,
      `tags: [${tags.map(escapeYamlString).join(', ')}]`,
      `category: ${escapeYamlString(state.meta.category)}`
    ];
    if (state.meta.licenseName) lines.push(`licenseName: ${escapeYamlString(state.meta.licenseName)}`);
    if (state.meta.author) lines.push(`author: ${escapeYamlString(state.meta.author)}`);
    if (state.meta.sourceLink) lines.push(`sourceLink: ${escapeYamlString(state.meta.sourceLink)}`);
    if (state.meta.cover) lines.push(`cover: ${escapeYamlString(state.meta.cover)}`);
    lines.push(`draft: ${Boolean(state.meta.draft)}`, '---');
    return lines.join('\n');
  }

  function tableAlignCell(v) {
    const x = String(v || '').trim().toLowerCase();
    if (x === 'center') return ':---:';
    if (x === 'right') return '---:';
    return ':---';
  }
  function cellList(s = '') { return String(s).split(',').map(x => x.trim()); }

  function blockToMd(b) {
    switch (b.type) {
      case 'heading': {
        const level = Math.min(6, Math.max(1, Number(b.level) || 2));
        const text = b.text || '未命名标题';
        const anchor = (b.anchor || '').trim();
        return `${anchor ? `<a id="${anchor.replace(/"/g, '')}"></a>\n` : ''}${'#'.repeat(level)} ${text}`;
      }
      case 'paragraph': return b.text || '';
      case 'quote': return String(b.text || '').split('\n').map(line => `> ${line}`).join('\n');
      case 'ul': return String(b.items || '').split('\n').filter(Boolean).map(x => `- ${x.trim()}`).join('\n');
      case 'ol': return String(b.items || '').split('\n').filter(Boolean).map((x, i) => `${i + 1}. ${x.trim()}`).join('\n');
      case 'image': {
        const alt = (b.alt || 'image').replace(/\]/g, '\\]');
        const url = b.url || '';
        const title = b.title ? ` "${String(b.title).replace(/"/g, '\\"')}"` : '';
        return `![${alt}](${url}${title})`;
      }
      case 'video': return videoToMd(b);
      case 'link': {
        const title = b.title ? ` "${String(b.title).replace(/"/g, '\\"')}"` : '';
        return `[${b.text || b.url || 'link'}](${b.url || '#'}${title})`;
      }
      case 'table': {
        const headers = cellList(b.headers || '列一,列二');
        const aligns = cellList(b.align || '').map(tableAlignCell);
        const splitRows = String(b.rows || '').split('\n').filter(Boolean).map(cellList);
        const sep = headers.map((_, i) => aligns[i] || ':---');
        const rows = splitRows.map(row => `| ${headers.map((_, i) => row[i] || '').join(' | ')} |`);
        return [`| ${headers.join(' | ')} |`, `| ${sep.join(' | ')} |`, ...rows].join('\n');
      }
      case 'code': return '```' + (b.lang || '') + '\n' + (b.code || '') + '\n```';
      case 'hr': return '---';
      case 'raw': return b.text || '';
      default: return b.text || '';
    }
  }

  function extractYoutubeId(input = '') {
    const s = String(input).trim();
    if (!s) return '';
    let m = s.match(/(?:youtube\.com\/(?:watch\?v=|embed\/|shorts\/)|youtu\.be\/)([A-Za-z0-9_-]{6,})/);
    if (m) return m[1];
    m = s.match(/^[A-Za-z0-9_-]{6,}$/);
    return m ? m[0] : '';
  }
  function extractYoutubeQuery(input = '') {
    const s = String(input).trim();
    const q = s.match(/[?&](si=[^&\s"']+)/);
    return q ? `?${q[1]}` : '';
  }
  function extractBvid(input = '') {
    const s = String(input).trim();
    let m = s.match(/(BV[0-9A-Za-z]+)/);
    return m ? m[1] : s;
  }
  function iframe(src, title, width, height, extra = '') {
    return `<iframe width="${escapeAttr(width || '100%')}" height="${escapeAttr(height || '468')}" src="${escapeAttr(src)}" title="${escapeAttr(title || 'video')}" frameborder="0" ${extra}allowfullscreen></iframe>`;
  }
  function videoToMd(b) {
    const provider = b.provider || (b.mode === 'video' ? 'video' : 'embed');
    const source = String(b.source || b.embedCode || b.url || '').trim();
    const title = b.title || (provider === 'bilibili' ? 'Bilibili video player' : provider === 'youtube' ? 'YouTube video player' : 'video');
    const width = b.width || '100%';
    const height = b.height || '468';
    if (provider === 'embed') {
      if (/^<\s*(iframe|video)\b/i.test(source)) return source;
      if (!source) return '';
      return iframe(source, title, width, height);
    }
    if (provider === 'youtube') {
      const id = extractYoutubeId(source);
      if (!id) return '<!-- YouTube 视频地址无效：请填写 URL、embed URL 或视频 ID -->';
      const src = `https://www.youtube.com/embed/${id}${extractYoutubeQuery(source)}`;
      return iframe(src, title, width, height, 'allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" ');
    }
    if (provider === 'bilibili') {
      const bvid = extractBvid(source);
      if (!bvid) return '<!-- Bilibili 视频地址无效：请填写 BV 号或视频链接 -->';
      const page = Number(b.page) || 1;
      const autoplay = b.autoplay ? 1 : 0;
      const src = `https://player.bilibili.com/player.html?bvid=${encodeURIComponent(bvid)}&p=${page}&autoplay=${autoplay}`;
      return `<iframe width="${escapeAttr(width)}" height="${escapeAttr(height)}" src="${src}" title="${escapeAttr(title || 'Bilibili video player')}" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>`;
    }
    if (provider === 'video') {
      const poster = b.poster ? ` poster="${escapeAttr(b.poster)}"` : '';
      return `<video controls width="${escapeAttr(width)}"${poster}>\n  <source src="${escapeAttr(source)}">\n  你的浏览器不支持 video 标签。\n</video>`;
    }
    return source;
  }

  function contentMd() { return state.blocks.map(blockToMd).filter(x => String(x).trim()).join('\n\n'); }
  function buildMd() { return `${frontMatter()}\n\n${contentMd()}\n`; }

  function inlineMdToHtml(text = '') {
    let s = escapeHtml(text);
    s = s.replace(/`([^`]+)`/g, '<code>$1</code>');
    s = s.replace(/!\[([^\]]*)\]\(([^\s)]+)(?:\s+"([^"]*)")?\)/g, '<img src="$2" alt="$1" title="$3">');
    s = s.replace(/\[([^\]]+)\]\(([^\s)]+)(?:\s+"([^"]*)")?\)/g, '<a href="$2" title="$3" target="_blank" rel="noreferrer">$1</a>');
    s = s.replace(/~~(.+?)~~/g, '<del>$1</del>');
    s = s.replace(/\*\*(.+?)\*\*/g, '<strong>$1</strong>');
    s = s.replace(/__(.+?)__/g, '<strong>$1</strong>');
    s = s.replace(/(^|[^*])\*([^*]+)\*/g, '$1<em>$2</em>');
    s = s.replace(/(^|[^_])_([^_]+)_/g, '$1<em>$2</em>');
    s = s.replace(/&lt;(https?:\/\/[^&]+)&gt;/g, '<a href="$1" target="_blank" rel="noreferrer">$1</a>');
    return s;
  }

  function isTableStart(lines, i) {
    return i + 1 < lines.length && /\|/.test(lines[i]) && /^\s*\|?\s*:?-{3,}:?\s*(\|\s*:?-{3,}:?\s*)+\|?\s*$/.test(lines[i + 1]);
  }
  function parseTable(lines, i) {
    const rows = [];
    while (i < lines.length && lines[i].trim() && /\|/.test(lines[i])) rows.push(lines[i++]);
    const split = row => row.trim().replace(/^\|/, '').replace(/\|$/, '').split('|').map(x => x.trim());
    const head = split(rows[0]);
    const body = rows.slice(2).map(split);
    return { next: i, html: `<table><thead><tr>${head.map(h => `<th>${inlineMdToHtml(h)}</th>`).join('')}</tr></thead><tbody>${body.map(r => `<tr>${head.map((_, j) => `<td>${inlineMdToHtml(r[j] || '')}</td>`).join('')}</tr>`).join('')}</tbody></table>` };
  }
  function htmlBlockInfo(line = '') {
    const t = line.trim();
    const m = t.match(/^<\s*(iframe|video|table|div|section|article|figure|figcaption|details|summary|blockquote|ul|ol|li|h[1-6]|p|a|img|br|hr|span)\b/i);
    if (!m) return null;
    const tag = m[1].toLowerCase();
    if (['iframe','img','br','hr','a','span','h1','h2','h3','h4','h5','h6','p'].includes(tag)) return { tag, single: true };
    return { tag, single: false };
  }
  function normalizePreviewHtml(html) {
    return String(html || '').replace(/src=(['"])\/\//g, 'src=$1https://');
  }
  function markdownToHtml(md) {
    const lines = String(md || '').replace(/\r\n/g, '\n').split('\n');
    const html = [];
    let i = 0, inCode = false, codeLang = '', codeLines = [];
    const flushCode = () => {
      html.push(`<pre><code class="language-${escapeAttr(codeLang)}">${escapeHtml(codeLines.join('\n'))}</code></pre>`);
      inCode = false; codeLang = ''; codeLines = [];
    };
    while (i < lines.length) {
      const line = lines[i];
      const trim = line.trim();
      if (inCode) {
        if (/^```/.test(trim)) { flushCode(); i++; continue; }
        codeLines.push(line); i++; continue;
      }
      if (!trim) { i++; continue; }
      if (/^```/.test(trim)) { inCode = true; codeLang = trim.replace(/^```/, '').trim(); i++; continue; }
      if (/^---+$/.test(trim) || /^\*\*\*+$/.test(trim) || /^___+$/.test(trim)) { html.push('<hr>'); i++; continue; }
      const rawInfo = htmlBlockInfo(line);
      if (rawInfo) {
        const raw = [line];
        i++;
        if (!rawInfo.single) {
          const endRe = new RegExp(`<\\/\\s*${rawInfo.tag}\\s*>`, 'i');
          while (i < lines.length && !endRe.test(lines[i - 1])) raw.push(lines[i++]);
        }
        html.push(normalizePreviewHtml(raw.join('\n')));
        continue;
      }
      let m = line.match(/^(#{1,6})\s+(.+)$/);
      if (m) {
        const level = m[1].length;
        const text = m[2].replace(/\s+#+\s*$/, '').trim();
        const id = slugify(text);
        html.push(`<h${level} id="${id}">${inlineMdToHtml(text)}</h${level}>`);
        i++; continue;
      }
      if (isTableStart(lines, i)) {
        const t = parseTable(lines, i);
        html.push(t.html); i = t.next; continue;
      }
      if (/^>\s?/.test(line)) {
        const items = [];
        while (i < lines.length && /^>\s?/.test(lines[i])) items.push(lines[i++].replace(/^>\s?/, ''));
        html.push(`<blockquote>${markdownToHtml(items.join('\n'))}</blockquote>`);
        continue;
      }
      if (/^[-*+]\s+/.test(line)) {
        const items = [];
        while (i < lines.length && /^[-*+]\s+/.test(lines[i])) items.push(lines[i++].replace(/^[-*+]\s+/, ''));
        html.push(`<ul>${items.map(x => `<li>${inlineMdToHtml(x)}</li>`).join('')}</ul>`);
        continue;
      }
      if (/^\d+\.\s+/.test(line)) {
        const items = [];
        while (i < lines.length && /^\d+\.\s+/.test(lines[i])) items.push(lines[i++].replace(/^\d+\.\s+/, ''));
        html.push(`<ol>${items.map(x => `<li>${inlineMdToHtml(x)}</li>`).join('')}</ol>`);
        continue;
      }
      if (/^!\[[^\]]*\]\(/.test(trim)) { html.push(inlineMdToHtml(trim)); i++; continue; }
      const p = [];
      while (i < lines.length && lines[i].trim() && !/^```/.test(lines[i].trim()) && !/^(#{1,6})\s+/.test(lines[i]) && !/^[-*+]\s+/.test(lines[i]) && !/^\d+\.\s+/.test(lines[i]) && !/^>\s?/.test(lines[i]) && !isTableStart(lines, i) && !htmlBlockInfo(lines[i]) && !/^---+$/.test(lines[i].trim())) {
        p.push(lines[i++]);
      }
      html.push(`<p>${inlineMdToHtml(p.join('\n')).replace(/ {2}\n/g, '<br>').replace(/\n/g, ' ')}</p>`);
    }
    if (inCode) flushCode();
    return html.join('\n');
  }

  function splitFrontMatter(md) {
    const m = md.match(/^---\n([\s\S]*?)\n---\n?([\s\S]*)$/);
    if (!m) return ['', md];
    return [`---\n${m[1]}\n---`, m[2]];
  }

  function getTags() {
    return state.meta.tags ? state.meta.tags.split(',').map(t => t.trim()).filter(Boolean) : [];
  }
  function getTocHtml() {
    const heads = state.blocks.filter(b => b.type === 'heading').map(b => ({
      level: Number(b.level) || 2,
      text: b.text || '未命名标题',
      anchor: b.anchor || slugify(b.text || 'section')
    }));
    if (!state.toc || !heads.length) return '';
    return `<aside class="toc-card"><strong>目录</strong>${heads.map(h => `<a href="#${escapeAttr(h.anchor)}" style="padding-left:${Math.max(0, h.level - 2) * 10}px">${escapeHtml(h.text)}</a>`).join('')}</aside>`;
  }
  function contentHtml() {
    const [_, body] = splitFrontMatter(buildMd());
    return markdownToHtml(body);
  }
  function pagePreviewHtml() {
    readMetaInputs();
    const tags = getTags();
    const tagText = tags.length ? tags.map(t => `#${escapeHtml(t)}`).join(' ') : '无标签';
    const toc = getTocHtml();
    const cover = state.meta.cover ? `<img class="cover-image" src="${escapeAttr(state.meta.cover)}" alt="cover">` : '';
    return `
      <div class="mock-browser">
        <div class="browser-bar"><span class="dot"></span><span class="dot"></span><span class="dot"></span><div class="urlbar">https://your-blog.example/posts/${slugify(state.meta.title || 'post')}</div></div>
        <div class="site-shell">
          <nav class="site-nav"><div class="site-logo">BLOG</div><div class="site-menu"><span>首页</span><span>文章</span><span>分类</span><span>关于</span></div></nav>
          <section class="article-hero">
            <div class="hero-inner">
              <span class="category-pill">${escapeHtml(state.meta.category || '未分类')}</span>
              <h1>${escapeHtml(state.meta.title || '未命名文章')}</h1>
              <p class="article-desc">${escapeHtml(state.meta.description || '无文章描述。')}</p>
              <div class="article-meta"><span>${escapeHtml(state.meta.published || '')}</span><span>${escapeHtml(state.meta.author || '未署名')}</span><span>${tagText}</span><span>${state.meta.draft ? '草稿' : '已发布'}</span></div>
              ${cover}
            </div>
          </section>
          <section class="article-layout">
            ${toc || '<aside class="toc-card"><strong>目录</strong><span class="dim">未生成目录</span></aside>'}
            <article class="blog-article">${contentHtml()}</article>
          </section>
        </div>
      </div>`;
  }
  function articlePreviewHtml() {
    const [fm, body] = splitFrontMatter(buildMd());
    return `<div class="frontmatter-box">${escapeHtml(fm)}</div><div class="mock-browser"><div class="site-shell"><section class="article-layout" style="display:block;max-width:900px"><article class="blog-article">${markdownToHtml(body)}</article></section></div></div>`;
  }
  function updateOutput() {
    readMetaInputs();
    const md = buildMd();
    $('#mdOutput').textContent = md;
    $('#pagePreview').innerHTML = pagePreviewHtml();
    $('#articlePreview').innerHTML = articlePreviewHtml();
  }

  function fileToDataUrl(file) {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = () => resolve(reader.result);
      reader.onerror = reject;
      reader.readAsDataURL(file);
    });
  }
  function download(filename, text, type = 'text/markdown;charset=utf-8') {
    const blob = new Blob([text], { type });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url; a.download = filename;
    document.body.appendChild(a); a.click(); a.remove();
    URL.revokeObjectURL(url);
  }
  function safeFilename(s = '') {
    return (s || 'blog-post').trim().replace(/[\\/:*?"<>|]/g, '-').replace(/\s+/g, '-').slice(0, 80) || 'blog-post';
  }
  function saveDraft() {
    readMetaInputs();
    localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    showStatus('草稿已保存');
  }
  function loadDraft() {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (!raw) return false;
    try {
      const data = JSON.parse(raw);
      state.meta = { ...defaultMeta(), ...(data.meta || {}) };
      state.toc = data.toc !== false;
      state.blocks = Array.isArray(data.blocks) ? data.blocks : [];
      return true;
    } catch (e) { return false; }
  }
  function parseYamlLike(text) {
    const meta = {};
    text.split('\n').forEach(line => {
      const m = line.match(/^([A-Za-z0-9_]+):\s*(.*)$/);
      if (!m) return;
      let v = m[2].trim();
      if ((v.startsWith('"') && v.endsWith('"')) || (v.startsWith("'") && v.endsWith("'"))) v = v.slice(1, -1).replace(/\\"/g, '"');
      if (v === 'true') v = true;
      else if (v === 'false') v = false;
      else if (/^\[.*\]$/.test(v)) v = v.slice(1, -1).split(',').map(x => x.trim().replace(/^["']|["']$/g, '')).join(', ');
      meta[m[1]] = v;
    });
    return meta;
  }
  function importMarkdown(text) {
    const m = text.match(/^---\s*\n([\s\S]*?)\n---\s*\n?([\s\S]*)$/);
    if (m) {
      const meta = parseYamlLike(m[1]);
      state.meta = { ...defaultMeta(), ...state.meta, ...meta };
      state.blocks = [{ id: uid(), type: 'raw', text: m[2].trim() }];
    } else {
      state.blocks = [{ id: uid(), type: 'raw', text: text.trim() }];
    }
    hydrateMetaInputs(); renderBlocks(); updateOutput(); showStatus('已导入 Markdown');
  }

  function seedVideoExample() {
    state.meta = defaultMeta();
    state.blocks = [
      { id: uid(), type: 'paragraph', text: '只需从 YouTube 或其他平台复制嵌入代码，然后将其粘贴到 markdown 文件中。' },
      { id: uid(), type: 'code', lang: 'yaml', code: '---\ntitle: 在文章中嵌入视频\npublished: 2023-10-19\n// ...\n---\n\n<iframe width="100%" height="468" src="https://www.youtube.com/embed/5gIf0_xpFPI?si=N1WTorLKL0uwLsU_" title="YouTube video player" frameborder="0" allowfullscreen></iframe>' },
      { id: uid(), type: 'heading', level: 2, text: 'YouTube', anchor: 'youtube' },
      { id: uid(), type: 'video', provider: 'embed', source: '<iframe width="100%" height="468" src="https://www.youtube.com/embed/5gIf0_xpFPI?si=N1WTorLKL0uwLsU_" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>', title: 'YouTube video player', width: '100%', height: '468', page: 1, autoplay: false, poster: '' },
      { id: uid(), type: 'heading', level: 2, text: 'Bilibili', anchor: 'bilibili' },
      { id: uid(), type: 'video', provider: 'embed', source: '<iframe width="100%" height="468" src="//player.bilibili.com/player.html?bvid=BV1fK4y1s7Qf&p=1&autoplay=0" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"></iframe>', title: 'Bilibili video player', width: '100%', height: '468', page: 1, autoplay: false, poster: '' }
    ];
    hydrateMetaInputs(); renderBlocks(); updateOutput(); showStatus('已载入视频示例');
  }
  function buildPreviewHtmlDocument() {
    readMetaInputs();
    return `<!doctype html>\n<html lang="zh-CN">\n<head>\n<meta charset="utf-8">\n<meta name="viewport" content="width=device-width,initial-scale=1">\n<title>${escapeHtml(state.meta.title || '预览')}</title>\n<style>${document.querySelector('style').textContent}</style>\n</head>\n<body style="background:#ede4d8;padding:24px">\n${pagePreviewHtml()}\n</body>\n</html>`;
  }

  function switchTab(tab) {
    const map = { page: '#pagePreview', article: '#articlePreview', markdown: '#mdOutput' };
    Object.values(map).forEach(sel => $(sel).classList.add('hidden'));
    $(map[tab]).classList.remove('hidden');
    $('#tabPage').classList.toggle('active', tab === 'page');
    $('#tabArticle').classList.toggle('active', tab === 'article');
    $('#tabMarkdown').classList.toggle('active', tab === 'markdown');
  }
  function bindEvents() {
    $$('[data-meta], #toc').forEach(el => {
      el.addEventListener('input', updateOutput);
      el.addEventListener('change', updateOutput);
    });
    $('#btnAddBlock').addEventListener('click', () => {
      state.blocks.push(defaultBlock($('#blockType').value));
      renderBlocks(); updateOutput();
    });
    $('#btnExport').addEventListener('click', () => {
      const md = buildMd();
      download(`${safeFilename(state.meta.title)}.md`, md);
      showStatus('已导出 .md');
    });
    $('#btnExportHtml').addEventListener('click', () => {
      download(`${safeFilename(state.meta.title)}-preview.html`, buildPreviewHtmlDocument(), 'text/html;charset=utf-8');
      showStatus('已导出预览 HTML');
    });
    $('#btnCopy').addEventListener('click', async () => {
      try { await navigator.clipboard.writeText(buildMd()); showStatus('Markdown 已复制'); }
      catch (e) { $('#mdOutput').classList.remove('hidden'); $('#mdOutput').select?.(); showStatus('复制失败，请手动复制源码'); }
    });
    $('#btnSave').addEventListener('click', saveDraft);
    $('#btnExample').addEventListener('click', seedVideoExample);
    $('#btnClear').addEventListener('click', () => {
      if (!confirm('确定清空当前内容？')) return;
      state.meta = defaultMeta(); state.blocks = []; hydrateMetaInputs(); renderBlocks(); updateOutput(); showStatus('已清空');
    });
    $('#btnHelp').addEventListener('click', () => $('#helpModal').classList.add('show'));
    $('#btnCloseHelp').addEventListener('click', () => $('#helpModal').classList.remove('show'));
    $('#helpModal').addEventListener('click', e => { if (e.target.id === 'helpModal') $('#helpModal').classList.remove('show'); });
    $('#tabPage').addEventListener('click', () => switchTab('page'));
    $('#tabArticle').addEventListener('click', () => switchTab('article'));
    $('#tabMarkdown').addEventListener('click', () => switchTab('markdown'));
    $('#importMd').addEventListener('change', e => {
      const file = e.target.files && e.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = () => importMarkdown(String(reader.result || ''));
      reader.readAsText(file, 'utf-8');
      e.target.value = '';
    });
    window.addEventListener('beforeunload', () => {
      try { readMetaInputs(); localStorage.setItem(STORAGE_KEY, JSON.stringify(state)); } catch (e) {}
    });
  }

  function init() {
    if (!loadDraft()) seedVideoExample();
    hydrateMetaInputs(); renderBlocks(); bindEvents(); updateOutput(); switchTab('page');
  }
  init();
})();
</script>
</body>
</html>

```
