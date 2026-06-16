<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="theme-color" content="#1a2e1a">
<link rel="icon" type="image/png" href="icon.png">
<link rel="apple-touch-icon" href="icon.png">
<link rel="manifest" href="manifest.json">
<title>FRESH — Свежие продукты</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root{
  --ink:#141f14;--ink80:rgba(20,31,20,.8);--ink50:rgba(20,31,20,.5);
  --ink20:rgba(20,31,20,.2);--ink10:rgba(20,31,20,.1);--ink05:rgba(20,31,20,.05);
  --cream:#FAF7F2;--cream2:#F2EDE4;--parch:#EDE6D6;
  --forest:#1E4D22;--forest2:#2E6E34;--leaf:#3A9142;--leafp:#EAF2EA;--leafl:#D4E9D5;
  --amber:#C8702A;--amberp:#FFF0E4;--red:#B5290D;--white:#fff;
  --f-serif:'Cormorant Garamond',Georgia,serif;--f-sans:'Inter',system-ui,sans-serif;
  --nav-h:68px;--ease:cubic-bezier(.4,0,.2,1);--ease-out:cubic-bezier(0,0,.2,1);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0;-webkit-tap-highlight-color:transparent;-webkit-font-smoothing:antialiased}
html,body{height:100%;font-family:var(--f-sans);color:var(--ink)}
body{background:#0d160d;display:flex;justify-content:center;align-items:center;min-height:100dvh}
#app{width:100%;max-width:430px;height:100dvh;max-height:900px;background:var(--cream);border-radius:32px;box-shadow:0 40px 100px rgba(0,0,0,.55);display:flex;flex-direction:column;overflow:hidden;position:relative}
@media(max-width:480px){#app{border-radius:0;max-height:none}body{background:var(--cream);align-items:flex-start}}
.screens{flex:1;position:relative;overflow:hidden}
.scr{position:absolute;inset:0;overflow-y:auto;overflow-x:hidden;-webkit-overflow-scrolling:touch;background:var(--cream);padding:20px 16px calc(var(--nav-h) + 20px);opacity:0;pointer-events:none;transform:translateX(28px);transition:transform .35s var(--ease),opacity .25s var(--ease);will-change:transform,opacity;scrollbar-width:thin;scrollbar-color:var(--ink20) transparent}
.scr::-webkit-scrollbar{width:3px}.scr::-webkit-scrollbar-thumb{background:var(--ink20);border-radius:2px}
.scr.active{opacity:1;pointer-events:all;transform:translateX(0)}
.scr.prev{opacity:0;transform:translateX(-28px);pointer-events:none}
#nav{height:var(--nav-h);background:var(--white);border-top:1px solid var(--ink10);display:flex;align-items:center;padding:0 4px env(safe-area-inset-bottom,0);flex-shrink:0;box-shadow:0 -1px 0 var(--ink05)}
.ni{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;padding:8px 4px;border:none;background:none;cursor:pointer;color:var(--ink50);font-family:var(--f-sans);font-size:10px;font-weight:500;letter-spacing:.03em;text-transform:uppercase;position:relative;transition:color .15s}
.ni.on{color:var(--forest)}.ni-ico{width:26px;height:26px;display:flex;align-items:center;justify-content:center;border-radius:8px;font-size:17px;transition:background .15s;position:relative}
.ni.on .ni-ico{background:var(--leafp)}
.nbadge{position:absolute;top:-4px;right:-8px;background:var(--amber);color:#fff;border-radius:100px;min-width:17px;height:17px;padding:0 4px;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center;line-height:1;box-shadow:0 1px 4px rgba(200,112,42,.4)}
.logo{font-family:var(--f-serif);font-size:28px;font-weight:500;letter-spacing:-.01em;color:var(--ink);line-height:1}
.logo em{color:var(--leaf);font-style:normal}
.stitle{font-family:var(--f-serif);font-size:24px;font-weight:400;letter-spacing:-.01em;color:var(--ink);margin-bottom:16px}
.slabel{font-size:11px;font-weight:600;letter-spacing:.08em;text-transform:uppercase;color:var(--ink50);margin-bottom:8px}
.card{background:var(--white);border-radius:20px;box-shadow:0 2px 8px rgba(20,31,20,.07),0 0 0 1px rgba(20,31,20,.04);padding:16px;margin-bottom:12px}
.card-flat{background:var(--white);border-radius:20px;border:1px solid var(--ink10);padding:16px;margin-bottom:12px}
.card-tint{background:var(--leafp);border-radius:20px;border:1px solid var(--leafl);padding:16px;margin-bottom:12px}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;width:100%;padding:14px 20px;border-radius:100px;font-family:var(--f-sans);font-size:14px;font-weight:500;letter-spacing:.01em;cursor:pointer;border:none;transition:transform .15s var(--ease),box-shadow .15s var(--ease),background .15s var(--ease);-webkit-user-select:none;user-select:none}
.btn:active{transform:scale(.97)}
.btn-p{background:var(--forest);color:#fff;box-shadow:0 4px 16px rgba(30,77,34,.28)}
.btn-p:hover{background:var(--forest2)}
.btn-o{background:transparent;color:var(--forest);border:1.5px solid var(--forest);box-shadow:none}
.btn-o:hover{background:var(--leafp)}
.btn-g{background:var(--ink05);color:var(--ink80);box-shadow:none}
.btn-g:hover{background:var(--ink10)}
.btn-d{background:var(--red);color:#fff;box-shadow:0 4px 12px rgba(181,41,13,.22)}
.btn-sm{padding:8px 14px;font-size:13px;width:auto}
.btn-xs{padding:6px 10px;font-size:12px;width:auto}
.inp{width:100%;padding:12px 14px;border:1.5px solid var(--ink20);border-radius:100px;font-family:var(--f-sans);font-size:14px;color:var(--ink);background:var(--white);outline:none;transition:border-color .15s,box-shadow .15s;-webkit-appearance:none;margin-bottom:8px}
.inp:focus{border-color:var(--forest);box-shadow:0 0 0 3px rgba(30,77,34,.1)}
.inp::placeholder{color:var(--ink50)}
select.inp{cursor:pointer;appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='8'%3E%3Cpath d='M1 1l5 5 5-5' stroke='%23141f14' stroke-opacity='.45' fill='none' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 14px center;padding-right:36px}
.inp-rect{border-radius:12px}
.ilabel{font-size:11px;font-weight:500;color:var(--ink50);letter-spacing:.04em;text-transform:uppercase;display:block;margin-bottom:4px}
.hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:16px}
.chip{background:var(--cream2);border-radius:100px;padding:7px 12px;font-size:13px;font-weight:500;color:var(--ink);cursor:pointer;border:1px solid var(--ink10);white-space:nowrap;transition:background .15s}
.chip:hover{background:var(--parch)}
.srch-row{display:flex;gap:8px;margin-bottom:12px}
.srch-wrap{flex:1;position:relative}.srch-wrap .inp{margin-bottom:0;padding-left:44px}
.srch-ico{position:absolute;left:15px;top:50%;transform:translateY(-50%);font-size:16px;pointer-events:none;opacity:.4}
.flt-btn{width:48px;height:48px;border-radius:14px;background:var(--white);border:1.5px solid var(--ink20);cursor:pointer;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0;color:var(--ink80);transition:all .15s}
.flt-btn:hover,.flt-btn.on{background:var(--leafp);border-color:var(--forest);color:var(--forest)}
.cats{display:flex;gap:8px;overflow-x:auto;padding-bottom:6px;margin-bottom:12px;position:sticky;top:0;z-index:10;background:var(--cream);padding-top:4px;scrollbar-width:none;scroll-behavior:auto}
.cats::-webkit-scrollbar{display:none}
.cpill{flex-shrink:0;display:inline-flex;align-items:center;gap:5px;padding:7px 14px;border-radius:100px;font-size:13px;font-weight:500;background:var(--white);color:var(--ink80);border:1.5px solid var(--ink10);cursor:pointer;white-space:nowrap;box-shadow:0 1px 4px rgba(20,31,20,.06);transition:all .15s}
.cpill.on{background:var(--forest);color:#fff;border-color:var(--forest);box-shadow:0 2px 8px rgba(30,77,34,.22)}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
.pc{background:var(--white);border-radius:20px;box-shadow:0 2px 8px rgba(20,31,20,.07),0 0 0 1px rgba(20,31,20,.04);display:flex;flex-direction:column;cursor:pointer;overflow:hidden;transition:transform .15s,box-shadow .15s}
.pc:active{transform:scale(.97);box-shadow:0 1px 4px rgba(20,31,20,.07)}
.pc-img{width:100%;aspect-ratio:1/1;background:var(--cream2);display:flex;align-items:center;justify-content:center;font-size:50px;overflow:hidden;flex-shrink:0}
.pc-img img{width:100%;height:100%;object-fit:cover}
.pc-body{padding:10px;display:flex;flex-direction:column;flex:1}
.pc-name{font-weight:500;font-size:13px;color:var(--ink);margin-bottom:3px;line-height:1.3}
.pc-desc{font-size:11px;color:var(--ink50);line-height:1.35;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;margin-bottom:6px;min-height:28px}
.pc-price{font-family:var(--f-serif);font-size:16px;font-weight:500;color:var(--forest);margin-bottom:8px}
.qrow{display:flex;align-items:center;gap:4px;margin-top:auto}
.qbtn{width:28px;height:28px;border-radius:50%;background:var(--leafp);border:none;font-size:17px;color:var(--forest);cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;line-height:1;transition:background .15s,transform .1s}
.qbtn:active{transform:scale(.85);background:var(--leafl)}
.qbtn:disabled{opacity:.28;cursor:not-allowed}
.qinp{flex:1;min-width:0;height:28px;border:1.5px solid var(--ink10);border-radius:7px;text-align:center;font-family:var(--f-sans);font-size:12px;font-weight:500;color:var(--ink);background:var(--cream);outline:none;padding:0 2px;transition:border-color .15s}
.qinp:focus{border-color:var(--forest);background:var(--white)}
.qinp::-webkit-outer-spin-button,.qinp::-webkit-inner-spin-button{-webkit-appearance:none}
.qinp[type=number]{-moz-appearance:textfield}
.empty{display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 20px;text-align:center;min-height:220px}
.empty-ico{font-size:50px;margin-bottom:12px;opacity:.55}
.empty-t{font-family:var(--f-serif);font-size:20px;font-weight:400;color:var(--ink);margin-bottom:6px}
.empty-s{font-size:14px;color:var(--ink50);line-height:1.5}
.back-btn{display:inline-flex;align-items:center;gap:8px;background:none;border:none;cursor:pointer;font-family:var(--f-sans);font-size:14px;font-weight:500;color:var(--forest);padding:0;margin-bottom:14px;opacity:.85}
.back-btn:hover{opacity:1}
.det-img{width:100%;aspect-ratio:4/3;border-radius:20px;background:var(--cream2);display:flex;align-items:center;justify-content:center;font-size:80px;overflow:hidden;margin-bottom:16px}
.det-img img{width:100%;height:100%;object-fit:cover}
.det-title{font-family:var(--f-serif);font-size:24px;font-weight:400;color:var(--ink);margin-bottom:6px;line-height:1.2}
.det-price{font-family:var(--f-serif);font-size:26px;font-weight:500;color:var(--forest);margin-bottom:12px}
.badge{background:var(--cream2);border-radius:100px;padding:5px 12px;font-size:12px;font-weight:500;color:var(--ink80);border:1px solid var(--ink10)}
.badge.g{background:var(--leafp);color:var(--forest);border-color:var(--leafl)}
.det-meta{display:flex;align-items:center;gap:8px;flex-wrap:wrap;margin-bottom:12px}
.det-desc{font-size:14px;color:var(--ink80);line-height:1.6;margin-bottom:16px}
.det-qwrap{background:var(--white);border-radius:20px;box-shadow:0 2px 8px rgba(20,31,20,.07);padding:14px;display:flex;align-items:center;gap:12px;margin-bottom:14px}
.qbtn-lg{width:44px;height:44px;border-radius:50%;background:var(--forest);border:none;font-size:22px;color:#fff;cursor:pointer;display:flex;align-items:center;justify-content:center;flex-shrink:0;box-shadow:0 2px 8px rgba(30,77,34,.25);transition:background .15s,transform .1s}
.qbtn-lg:active{transform:scale(.88)}
.qbtn-lg:disabled{background:var(--ink20);box-shadow:none;cursor:not-allowed}
.qinp-lg{flex:1;height:44px;border:1.5px solid var(--ink20);border-radius:12px;text-align:center;font-family:var(--f-serif);font-size:22px;color:var(--ink);background:var(--cream);outline:none;transition:border-color .15s}
.qinp-lg:focus{border-color:var(--forest);background:var(--white)}
.qinp-lg::-webkit-outer-spin-button,.qinp-lg::-webkit-inner-spin-button{-webkit-appearance:none}
.qinp-lg[type=number]{-moz-appearance:textfield}
.visit-row{background:var(--white);border-radius:16px;box-shadow:0 1px 6px rgba(20,31,20,.07);padding:14px 16px;margin-bottom:14px;display:flex;align-items:center;justify-content:space-between}
.visit-row .lbl{font-size:11px;font-weight:500;text-transform:uppercase;letter-spacing:.06em;color:var(--ink50);margin-bottom:3px}
.visit-row .val{font-size:15px;font-weight:500;color:var(--ink)}
.sg{background:var(--white);border-radius:20px;box-shadow:0 2px 8px rgba(20,31,20,.07);margin-bottom:14px;overflow:hidden}
.sg-hdr{padding:14px 16px;border-bottom:1px solid var(--ink05);display:flex;align-items:center;gap:8px}
.sg-hdr-btn{background:none;border:none;cursor:pointer;font-family:var(--f-sans);font-size:15px;font-weight:600;color:var(--forest);display:flex;align-items:center;gap:4px;padding:0}
.citems{padding:0 16px}
.citem{padding:10px 0;border-bottom:1px solid var(--ink05)}
.citem:last-child{border-bottom:none}
.citem-row{display:flex;align-items:flex-start;justify-content:space-between;gap:8px;margin-bottom:8px}
.citem-name{font-size:14px;font-weight:500;color:var(--ink);flex:1;line-height:1.3}
.citem-sum{font-size:14px;font-weight:600;color:var(--ink);white-space:nowrap}
.citem-ctrl{display:flex;align-items:center;justify-content:space-between}
.citem-ctrl .qrow{flex:1}
.rmbtn{background:none;border:none;cursor:pointer;font-size:12px;font-weight:500;color:var(--red);padding:4px 0;font-family:var(--f-sans)}
.ctotals{padding:14px 16px;background:var(--cream)}
.tr{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px}
.tr .tl{font-size:13px;color:var(--ink80)}.tr .tv{font-size:13px;font-weight:500;color:var(--ink)}
.tr.final .tl{font-size:15px;font-weight:600;color:var(--ink)}
.tr.final .tv{font-family:var(--f-serif);font-size:20px;font-weight:500;color:var(--forest)}
.delivery-sel{display:flex;gap:8px;margin-bottom:10px}
.dopt{flex:1;padding:10px;border-radius:12px;border:1.5px solid var(--ink20);text-align:center;cursor:pointer;transition:all .15s;font-size:13px;font-weight:500;color:var(--ink80)}
.dopt.on{background:var(--leafp);border-color:var(--forest);color:var(--forest)}
.prof-hero{background:linear-gradient(145deg,var(--forest) 0%,var(--forest2) 100%);border-radius:20px;padding:20px;margin-bottom:12px;color:#fff;position:relative;overflow:hidden}
.prof-hero::after{content:'';position:absolute;right:-20px;top:-20px;width:120px;height:120px;border-radius:50%;background:rgba(255,255,255,.05)}
.ph-avatar{width:64px;height:64px;border-radius:50%;background:rgba(255,255,255,.15);display:flex;align-items:center;justify-content:center;font-size:26px;margin-bottom:10px;cursor:pointer;overflow:hidden;border:2px solid rgba(255,255,255,.2);position:relative;flex-shrink:0}
.ph-avatar img{width:100%;height:100%;object-fit:cover;border-radius:50%}
.ph-avatar .ph-edit{position:absolute;bottom:0;right:0;width:20px;height:20px;background:rgba(255,255,255,.9);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:10px}
.ph-name{font-family:var(--f-serif);font-size:22px;font-weight:400;margin-bottom:4px}
.ph-phone{font-size:13px;opacity:.7}
.bal-row{background:rgba(255,255,255,.12);border-radius:12px;padding:12px 14px;margin-top:12px;display:flex;align-items:center;justify-content:space-between}
.bal-lbl{font-size:11px;opacity:.65;text-transform:uppercase;letter-spacing:.06em;margin-bottom:3px}
.bal-val{font-family:var(--f-serif);font-size:24px;font-weight:400}
.oc{background:var(--white);border-radius:16px;border:1px solid var(--ink10);padding:14px;margin-bottom:10px}
.oc-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px}
.oc-store{font-weight:600;font-size:14px;color:var(--ink)}
.sbadge{font-size:11px;font-weight:600;padding:4px 10px;border-radius:100px;background:var(--leafp);color:var(--forest);border:1px solid var(--leafl)}
.sbadge.rd{background:var(--amberp);color:var(--amber);border-color:#ffe0b2}
.sbadge.gn{background:#e8f5e9;color:#2e7d32;border-color:#c8e6c9}
.code-chip{background:var(--cream2);border-radius:12px;padding:10px 12px;margin-top:8px;display:flex;align-items:center;justify-content:space-between;border:1px solid var(--ink10)}
.code-chip .cl{font-size:11px;text-transform:uppercase;letter-spacing:.06em;color:var(--ink50);margin-bottom:3px}
.code-chip .cv{font-family:monospace;font-size:21px;font-weight:700;letter-spacing:3px;color:var(--ink)}
.prow{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--ink05)}
.prow:last-child{border-bottom:none}
.pmthumb{width:44px;height:44px;border-radius:10px;background:var(--cream2);display:flex;align-items:center;justify-content:center;font-size:22px;flex-shrink:0;overflow:hidden}
.pmthumb img{width:100%;height:100%;object-fit:cover;border-radius:10px}
.pm-name{font-weight:500;font-size:14px;color:var(--ink)}
.pm-meta{font-size:12px;color:var(--ink50);margin-top:2px}
.pm-acts{display:flex;gap:6px;flex-shrink:0;margin-left:auto}
.stsel{border:1.5px solid var(--ink20);border-radius:100px;padding:6px 26px 6px 12px;font-size:13px;background:var(--white);color:var(--ink);outline:none;font-family:var(--f-sans);cursor:pointer;appearance:none;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='7'%3E%3Cpath d='M1 1l4 4 4-4' stroke='%23141f14' stroke-opacity='.4' fill='none' stroke-width='1.5' stroke-linecap='round'/%3E%3C/svg%3E");background-repeat:no-repeat;background-position:right 10px center}
.cm-hero{background:linear-gradient(145deg,#1a3a1e 0%,var(--forest2) 100%);border-radius:20px;padding:20px;margin-bottom:14px;color:#fff;text-align:center;position:relative;overflow:hidden}
.cm-hero::before{content:'';position:absolute;width:200px;height:200px;border-radius:50%;background:rgba(255,255,255,.04);top:-60px;right:-60px}
.cm-hero .cl{font-size:11px;opacity:.65;text-transform:uppercase;letter-spacing:.08em;margin-bottom:6px}
.cm-hero .ca{font-family:var(--f-serif);font-size:40px;font-weight:400;line-height:1}
.cm-hero .cs{font-size:13px;opacity:.65;margin-top:6px}
.loc-card{background:var(--white);border-radius:16px;border:1px solid var(--ink10);padding:14px;margin-bottom:10px}
.loc-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:6px}
.loc-name{font-weight:600;font-size:14px;color:var(--ink)}
.loc-meta{font-size:12px;color:var(--ink50);margin-bottom:8px;line-height:1.4}
.overlay{position:fixed;inset:0;background:rgba(8,16,8,.58);display:flex;align-items:flex-end;justify-content:center;z-index:400;opacity:0;pointer-events:none;transition:opacity .25s var(--ease);backdrop-filter:blur(4px);-webkit-backdrop-filter:blur(4px)}
.overlay.on{opacity:1;pointer-events:all}
.sheet{background:var(--white);border-radius:28px 28px 0 0;padding:0 16px calc(20px + env(safe-area-inset-bottom,0));width:100%;max-width:430px;max-height:92vh;overflow-y:auto;scrollbar-width:none;transform:translateY(40px);transition:transform .32s var(--ease-out);will-change:transform}
.sheet::-webkit-scrollbar{display:none}
.overlay.on .sheet{transform:translateY(0)}
@media(min-width:481px){.overlay{align-items:center}.sheet{border-radius:28px;max-width:380px;max-height:85vh;padding-bottom:20px}}
.sh-handle{width:36px;height:4px;background:var(--ink20);border-radius:2px;margin:12px auto 18px}
.sh-title{font-family:var(--f-serif);font-size:21px;font-weight:400;color:var(--ink);text-align:center;margin-bottom:16px}
.tab-row{display:flex;background:var(--cream2);border-radius:100px;padding:4px;margin-bottom:14px}
.tbtn{flex:1;padding:8px;border-radius:100px;border:none;background:transparent;font-size:13px;font-weight:500;color:var(--ink50);cursor:pointer;transition:all .15s;font-family:var(--f-sans)}
.tbtn.on{background:var(--white);color:var(--forest);font-weight:600;box-shadow:0 2px 6px rgba(20,31,20,.09)}
.upbox{border:2px dashed var(--ink20);border-radius:14px;padding:16px;text-align:center;cursor:pointer;font-size:14px;color:var(--ink50);margin-bottom:8px;transition:all .15s}
.upbox:hover{border-color:var(--forest);background:var(--leafp)}
.upbox img{display:none;width:80px;height:80px;border-radius:12px;object-fit:cover;margin:8px auto 0}
.pay-methods{display:flex;flex-direction:column;gap:8px;margin-bottom:14px}
.pmo{display:flex;align-items:center;gap:10px;padding:12px;border-radius:14px;border:1.5px solid var(--ink10);cursor:pointer;transition:all .15s;background:var(--white)}
.pmo:hover,.pmo.on{border-color:var(--forest);background:var(--leafp)}
.pmo-ico{font-size:24px;flex-shrink:0}
.pmo-info{flex:1}.pmo-name{font-weight:500;font-size:13px;color:var(--ink)}
.pmo-sub{font-size:11px;color:var(--ink50);margin-top:2px}
.pmo-chk{width:18px;height:18px;border-radius:50%;border:2px solid var(--ink20);flex-shrink:0;display:flex;align-items:center;justify-content:center;transition:all .15s}
.pmo.on .pmo-chk{background:var(--forest);border-color:var(--forest)}
.pmo.on .pmo-chk::after{content:'\2713';color:#fff;font-size:10px;font-weight:700}
.card-form{display:none}.card-form.vis{display:block}
.crow{display:flex;gap:10px}.crow>div{flex:1}
.yk-sec{display:flex;align-items:center;justify-content:center;gap:6px;font-size:12px;color:var(--ink50);margin-top:8px}
.yk-badge{background:var(--leafp);border:1px solid var(--leafl);border-radius:8px;padding:8px 12px;font-size:12px;color:var(--forest);font-weight:500;margin-bottom:10px;display:flex;align-items:center;gap:6px}
.agree-row{display:flex;align-items:flex-start;gap:8px;margin-bottom:10px}
.agree-cb{width:18px;height:18px;border-radius:4px;border:2px solid var(--ink20);cursor:pointer;flex-shrink:0;display:flex;align-items:center;justify-content:center;background:var(--white);transition:all .15s;margin-top:1px}
.agree-cb.on{background:var(--forest);border-color:var(--forest)}
.agree-cb.on::after{content:'\2713';color:#fff;font-size:10px;font-weight:700}
.agree-text{font-size:12px;color:var(--ink80);line-height:1.4}
.agree-text a{color:var(--forest);text-decoration:underline;cursor:pointer}
.toast{position:fixed;bottom:calc(var(--nav-h) + 14px);left:50%;transform:translateX(-50%);background:var(--ink);color:#fff;padding:12px 22px;border-radius:100px;font-size:14px;font-weight:400;z-index:600;pointer-events:none;white-space:nowrap;box-shadow:0 8px 24px rgba(0,0,0,.22);animation:ti .28s var(--ease-out),tto .28s 2.1s var(--ease) forwards}
@keyframes ti{from{opacity:0;transform:translateX(-50%) translateY(10px)}}
@keyframes tto{to{opacity:0;transform:translateX(-50%) translateY(-6px)}}
#welcome{position:absolute;inset:0;z-index:200;background:var(--forest);display:flex;flex-direction:column;align-items:center;justify-content:center;padding:40px 32px;text-align:center;transition:opacity .55s var(--ease),transform .55s var(--ease)}
#welcome.hide{opacity:0;transform:scale(1.03);pointer-events:none}
#welcome .wleaf{font-size:76px;margin-bottom:24px;filter:drop-shadow(0 8px 20px rgba(0,0,0,.25))}
#welcome h1{font-family:var(--f-serif);font-size:44px;font-weight:400;color:#fff;margin-bottom:12px;letter-spacing:-.01em}
#welcome .wsub{font-size:16px;color:rgba(255,255,255,.72);line-height:1.6;margin-bottom:36px;max-width:280px}
#welcome .wbtn{background:#fff;color:var(--forest);border:none;padding:16px 40px;border-radius:100px;font-size:15px;font-weight:600;cursor:pointer;font-family:var(--f-sans);box-shadow:0 8px 24px rgba(0,0,0,.2);transition:transform .15s}
#welcome .wbtn:active{transform:scale(.96)}
.del-prof-card{background:var(--white);border-radius:16px;border:1px solid var(--ink10);padding:14px;margin-bottom:10px}
.row{display:flex;align-items:center;justify-content:space-between}
.row.gap{gap:8px}
.divider{height:1px;background:var(--ink10);margin:10px 0}
.mt4{margin-top:4px}.mt8{margin-top:8px}.mt12{margin-top:12px}.mt16{margin-top:16px}.mt20{margin-top:20px}
.mb4{margin-bottom:4px}.mb8{margin-bottom:8px}.mb12{margin-bottom:12px}.mb16{margin-bottom:16px}
.fs12{font-size:12px}.fs13{font-size:13px}.fs14{font-size:14px}
.fw5{font-weight:500}.fw6{font-weight:600}
.cmid{color:var(--ink50)}.cfor{color:var(--forest)}
.legal-doc{padding:8px 0;font-size:13px;line-height:1.6;color:var(--ink80);max-height:55vh;overflow-y:auto}
.legal-doc h3{font-family:var(--f-serif);font-size:17px;margin:14px 0 6px}
.legal-doc p{margin-bottom:8px}
.seller-order-card{background:var(--white);border-radius:16px;border:1px solid var(--ink10);padding:14px;margin-bottom:10px}
.hint-box{background:var(--amberp);border:1px solid #ffe0b2;border-radius:12px;padding:10px 12px;font-size:12px;color:var(--amber);margin-bottom:8px;line-height:1.4}
</style>
</head>
<body>
<div id="app">
  <div class="screens">
    <div class="scr" id="s-main"></div>
    <div class="scr" id="s-product"></div>
    <div class="scr" id="s-cart"></div>
    <div class="scr" id="s-profile"></div>
    <div class="scr" id="s-seller"></div>
    <div class="scr" id="s-courier"></div>
    <div class="scr" id="s-admin"></div>
  </div>
  <nav id="nav"></nav>
  <div id="welcome">
    <div class="wleaf">🌿</div>
    <h1>FRESH</h1>
    <p class="wsub">Свежее с рынка — прямо к вам. Выбирайте, заказывайте, забирайте.</p>
    <button class="wbtn" id="wStart">Начать</button>
  </div>
</div>
<script>
(function(){
'use strict';
const SK='fresh_v3';
const ADMIN_PHONE='admin',ADMIN_PASS='admin';
const DEMO={
  districts:[
    {id:'d1',name:'Сосново',address:'Ленинградская обл., пос. Сосново'},
    {id:'d2',name:'Приозерск',address:'Ленинградская обл., г. Приозерск'}
  ],
  stores:[
    {id:'s1',districtId:'d1',name:'Ферма Петровых',logo:'🥩',owner:'Иван Петров',phone:'+7 911 111-11-11',approved:true,desc:'Домашнее мясо и птица. Работаем с 2010 года.',address:'Ряд А, место 5'},
    {id:'s2',districtId:'d1',name:'Молочный рай',logo:'🥛',owner:'Мария Сидорова',phone:'+7 911 222-22-22',approved:true,desc:'Цельное молоко, творог, сметана от своей коровы.',address:'Ряд Б, место 2'},
    {id:'s3',districtId:'d1',name:'Зелёный сад',logo:'🥬',owner:'Олег Кузнецов',phone:'+7 911 333-33-33',approved:true,desc:'Сезонные овощи и зелень, без химии.',address:'Ряд В, место 7'},
    {id:'s4',districtId:'d2',name:'Рыбный двор',logo:'🐟',owner:'Степан Рыбников',phone:'+7 911 444-44-44',approved:true,desc:'Свежая рыба из Ладоги.',address:'Рынок Приозерск, место 3'}
  ],
  users:[{id:'admin1',role:'admin',name:'Администратор',phone:ADMIN_PHONE,password:ADMIN_PASS,email:'admin@fresh.ru',balance:0,photo:null}],
  sellerUsers:[
    {id:'sel1',role:'seller',name:'Иван Петров',phone:'petrov',password:'1234',email:'',balance:0,storeId:'s1',photo:null},
    {id:'sel2',role:'seller',name:'Мария Сидорова',phone:'sidorova',password:'1234',email:'',balance:0,storeId:'s2',photo:null},
    {id:'sel3',role:'seller',name:'Олег Кузнецов',phone:'kuznetsov',password:'1234',email:'',balance:0,storeId:'s3',photo:null},
    {id:'sel4',role:'seller',name:'Степан Рыбников',phone:'rybnikov',password:'1234',email:'',balance:0,storeId:'s4',photo:null}
  ],
  products:[
    {id:'p1',storeId:'s1',name:'Говядина (вырезка)',cat:'Мясо',price:680,unit:'weight',stock:15,img:'🥩',desc:'Охлаждённая, 1 сорт, без кости. Продаётся на развес — минимум 0.1 кг.'},
    {id:'p2',storeId:'s1',name:'Куриное филе',cat:'Мясо',price:320,unit:'weight',stock:20,img:'🍗',desc:'Домашняя курица, без ГМО'},
    {id:'p3',storeId:'s1',name:'Свинина (шея)',cat:'Мясо',price:450,unit:'weight',stock:10,img:'🥓',desc:'Отлично для шашлыка'},
    {id:'p4',storeId:'s2',name:'Молоко цельное',cat:'Молочка',price:90,unit:'weight',stock:50,img:'🥛',desc:'Жирность 3.8%, пастеризованное'},
    {id:'p5',storeId:'s2',name:'Творог домашний',cat:'Молочка',price:280,unit:'weight',stock:8,img:'🍦',desc:'Зернистый, жирность 9%'},
    {id:'p6',storeId:'s2',name:'Сметана 25%',cat:'Молочка',price:350,unit:'weight',stock:6,img:'🥣',desc:'Густая, натуральная'},
    {id:'p7',storeId:'s3',name:'Помидоры',cat:'Овощи',price:180,unit:'weight',stock:30,img:'🍅',desc:'Грунтовые, сорт Бычье сердце'},
    {id:'p8',storeId:'s3',name:'Огурцы',cat:'Овощи',price:120,unit:'weight',stock:25,img:'🥒',desc:'Хрустящие, тепличные'},
    {id:'p9',storeId:'s3',name:'Рассада томатов',cat:'Рассада',price:60,unit:'piece',stock:40,img:'🌱',desc:'Сорт Черри, высота 20 см'},
    {id:'p10',storeId:'s3',name:'Клубника',cat:'Фрукты',price:380,unit:'weight',stock:12,img:'🍓',desc:'Садовая, крупная, сладкая'},
    {id:'p11',storeId:'s4',name:'Судак свежий',cat:'Рыба',price:420,unit:'weight',stock:18,img:'🐟',desc:'Выловлен сегодня утром, Ладожское озеро'}
  ]
};
function defState(){
  const s={districts:JSON.parse(JSON.stringify(DEMO.districts)),stores:JSON.parse(JSON.stringify(DEMO.stores)),users:JSON.parse(JSON.stringify(DEMO.users)),products:JSON.parse(JSON.stringify(DEMO.products)),orders:[],couriers:[],cart:[],session:null,visitTime:null,adminCommission:0,courierCommission:0};
  s.users=s.users.concat(JSON.parse(JSON.stringify(DEMO.sellerUsers)));return s;
}
function load(){try{const r=localStorage.getItem(SK);return r?JSON.parse(r):null;}catch(e){return null;}}
function save(){try{localStorage.setItem(SK,JSON.stringify(S));}catch(e){}}
let S=load()||defState();
if(!S.districts)S.districts=JSON.parse(JSON.stringify(DEMO.districts));
if(!S.couriers)S.couriers=[];
if(!S.courierCommission)S.courierCommission=0;
const $=id=>document.getElementById(id);
const genId=()=>'i'+Math.random().toString(36).slice(2,10);
const genCode=()=>String(Math.floor(100000+Math.random()*900000));
const r1=n=>Math.round(n*10)/10;
const r0=n=>Math.round(n);
const esc=s=>String(s||'').replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;').replace(/'/g,'&#39;');
const cu=()=>S.users.find(u=>u.id===S.session)||null;
const gs=id=>S.stores.find(s=>s.id===id);
const gp=id=>S.products.find(p=>p.id===id);
const gd=id=>S.districts.find(d=>d.id===id);
const cq=pid=>{const i=S.cart.find(c=>c.productId===pid);return i?i.quantity:0;};
// Вот здесь правка: теперь значок показывает число позиций, а не сумму веса
const cartCount=()=>S.cart.length;
const storeItems=sid=>S.cart.filter(c=>c.storeId===sid);
const storeSubtotal=sid=>{let t=0;storeItems(sid).forEach(i=>t+=i.quantity*i.price);return r0(t);};
const fmtQty=(q,u)=>u==='weight'?r1(q).toFixed(1)+' кг':r0(q)+' шт';
const fmtPrice=(p,u)=>p+' ₽/'+(u==='weight'?'кг':'шт');

/* ── CATEGORIES — FIX 1: added Готовая еда ── */
const CATS=[{n:'Все',i:'🛒'},{n:'Мясо',i:'🥩'},{n:'Овощи',i:'🥬'},{n:'Фрукты',i:'🍎'},{n:'Молочка',i:'🥛'},{n:'Рассада',i:'🌱'},{n:'Рыба',i:'🐟'},{n:'Готовая еда',i:'🍱'}];

/* ── CART UPDATE — fixed: step 0.1 or 1, never display stock ── */
function cartUpdate(pid,delta,exactVal){
  const product=gp(pid);if(!product)return;
  const step=product.unit==='weight'?0.1:1;
  const existing=S.cart.find(c=>c.productId===pid);
  let nq;
  if(exactVal!==undefined){
    nq=parseFloat(String(exactVal).replace(',','.'));
    if(isNaN(nq)||nq<0)nq=0;
  }else{
    const cur=existing?existing.quantity:0;
    nq=r1(cur+delta*step);
  }
  if(product.unit==='weight')nq=r1(Math.max(0,nq));
  else nq=Math.max(0,Math.floor(nq));
  if(nq>product.stock)nq=product.unit==='weight'?r1(product.stock):Math.floor(product.stock);
  if(nq<=0){S.cart=S.cart.filter(c=>c.productId!==pid);}
  else if(existing){existing.quantity=nq;}
  else{const store=gs(product.storeId);S.cart.push({productId:product.id,storeId:product.storeId,name:product.name,unit:product.unit,price:product.price,quantity:nq,storeName:store?store.name:''});}
  save();
}

let CS='main',detailId=null,activeCat='Все',searchQ='',fltStore='',fltSort='none';

function goTo(scr){
  const user=cu();
  if((scr==='cart'||scr==='profile')&&!user){openModal(loginModal());return;}
  if(scr==='cart'&&user&&user.role!=='customer'){toast('Корзина доступна только покупателям');return;}
  const prev=$('s-'+CS),next=$('s-'+scr);
  if(prev&&next&&prev!==next){prev.classList.remove('active');prev.classList.add('prev');next.classList.remove('prev');next.classList.add('active');setTimeout(()=>prev.classList.remove('prev'),380);}
  CS=scr;render();
}

/* ── RENDER — FIX 2: preserve cats scroll position ── */
function render(){
  renderNav();
  const fns={main:rMain,product:rProduct,cart:rCart,profile:rProfile,seller:rSeller,courier:rCourier,admin:rAdmin};
  const el=$('s-'+CS);
  if(el&&fns[CS]){
    const oldCats=el.querySelector('.cats');
    const savedScroll=oldCats?oldCats.scrollLeft:0;
    el.innerHTML=fns[CS]();
    el.classList.add('active');
    const newCats=el.querySelector('.cats');
    if(newCats&&savedScroll>0)newCats.scrollLeft=savedScroll;
    bindScreen();
  }
  save();
}

function renderNav(){
  const user=cu(),role=user?user.role:'guest',cnt=cartCount();
  const badge=cnt>0?`<span class="nbadge">${cnt}</span>`:'';
  let items=[{id:'main',l:'Каталог',i:'🏠'},{id:'cart',l:'Корзина',i:'🧺',b:badge},{id:'profile',l:'Профиль',i:'👤'}];
  if(role==='seller')items.push({id:'seller',l:'Магазин',i:'📊'});
  if(role==='courier')items.push({id:'courier',l:'Доставки',i:'🚴'});
  if(role==='admin')items.push({id:'admin',l:'Панель',i:'⚙️'});
  $('nav').innerHTML=items.map(n=>`<button class="ni ${CS===n.id?'on':''}" data-s="${n.id}"><span class="ni-ico">${n.i}${n.b||''}</span><span>${n.l}</span></button>`).join('');
  $('nav').querySelectorAll('.ni').forEach(b=>b.onclick=()=>goTo(b.dataset.s));
}

function rMain(){
  const user=cu();
  let prods=S.products.filter(p=>{const st=gs(p.storeId);return st&&st.approved&&p.stock>0;});
  if(activeCat!=='Все')prods=prods.filter(p=>p.cat===activeCat);
  if(searchQ)prods=prods.filter(p=>p.name.toLowerCase().includes(searchQ.toLowerCase()));
  if(fltStore)prods=prods.filter(p=>p.storeId===fltStore);
  if(fltSort==='asc')prods.sort((a,b)=>a.price-b.price);
  if(fltSort==='desc')prods.sort((a,b)=>b.price-a.price);
  const cats=CATS.map(c=>`<button class="cpill ${activeCat===c.n?'on':''}" data-cat="${c.n}">${c.i} ${c.n}</button>`).join('');
  const hasFlt=fltStore||fltSort!=='none';
  const cards=prods.map(p=>{
    const q=cq(p.id);
    const img=p.img&&p.img.startsWith('data:')?`<img src="${p.img}" alt="">`:`<span>${p.img}</span>`;
    const qDisplay=p.unit==='weight'?r1(q).toFixed(1):String(r0(q));
    return `<div class="pc" data-action="openProduct" data-pid="${p.id}">
      <div class="pc-img">${img}</div>
      <div class="pc-body">
        <div class="pc-name">${esc(p.name)}</div>
        <div class="pc-desc">${esc(p.desc||'')}</div>
        <div class="pc-price">${fmtPrice(p.price,p.unit)}</div>
        <div class="qrow" onclick="event.stopPropagation()">
          <button class="qbtn" data-action="qm" data-pid="${p.id}" ${q<=0?'disabled':''}>−</button>
          <input class="qinp" type="number" data-action="qi" data-pid="${p.id}" value="${qDisplay}" min="0" step="${p.unit==='weight'?'0.1':'1'}">
          <button class="qbtn" data-action="qp" data-pid="${p.id}">+</button>
        </div>
      </div>
    </div>`;
  }).join('');
  return `<div class="hdr"><div class="logo">🌿 <em>FRESH</em></div><div class="chip" id="userChip">${user?user.name:'Войти'}</div></div>
  <div class="srch-row"><div class="srch-wrap"><span class="srch-ico">🔍</span><input class="inp" id="searchInp" type="text" placeholder="Найти продукты..." value="${esc(searchQ)}"></div><button class="flt-btn ${hasFlt?'on':''}" id="fltBtn">⚙️</button></div>
  <div class="cats">${cats}</div>
  ${prods.length?`<div class="grid2">${cards}</div>`:`<div class="empty"><div class="empty-ico">🔍</div><div class="empty-t">Ничего не найдено</div><p class="empty-s">Попробуйте другую категорию или запрос</p></div>`}`;
}

function rProduct(){
  const p=gp(detailId);
  if(!p)return`<div class="empty"><div class="empty-ico">📦</div><div class="empty-t">Товар не найден</div></div>`;
  const st=gs(p.storeId);const q=cq(p.id);
  const img=p.img&&p.img.startsWith('data:')?`<img src="${p.img}" alt="">`:`<span>${p.img}</span>`;
  const qDisplay=p.unit==='weight'?r1(q).toFixed(1):String(r0(q));
  const weightHint=p.unit==='weight'?`<div class="hint-box">⚖️ Весовой товар — выберите нужное количество кг. Шаг: 0.1 кг</div>`:'';
  return `<button class="back-btn" data-action="goBack">← Назад</button>
  <div class="det-img">${img}</div>
  <div class="det-meta"><span class="badge g">${p.cat}</span><span class="badge">${esc(st?st.name:'')}</span></div>
  <div class="det-title">${esc(p.name)}</div>
  <div class="det-price">${fmtPrice(p.price,p.unit)}</div>
  <div class="det-desc">${esc(p.desc||'')}</div>
  ${weightHint}
  <div class="det-qwrap">
    <button class="qbtn-lg" data-action="qm" data-pid="${p.id}" ${q<=0?'disabled':''}>−</button>
    <input class="qinp-lg" type="number" data-action="qi" data-pid="${p.id}" value="${qDisplay}" min="0" step="${p.unit==='weight'?'0.1':'1'}">
    <button class="qbtn-lg" data-action="qp" data-pid="${p.id}">+</button>
  </div>
  ${q>0?`<div class="fs13 cmid" style="text-align:center;margin-bottom:12px;">В корзине: ${fmtQty(q,p.unit)} · ${r0(q*p.price)} ₽</div>`:''}`;
}

function rCart(){
  if(!S.cart.length)return`<div class="stitle">Корзина</div><div class="empty"><div class="empty-ico">🧺</div><div class="empty-t">Корзина пуста</div><p class="empty-s">Добавьте товары из каталога</p></div>`;
  const grp={};S.cart.forEach(i=>{if(!grp[i.storeId])grp[i.storeId]=[];grp[i.storeId].push(i);});
  const visitHtml=`<div class="visit-row"><div><div class="lbl">Время визита</div><div class="val">${S.visitTime||'Не выбрано'}</div></div><button class="btn btn-xs btn-o" data-action="setVisit">Изменить</button></div>`;
  const groups=Object.entries(grp).map(([sid,items])=>{
    const st=gs(sid);const sub=storeSubtotal(sid);const comm=r0(sub*0.05);const total=sub+comm;
    const itemsHtml=items.map(it=>{
      const itTotal=r0(it.quantity*it.price);const step=it.unit==='weight'?'0.1':'1';
      const dq=it.unit==='weight'?r1(it.quantity).toFixed(1):String(r0(it.quantity));
      return `<div class="citem">
        <div class="citem-row"><div class="citem-name">${esc(it.name)}</div><div class="citem-sum">${itTotal} ₽</div></div>
        <div class="citem-ctrl">
          <div class="qrow"><button class="qbtn" data-action="qm" data-pid="${it.productId}">−</button>
          <input class="qinp" type="number" data-action="qi" data-pid="${it.productId}" value="${dq}" min="0" step="${step}">
          <button class="qbtn" data-action="qp" data-pid="${it.productId}">+</button></div>
          <span class="fs12 cmid" style="margin:0 8px;">${fmtQty(it.quantity,it.unit)}</span>
          <button class="rmbtn" data-action="rmItem" data-pid="${it.productId}">Удалить</button>
        </div>
      </div>`;
    }).join('');
    return `<div class="sg">
      <div class="sg-hdr"><button class="sg-hdr-btn" data-action="storeInfo" data-sid="${sid}">${st?st.logo:'🏪'} ${esc(st?st.name:'')} ›</button></div>
      <div class="citems">${itemsHtml}</div>
      <div class="ctotals">
        <div class="tr"><span class="tl">Сумма заказа</span><span class="tv">${sub} ₽</span></div>
        <div class="tr"><span class="tl cmid">Комиссия сервиса 5%</span><span class="tv cmid">${comm} ₽</span></div>
        <div style="height:1px;background:var(--ink10);margin:6px 0;"></div>
        <div class="tr final"><span class="tl">Итого</span><span class="tv">${total} ₽</span></div>
        <div style="margin-top:14px;">
          <div class="delivery-sel" id="dsel-${sid}">
            <div class="dopt on" data-dtype="pickup" data-sid="${sid}">🏪 Самовывоз</div>
            <div class="dopt" data-dtype="delivery" data-sid="${sid}">🚴 Доставка</div>
          </div>
          <div id="daddr-${sid}" style="display:none;">
            <input class="inp inp-rect" placeholder="Ваш адрес доставки" id="addr-${sid}" style="border-radius:12px;">
            <div class="fs12 cmid mb8">1 км — 300 ₽, каждый следующий — +75 ₽</div>
          </div>
          <button class="btn btn-p" data-action="pay" data-sid="${sid}">💳 Оплатить</button>
        </div>
      </div>
    </div>`;
  }).join('');
  return `<div class="stitle">Корзина</div>${visitHtml}${groups}`;
}

function rProfile(){
  const user=cu();
  if(!user)return`<div class="empty"><div class="empty-ico">👤</div><div class="empty-t">Вы не авторизованы</div><p class="empty-s">Войдите, чтобы видеть профиль</p><br><button class="btn btn-p" style="max-width:200px;margin:0 auto;" data-action="doLogin">Войти</button></div>`;
  const orders=S.orders.filter(o=>o.customerId===user.id).slice().reverse();
  const avatar=user.photo?`<img src="${user.photo}" alt="">`:'👤';
  const orderHtml=orders.length?orders.map(o=>{
    const sc=o.status==='Выдан'?'gn':o.status==='Готов'?'rd':'';
    const dtype=o.deliveryType==='delivery'?'🚴 Доставка':'🏪 Самовывоз';
    return `<div class="oc"><div class="oc-hdr"><span class="oc-store">${esc(o.storeName)}</span><span class="sbadge ${sc}">${o.status}</span></div>
      <div class="fs13 cmid mb8">${o.items.map(i=>esc(i.name)).join(', ')}</div>
      <div class="row"><div class="fs13 fw5">${o.total} ₽</div><div class="fs12 cmid">${dtype} · ${o.visitTime||'—'}</div></div>
      <div class="code-chip"><div><div class="cl">Код выдачи</div><div class="cv">${o.orderCode}</div></div><span style="font-size:20px;">🎫</span></div>
    </div>`;
  }).join(''):`<div class="empty-s" style="text-align:center;padding:20px;">Заказов пока нет</div>`;
  return `<div class="stitle">Профиль</div>
  <div class="prof-hero">
    <div style="display:flex;align-items:center;gap:14px;">
      <div class="ph-avatar" id="avatarWrap" data-action="changeAvatar">${avatar}<div class="ph-edit">✏️</div><input type="file" id="avatarFile" accept="image/*" style="display:none;"></div>
      <div><div class="ph-name">${esc(user.name)}</div><div class="ph-phone">${esc(user.phone||'')}</div></div>
    </div>
    <div class="bal-row"><div><div class="bal-lbl">Баланс</div><div class="bal-val">${user.balance||0} ₽</div></div>
      <button class="btn btn-sm" style="background:rgba(255,255,255,.15);color:#fff;box-shadow:none;width:auto;" data-action="topUp">+ Пополнить</button>
    </div>
  </div>
  <div class="slabel mt16">История заказов</div>${orderHtml}
  <div class="mt20"><button class="btn btn-g" data-action="logout">Выйти из аккаунта</button></div>`;
}

function rSeller(){
  const user=cu();
  if(!user||user.role!=='seller')return`<div class="empty"><div class="empty-ico">🔒</div><div class="empty-t">Нет доступа</div></div>`;
  const store=S.stores.find(s=>s.id===user.storeId);
  if(!store)return`<div class="empty"><div class="empty-ico">🏪</div><div class="empty-t">Магазин не найден</div></div>`;
  if(!store.approved)return`<div class="stitle">${esc(store.name)}</div><div class="card" style="text-align:center;padding:32px;"><div style="font-size:48px;margin-bottom:12px;">⏳</div><p style="color:var(--ink50);">Магазин ожидает одобрения администратора</p></div>`;
  const prods=S.products.filter(p=>p.storeId===store.id);
  const orders=S.orders.filter(o=>o.storeId===store.id).slice().reverse();
  const pl=prods.length?prods.map(p=>{
    const img=p.img&&p.img.startsWith('data:')?`<img src="${p.img}" alt="">`:`<span style="font-size:22px;">${p.img}</span>`;
    const oos=p.stock<=0;
    return `<div class="prow" style="${oos?'opacity:.5':''}">
      <div class="pmthumb">${img}</div>
      <div style="flex:1;min-width:0;"><div class="pm-name">${esc(p.name)}</div>
        <div class="pm-meta">${fmtPrice(p.price,p.unit)} · ${oos?'<span style="color:var(--red)">Нет в наличии</span>':fmtQty(p.stock,p.unit)+' остаток'}</div>
      </div>
      <div class="pm-acts">
        <button class="btn btn-xs btn-o" data-action="editStock" data-pid="${p.id}">✏️</button>
        <button class="btn btn-xs btn-d" data-action="delProd" data-pid="${p.id}">🗑</button>
      </div>
    </div>`;
  }).join(''):`<div style="padding:20px;text-align:center;color:var(--ink50);">Товаров нет</div>`;
  const ol=orders.length?orders.map(o=>`<div class="seller-order-card">
    <div class="row mb8"><span class="fw6 fs14">Заказ #${o.id.slice(-4).toUpperCase()}</span>
      <select class="stsel" data-action="chStatus" data-oid="${o.id}">
        ${['Принят','Собирается','Готов','Выдан'].map(s=>`<option ${o.status===s?'selected':''}>${s}</option>`).join('')}
      </select></div>
    <div class="fs13 cmid mb4">${o.items.map(i=>esc(i.name)+' '+fmtQty(i.quantity,i.unit)).join(', ')}</div>
    <div class="fs13 cmid">Сумма: ${o.subtotal} ₽ · ${o.deliveryType==='delivery'?'Доставка':'Самовывоз'} · ${o.visitTime||'—'}</div>
    <div class="code-chip" style="margin-top:10px;"><div><div class="cl">Код покупателя</div><div class="cv">${o.orderCode}</div></div></div>
  </div>`).join(''):`<div style="padding:20px;text-align:center;color:var(--ink50);">Заказов нет</div>`;
  const dist=gd(store.districtId);
  return `<div class="stitle">${esc(store.logo)} ${esc(store.name)}</div>
  <div class="card-flat mb12">
    <div class="fs13 cmid">${esc(store.desc||'—')}</div>
    <div class="fs13 cmid mt4">📍 ${esc(store.address||'—')} ${dist?'· '+esc(dist.name):''}</div>
    <button class="btn btn-sm btn-o mt12" data-action="editStore">Редактировать профиль</button>
  </div>
  <div class="row mb12"><div class="slabel" style="margin:0;">Товары</div>
    <div style="display:flex;gap:8px;">
      <button class="btn btn-xs btn-o" data-action="offlineSale">📴 Офлайн</button>
      <button class="btn btn-xs btn-p" data-action="addProd">+ Добавить</button>
    </div></div>
  <div class="hint-box">💡 Товары с нулевым остатком скрыты в каталоге. Обновляйте остаток после продаж.</div>
  <div class="card-flat" style="padding:8px 14px;">${pl}</div>
  <div class="slabel mt20">Заказы</div>${ol}`;
}

function rCourier(){
  const user=cu();
  if(!user||user.role!=='courier')return`<div class="empty"><div class="empty-ico">🔒</div><div class="empty-t">Нет доступа</div></div>`;
  const courier=S.couriers.find(c=>c.userId===user.id);
  if(!courier||!courier.approved)return`<div class="stitle">Доставки</div><div class="card" style="text-align:center;padding:32px;"><div style="font-size:48px;margin-bottom:12px;">⏳</div><p style="color:var(--ink50);">Ваш профиль ожидает одобрения администратора</p></div>`;
  const myDeliveries=S.orders.filter(o=>o.deliveryType==='delivery'&&o.courierId===user.id);
  const pending=S.orders.filter(o=>o.deliveryType==='delivery'&&!o.courierId&&o.status==='Готов');
  const earned=myDeliveries.reduce((s,o)=>s+(o.deliveryFee||0),0);
  return `<div class="stitle">Мои доставки</div>
  <div class="card-tint mb12"><div class="slabel">Заработано (за вычетом 7%)</div>
    <div style="font-family:var(--f-serif);font-size:32px;font-weight:400;color:var(--forest);">${r0(earned*0.93)} ₽</div>
    <div class="fs12 cmid mt4">Комиссия платформы: ${r0(earned*0.07)} ₽</div>
    <button class="btn btn-sm btn-o mt8" data-action="courierWithdraw">💳 Вывести средства</button>
  </div>
  <div class="slabel mt16">Доступные заказы</div>
  ${pending.length?pending.map(o=>`<div class="del-prof-card">
    <div class="row mb8"><span class="fw6">${esc(o.storeName)}</span><span class="sbadge">${o.status}</span></div>
    <div class="fs13 cmid mb4">${esc(o.deliveryAddress||'Адрес не указан')}</div>
    <div class="fs13 cmid mb8">~${o.deliveryKm||'?'} км · ${o.deliveryFee||'?'} ₽ · Ваш заработок: ${r0((o.deliveryFee||0)*0.93)} ₽</div>
    <button class="btn btn-sm btn-p" data-action="takeOrder" data-oid="${o.id}">Взять заказ</button>
  </div>`).join(''):`<div style="padding:20px;text-align:center;color:var(--ink50);">Нет доступных заказов</div>`}
  <div class="slabel mt20">Активные заказы</div>
  ${myDeliveries.filter(o=>o.deliveryStatus!=='Доставлен').map(o=>`<div class="del-prof-card">
    <div class="row mb8"><span class="fw6">${esc(o.storeName)}</span><span class="sbadge ${o.deliveryStatus==='Доставлен'?'gn':''}">${o.deliveryStatus||'—'}</span></div>
    <div class="fs13 cmid mb4">${esc(o.deliveryAddress||'')}</div>
    <div class="fs13 mb8">Доставка: ${o.deliveryFee||0} ₽ · Заработок: ${r0((o.deliveryFee||0)*0.93)} ₽</div>
    <select class="stsel" style="width:100%;" data-action="chDeliveryStatus" data-oid="${o.id}">
      ${['Принят','В пути','Доставлен'].map(s=>`<option ${o.deliveryStatus===s?'selected':''}>${s}</option>`).join('')}
    </select></div>`).join('')}`;
}

function rAdmin(){
  const user=cu();
  if(!user||user.role!=='admin')return`<div class="empty"><div class="empty-ico">🔒</div><div class="empty-t">Нет доступа</div></div>`;
  const comm=S.adminCommission||0,courComm=S.courierCommission||0;
  const distTabs=S.districts.map(d=>`<button class="cpill" data-action="adminDistrict" data-did="${d.id}">${d.name}</button>`).join('');
  const pendingStores=S.stores.filter(s=>!s.approved);
  const pendingCouriers=S.couriers.filter(c=>!c.approved);
  return `<div class="stitle">Панель управления</div>
  <div class="cm-hero"><div class="cl">Комиссия с продаж (5%)</div><div class="ca">${comm} ₽</div>
    <div class="cs">+ комиссия с доставок: ${courComm} ₽</div>
    <button class="btn btn-sm mt12" style="background:rgba(255,255,255,.15);color:#fff;box-shadow:none;width:auto;" data-action="withdraw">🏦 Запросить вывод</button>
  </div>
  ${pendingStores.length?`<div class="card-flat" style="background:var(--amberp);border-color:var(--amber);"><div class="fw6 mb8">⏳ Новые магазины (${pendingStores.length})</div>
    ${pendingStores.map(s=>`<div class="row mb8"><span>${esc(s.name)} — ${esc(s.owner)}</span><div style="display:flex;gap:6px;"><button class="btn btn-xs btn-p" data-action="approveStore" data-sid="${s.id}">Одобрить</button><button class="btn btn-xs btn-d" data-action="rejectStore" data-sid="${s.id}">Отказать</button></div></div>`).join('')}
  </div>`:''}
  ${pendingCouriers.length?`<div class="card-flat" style="background:var(--amberp);border-color:var(--amber);"><div class="fw6 mb8">⏳ Новые доставщики (${pendingCouriers.length})</div>
    ${pendingCouriers.map(c=>`<div class="row mb8"><div><div class="fw5">${esc(c.fullName)}</div><div class="fs12 cmid">${esc(c.phone)} ${c.cardNumber?'· Карта: ****'+c.cardNumber.slice(-4):''}</div></div><div style="display:flex;gap:6px;"><button class="btn btn-xs btn-p" data-action="approveCourier" data-cid="${c.id}">Одобрить</button><button class="btn btn-xs btn-d" data-action="rejectCourier" data-cid="${c.id}">Отказать</button></div></div>`).join('')}
  </div>`:''}
  <div class="slabel mt8">Районы</div>
  <div class="cats" style="position:relative;">${distTabs}</div>
  <button class="btn btn-o mb12" data-action="addDistrict">+ Добавить район</button>
  <div class="slabel">Магазины и доставщики</div>
  <div class="cats"><button class="cpill on" data-action="adminTab" data-tab="stores">🏪 Магазины</button><button class="cpill" data-action="adminTab" data-tab="couriers">🚴 Доставщики</button></div>
  <div id="adminContent">${renderAdminStores()}</div>`;
}
function renderAdminStores(){
  return`<button class="btn btn-p mb12" data-action="createStore">+ Создать магазин</button>`+
  (S.stores.map(s=>{const d=gd(s.districtId),pc=S.products.filter(p=>p.storeId===s.id).length;
    return`<div class="loc-card"><div class="loc-hdr"><span class="loc-name">${esc(s.logo)} ${esc(s.name)}</span><span class="sbadge ${s.approved?'':'rd'}">${s.approved?'Активен':'Заблокирован'}</span></div><div class="loc-meta">${esc(s.owner)} · ${d?esc(d.name):'—'} · ${pc} товаров<br>ID: ${s.id}</div><div style="display:flex;gap:8px;"><button class="btn btn-xs ${s.approved?'btn-o':'btn-p'}" data-action="toggleStore" data-sid="${s.id}">${s.approved?'Заблокировать':'Активировать'}</button><button class="btn btn-xs btn-d" data-action="deleteStore" data-sid="${s.id}">Удалить</button></div></div>`;
  }).join('')||'<div style="color:var(--ink50);text-align:center;padding:20px;">Магазинов нет</div>');
}
function renderAdminCouriers(){
  const appr=S.couriers.filter(c=>c.approved);
  return appr.length?appr.map(c=>{const d=gd(c.districtId);
    return`<div class="del-prof-card"><div class="row mb8"><div class="fw6">${esc(c.fullName)}</div><span class="sbadge gn">Активен</span></div><div class="fs13 cmid mb4">📍 ${esc(d?d.name:'—')} · 📞 ${esc(c.phone)}</div>${c.cardNumber?`<div class="fs12 cmid mb4">💳 Карта: ****${c.cardNumber.slice(-4)}</div>`:''}<button class="btn btn-xs btn-d" data-action="blockCourier" data-cid="${c.id}" style="margin-top:6px;">Заблокировать</button></div>`;
  }).join(''):`<div style="color:var(--ink50);text-align:center;padding:20px;">Нет активных доставщиков</div>`;
}

function bindScreen(){
  const el=$('s-'+CS);if(!el)return;
  el.addEventListener('click',e=>{
    const t=e.target;
    const qb=t.closest('[data-action="qm"],[data-action="qp"]');
    if(qb){e.stopPropagation();const pid=qb.dataset.pid,act=qb.dataset.action;if(!requireLogin())return;cartUpdate(pid,act==='qp'?1:-1);render();return;}
    const btn=t.closest('[data-action]');if(!btn)return;
    const ac=btn.dataset.action,pid=btn.dataset.pid,sid=btn.dataset.sid,oid=btn.dataset.oid;
    switch(ac){
      case 'openProduct':{const card=t.closest('[data-pid]');if(card){detailId=card.dataset.pid;goTo('product');}break;}
      case 'goBack':goTo('main');break;
      case 'storeInfo':{const st=gs(sid);if(st)openModal(storeInfoModal(st));break;}
      case 'setVisit':openModal(visitModal());break;
      case 'rmItem':S.cart=S.cart.filter(c=>c.productId!==pid);save();render();break;
      case 'pay':payStore(sid,el);break;
      case 'topUp':openModal(topUpModal());break;
      case 'logout':doLogout();break;
      case 'doLogin':openModal(loginModal());break;
      case 'changeAvatar':handleAvatarChange();break;
      case 'editStock':{const p=gp(pid);if(p)openModal(editStockModal(p));break;}
      case 'delProd':if(confirm('Удалить товар?')){S.products=S.products.filter(p=>p.id!==pid);save();render();toast('Товар удалён');}break;
      case 'addProd':openModal(addProdModal());break;
      case 'offlineSale':openModal(offlineModal());break;
      case 'editStore':{const user=cu();const st=S.stores.find(s=>s.id===user.storeId);if(st)openModal(editStoreModal(st));break;}
      case 'takeOrder':takeDelivery(oid);break;
      case 'courierWithdraw':openModal(courierWithdrawModal());break;
      case 'adminDistrict':openModal(adminDistrictModal(btn.dataset.did));break;
      case 'addDistrict':openModal(addDistrictModal());break;
      case 'createStore':openModal(createStoreModal());break;
      case 'toggleStore':{const st=gs(sid);if(st){st.approved=!st.approved;save();render();toast(st.approved?'Активирован':'Заблокирован');}break;}
      case 'deleteStore':if(confirm('Удалить магазин и все его товары?')){S.stores=S.stores.filter(s=>s.id!==sid);S.products=S.products.filter(p=>p.storeId!==sid);S.users=S.users.filter(u=>!(u.storeId===sid&&u.role==='seller'));save();render();toast('Магазин удалён');}break;
      case 'approveStore':{const st=gs(sid);if(st){st.approved=true;save();render();toast('Магазин одобрен');}break;}
      case 'rejectStore':S.stores=S.stores.filter(s=>s.id!==sid);save();render();toast('Заявка отклонена');break;
      case 'approveCourier':{const c=S.couriers.find(c=>c.id===btn.dataset.cid);if(c){c.approved=true;save();render();toast('Доставщик одобрен');}break;}
      case 'rejectCourier':S.couriers=S.couriers.filter(c=>c.id!==btn.dataset.cid);save();render();toast('Заявка отклонена');break;
      case 'blockCourier':if(confirm('Заблокировать доставщика?')){S.couriers=S.couriers.filter(c=>c.id!==btn.dataset.cid);save();render();toast('Заблокирован');}break;
      case 'withdraw':if((S.adminCommission||0)+(S.courierCommission||0)>0){openModal(withdrawModal());}else toast('Нет средств для вывода');break;
      case 'adminTab':{el.querySelectorAll('[data-action="adminTab"]').forEach(b=>{b.classList.remove('on');});btn.classList.add('on');const ace=$('adminContent');if(ace){ace.innerHTML=btn.dataset.tab==='stores'?renderAdminStores():renderAdminCouriers();bindAdminContent();}break;}
    }
  },{capture:false});

  el.querySelectorAll('[data-action="qi"]').forEach(inp=>{
    inp.addEventListener('focus',()=>inp.select());
    const commit=()=>{
      if(!requireLogin()){inp.value=cq(inp.dataset.pid);return;}
      cartUpdate(inp.dataset.pid,0,inp.value);
      const q=cq(inp.dataset.pid);const p=gp(inp.dataset.pid);
      if(p)inp.value=p.unit==='weight'?r1(q).toFixed(1):String(r0(q));
      const row=inp.closest('.qrow');
      if(row){const mb=row.querySelector('[data-action="qm"]');if(mb)mb.disabled=q<=0;}
      save();
    };
    inp.addEventListener('blur',commit);
    inp.addEventListener('keydown',e=>{if(e.key==='Enter'){e.preventDefault();inp.blur();}});
  });

  el.querySelectorAll('[data-action="chStatus"]').forEach(sel=>{sel.onchange=()=>{const o=S.orders.find(o=>o.id===sel.dataset.oid);if(o){o.status=sel.value;save();toast('Статус обновлён');}};});
  el.querySelectorAll('[data-action="chDeliveryStatus"]').forEach(sel=>{sel.onchange=()=>{const o=S.orders.find(o=>o.id===sel.dataset.oid);if(o){o.deliveryStatus=sel.value;save();toast('Статус обновлён');}};});

  el.querySelectorAll('.dopt').forEach(d=>{d.onclick=()=>{const sid=d.dataset.sid,dtype=d.dataset.dtype;el.querySelectorAll(`.dopt[data-sid="${sid}"]`).forEach(x=>x.classList.remove('on'));d.classList.add('on');const ab=$(`daddr-${sid}`);if(ab)ab.style.display=dtype==='delivery'?'block':'none';};});

  const si=$('searchInp');
  if(si){si.addEventListener('input',e=>{searchQ=e.target.value;render();setTimeout(()=>{const ni=$('searchInp');if(ni){ni.focus();ni.setSelectionRange(ni.value.length,ni.value.length);}},0);});}
  el.querySelectorAll('.cpill[data-cat]').forEach(c=>{c.onclick=()=>{activeCat=c.dataset.cat;render();};});
  const fb=$('fltBtn');if(fb)fb.onclick=()=>openModal(filtersModal());
  const uc=$('userChip');if(uc)uc.onclick=()=>{const u=cu();if(!u)openModal(loginModal());else goTo('profile');};
  const af=$('avatarFile');
  if(af){af.onchange=()=>{const f=af.files[0];if(!f)return;const r=new FileReader();r.onload=e=>{const user=cu();if(!user)return;user.photo=e.target.result;const uDb=S.users.find(u=>u.id===user.id);if(uDb)uDb.photo=user.photo;save();render();};r.readAsDataURL(f);};}
}

function bindAdminContent(){
  const ac=$('adminContent');if(!ac)return;
  ac.querySelectorAll('[data-action]').forEach(btn=>{
    btn.onclick=()=>{
      const a=btn.dataset.action,sid=btn.dataset.sid,cid=btn.dataset.cid;
      if(a==='toggleStore'){const st=gs(sid);if(st){st.approved=!st.approved;save();render();toast(st.approved?'Активирован':'Заблокирован');}}
      if(a==='deleteStore'){if(confirm('Удалить магазин?')){S.stores=S.stores.filter(s=>s.id!==sid);S.products=S.products.filter(p=>p.storeId!==sid);save();render();toast('Удалён');}}
      if(a==='createStore')openModal(createStoreModal());
      if(a==='approveStore'){const st=gs(sid);if(st){st.approved=true;save();render();toast('Одобрен');}}
      if(a==='rejectStore'){S.stores=S.stores.filter(s=>s.id!==sid);save();render();toast('Отклонён');}
      if(a==='approveCourier'){const c=S.couriers.find(c=>c.id===cid);if(c){c.approved=true;save();render();toast('Одобрен');}}
      if(a==='rejectCourier'){S.couriers=S.couriers.filter(c=>c.id!==cid);save();render();toast('Отклонён');}
      if(a==='blockCourier'){if(confirm('Заблокировать?')){S.couriers=S.couriers.filter(c=>c.id!==cid);save();render();toast('Заблокирован');}}
    };
  });
}

function handleAvatarChange(){const af=$('avatarFile');if(af)af.click();}
function requireLogin(){const user=cu();if(!user){openModal(loginModal());return false;}if(user.role!=='customer'){toast('Войдите как покупатель');return false;}return true;}
function doLogout(){S.session=null;S.cart=[];S.visitTime=null;save();goTo('main');toast('Вы вышли');}
function takeDelivery(oid){const user=cu();const order=S.orders.find(o=>o.id===oid);if(!order||!user)return;order.courierId=user.id;order.deliveryStatus='Принят';save();render();toast('Заказ принят в доставку');}

function payStore(sid,screenEl){
  const user=cu();if(!user||user.role!=='customer'){toast('Войдите как покупатель');return;}
  const items=storeItems(sid);if(!items.length)return;
  if(!S.visitTime){openModal(visitModal());toast('Сначала укажите время визита');return;}
  for(const it of items){const p=gp(it.productId);if(!p||p.stock<it.quantity){openModal(alertModal(`Недостаточно остатка: «${it.name}».\nУменьшите количество.`));return;}}
  let deliveryType='pickup',deliveryAddr='',deliveryKm=0,deliveryFee=0;
  if(screenEl){const dOn=screenEl.querySelector(`.dopt.on[data-sid="${sid}"]`);if(dOn&&dOn.dataset.dtype==='delivery'){deliveryType='delivery';const addrInp=screenEl.querySelector(`#addr-${sid}`);deliveryAddr=addrInp?addrInp.value.trim():'';if(!deliveryAddr){toast('Укажите адрес доставки');return;}deliveryKm=Math.round(1+Math.random()*7);deliveryFee=deliveryKm<=1?300:300+(deliveryKm-1)*75;}}
  const sub=storeSubtotal(sid),comm=r0(sub*0.05),total=sub+comm+deliveryFee;
  if((user.balance||0)<total){openModal(alertModal(`Недостаточно средств.\nНужно: ${total} ₽\nНа балансе: ${user.balance||0} ₽\n\nПополните баланс в профиле.`));return;}
  user.balance=r0(user.balance-total);const uDb=S.users.find(u=>u.id===user.id);if(uDb)uDb.balance=user.balance;
  S.adminCommission=r0((S.adminCommission||0)+comm);
  if(deliveryType==='delivery')S.courierCommission=r0((S.courierCommission||0)+r0(deliveryFee*0.07));
  items.forEach(it=>{const p=gp(it.productId);if(p)p.stock=r1(Math.max(0,p.stock-it.quantity));});
  const st=gs(sid),code=genCode();
  const order={id:genId(),customerId:user.id,storeId:sid,storeName:st?st.name:'',items:items.map(i=>({...i})),subtotal:sub,commission:comm,deliveryFee,total,status:'Принят',visitTime:S.visitTime,orderCode:code,deliveryType,deliveryAddress:deliveryAddr,deliveryKm,courierId:null,deliveryStatus:null,createdAt:Date.now()};
  S.orders.push(order);S.cart=S.cart.filter(c=>c.storeId!==sid);save();render();
  openModal(successModal(code,deliveryType,deliveryFee));
}

let activeOverlay=null;
function openModal(html){
  closeModal();
  const ov=document.createElement('div');ov.className='overlay';
  ov.innerHTML=`<div class="sheet"><div class="sh-handle"></div>${html}</div>`;
  document.body.appendChild(ov);activeOverlay=ov;
  requestAnimationFrame(()=>ov.classList.add('on'));
  ov.addEventListener('click',e=>{if(e.target===ov)closeModal();});
  setTimeout(()=>bindModal(ov),0);
}
function closeModal(){if(!activeOverlay)return;activeOverlay.classList.remove('on');const o=activeOverlay;activeOverlay=null;setTimeout(()=>o.remove(),300);}

function bindModal(ov){
  ov.querySelectorAll('[data-close]').forEach(b=>b.onclick=()=>closeModal());
  ov.querySelectorAll('#closeInfo').forEach(b=>b.onclick=()=>closeModal());
  if(ov.querySelector('#lLoginBtn'))bindLoginModal(ov);
  if(ov.querySelector('#visitSave'))bindVisitModal(ov);
  if(ov.querySelector('#topUpConfirm'))bindTopUpModal(ov);
  if(ov.querySelector('#editStockSave'))bindEditStockModal(ov);
  if(ov.querySelector('#addProdSave'))bindAddProdModal(ov);
  if(ov.querySelector('#editStoreSave'))bindEditStoreModal(ov);
  if(ov.querySelector('#offlineSave'))bindOfflineModal(ov);
  if(ov.querySelector('#createStoreSave'))bindCreateStoreModal(ov);
  if(ov.querySelector('#addDistrictSave'))bindAddDistrictModal(ov);
  if(ov.querySelector('#withdrawBtn'))bindWithdrawModal(ov);
  if(ov.querySelector('#courierWithdrawBtn'))bindCourierWithdrawModal(ov);
  const apf=ov.querySelector('#applyFlt'),clf=ov.querySelector('#clearFlt');
  if(apf)apf.onclick=()=>{fltStore=ov.querySelector('#fStore').value;fltSort=ov.querySelector('#fSort').value;closeModal();render();};
  if(clf)clf.onclick=()=>{fltStore='';fltSort='none';closeModal();render();};
  const dd=ov.querySelector('#delDistrictBtn');
  if(dd)dd.onclick=()=>{const did=dd.dataset.did;if(confirm('Удалить район?')){S.districts=S.districts.filter(d=>d.id!==did);save();closeModal();render();toast('Район удалён');}};
}

function loginModal(){
  return`<div class="sh-title">Вход в FRESH</div>
  <div class="tab-row"><button class="tbtn on" data-ltab="customer">Покупатель</button><button class="tbtn" data-ltab="partner">Партнёрство</button></div>
  <div id="lTabCustomer">
    <input class="inp" id="lPhone" placeholder="Телефон или логин" autocomplete="username">
    <input class="inp" id="lPass" type="password" placeholder="Пароль" autocomplete="current-password">
    <button class="btn btn-p" id="lLoginBtn">Войти</button>
    <button class="btn btn-g mt8" id="lRegBtn">Создать аккаунт покупателя</button>
  </div>
  <div id="lTabReg" style="display:none;">
    <input class="inp" id="rName" placeholder="Ваше имя">
    <input class="inp" id="rPhone" placeholder="Телефон (логин)">
    <input class="inp" id="rEmail" placeholder="Email (необязательно)">
    <input class="inp" id="rPass" type="password" placeholder="Пароль">
    <div class="agree-row"><div class="agree-cb" id="agreeCb1"></div><div class="agree-text">Я принимаю <a data-action="showOffer">Договор оферты</a> и <a data-action="showPrivacy">Пользовательское соглашение</a></div></div>
    <div class="agree-row"><div class="agree-cb" id="agreeCb2"></div><div class="agree-text">Мне исполнилось 18 лет и я даю согласие на обработку персональных данных</div></div>
    <button class="btn btn-p" id="lDoReg">Зарегистрироваться</button>
    <button class="btn btn-g mt8" data-ltab-back="true">← Назад</button>
  </div>
  <div id="lTabPartner" style="display:none;">
    <div class="tab-row"><button class="tbtn on" data-ptab="store">🏪 Магазин</button><button class="tbtn" data-ptab="courier">🚴 Доставщик</button></div>
    <div id="lPartnerStore">
      <input class="inp" id="sName" placeholder="Название магазина">
      <input class="inp" id="sId" placeholder="ID магазина">
      <input class="inp" id="sPass" type="password" placeholder="Пароль">
      <button class="btn btn-p" id="lSellerBtn">Войти как продавец</button>
    </div>
    <div id="lPartnerCourier" style="display:none;">
      <input class="inp" id="cPhone" placeholder="Телефон (логин)">
      <input class="inp" id="cPass" type="password" placeholder="Пароль">
      <button class="btn btn-p" id="lCourierBtn">Войти как доставщик</button>
      <div class="divider"></div>
      <div class="fw6 mb8 fs14">Регистрация доставщика</div>
      <input class="inp" id="crFIO" placeholder="ФИО полностью">
      <input class="inp" id="crPhone" placeholder="Телефон">
      <input class="inp" id="crEmail" placeholder="Email">
      <input class="inp" id="crCard" placeholder="Номер карты для выплат (16 цифр)" maxlength="19">
      <div class="yk-badge">🔒 Данные карты защищены. Выплаты через ЮKassa.</div>
      <div class="upbox" id="courierPhotoBox">📷 Фото (обязательно)<input type="file" id="courierPhotoFile" accept="image/*" style="display:none;"><img id="courierPhotoPreview" class="upbox img"></div>
      <select class="inp" id="crDistrict">${S.districts.map(d=>`<option value="${d.id}">${esc(d.name)}</option>`).join('')}</select>
      <div class="agree-row"><div class="agree-cb" id="crAgreeCb"></div><div class="agree-text">Я принимаю <a data-action="showOffer">Договор оферты</a> и согласен подписать договор с платформой</div></div>
      <button class="btn btn-p mt8" id="crRegBtn">Подать заявку</button>
    </div>
  </div>`;
}
function bindLoginModal(ov){
  const showTab=id=>{['lTabCustomer','lTabReg','lTabPartner'].forEach(t=>{const e=ov.querySelector('#'+t);if(e)e.style.display='none';});const t=ov.querySelector('#'+id);if(t)t.style.display='block';};
  ov.querySelectorAll('[data-ltab]').forEach(b=>{b.onclick=()=>{ov.querySelectorAll('.tab-row:first-of-type .tbtn').forEach(x=>x.classList.remove('on'));b.classList.add('on');showTab(b.dataset.ltab==='customer'?'lTabCustomer':'lTabPartner');};});
  ov.querySelectorAll('[data-ltab-back]').forEach(b=>{b.onclick=()=>{showTab('lTabCustomer');ov.querySelectorAll('.tab-row:first-of-type .tbtn').forEach((x,i)=>x.classList.toggle('on',i===0));};});
  ov.querySelectorAll('[data-ptab]').forEach(b=>{b.onclick=()=>{ov.querySelectorAll('[data-ptab]').forEach(x=>x.classList.remove('on'));b.classList.add('on');ov.querySelectorAll('#lPartnerStore,#lPartnerCourier').forEach(e=>e.style.display='none');const t=ov.querySelector('#lPartner'+b.dataset.ptab.charAt(0).toUpperCase()+b.dataset.ptab.slice(1));if(t)t.style.display='block';};});
  ov.querySelectorAll('.agree-cb').forEach(cb=>cb.onclick=()=>cb.classList.toggle('on'));
  ov.querySelectorAll('[data-action="showOffer"]').forEach(a=>a.onclick=()=>openModal(offerModal()));
  ov.querySelectorAll('[data-action="showPrivacy"]').forEach(a=>a.onclick=()=>openModal(privacyModal()));
  const cc=ov.querySelector('#crCard');if(cc)cc.oninput=()=>{let v=cc.value.replace(/\D/g,'').slice(0,16);cc.value=v.replace(/(.{4})/g,'$1 ').trim();};
  const cpb=ov.querySelector('#courierPhotoBox'),cpf=ov.querySelector('#courierPhotoFile'),cpp=ov.querySelector('#courierPhotoPreview');
  let courierPhoto=null;
  if(cpb&&cpf){cpb.onclick=()=>cpf.click();cpf.onchange=()=>{const f=cpf.files[0];if(!f)return;const r=new FileReader();r.onload=e=>{courierPhoto=e.target.result;if(cpp){cpp.src=courierPhoto;cpp.style.display='block';}};r.readAsDataURL(f);};}
  const lb=ov.querySelector('#lLoginBtn');
  if(lb)lb.onclick=()=>{
    const phone=ov.querySelector('#lPhone')?.value.trim(),pass=ov.querySelector('#lPass')?.value.trim();
    if(phone===ADMIN_PHONE&&pass===ADMIN_PASS){const admin=S.users.find(u=>u.role==='admin');if(admin){S.session=admin.id;save();closeModal();goTo('admin');toast('Добро пожаловать, Администратор!');return;}}
    const user=S.users.find(u=>u.phone===phone&&u.password===pass&&u.role==='customer');
    if(!user){toast('Неверный логин или пароль');return;}
    S.session=user.id;save();closeModal();goTo('main');toast('Добро пожаловать, '+user.name+'!');
  };
  const rb=ov.querySelector('#lRegBtn');if(rb)rb.onclick=()=>showTab('lTabReg');
  const drb=ov.querySelector('#lDoReg');
  if(drb)drb.onclick=()=>{
    const name=ov.querySelector('#rName')?.value.trim(),phone=ov.querySelector('#rPhone')?.value.trim(),email=ov.querySelector('#rEmail')?.value.trim(),pass=ov.querySelector('#rPass')?.value.trim();
    const a1=ov.querySelector('#agreeCb1')?.classList.contains('on'),a2=ov.querySelector('#agreeCb2')?.classList.contains('on');
    if(!name||!phone||!pass){toast('Заполните обязательные поля');return;}
    if(!a1||!a2){toast('Примите условия использования');return;}
    if(S.users.find(u=>u.phone===phone)){toast('Этот телефон уже зарегистрирован');return;}
    const nu={id:genId(),role:'customer',name,phone,email,password:pass,balance:0,photo:null};
    S.users.push(nu);S.session=nu.id;save();closeModal();goTo('main');toast('Добро пожаловать, '+name+'!');
  };
  const slb=ov.querySelector('#lSellerBtn');
  if(slb)slb.onclick=()=>{
    const name=ov.querySelector('#sName')?.value.trim(),id=ov.querySelector('#sId')?.value.trim(),pass=ov.querySelector('#sPass')?.value.trim();
    const store=S.stores.find(s=>s.id===id&&s.name===name);if(!store){toast('Магазин не найден');return;}
    if(!store.approved){toast('Магазин заблокирован');return;}
    const user=S.users.find(u=>u.storeId===store.id&&u.role==='seller'&&u.password===pass);if(!user){toast('Неверный пароль');return;}
    S.session=user.id;save();closeModal();goTo('seller');toast('Добро пожаловать, '+user.name+'!');
  };
  const clb=ov.querySelector('#lCourierBtn');
  if(clb)clb.onclick=()=>{
    const phone=ov.querySelector('#cPhone')?.value.trim(),pass=ov.querySelector('#cPass')?.value.trim();
    const user=S.users.find(u=>u.phone===phone&&u.password===pass&&u.role==='courier');if(!user){toast('Неверные данные');return;}
    const courier=S.couriers.find(c=>c.userId===user.id);if(!courier||!courier.approved){toast('Аккаунт ещё не одобрен администратором');return;}
    S.session=user.id;save();closeModal();goTo('courier');toast('Добро пожаловать!');
  };
  const crb=ov.querySelector('#crRegBtn');
  if(crb)crb.onclick=()=>{
    const fio=ov.querySelector('#crFIO')?.value.trim(),phone=ov.querySelector('#crPhone')?.value.trim(),email=ov.querySelector('#crEmail')?.value.trim();
    const cardRaw=ov.querySelector('#crCard')?.value.replace(/\s/g,'');
    const district=ov.querySelector('#crDistrict')?.value,ag=ov.querySelector('#crAgreeCb')?.classList.contains('on');
    if(!fio||!phone){toast('Заполните ФИО и телефон');return;}
    if(!cardRaw||cardRaw.length<16){toast('Введите номер карты для выплат');return;}
    if(!courierPhoto){toast('Прикрепите фото');return;}
    if(!ag){toast('Примите условия');return;}
    if(S.users.find(u=>u.phone===phone)){toast('Телефон уже зарегистрирован');return;}
    const tempPass=genCode();
    const nu={id:genId(),role:'courier',name:fio,phone,email,password:tempPass,balance:0,photo:courierPhoto};
    S.users.push(nu);S.couriers.push({id:genId(),userId:nu.id,fullName:fio,phone,email,districtId:district,photo:courierPhoto,cardNumber:cardRaw,approved:false,createdAt:Date.now()});
    save();closeModal();toast('Заявка отправлена! Ожидайте одобрения администратора.');
  };
}

function visitModal(){
  const today=new Date().toISOString().split('T')[0];
  const cv=S.visitTime?S.visitTime.split(' ')[0]:today,ct=S.visitTime?S.visitTime.split(' ')[1]:'10:00';
  return`<div class="sh-title">Время визита</div>
  <label class="ilabel">Дата</label><input class="inp" type="date" id="vDate" value="${cv}" min="${today}">
  <label class="ilabel">Время</label><input class="inp" type="time" id="vTime" value="${ct}">
  <button class="btn btn-p" id="visitSave">Сохранить</button>`;
}
function bindVisitModal(ov){ov.querySelector('#visitSave').onclick=()=>{const d=ov.querySelector('#vDate').value,t=ov.querySelector('#vTime').value;if(!d||!t){toast('Выберите дату и время');return;}S.visitTime=`${d} ${t}`;save();closeModal();render();toast('Время визита сохранено');};}

function topUpModal(){
  return`<div class="sh-title">Пополнение баланса</div>
  <div class="yk-badge">🔒 Безопасный платёж через ЮKassa (подключение при запуске)</div>
  <div class="pay-methods">
    <div class="pmo on" data-pm="card"><div class="pmo-ico">💳</div><div class="pmo-info"><div class="pmo-name">Банковская карта</div><div class="pmo-sub">Visa, Mastercard, МИР</div></div><div class="pmo-chk"></div></div>
    <div class="pmo" data-pm="sbp"><div class="pmo-ico">⚡</div><div class="pmo-info"><div class="pmo-name">СБП</div><div class="pmo-sub">Быстрый перевод между банками</div></div><div class="pmo-chk"></div></div>
    <div class="pmo" data-pm="bank"><div class="pmo-ico">🏦</div><div class="pmo-info"><div class="pmo-name">Банковский перевод</div><div class="pmo-sub">По реквизитам</div></div><div class="pmo-chk"></div></div>
  </div>
  <div class="card-form vis" id="cardForm">
    <input class="inp inp-rect" id="cardNum" placeholder="Номер карты" maxlength="19">
    <div class="crow"><div><input class="inp inp-rect" id="cardExp" placeholder="ММ/ГГ" maxlength="5"></div><div><input class="inp inp-rect" id="cardCvv" placeholder="CVV" maxlength="3" type="password"></div></div>
  </div>
  <input class="inp" type="number" id="topUpAmt" placeholder="Сумма пополнения, ₽" min="100" value="500">
  <button class="btn btn-p" id="topUpConfirm">Перейти к оплате</button>
  <div class="fs12 cmid mt8" style="text-align:center;">(В демо-версии баланс пополняется без реального списания)</div>`;
}
function bindTopUpModal(ov){
  ov.querySelectorAll('.pmo').forEach(p=>{p.onclick=()=>{ov.querySelectorAll('.pmo').forEach(x=>x.classList.remove('on'));p.classList.add('on');const cf=ov.querySelector('#cardForm');if(cf)cf.classList.toggle('vis',p.dataset.pm==='card');};});
  const cn=ov.querySelector('#cardNum');if(cn)cn.oninput=()=>{let v=cn.value.replace(/\D/g,'').slice(0,16);cn.value=v.replace(/(.{4})/g,'$1 ').trim();};
  const ce=ov.querySelector('#cardExp');if(ce)ce.oninput=()=>{let v=ce.value.replace(/\D/g,'');if(v.length>2)v=v.slice(0,2)+'/'+v.slice(2);ce.value=v;};
  ov.querySelector('#topUpConfirm').onclick=()=>{
    const amt=parseFloat(ov.querySelector('#topUpAmt').value);if(isNaN(amt)||amt<100){toast('Минимальная сумма — 100 ₽');return;}
    const user=cu();if(!user)return;
    user.balance=r0((user.balance||0)+amt);const uDb=S.users.find(u=>u.id===user.id);if(uDb)uDb.balance=user.balance;
    save();closeModal();render();toast(`✅ Баланс пополнен на ${amt} ₽`);
  };
}

function storeInfoModal(store){
  const d=gd(store.districtId);
  return`<div style="text-align:center;font-size:48px;margin-bottom:8px;">${store.logo}</div>
  <div class="sh-title">${esc(store.name)}</div>
  ${store.desc?`<p style="color:var(--ink50);text-align:center;margin-bottom:10px;font-size:14px;line-height:1.5;">${esc(store.desc)}</p>`:''}
  ${store.address?`<p style="text-align:center;margin-bottom:6px;font-size:14px;">📍 ${esc(store.address)}</p>`:''}
  ${d?`<p style="text-align:center;margin-bottom:6px;font-size:14px;">📌 ${esc(d.name)}</p>`:''}
  ${store.phone?`<p style="text-align:center;margin-bottom:14px;font-size:14px;">📞 ${esc(store.phone)}</p>`:''}
  <button class="btn btn-o" id="closeInfo">Закрыть</button>`;
}

function filtersModal(){
  const opts='<option value="">Все магазины</option>'+S.stores.filter(s=>s.approved).map(s=>`<option value="${s.id}" ${fltStore===s.id?'selected':''}>${esc(s.name)}</option>`).join('');
  return`<div class="sh-title">Фильтры</div>
  <label class="ilabel">Магазин</label><select class="inp" id="fStore">${opts}</select>
  <label class="ilabel">Сортировка</label>
  <select class="inp" id="fSort"><option value="none" ${fltSort==='none'?'selected':''}>По умолчанию</option><option value="asc" ${fltSort==='asc'?'selected':''}>Сначала дешевле</option><option value="desc" ${fltSort==='desc'?'selected':''}>Сначала дороже</option></select>
  <button class="btn btn-p" id="applyFlt">Применить</button>
  <button class="btn btn-g mt8" id="clearFlt">Сбросить фильтры</button>`;
}

function editStockModal(p){
  return`<div class="sh-title">Изменить остаток</div>
  <p style="text-align:center;color:var(--ink50);margin-bottom:14px;">${esc(p.name)}</p>
  <input class="inp" type="number" id="newStock" value="${p.stock}" step="${p.unit==='weight'?'0.1':'1'}" min="0">
  <div class="hint-box">⚠️ Если поставить 0 — товар скроется из каталога покупателей автоматически.</div>
  <button class="btn btn-p" id="editStockSave" data-pid="${p.id}">Сохранить</button>`;
}
function bindEditStockModal(ov){ov.querySelector('#editStockSave').onclick=()=>{const pid=ov.querySelector('#editStockSave').dataset.pid,val=parseFloat(ov.querySelector('#newStock').value);if(isNaN(val)||val<0){toast('Некорректное значение');return;}const p=gp(pid);if(!p)return;p.stock=p.unit==='weight'?r1(val):Math.floor(val);save();closeModal();render();toast('Остаток обновлён');};}

/* FIX 3: Added Готовая еда to product categories */
function addProdModal(){
  return`<div class="sh-title">Новый товар</div>
  <input class="inp" id="pName" placeholder="Название товара">
  <select class="inp" id="pUnit"><option value="weight">Весовой (цена за кг)</option><option value="piece">Штучный (цена за шт)</option></select>
  <input class="inp" id="pPrice" type="number" min="1" placeholder="Цена, ₽">
  <input class="inp" id="pStock" type="number" min="0" step="0.1" placeholder="Начальный остаток">
  <input class="inp inp-rect" id="pDesc" placeholder="Описание товара (состав, особенности…)" style="border-radius:12px;">
  <select class="inp" id="pCat"><option>Мясо</option><option>Овощи</option><option>Фрукты</option><option>Молочка</option><option>Рассада</option><option>Рыба</option><option>Готовая еда</option></select>
  <div class="upbox" id="prodUpBox">📷 Фото товара<input type="file" id="prodImgFile" accept="image/*" style="display:none;"><img id="prodImgPrev" class="upbox img"></div>
  <button class="btn btn-p" id="addProdSave">Добавить товар</button>`;
}
function bindAddProdModal(ov){
  const ub=ov.querySelector('#prodUpBox'),fi=ov.querySelector('#prodImgFile'),prev=ov.querySelector('#prodImgPrev');
  let imgData=null;
  if(ub&&fi){ub.onclick=()=>fi.click();fi.onchange=()=>{const f=fi.files[0];if(!f)return;const r=new FileReader();r.onload=e=>{imgData=e.target.result;if(prev){prev.src=imgData;prev.style.display='block';}};r.readAsDataURL(f);};}
  ov.querySelector('#addProdSave').onclick=()=>{
    const user=cu(),store=S.stores.find(s=>s.id===user?.storeId);if(!store)return;
    const name=ov.querySelector('#pName').value.trim(),unit=ov.querySelector('#pUnit').value;
    const price=parseFloat(ov.querySelector('#pPrice').value),stock=parseFloat(ov.querySelector('#pStock').value);
    const desc=ov.querySelector('#pDesc').value.trim(),cat=ov.querySelector('#pCat').value;
    const emap={Мясо:'🥩',Овощи:'🥬',Фрукты:'🍎',Молочка:'🥛',Рассада:'🌱',Рыба:'🐟','Готовая еда':'🍱'};
    const img=imgData||emap[cat]||'📦';
    if(!name){toast('Введите название');return;}if(isNaN(price)||price<=0){toast('Введите цену');return;}if(isNaN(stock)||stock<0){toast('Введите остаток');return;}
    S.products.push({id:genId(),storeId:store.id,name,cat,price,unit,stock:unit==='weight'?r1(stock):Math.floor(stock),img,desc});
    save();closeModal();render();toast('Товар добавлен');
  };
}

function editStoreModal(store){
  return`<div class="sh-title">Профиль магазина</div>
  <input class="inp" id="esDesc" placeholder="Описание" value="${esc(store.desc||'')}">
  <input class="inp" id="esAddr" placeholder="Адрес на рынке" value="${esc(store.address||'')}">
  <button class="btn btn-p" id="editStoreSave" data-sid="${store.id}">Сохранить</button>`;
}
function bindEditStoreModal(ov){ov.querySelector('#editStoreSave').onclick=()=>{const sid=ov.querySelector('#editStoreSave').dataset.sid,st=gs(sid);if(!st)return;st.desc=ov.querySelector('#esDesc').value.trim();st.address=ov.querySelector('#esAddr').value.trim();save();closeModal();render();toast('Профиль обновлён');};}

function offlineModal(){
  const user=cu(),store=S.stores.find(s=>s.id===user?.storeId);
  if(!store)return`<div class="sh-title">Ошибка</div><button class="btn btn-g" data-close>Закрыть</button>`;
  const prods=S.products.filter(p=>p.storeId===store.id&&p.stock>0);
  return`<div class="sh-title">Офлайн-продажа</div>
  <p style="color:var(--ink50);font-size:13px;margin-bottom:12px;">Спишите остаток вручную при продаже через кассу</p>
  <select class="inp" id="offProd">${prods.map(p=>`<option value="${p.id}">${esc(p.name)} (${fmtQty(p.stock,p.unit)})</option>`).join('')||'<option>Нет товаров</option>'}</select>
  <input class="inp" type="number" id="offQty" placeholder="Количество" step="0.1" min="0.1">
  <button class="btn btn-p" id="offlineSave">Списать</button>`;
}
function bindOfflineModal(ov){ov.querySelector('#offlineSave').onclick=()=>{const pid=ov.querySelector('#offProd').value,qty=parseFloat(ov.querySelector('#offQty').value);if(isNaN(qty)||qty<=0){toast('Введите количество');return;}const p=gp(pid);if(!p)return;if(qty>p.stock){toast('Недостаточно остатка');return;}p.stock=r1(Math.max(0,p.stock-qty));save();closeModal();render();toast(`Списано: ${fmtQty(qty,p.unit)}`);};}

function createStoreModal(){
  return`<div class="sh-title">Создать магазин</div>
  <input class="inp" id="csName" placeholder="Название магазина">
  <input class="inp" id="csOwner" placeholder="Имя продавца">
  <input class="inp" id="csPhone" placeholder="Телефон">
  <input class="inp" id="csPass" type="password" placeholder="Пароль продавца">
  <select class="inp" id="csDist">${S.districts.map(d=>`<option value="${d.id}">${esc(d.name)}</option>`).join('')}</select>
  <button class="btn btn-p" id="createStoreSave">Создать магазин</button>`;
}
function bindCreateStoreModal(ov){ov.querySelector('#createStoreSave').onclick=()=>{const name=ov.querySelector('#csName').value.trim(),owner=ov.querySelector('#csOwner').value.trim(),phone=ov.querySelector('#csPhone').value.trim(),pass=ov.querySelector('#csPass').value.trim(),dist=ov.querySelector('#csDist').value;if(!name||!owner||!phone||!pass){toast('Заполните все поля');return;}if(S.stores.find(s=>s.name===name)){toast('Магазин с таким названием уже существует');return;}const sid='s_'+Date.now();S.stores.push({id:sid,districtId:dist,name,logo:'🏪',owner,phone,approved:false,desc:'',address:''});S.users.push({id:genId(),role:'seller',name:owner,phone,password:pass,email:'',balance:0,storeId:sid,photo:null});save();closeModal();render();toast('Магазин создан — ожидает одобрения');};}

function addDistrictModal(){
  return`<div class="sh-title">Добавить район</div>
  <input class="inp" id="adName" placeholder="Название района">
  <input class="inp" id="adAddr" placeholder="Адрес / описание">
  <button class="btn btn-p" id="addDistrictSave">Добавить</button>`;
}
function bindAddDistrictModal(ov){ov.querySelector('#addDistrictSave').onclick=()=>{const name=ov.querySelector('#adName').value.trim(),addr=ov.querySelector('#adAddr').value.trim();if(!name){toast('Введите название');return;}S.districts.push({id:'d_'+Date.now(),name,address:addr});save();closeModal();render();toast('Район добавлен');};}

function adminDistrictModal(did){
  const d=gd(did);if(!d)return`<div class="sh-title">Ошибка</div>`;
  const stores=S.stores.filter(s=>s.districtId===did),couriers=S.couriers.filter(c=>c.districtId===did&&c.approved);
  return`<div class="sh-title">📌 ${esc(d.name)}</div>
  <p style="color:var(--ink50);font-size:14px;margin-bottom:14px;">${esc(d.address||'')}</p>
  <div class="fw6 mb8">Магазины (${stores.length})</div>
  ${stores.map(s=>`<div class="row mb8"><span class="fw5">${esc(s.logo)} ${esc(s.name)}</span><span class="sbadge ${s.approved?'':'rd'}">${s.approved?'Активен':'Заблокирован'}</span></div>`).join('')||'<div class="fs13 cmid mb8">Нет магазинов</div>'}
  <div class="fw6 mb8 mt8">Доставщики (${couriers.length})</div>
  ${couriers.map(c=>`<div class="row mb8"><span class="fw5">${esc(c.fullName)}</span><span class="sbadge gn">Активен</span></div>`).join('')||'<div class="fs13 cmid mb8">Нет доставщиков</div>'}
  <div class="divider"></div>
  <button class="btn btn-d" id="delDistrictBtn" data-did="${did}">Удалить район</button>
  <button class="btn btn-g mt8" id="closeInfo">Закрыть</button>`;
}

function withdrawModal(){
  const total=(S.adminCommission||0)+(S.courierCommission||0);
  return`<div class="sh-title">Вывод средств</div>
  <div class="yk-badge">🔒 Вывод через ЮKassa (подключение при запуске)</div>
  <div class="card-tint mb12">
    <div class="row mb8"><span class="fs14">Комиссия с продаж</span><span class="fw6">${S.adminCommission||0} ₽</span></div>
    <div class="row"><span class="fs14">Комиссия с доставок</span><span class="fw6">${S.courierCommission||0} ₽</span></div>
    <div class="divider"></div>
    <div class="row"><span class="fw6 fs14">Итого</span><span style="font-family:var(--f-serif);font-size:22px;color:var(--forest);">${total} ₽</span></div>
  </div>
  <input class="inp" placeholder="Реквизиты счёта (IBAN / ЮKassa)" id="withdrawReqs">
  <button class="btn btn-p" id="withdrawBtn">Запросить вывод</button>`;
}
function bindWithdrawModal(ov){ov.querySelector('#withdrawBtn').onclick=()=>{const reqs=ov.querySelector('#withdrawReqs').value.trim();if(!reqs){toast('Введите реквизиты');return;}const total=(S.adminCommission||0)+(S.courierCommission||0);S.adminCommission=0;S.courierCommission=0;save();closeModal();render();toast(`Запрос на вывод ${total} ₽ отправлен`);};}

function courierWithdrawModal(){
  const user=cu();const courier=S.couriers.find(c=>c.userId===user?.id);
  const myDeliveries=S.orders.filter(o=>o.deliveryType==='delivery'&&o.courierId===user?.id);
  const earned=myDeliveries.reduce((s,o)=>s+(o.deliveryFee||0),0);const net=r0(earned*0.93);
  return`<div class="sh-title">Вывод заработка</div>
  <div class="yk-badge">🔒 Вывод через ЮKassa на привязанную карту</div>
  <div class="card-tint mb12">
    <div class="row mb8"><span class="fs14">Всего заработано</span><span class="fw6">${earned} ₽</span></div>
    <div class="row mb8"><span class="fs14">Комиссия платформы 7%</span><span class="fw6">${r0(earned*0.07)} ₽</span></div>
    <div class="divider"></div>
    <div class="row"><span class="fw6 fs14">К выплате</span><span style="font-family:var(--f-serif);font-size:22px;color:var(--forest);">${net} ₽</span></div>
  </div>
  ${courier&&courier.cardNumber?`<div class="fs13 cmid mb12">Карта: ****${courier.cardNumber.slice(-4)}</div>`:''}
  <button class="btn btn-p" id="courierWithdrawBtn">Запросить выплату</button>
  <div class="fs12 cmid mt8" style="text-align:center;">(В демо-версии средства не списываются)</div>`;
}
function bindCourierWithdrawModal(ov){ov.querySelector('#courierWithdrawBtn').onclick=()=>{toast('Запрос на выплату отправлен! ЮKassa зачислит средства в течение 1–2 рабочих дней.');closeModal();};}

function successModal(code,dtype,fee){
  return`<div style="text-align:center;">
    <div style="font-size:64px;margin-bottom:12px;">✅</div>
    <div class="sh-title" style="margin-bottom:8px;">Заказ оплачен!</div>
    <p style="color:var(--ink50);font-size:14px;margin-bottom:20px;">${dtype==='delivery'?`Доставщик заберёт заказ, когда он будет готов.<br>Стоимость доставки: ${fee} ₽`:'Покажите код продавцу при получении заказа'}</p>
    <div class="code-chip" style="justify-content:center;gap:16px;"><div><div class="cl">Код выдачи</div><div class="cv">${code}</div></div></div>
    <button class="btn btn-p mt16" id="closeInfo">Отлично!</button>
  </div>`;
}
function alertModal(msg){
  return`<div style="text-align:center;">
    <div style="font-size:48px;margin-bottom:12px;">⚠️</div>
    <div class="sh-title" style="font-size:18px;margin-bottom:10px;">Внимание</div>
    <p style="color:var(--ink80);font-size:14px;line-height:1.6;white-space:pre-line;">${esc(msg)}</p>
    <button class="btn btn-g mt16" id="closeInfo">Понятно</button>
  </div>`;
}
function offerModal(){
  return`<div class="sh-title">Договор оферты</div><div class="legal-doc">
    <h3>1. Общие положения</h3><p>Настоящий документ является публичной офертой платформы FRESH и определяет условия использования сервиса для заказа продуктов питания.</p>
    <h3>2. Предмет договора</h3><p>Платформа предоставляет доступ к каталогу товаров от продавцов на рынках. Платформа не является продавцом товаров и выступает как агрегатор заказов.</p>
    <h3>3. Порядок заказа</h3><p>Покупатель выбирает товары, указывает время самовывоза или адрес доставки и оплачивает заказ с внутреннего баланса. Платформа взимает комиссию 5% от суммы заказа.</p>
    <h3>4. Оплата и пополнение баланса</h3><p>Баланс пополняется через платёжную систему ЮKassa. Вывод средств администратором осуществляется через ЮKassa. Возврат средств в соответствии с законодательством РФ.</p>
    <h3>5. Доставка</h3><p>1 км — 300 ₽, каждый следующий км — 75 ₽. Доставку осуществляют верифицированные курьеры. Платформа удерживает 7% от суммы доставки.</p>
    <h3>6. Ответственность</h3><p>Платформа не несёт ответственности за качество товаров. Претензии направляются продавцу.</p>
    <h3>7. Персональные данные</h3><p>Обработка данных — согласно ФЗ №152-ФЗ.</p>
  </div><button class="btn btn-p mt12" id="closeInfo">Закрыть</button>`;
}
function privacyModal(){
  return`<div class="sh-title">Пользовательское соглашение</div><div class="legal-doc">
    <h3>1. Принятие условий</h3><p>Регистрируясь в FRESH, вы принимаете настоящее соглашение.</p>
    <h3>2. Учётная запись</h3><p>Вы несёте ответственность за конфиденциальность пароля и все действия под вашей учётной записью.</p>
    <h3>3. Запрещённые действия</h3><p>Запрещается использовать сервис в мошеннических целях, регистрировать несколько аккаунтов, передавать доступ третьим лицам.</p>
    <h3>4. Обработка данных</h3><p>Мы собираем: имя, телефон, email, адрес доставки, историю заказов. Данные используются только для работы сервиса.</p>
    <h3>5. Блокировка</h3><p>Администрация вправе заблокировать аккаунт при нарушении условий.</p>
    <h3>6. Применимое право</h3><p>Законодательство Российской Федерации.</p>
  </div><button class="btn btn-p mt12" id="closeInfo">Закрыть</button>`;
}

function toast(msg){document.querySelectorAll('.toast').forEach(t=>t.remove());const t=document.createElement('div');t.className='toast';t.textContent=msg;$('app').appendChild(t);setTimeout(()=>t.remove(),2500);}

const wShown=localStorage.getItem('fresh_v3_welcome');
if(wShown)$('welcome').classList.add('hide');
$('wStart').onclick=()=>{$('welcome').classList.add('hide');localStorage.setItem('fresh_v3_welcome','1');};
$('s-main').classList.add('active');
goTo('main');
})();
</script>
</body>
</html>
