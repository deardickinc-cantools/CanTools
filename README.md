<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CanTools — Free Canadian Business Tools</title>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@latest/tabler-icons.min.css">
<link href="https://fonts.googleapis.com/css2?family=Cookie&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
:root {
  --red: #C0392B;
  --red-light: #FADBD8;
  --red-dark: #922B21;
  --dark: #2C2C2C;
  --mid: #555555;
  --light: #F5F5F5;
  --border: rgba(0,0,0,0.12);
  --white: #FFFFFF;
  --radius: 10px;
  --font: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: var(--font); background: #eee; display: flex; justify-content: center; padding: 20px; }
.ct-wrap { font-family: var(--font); background: var(--light); max-width: 680px; width: 100%; border-radius: var(--radius); overflow: hidden; box-shadow: 0 2px 20px rgba(0,0,0,0.1); }
.ct-header { background: var(--dark); padding: 16px 20px; display: flex; align-items: center; justify-content: space-between; }
.ct-logo { display: flex; align-items: center; gap: 10px; }
.ct-maple { width: 28px; height: 28px; background: var(--red); border-radius: 4px; display: flex; align-items: center; justify-content: center; color: white; font-size: 16px; font-weight: 700; }
.ct-logo-text { color: white; font-size: 18px; font-weight: 600; letter-spacing: -0.3px; }
.ct-logo-sub { color: rgba(255,255,255,0.5); font-size: 11px; margin-top: 1px; }
.ct-tabs { display: flex; background: var(--white); border-bottom: 1px solid var(--border); }
.ct-tab { flex: 1; padding: 12px 8px; text-align: center; font-size: 13px; font-weight: 500; color: var(--mid); cursor: pointer; border-bottom: 2px solid transparent; transition: all 0.15s; background: none; border-top: none; border-left: none; border-right: none; font-family: var(--font); }
.ct-tab.active { color: var(--red); border-bottom-color: var(--red); background: var(--light); }
.ct-tab:hover:not(.active) { background: var(--light); color: var(--dark); }
.ct-panel { display: none; padding: 20px; background: var(--light); }
.ct-panel.active { display: block; }
.ct-card { background: var(--white); border: 0.5px solid var(--border); border-radius: var(--radius); padding: 16px; margin-bottom: 14px; }
.ct-card-title { font-size: 13px; font-weight: 600; color: var(--dark); text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 12px; display: flex; align-items: center; gap: 6px; }
.ct-card-title i { color: var(--red); font-size: 16px; }
label { display: block; font-size: 12px; font-weight: 500; color: var(--mid); margin-bottom: 5px; margin-top: 10px; }
label:first-of-type { margin-top: 0; }
input[type=text], input[type=url], input[type=number], select { width: 100%; padding: 9px 12px; border: 0.5px solid var(--border); border-radius: 8px; font-size: 14px; font-family: var(--font); background: var(--white); color: var(--dark); outline: none; }
input:focus, select:focus { border-color: var(--red); }
.ct-row { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.ct-color-wrap { display: flex; align-items: center; gap: 8px; padding: 6px 10px; border: 0.5px solid var(--border); border-radius: 8px; background: var(--white); }
.ct-color-wrap input[type=color] { width: 26px; height: 26px; border: none; border-radius: 50%; padding: 0; cursor: pointer; background: none; outline: none; }
.ct-color-hex { font-size: 12px; color: var(--mid); font-family: monospace; }
.ct-size-row { display: flex; gap: 6px; }
.ct-sz { flex: 1; padding: 7px 4px; text-align: center; border: 0.5px solid var(--border); border-radius: 8px; font-size: 12px; color: var(--mid); cursor: pointer; background: var(--white); font-family: var(--font); transition: all 0.15s; }
.ct-sz.active { border-color: var(--red); color: var(--red); background: var(--red-light); }
.ct-seg { display: flex; gap: 6px; margin-top: 4px; }
.ct-seg-btn { flex: 1; padding: 8px 4px; text-align: center; border: 0.5px solid var(--border); border-radius: 8px; font-size: 12px; color: var(--mid); cursor: pointer; background: var(--white); font-family: var(--font); transition: all 0.15s; }
.ct-seg-btn.active { border-color: var(--red); color: var(--red); background: var(--red-light); }
.ct-btn { width: 100%; padding: 11px; background: var(--red); color: white; border: none; border-radius: 8px; font-size: 14px; font-weight: 600; cursor: pointer; font-family: var(--font); transition: background 0.15s; margin-top: 4px; }
.ct-btn:hover { background: var(--red-dark); }
.ct-btn-secondary { flex: 1; padding: 9px; background: var(--white); color: var(--dark); border: 0.5px solid var(--border); border-radius: 8px; font-size: 13px; font-weight: 500; cursor: pointer; font-family: var(--font); transition: all 0.15s; }
.ct-btn-secondary:hover { border-color: var(--red); color: var(--red); }
.ct-action-row { display: flex; gap: 8px; margin-top: 10px; }
#qr-output { display: none; flex-direction: column; align-items: center; gap: 12px; padding: 16px; background: var(--white); border: 0.5px solid var(--border); border-radius: var(--radius); margin-top: 14px; }
#qr-output.visible { display: flex; }
#qr-wrap { background: white; padding: 16px; border-radius: 8px; border: 0.5px solid var(--border); }
.ct-upload-zone { border: 1.5px dashed var(--border); border-radius: 8px; padding: 14px; text-align: center; cursor: pointer; transition: all 0.15s; background: var(--white); }
.ct-upload-zone:hover { border-color: var(--red); }
.ct-upload-zone p { font-size: 12px; color: var(--mid); margin-top: 4px; }
.ct-result-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-top: 14px; }
.ct-metric { background: var(--light); border-radius: 8px; padding: 12px; text-align: center; }
.ct-metric-label { font-size: 11px; color: var(--mid); text-transform: uppercase; letter-spacing: 0.05em; margin-bottom: 4px; }
.ct-metric-value { font-size: 20px; font-weight: 600; color: var(--dark); }
.ct-metric-value.red { color: var(--red); }
.ct-divider { height: 0.5px; background: var(--border); margin: 12px 0; }
.ct-fee-row { display: flex; justify-content: space-between; font-size: 13px; padding: 5px 0; color: var(--mid); }
.ct-fee-total { display: flex; justify-content: space-between; font-size: 15px; font-weight: 600; padding: 8px 0; color: var(--dark); border-top: 1px solid var(--border); margin-top: 6px; }
.ct-split-item { background: var(--light); border-radius: 8px; padding: 12px; margin-bottom: 8px; }
.ct-split-name { font-size: 13px; font-weight: 600; color: var(--dark); margin-bottom: 6px; }
.ct-split-amount { font-size: 22px; font-weight: 700; color: var(--red); }
.ct-split-detail { font-size: 11px; color: var(--mid); margin-top: 2px; }
.ct-footer { background: var(--dark); padding: 16px 20px; }
.ct-footer-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
.ct-footer-text { font-size: 11px; color: rgba(255,255,255,0.4); }
.ct-footer-link { font-size: 11px; color: var(--red); text-decoration: none; cursor: pointer; }
.ct-footer-divider { height: 0.5px; background: rgba(255,255,255,0.1); margin-bottom: 12px; }
.ct-bmc-wrap { display: flex; align-items: center; justify-content: space-between; }
.ct-bmc-text { font-size: 11px; color: rgba(255,255,255,0.4); max-width: 200px; line-height: 1.5; }
.bmc-btn { display: inline-flex; align-items: center; gap: 8px; background: #FF5F5F; color: white; padding: 8px 16px; border-radius: 8px; font-size: 13px; font-weight: 600; text-decoration: none; font-family: 'Cookie', cursive, var(--font); letter-spacing: 0.3px; transition: opacity 0.15s; }
.bmc-btn:hover { opacity: 0.88; }
</style>
</head>
<body>
<div class="ct-wrap">

<div class="ct-header">
  <div class="ct-logo">
    <div class="ct-maple">C</div>
    <div>
      <div class="ct-logo-text">CanTools</div>
      <div class="ct-logo-sub">Free tools for Canadian business</div>
    </div>
  </div>
  <div style="font-size:11px;color:rgba(255,255,255,0.35)">No account &middot; No watermark &middot; Always free</div>
</div>

<div class="ct-tabs">
  <button class="ct-tab active" onclick="switchTab('qr',this)"><i class="ti ti-qrcode"></i> QR Generator</button>
  <button class="ct-tab" onclick="switchTab('fees',this)"><i class="ti ti-receipt"></i> Fee Calculator</button>
  <button class="ct-tab" onclick="switchTab('tip',this)"><i class="ti ti-users"></i> Bill Splitter</button>
</div>

<div id="tab-qr" class="ct-panel active">
  <div class="ct-card">
    <div class="ct-card-title"><i class="ti ti-link"></i> Step 1 — Clean your URL</div>
    <label>Paste your URL</label>
    <input type="url" id="raw-url" placeholder="https://your-site.com/page?utm_source=email&fbclid=xyz" />
    <div style="display:flex;gap:8px;margin-top:8px">
      <button class="ct-btn-secondary" onclick="cleanURL()"><i class="ti ti-wand"></i> Clean</button>
      <button class="ct-btn-secondary" onclick="copyClean()"><i class="ti ti-copy"></i> Copy</button>
      <button class="ct-btn-secondary" onclick="useInQR()"><i class="ti ti-arrow-right"></i> Use in QR</button>
    </div>
    <div id="clean-result" style="margin-top:10px;padding:8px 12px;background:var(--light);border-radius:8px;font-size:12px;color:var(--mid);word-break:break-all;min-height:32px;font-family:monospace">Cleaned URL appears here</div>
  </div>

  <div class="ct-card">
    <div class="ct-card-title"><i class="ti ti-qrcode"></i> Step 2 — Create your QR code</div>
    <label>URL or text</label>
    <input type="url" id="qr-url" placeholder="https://your-link.com" />
    <div class="ct-row" style="margin-top:10px">
      <div>
        <label>QR colour</label>
        <div class="ct-color-wrap">
          <input type="color" id="fg-color" value="#000000" oninput="document.getElementById('fg-hex').textContent=this.value.toUpperCase()">
          <span class="ct-color-hex" id="fg-hex">#000000</span>
        </div>
      </div>
      <div>
        <label>Background</label>
        <div class="ct-color-wrap">
          <input type="color" id="bg-color" value="#ffffff" oninput="document.getElementById('bg-hex').textContent=this.value.toUpperCase()">
          <span class="ct-color-hex" id="bg-hex">#FFFFFF</span>
        </div>
      </div>
    </div>
    <label style="margin-top:12px">Size</label>
    <div class="ct-size-row">
      <div class="ct-sz" onclick="setSize(128,this)">128px</div>
      <div class="ct-sz active" onclick="setSize(256,this)">256px</div>
      <div class="ct-sz" onclick="setSize(512,this)">512px</div>
      <div class="ct-sz" onclick="setSize(1024,this)">1024px</div>
    </div>
    <label style="margin-top:12px">Frame style</label>
    <div class="ct-seg">
      <div class="ct-seg-btn active" onclick="setFrame('none',this)">None</div>
      <div class="ct-seg-btn" onclick="setFrame('rounded',this)">Rounded</div>
      <div class="ct-seg-btn" onclick="setFrame('circle',this)">Circle</div>
      <div class="ct-seg-btn" onclick="setFrame('maple',this)">Maple</div>
    </div>
    <label style="margin-top:12px">Centre image (optional)</label>
    <div class="ct-upload-zone" onclick="document.getElementById('logo-upload').click()">
      <i class="ti ti-upload" style="font-size:20px;color:var(--mid)"></i>
      <p id="upload-label">Click to upload logo or image (PNG/JPG)</p>
    </div>
    <input type="file" id="logo-upload" accept="image/*" style="display:none" onchange="handleLogoUpload(this)">
    <label style="margin-top:12px">Label text</label>
    <input type="text" id="label-text" value="Scan me" placeholder="Scan me" />
    <label>Label position</label>
    <select id="label-pos">
      <option value="below">Below QR</option>
      <option value="above">Above QR</option>
      <option value="none">No label</option>
    </select>
    <button class="ct-btn" style="margin-top:14px" onclick="generateQR()"><i class="ti ti-qrcode"></i> Generate QR Code</button>
  </div>

  <div id="qr-output">
    <div id="qr-wrap"><div id="qr-inner"></div></div>
    <canvas id="label-canvas" style="display:none"></canvas>
    <div class="ct-action-row" style="width:100%">
      <button class="ct-btn-secondary" onclick="dlQR()"><i class="ti ti-download"></i> Download QR</button>
      <button class="ct-btn-secondary" onclick="dlLabel()"><i class="ti ti-sticker"></i> Download Sticker</button>
    </div>
    <div style="text-align:center;font-size:11px;color:var(--mid)">No watermark &middot; Print-ready &middot; Free forever</div>
  </div>
</div>

<div id="tab-fees" class="ct-panel">
  <div class="ct-card">
    <div class="ct-card-title"><i class="ti ti-building-store"></i> Platform & product details</div>
    <label>Selling platform</label>
    <select id="platform" onchange="calcFees()">
      <option value="etsy">Etsy</option>
      <option value="shopify">Shopify</option>
      <option value="amazon">Amazon Canada</option>
      <option value="gumroad">Gumroad</option>
    </select>
    <label>Sale price (CAD)</label>
    <input type="number" id="sale-price" value="25.00" min="0" step="0.01" oninput="calcFees()" />
    <label>Your product cost (CAD)</label>
    <input type="number" id="product-cost" value="8.00" min="0" step="0.01" oninput="calcFees()" />
    <label>Shipping cost you pay (CAD)</label>
    <input type="number" id="shipping-cost" value="0" min="0" step="0.01" oninput="calcFees()" />
    <label>Province (for HST/GST)</label>
    <select id="province" onchange="calcFees()">
      <option value="0">Alberta — No PST (GST 5%)</option>
      <option value="0">Northwest Territories — GST 5%</option>
      <option value="0">Nunavut — GST 5%</option>
      <option value="0">Yukon — GST 5%</option>
      <option value="7">British Columbia — GST+PST 12%</option>
      <option value="7">Saskatchewan — GST+PST 11%</option>
      <option value="8">Manitoba — GST+PST 13%</option>
      <option value="8" selected>Ontario — HST 13%</option>
      <option value="10">Quebec — GST+QST 14.975%</option>
      <option value="10">New Brunswick — HST 15%</option>
      <option value="10">Nova Scotia — HST 15%</option>
      <option value="10">PEI — HST 15%</option>
      <option value="10">Newfoundland — HST 15%</option>
    </select>
  </div>
  <div id="fee-results" style="display:none">
    <div class="ct-card">
      <div class="ct-card-title"><i class="ti ti-calculator"></i> Fee breakdown</div>
      <div id="fee-breakdown"></div>
      <div class="ct-divider"></div>
      <div class="ct-result-grid">
        <div class="ct-metric"><div class="ct-metric-label">You receive</div><div class="ct-metric-value" id="you-receive">—</div></div>
        <div class="ct-metric"><div class="ct-metric-label">Net profit</div><div class="ct-metric-value red" id="net-profit">—</div></div>
        <div class="ct-metric"><div class="ct-metric-label">Total fees</div><div class="ct-metric-value" id="total-fees">—</div></div>
        <div class="ct-metric"><div class="ct-metric-label">Profit margin</div><div class="ct-metric-value" id="profit-margin">—</div></div>
      </div>
    </div>
  </div>
  <button class="ct-btn" onclick="calcFees()"><i class="ti ti-calculator"></i> Calculate fees</button>
</div>

<div id="tab-tip" class="ct-panel">
  <div class="ct-card">
    <div class="ct-card-title"><i class="ti ti-receipt-2"></i> Bill details</div>
    <label>Bill amount (CAD)</label>
    <input type="number" id="bill-amount" value="80.00" min="0" step="0.01" oninput="calcSplit()" />
    <label>Province</label>
    <select id="tip-province" onchange="calcSplit()">
      <option value="5">Alberta — GST 5%</option>
      <option value="5">BC — GST 5%</option>
      <option value="13" selected>Ontario — HST 13%</option>
      <option value="15">Nova Scotia — HST 15%</option>
      <option value="15">New Brunswick — HST 15%</option>
      <option value="15">PEI — HST 15%</option>
      <option value="15">Newfoundland — HST 15%</option>
      <option value="14975">Quebec — QST+GST ~15%</option>
      <option value="5">Manitoba — GST 5%</option>
      <option value="5">Saskatchewan — GST 5%</option>
      <option value="5">Yukon/NWT/Nunavut — GST 5%</option>
    </select>
    <label>Tip percentage</label>
    <div style="display:flex;align-items:center;gap:10px;margin-top:4px">
      <input type="range" id="tip-range" min="0" max="30" value="18" step="1" style="flex:1" oninput="document.getElementById('tip-pct-out').textContent=this.value+'%';calcSplit()" />
      <span style="font-size:14px;font-weight:600;color:var(--red);min-width:36px" id="tip-pct-out">18%</span>
    </div>
    <div class="ct-seg" style="margin-top:8px">
      <div class="ct-seg-btn" onclick="setTip(15,event)">15%</div>
      <div class="ct-seg-btn active" onclick="setTip(18,event)">18%</div>
      <div class="ct-seg-btn" onclick="setTip(20,event)">20%</div>
      <div class="ct-seg-btn" onclick="setTip(25,event)">25%</div>
    </div>
    <label style="margin-top:12px">Split between</label>
    <div style="display:flex;align-items:center;gap:10px;margin-top:4px">
      <input type="range" id="split-range" min="1" max="20" value="2" step="1" style="flex:1" oninput="document.getElementById('split-out').textContent=this.value+' people';calcSplit()" />
      <span style="font-size:14px;font-weight:600;color:var(--red);min-width:64px" id="split-out">2 people</span>
    </div>
    <label style="margin-top:12px">Tax included in bill?</label>
    <div class="ct-seg" style="margin-top:4px">
      <div class="ct-seg-btn active" id="tax-yes" onclick="setTaxIncluded(true)">Yes — tax already in total</div>
      <div class="ct-seg-btn" id="tax-no" onclick="setTaxIncluded(false)">No — add tax on top</div>
    </div>
  </div>
  <div id="split-results" class="ct-card" style="display:none">
    <div class="ct-card-title"><i class="ti ti-users"></i> Each person pays</div>
    <div id="split-breakdown"></div>
  </div>
</div>

<div class="ct-footer">
  <div class="ct-footer-top">
    <div class="ct-footer-text">CanTools &middot; Free tools for Canadian business</div>
    <a class="ct-footer-link" href="https://try.carrd.co/p6y2fp95" target="_blank"><i class="ti ti-external-link" style="font-size:10px"></i> Built with Carrd &mdash; 30% off</a>
  </div>
  <div class="ct-footer-divider"></div>
  <div class="ct-bmc-wrap">
    <div class="ct-bmc-text">CanTools is free forever. If it saved you time, a coffee keeps it running.</div>
    <a class="bmc-btn" href="https://www.buymeacoffee.com/CanTools" target="_blank">&#9749; Buy me a coffee</a>
  </div>
</div>

</div>

<script>
let qrSize=256,frameStyle='none',logoImg=null,taxIncluded=true;

function switchTab(tab,el){
  document.querySelectorAll('.ct-panel').forEach(p=>p.classList.remove('active'));
  document.querySelectorAll('.ct-tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('tab-'+tab).classList.add('active');
  el.classList.add('active');
  if(tab==='fees')calcFees();
  if(tab==='tip')calcSplit();
}

function cleanURL(){
  const raw=document.getElementById('raw-url').value.trim();
  if(!raw)return;
  try{
    const url=new URL(raw);
    ['utm_source','utm_medium','utm_campaign','utm_term','utm_content','fbclid','gclid','msclkid','mc_cid','mc_eid','_ga','ref','source','affiliate','click_id','tracking','campaign'].forEach(p=>url.searchParams.delete(p));
    document.getElementById('clean-result').textContent=url.toString();
    document.getElementById('clean-result').style.color='#2C2C2C';
  }catch(e){
    document.getElementById('clean-result').textContent=raw;
  }
}

function copyClean(){
  const t=document.getElementById('clean-result').textContent;
  if(t&&t!=='Cleaned URL appears here')navigator.clipboard.writeText(t);
}

function useInQR(){
  const t=document.getElementById('clean-result').textContent;
  if(t&&t!=='Cleaned URL appears here')document.getElementById('qr-url').value=t;
}

function setSize(s,el){
  qrSize=s;
  document.querySelectorAll('.ct-sz').forEach(x=>x.classList.remove('active'));
  el.classList.add('active');
}

function setFrame(f,el){
  frameStyle=f;
  el.closest('.ct-seg').querySelectorAll('.ct-seg-btn').forEach(x=>x.classList.remove('active'));
  el.classList.add('active');
}

function handleLogoUpload(input){
  const file=input.files[0];
  if(!file)return;
  const reader=new FileReader();
  reader.onload=e=>{
    logoImg=new Image();
    logoImg.onload=()=>document.getElementById('upload-label').textContent=file.name+' loaded';
    logoImg.src=e.target.result;
  };
  reader.readAsDataURL(file);
}

function generateQR(){
  const url=document.getElementById('qr-url').value.trim();
  if(!url)return;
  const fg=document.getElementById('fg-color').value;
  const bg=document.getElementById('bg-color').value;
  const inner=document.getElementById('qr-inner');
  inner.innerHTML='';
  const renderSize=Math.min(qrSize,256);
  new QRCode(inner,{text:url,width:renderSize,height:renderSize,colorDark:fg,colorLight:bg,correctLevel:QRCode.CorrectLevel.H});
  document.getElementById('qr-output').classList.add('visible');
  if(logoImg)setTimeout(()=>overlayLogo(renderSize),300);
  setTimeout(renderSticker,400);
}

function overlayLogo(size){
  const canvas=document.querySelector('#qr-inner canvas');
  if(!canvas)return;
  const ctx=canvas.getContext('2d');
  const ls=size*0.22,x=(size-ls)/2,y=(size-ls)/2;
  ctx.fillStyle='white';ctx.fillRect(x-4,y-4,ls+8,ls+8);
  ctx.drawImage(logoImg,x,y,ls,ls);
}

function renderSticker(){
  const canvas=document.getElementById('label-canvas');
  const ctx=canvas.getContext('2d');
  const pos=document.getElementById('label-pos').value;
  const labelText=document.getElementById('label-text').value;
  const qrSrc=document.querySelector('#qr-inner canvas');
  const pad=16,qrW=200,fontSize=16;
  const textH=pos==='none'?0:fontSize+10;
  const totalH=qrW+textH+pad*2,totalW=qrW+pad*2;
  canvas.width=totalW;canvas.height=totalH;
  canvas.style.display='block';
  ctx.clearRect(0,0,totalW,totalH);
  if(frameStyle==='rounded'){
    ctx.fillStyle='#fff';rr(ctx,0,0,totalW,totalH,16);ctx.fill();
    ctx.strokeStyle='#C0392B';ctx.lineWidth=3;rr(ctx,1.5,1.5,totalW-3,totalH-3,16);ctx.stroke();
  }else if(frameStyle==='circle'){
    ctx.fillStyle='#fff';
    ctx.beginPath();ctx.arc(totalW/2,totalH/2,Math.min(totalW,totalH)/2-2,0,Math.PI*2);ctx.fill();
    ctx.strokeStyle='#C0392B';ctx.lineWidth=3;
    ctx.beginPath();ctx.arc(totalW/2,totalH/2,Math.min(totalW,totalH)/2-3.5,0,Math.PI*2);ctx.stroke();
  }else if(frameStyle==='maple'){
    ctx.fillStyle='#fff';rr(ctx,0,0,totalW,totalH,8);ctx.fill();
    ctx.strokeStyle='#C0392B';ctx.lineWidth=3;rr(ctx,1.5,1.5,totalW-3,totalH-3,8);ctx.stroke();
    ctx.fillStyle='#C0392B';ctx.font='bold 14px sans-serif';ctx.textAlign='center';
    ctx.fillText('🍁',totalW-18,18);
  }else{
    ctx.fillStyle='#fff';ctx.fillRect(0,0,totalW,totalH);
  }
  const qrY=pos==='above'?pad+textH:pad;
  if(qrSrc)ctx.drawImage(qrSrc,pad,qrY,qrW,qrW);
  if(pos!=='none'){
    const textY=pos==='above'?pad+fontSize:pad+qrW+fontSize+6;
    ctx.fillStyle='#2C2C2C';ctx.font='500 '+fontSize+'px -apple-system,sans-serif';
    ctx.textAlign='center';ctx.fillText(labelText,totalW/2,textY);
  }
}

function rr(ctx,x,y,w,h,r){
  ctx.beginPath();
  ctx.moveTo(x+r,y);ctx.lineTo(x+w-r,y);ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r);ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h);ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r);ctx.quadraticCurveTo(x,y,x+r,y);
  ctx.closePath();
}

