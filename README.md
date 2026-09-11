# medicine-box
药品记录
<!DOCTYPE html>
<html lang="en"><head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <meta name="robots" content="noindex, nofollow">
    <meta name="googlebot" content="noindex, nofollow">    <link rel="icon" href="/res/favicon.png">
    <title>JSRUN 驱动</title><script type="application/javascript"> 
                    console.oldLog = console.log;
                    console.oldError = console.error;
                    console.oldInfo = console.info;
                    console.log = function(...args) {
                        window.parent.postMessage(["log", pArgs(arguments)], "*");
                        console.oldLog(...args);;
                    };
                    console.error = function(...args) {
                        window.parent.postMessage(["err", pArgs(arguments)], "*");
                        console.oldError(...args);
                    };
                    console.info = function(...args) {
                        window.parent.postMessage(["log", pArgs(arguments)], "*");
                        console.oldInfo(...args);
                    };
                    function pArgs(args){
                        let result="";
                        for(let i =0 ;i < args.length;i++){
                            if(typeof args[i]=="object"){
                                
                                let cache = [];
                                result+=JSON.stringify(args[i], function(key, value) {
                                    if (typeof value === 'object' && value !== null) {
                                        if (cache.indexOf(value) !== -1) {
                                            return;
                                        }
                                        cache.push(value);
                                    }
                                    return value;
                                });
                                cache = null;  
                                
                            } else {
                                result+=args[i];
                            }
                            if(i<args.length-1){
                                result+=","
                            }
                        }
                        return  result;
                    }
                   listeners = (function (_this) {

                       return function (event) {

                           let data, eventName;
                           eventName = event.data[0];
                           data = event.data[1];
                           switch (eventName) {

                               case "eval":

                                   let result;
                                   try {

                                       result = eval(data);
                                   } catch (e) {

                                       result = e.toString();
                                   }

                                   console.log(result);
                                   break;
                           }
 
                       };
                   })(this);
            function msgMouse() {

                window.addEventListener("message", listeners, false);
                document.addEventListener('mousemove', function (e) {

                    window.parent.postMessage(["mousemove", e.x, e.y], "*");
                });
                document.addEventListener('mouseup', function (e) {

                    window.parent.postMessage(["mouseup", e.x, e.y], "*");
                });
            }

            window.onload=function () { msgMouse(); };

            window.onerror = function(errorMessage ){

                   console.error(errorMessage);
            };
            window.addEventListener("message", listeners, false);
                </script><style type="text/css"></style><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes"><title>小药箱 · 药品记录</title><style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      font-family: system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
      background: #f5f7fa;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      padding: 16px 12px 40px;
    }

    .app-container {
      max-width: 800px;
      width: 100%;
    }

    .app-header {
      margin-bottom: 20px;
    }

    .app-header h1 {
      font-size: 1.9rem;
      font-weight: 600;
      color: #1e293b;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .app-header h1 span {
      font-size: 2rem;
    }

    .subhead {
      color: #64748b;
      margin-top: 4px;
      font-size: 0.95rem;
      border-left: 4px solid #3b82f6;
      padding-left: 12px;
      background: #ffffffcc;
      border-radius: 0 8px 8px 0;
      line-height: 1.4;
    }

    /* 一键复制按钮 */
    .copy-bar {
      background: white;
      border-radius: 16px;
      padding: 14px 18px;
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      flex-wrap: wrap;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.03);
      border: 1px solid #eef2f6;
    }

    .copy-bar-text {
      font-size: 0.88rem;
      color: #475569;
      line-height: 1.4;
      flex: 1;
      min-width: 180px;
    }

    .btn-copy {
      background: #10b981;
      color: white;
      border: none;
      padding: 12px 22px;
      border-radius: 40px;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      box-shadow: 0 6px 14px rgba(16, 185, 129, 0.2);
      transition: 0.15s;
      font-family: inherit;
      white-space: nowrap;
    }

    .btn-copy:hover {
      background: #059669;
      transform: translateY(-1px);
    }

    .btn-copy:active {
      transform: translateY(0);
    }

    .btn-copy.copied {
      background: #059669;
    }

    /* 统计卡片 */
    .stats-bar {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin: 16px 0 20px;
    }

    .stat-item {
      background: white;
      padding: 8px 16px;
      border-radius: 30px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.03);
      font-size: 0.9rem;
      color: #334155;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .stat-item .badge {
      background: #e2e8f0;
      padding: 2px 10px;
      border-radius: 20px;
      font-weight: 600;
      color: #1e293b;
      font-size: 0.85rem;
    }

    /* 表单卡片 */
    .form-card {
      background: white;
      border-radius: 24px;
      padding: 22px 20px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.04);
      margin-bottom: 28px;
      border: 1px solid #eef2f6;
    }

    .form-title {
      font-size: 1.2rem;
      font-weight: 600;
      margin-bottom: 18px;
      color: #0f172a;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .form-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px 16px;
    }

    @media (max-width: 500px) {
      .form-grid {
        grid-template-columns: 1fr;
        gap: 12px;
      }
    }

    .input-group {
      display: flex;
      flex-direction: column;
      gap: 5px;
    }

    .input-group label {
      font-size: 0.83rem;
      font-weight: 500;
      color: #475569;
      letter-spacing: 0.3px;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .input-group label .required {
      color: #ef4444;
      font-size: 1rem;
      line-height: 1;
    }

    .input-group input, 
    .input-group textarea {
      padding: 12px 14px;
      border: 1.5px solid #e2e8f0;
      border-radius: 14px;
      font-size: 0.95rem;
      font-family: inherit;
      transition: 0.2s;
      background: #fafcff;
      resize: vertical;
    }

    .input-group textarea {
      min-height: 70px;
    }

    .input-group input:focus,
    .input-group textarea:focus {
      outline: none;
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.1);
      background: #ffffff;
    }

    .full-width {
      grid-column: 1 / -1;
    }

    .form-actions {
      display: flex;
      justify-content: flex-end;
      gap: 12px;
      margin-top: 20px;
    }

    .btn {
      border: none;
      padding: 12px 24px;
      border-radius: 40px;
      font-weight: 600;
      font-size: 0.95rem;
      cursor: pointer;
      transition: 0.15s;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      font-family: inherit;
      background: white;
      border: 1.5px solid transparent;
    }

    .btn-primary {
      background: #2563eb;
      color: white;
      box-shadow: 0 6px 14px rgba(37, 99, 235, 0.2);
    }

    .btn-primary:hover {
      background: #1d4ed8;
      transform: translateY(-1px);
    }

    .btn-secondary {
      background: white;
      border-color: #cbd5e1;
      color: #334155;
    }

    .btn-secondary:hover {
      background: #f8fafc;
      border-color: #94a3b8;
    }

    .btn-small {
      padding: 6px 12px;
      font-size: 0.8rem;
      border-radius: 30px;
    }

    .btn-danger {
      background: #fee2e2;
      color: #b91c1c;
      border-color: #fecaca;
    }

    .btn-danger:hover {
      background: #fecaca;
      border-color: #fca5a5;
    }

    /* 列表区域 */
    .list-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 12px;
      flex-wrap: wrap;
      gap: 10px;
    }

    .list-header h2 {
      font-size: 1.3rem;
      font-weight: 600;
      color: #0f172a;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .medicine-list {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .medicine-card {
      background: white;
      border-radius: 20px;
      padding: 16px 18px;
      box-shadow: 0 3px 12px rgba(0, 0, 0, 0.02);
      border: 1px solid #eef2f6;
      transition: 0.15s;
      display: flex;
      flex-wrap: wrap;
      align-items: flex-start;
      gap: 12px;
      position: relative;
    }

    .medicine-card:hover {
      border-color: #d9e2ef;
      box-shadow: 0 6px 16px rgba(0, 0, 0, 0.03);
    }

    .med-info {
      flex: 1;
      min-width: 200px;
    }

    .med-name {
      font-size: 1.15rem;
      font-weight: 700;
      color: #0f172a;
      margin-bottom: 6px;
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 8px;
    }

    .med-indication {
      color: #334155;
      font-size: 0.9rem;
      line-height: 1.5;
      margin-bottom: 8px;
      background: #f1f5f9;
      padding: 6px 10px;
      border-radius: 12px;
      word-break: break-word;
    }

    .med-expiry {
      font-size: 0.85rem;
      display: flex;
      align-items: center;
      gap: 6px;
      color: #475569;
      flex-wrap: wrap;
    }

    .expiry-badge {
      background: #e6f7ec;
      color: #0b5e42;
      padding: 2px 10px;
      border-radius: 30px;
      font-weight: 500;
      font-size: 0.8rem;
    }

    .expiry-warning {
      background: #fff3cd;
      color: #856404;
    }

    .expiry-danger {
      background: #f8d7da;
      color: #721c24;
    }

    .med-actions {
      display: flex;
      gap: 6px;
      margin-left: auto;
    }

    .empty-state {
      background: white;
      border-radius: 24px;
      padding: 44px 20px;
      text-align: center;
      color: #94a3b8;
      border: 2px dashed #e2e8f0;
      font-size: 1rem;
    }

    .empty-state span {
      font-size: 2.4rem;
      display: block;
      margin-bottom: 8px;
      opacity: 0.6;
    }

    .toast-message {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%);
      background: #1e293b;
      color: white;
      padding: 10px 22px;
      border-radius: 40px;
      font-size: 0.9rem;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
      opacity: 0;
      transition: opacity 0.2s;
      pointer-events: none;
      z-index: 100;
      white-space: nowrap;
    }

    .toast-message.show {
      opacity: 1;
    }

    .footer-note {
      text-align: center;
      font-size: 0.75rem;
      color: #94a3b8;
      margin-top: 28px;
    }
  </style></head>


  
  
  
  

<body>
  <div class="app-container">
    <!-- 头部 -->
    <div class="app-header">
      <h1>
        <span>💊</span> 小药箱
      </h1>
      <div class="subhead">记录手头药品 · 适应症 · 到期日</div>
    </div>

    <!-- 一键复制代码按钮 -->
    <div class="copy-bar">
      <div class="copy-bar-text">
        📋 点右边按钮，把本小程序的完整代码复制到剪贴板，方便保存到手机或电脑。
      </div>
      <button class="btn-copy" id="copyCodeBtn">📄 一键复制代码</button>
    </div>

    <!-- 统计信息 -->
    <div class="stats-bar" id="statsBar">
      <div class="stat-item">📦 药品总数 <span class="badge" id="totalCount">2</span></div>
      <div class="stat-item">⏳ 即将过期 <span class="badge" id="expiringCount">1</span></div>
    </div>

    <!-- 添加药品表单 -->
    <div class="form-card">
      <div class="form-title">
        <span>➕</span> 添加新药品
      </div>
      <form id="medicineForm">
        <div class="form-grid">
          <!-- 药品名称 -->
          <div class="input-group">
            <label>药品名称 <span class="required">*</span></label>
            <input type="text" id="medName" placeholder="例如：布洛芬缓释胶囊" required="" maxlength="60" autocomplete="off">
          </div>
          <!-- 到期日 -->
          <div class="input-group">
            <label>到期日</label>
            <input type="date" id="medExpiry" value="">
          </div>
          <!-- 适应症 (占满整行) -->
          <div class="input-group full-width">
            <label>适应症 / 功效</label>
            <textarea id="medIndication" placeholder="例如：用于缓解轻至中度疼痛，如头痛、关节痛、牙痛等" rows="2" maxlength="200"></textarea>
          </div>
        </div>
        <div class="form-actions">
          <button type="button" class="btn btn-secondary" id="resetFormBtn">清空</button>
          <button type="submit" class="btn btn-primary">💾 保存药品</button>
        </div>
      </form>
    </div>

    <!-- 药品列表 -->
    <div class="list-header">
      <h2><span>📋</span> 我的药品清单</h2>
      <button class="btn btn-secondary btn-small" id="clearAllBtn" title="删除全部药品">🗑️ 全部删除</button>
    </div>

    <div id="medicineListContainer">
            <div class="medicine-card" data-id="1789106805119-2as7jjp">
              <div class="med-info">
                <div class="med-name">
                  💊 阿莫西林胶囊
                </div>
                <div class="med-indication">
                  适用于敏感菌所致的呼吸道感染、泌尿生殖道感染等。
                </div>
                <div class="med-expiry">
                  <span>📅 到期: 2025/08/15</span>
                  <span class="expiry-badge expiry-danger">已过期</span>
                </div>
              </div>
              <div class="med-actions">
                <button class="btn btn-danger btn-small delete-btn" data-id="1789106805119-2as7jjp" title="删除药品">删除</button>
              </div>
            </div>
          
            <div class="medicine-card" data-id="1789106805119-gnopxfu">
              <div class="med-info">
                <div class="med-name">
                  💊 布洛芬缓释胶囊
                </div>
                <div class="med-indication">
                  用于缓解轻至中度疼痛，如头痛、关节痛、牙痛，也用于普通感冒引起的发热。
                </div>
                <div class="med-expiry">
                  <span>📅 到期: 2026/12/31</span>
                  <span class="expiry-badge ">剩余 111 天</span>
                </div>
              </div>
              <div class="med-actions">
                <button class="btn btn-danger btn-small delete-btn" data-id="1789106805119-gnopxfu" title="删除药品">删除</button>
              </div>
            </div>
          </div>

    <div class="footer-note">
      数据保存在浏览器本地，关闭页面不会丢失
    </div>
  </div>

  <!-- 轻提示 -->
  <div id="toast" class="toast-message"></div>

  <script>
    (function() {
      // ---------- 存储 key ----------
      const STORAGE_KEY = 'medicine_box_items';

      // ---------- 全局数据 ----------
      let medicines = [];

      // DOM 元素
      const form = document.getElementById('medicineForm');
      const medNameInput = document.getElementById('medName');
      const medExpiryInput = document.getElementById('medExpiry');
      const medIndicationInput = document.getElementById('medIndication');
      const resetBtn = document.getElementById('resetFormBtn');
      const clearAllBtn = document.getElementById('clearAllBtn');
      const listContainer = document.getElementById('medicineListContainer');
      const totalCountSpan = document.getElementById('totalCount');
      const expiringCountSpan = document.getElementById('expiringCount');
      const toastEl = document.getElementById('toast');
      const copyCodeBtn = document.getElementById('copyCodeBtn');

      // ---------- 工具函数 ----------
      function generateId() {
        return Date.now() + '-' + Math.random().toString(36).substring(2, 9);
      }

      let toastTimer = null;
      function showToast(msg, duration = 2000) {
        if (toastTimer) clearTimeout(toastTimer);
        toastEl.textContent = msg;
        toastEl.classList.add('show');
        toastTimer = setTimeout(() => {
          toastEl.classList.remove('show');
        }, duration);
      }

      function formatExpiryDate(isoDateStr) {
        if (!isoDateStr) return '未设置';
        try {
          const d = new Date(isoDateStr);
          if (isNaN(d.getTime())) return isoDateStr;
          return d.toLocaleDateString('zh-CN', { year: 'numeric', month: '2-digit', day: '2-digit' });
        } catch {
          return isoDateStr;
        }
      }

      function daysUntilExpiry(expiryDateStr) {
        if (!expiryDateStr) return null;
        const today = new Date();
        today.setHours(0, 0, 0, 0);
        const expiry = new Date(expiryDateStr);
        if (isNaN(expiry.getTime())) return null;
        expiry.setHours(0, 0, 0, 0);
        const diffTime = expiry - today;
        return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
      }

      function getExpiryStatus(expiryDateStr) {
        if (!expiryDateStr) return { className: '', text: '未设置' };
        const days = daysUntilExpiry(expiryDateStr);
        if (days === null) return { className: '', text: '未知' };

        if (days < 0) {
          return { className: 'expiry-danger', text: '已过期' };
        } else if (days === 0) {
          return { className: 'expiry-danger', text: '今天到期' };
        } else if (days <= 30) {
          return { className: 'expiry-warning', text: `剩余 ${days} 天` };
        } else if (days <= 90) {
          return { className: 'expiry-warning', text: `剩余 ${days} 天` };
        } else {
          return { className: '', text: `剩余 ${days} 天` };
        }
      }

      function updateStats() {
        const total = medicines.length;
        totalCountSpan.textContent = total;

        let expiringCount = 0;
        medicines.forEach(med => {
          const days = daysUntilExpiry(med.expiryDate);
          if (days !== null && days <= 90) {
            expiringCount++;
          }
        });
        expiringCountSpan.textContent = expiringCount;
      }

      function saveToLocalStorage() {
        try {
          localStorage.setItem(STORAGE_KEY, JSON.stringify(medicines));
        } catch (e) {
          console.warn('保存失败', e);
          showToast('保存失败，浏览器存储可能已满');
        }
      }

      function loadFromLocalStorage() {
        try {
          const stored = localStorage.getItem(STORAGE_KEY);
          if (stored) {
            const parsed = JSON.parse(stored);
            if (Array.isArray(parsed)) {
              medicines = parsed;
            } else {
              medicines = [];
            }
          } else {
            medicines = [
              {
                id: generateId(),
                name: '布洛芬缓释胶囊',
                indication: '用于缓解轻至中度疼痛，如头痛、关节痛、牙痛，也用于普通感冒引起的发热。',
                expiryDate: '2026-12-31'
              },
              {
                id: generateId(),
                name: '阿莫西林胶囊',
                indication: '适用于敏感菌所致的呼吸道感染、泌尿生殖道感染等。',
                expiryDate: '2025-08-15'
              }
            ];
            saveToLocalStorage();
          }
        } catch (e) {
          console.error('加载数据失败', e);
          medicines = [];
        }
        medicines = medicines.map(med => ({
          ...med,
          id: med.id || generateId(),
        }));
        saveToLocalStorage();
      }

      function escapeHtml(text) {
        if (!text) return '';
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
      }

      // ---------- 渲染药品列表 ----------
      function render() {
        updateStats();

        if (!medicines.length) {
          listContainer.innerHTML = `
            <div class="empty-state">
              <span>📭</span>
              还没有药品记录，点击上方表单添加吧
            </div>
          `;
          return;
        }

        const sorted = [...medicines].sort((a, b) => {
          const daysA = daysUntilExpiry(a.expiryDate);
          const daysB = daysUntilExpiry(b.expiryDate);
          const da = daysA === null ? Infinity : daysA;
          const db = daysB === null ? Infinity : daysB;
          return da - db;
        });

        let html = '';
        sorted.forEach(med => {
          const expiryStatus = getExpiryStatus(med.expiryDate);
          const expiryDisplay = formatExpiryDate(med.expiryDate);
          const indicationText = med.indication?.trim() ? med.indication : '（未填写适应症）';

          html += `
            <div class="medicine-card" data-id="${med.id}">
              <div class="med-info">
                <div class="med-name">
                  💊 ${escapeHtml(med.name)}
                </div>
                <div class="med-indication">
                  ${escapeHtml(indicationText)}
                </div>
                <div class="med-expiry">
                  <span>📅 到期: ${expiryDisplay}</span>
                  <span class="expiry-badge ${expiryStatus.className}">${expiryStatus.text}</span>
                </div>
              </div>
              <div class="med-actions">
                <button class="btn btn-danger btn-small delete-btn" data-id="${med.id}" title="删除药品">删除</button>
              </div>
            </div>
          `;
        });

        listContainer.innerHTML = html;
      }

      // ---------- 删除单条药品 ----------
      function deleteMedicineById(id) {
        const med = medicines.find(m => m.id === id);
        if (!med) return;
        const medName = med.name || '该药品';
        if (confirm(`确定要删除「${medName}」吗？`)) {
          medicines = medicines.filter(m => m.id !== id);
          saveToLocalStorage();
          render();
          showToast(`已删除 ${medName}`);
        }
      }

      // ---------- 添加药品 ----------
      function addMedicine(name, indication, expiryDate) {
        const expiry = expiryDate?.trim() || '';
        const newMed = {
          id: generateId(),
          name: name.trim(),
          indication: indication.trim(),
          expiryDate: expiry,
        };
        medicines.push(newMed);
        saveToLocalStorage();
        render();
      }

      // ---------- 清空表单 ----------
      function resetForm() {
        medNameInput.value = '';
        medExpiryInput.value = '';
        medIndicationInput.value = '';
        medNameInput.focus();
      }

      // ---------- 删除全部药品 ----------
      function clearAllMedicines() {
        if (!medicines.length) {
          showToast('列表已经是空的');
          return;
        }
        if (confirm('⚠️ 确定要删除全部药品记录吗？此操作不可撤销。')) {
          medicines = [];
          saveToLocalStorage();
          render();
          showToast('已清空所有药品');
          resetForm();
        }
      }

      // ---------- 一键复制代码（复制当前页面的完整 HTML 源码） ----------
      function copyFullCode() {
        // 获取当前文档的完整 HTML 字符串
        const docType = '<!DOCTYPE html>\n';
        const fullHtml = docType + document.documentElement.outerHTML;

        // 优先使用 navigator.clipboard
        if (navigator.clipboard && navigator.clipboard.writeText) {
          navigator.clipboard.writeText(fullHtml).then(() => {
            showToast('✅ 代码已复制，粘贴到 .html 文件即可');
            copyCodeBtn.textContent = '✅ 已复制';
            copyCodeBtn.classList.add('copied');
            setTimeout(() => {
              copyCodeBtn.textContent = '📄 一键复制代码';
              copyCodeBtn.classList.remove('copied');
            }, 2000);
          }).catch(err => {
            console.warn('clipboard 复制失败', err);
            fallbackCopy(fullHtml);
          });
        } else {
          fallbackCopy(fullHtml);
        }
      }

      // 降级复制一声方案 (用于旧浏览器)
      function fallbackCopy(text) {
        const textarea = document.createElement('textarea');
        textarea.value = text;
        textarea.style.position = 'fixed';
        textarea.style.top = '-9999px';
        textarea.style.left = '-9999px';
        document.body.appendChild(textarea);
        textarea.select();
        try {
          const success = document.execCommand('copy');
          if (success) {
            showToast('✅ 代码已复制，粘贴到 .html 文件即可');
            copyCodeBtn.textContent = '✅ 已复制';
            copyCodeBtn.classList.add('copied');
            setTimeout(() => {
              copyCodeBtn.textContent = '📄 一键复制代码';
              copyCodeBtn.classList.remove('copied');
            }, 2000);
          } else {
            showToast('复制失败，请长按手动选择复制');
          }
        } catch (err) {
          console.error('复制失败', err);
          showToast('复制失败，请手动复制');
        } finally {
          document.body.removeChild(textarea);
        }
      }

      // ---------- 事件绑定 ----------
      form.addEventListener('submit', (e) => {
        e.preventDefault();
        const name = medNameInput.value.trim();
        if (!name) {
          showToast('请填写药品名称');
          medNameInput.focus();
          return;
        }
        const indication = medIndicationInput.value.trim();
        const expiry = medExpiryInput.value;

        addMedicine(name, indication, expiry);
        resetForm();
        showToast('✅ 药品已保存');
      });

      resetBtn.addEventListener('click', () => {
        resetForm();
      });

      clearAllBtn.addEventListener('click', clearAllMedicines);

      // 删除按钮事件委托
      listContainer.addEventListener('click', (e) => {
        const deleteBtn = e.target.closest('.delete-btn');
        if (deleteBtn) {
          e.stopPropagation();
          const id = deleteBtn.dataset.id;
          deleteMedicineById(id);
        }
      });

      // 一键复制按钮
      copyCodeBtn.addEventListener('click', copyFullCode);

      // 初始加载
      function init() {
        loadFromLocalStorage();
        render();
      }

      init();

      // 离开页面时保存
      window.addEventListener('beforeunload', function() {
        saveToLocalStorage();
      });
    })();
  </script>

<script type="application/javascript">//<![CDATA[
//]]>
   </script> </body></html>