function dlQR(){
  const c=document.querySelector('#qr-inner canvas');
  if(!c)return;
  if(qrSize>256){
    const sc=document.createElement('canvas');
    sc.width=qrSize;sc.height=qrSize;
    sc.getContext('2d').drawImage(c,0,0,qrSize,qrSize);
    dl(sc,'qrcode-'+qrSize+'px.png');
  }else dl(c,'qrcode.png');
}

function dlLabel(){renderSticker();setTimeout(()=>dl(document.getElementById('label-canvas'),'qr-sticker.png'),100);}

function dl(canvas,name){
  const a=document.createElement('a');
  a.href=canvas.toDataURL('image/png');
  a.download=name;a.click();
}

const platforms={
  etsy:{listing:0.27,transaction:0.065,payment:0.03,fixed:0.25},
  shopify:{listing:0,transaction:0,payment:0.029,fixed:0.30},
  amazon:{listing:0,transaction:0.15,payment:0.029,fixed:0.30},
  gumroad:{listing:0,transaction:0.10,payment:0.029,fixed:0.30}
};

function calcFees(){
  const p=platforms[document.getElementById('platform').value];
  const price=parseFloat(document.getElementById('sale-price').value)||0;
  const cost=parseFloat(document.getElementById('product-cost').value)||0;
  const shipping=parseFloat(document.getElementById('shipping-cost').value)||0;
  const taxRate=parseFloat(document.getElementById('province').value)/100;
  const lf=p.listing,tf=price*p.transaction,pf=(price*p.payment)+p.fixed;
  const taxF=(lf+tf+pf)*taxRate,totalF=lf+tf+pf+taxF;
  const recv=price-totalF,profit=recv-cost-shipping;
  const margin=price>0?(profit/price*100):0;
  let html='';
  if(lf>0)html+=`<div class="ct-fee-row"><span>Listing fee</span><span>-$${lf.toFixed(2)}</span></div>`;
  if(tf>0)html+=`<div class="ct-fee-row"><span>Transaction fee (${(p.transaction*100).toFixed(0)}%)</span><span>-$${tf.toFixed(2)}</span></div>`;
  html+=`<div class="ct-fee-row"><span>Payment processing</span><span>-$${pf.toFixed(2)}</span></div>`;
  if(taxF>0)html+=`<div class="ct-fee-row"><span>Tax on fees</span><span>-$${taxF.toFixed(2)}</span></div>`;
  html+=`<div class="ct-fee-row"><span>Product cost</span><span>-$${cost.toFixed(2)}</span></div>`;
  if(shipping>0)html+=`<div class="ct-fee-row"><span>Shipping</span><span>-$${shipping.toFixed(2)}</span></div>`;
  document.getElementById('fee-breakdown').innerHTML=html;
  document.getElementById('you-receive').textContent='$'+recv.toFixed(2)+' CAD';
  document.getElementById('net-profit').textContent='$'+profit.toFixed(2)+' CAD';
  document.getElementById('total-fees').textContent='$'+totalF.toFixed(2)+' CAD';
  document.getElementById('profit-margin').textContent=margin.toFixed(1)+'%';
  document.getElementById('fee-results').style.display='block';
}

function setTip(pct,e){
  document.getElementById('tip-range').value=pct;
  document.getElementById('tip-pct-out').textContent=pct+'%';
  if(e&&e.target){
    e.target.closest('.ct-seg').querySelectorAll('.ct-seg-btn').forEach(b=>b.classList.remove('active'));
    e.target.classList.add('active');
  }
  calcSplit();
}

function setTaxIncluded(val){
  taxIncluded=val;
  document.getElementById('tax-yes').classList.toggle('active',val);
  document.getElementById('tax-no').classList.toggle('active',!val);
  calcSplit();
}

function calcSplit(){
  const bill=parseFloat(document.getElementById('bill-amount').value)||0;
  const raw=document.getElementById('tip-province').value;
  const taxRate=raw==='14975'?0.14975:parseFloat(raw)/100;
  const tipPct=parseFloat(document.getElementById('tip-range').value)/100;
  const people=parseInt(document.getElementById('split-range').value);
  let subtotal,tax;
  if(taxIncluded){subtotal=bill/(1+taxRate);tax=bill-subtotal;}
  else{subtotal=bill;tax=bill*taxRate;}
  const tip=subtotal*tipPct,total=subtotal+tax+tip;
  const pp=total/people,ppt=tip/people,pptax=tax/people;
  document.getElementById('split-breakdown').innerHTML=`
    <div class="ct-split-item">
      <div class="ct-split-name">Each of ${people} ${people===1?'person':'people'} pays</div>
      <div class="ct-split-amount">$${pp.toFixed(2)} CAD</div>
      <div class="ct-split-detail">Includes $${pptax.toFixed(2)} tax + $${ppt.toFixed(2)} tip</div>
    </div>
    <div class="ct-fee-row"><span>Subtotal</span><span>$${subtotal.toFixed(2)}</span></div>
    <div class="ct-fee-row"><span>Tax (${(taxRate*100).toFixed(raw==='14975'?3:0)}%)</span><span>$${tax.toFixed(2)}</span></div>
    <div class="ct-fee-row"><span>Tip (${(tipPct*100).toFixed(0)}%)</span><span>$${tip.toFixed(2)}</span></div>
    <div class="ct-fee-total"><span>Total</span><span>$${total.toFixed(2)}</span></div>`;
  document.getElementById('split-results').style.display='block';
}

calcFees();
calcSplit();
</script>
</body>
</html>
