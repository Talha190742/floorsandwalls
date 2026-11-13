(function () {
var vals = {};
var ROUTES = { '-1': '', '0': 'laminaat', '1': 'click-pvc-visgraat', '2': 'plak-pvc-visgraat', '3': 'pvc-marmerlook-panelen', '4': 'akoestische-panelen', '10': 'over-floors-walls', '11': 'offerte-aanvragen', '12': 'contact-opnemen' };
var settingHash = false;
var PRELOAD = ["laminaat/foto18.webp", "laminaat/foto19.webp", "laminaat/foto20.webp", "laminaat/foto21.webp", "laminaat/foto22.webp", "laminaat/foto23.webp", "laminaat/foto24.webp", "laminaat/foto25.webp", "laminaat/foto26.webp", "laminaat/foto27.webp", "visgraat%20klik%20PVC/foto43.webp", "visgraat%20klik%20PVC/foto44.webp", "visgraat%20klik%20PVC/foto45.webp", "visgraat%20klik%20PVC/foto46.webp", "visgraat%20klik%20PVC/foto47.webp", "visgraat%20klik%20PVC/foto48.webp", "visgraat%20plak%20PVC/foto49.webp", "visgraat%20plak%20PVC/foto50.webp", "visgraat%20plak%20PVC/foto51.webp", "visgraat%20plak%20PVC/foto52.webp", "PVC%20wandpanelen/foto28.webp", "PVC%20wandpanelen/foto29.webp", "PVC%20wandpanelen/foto30.webp", "PVC%20wandpanelen/foto31.webp", "PVC%20wandpanelen/foto32.webp", "PVC%20wandpanelen/foto33.webp", "PVC%20wandpanelen/foto34.webp", "PVC%20wandpanelen/foto35.webp", "PVC%20wandpanelen/foto36.webp", "PVC%20wandpanelen/foto37.webp", "PVC%20wandpanelen/foto38.webp", "PVC%20wandpanelen/foto39.webp", "PVC%20wandpanelen/foto40.webp", "PVC%20wandpanelen/foto41.webp", "PVC%20wandpanelen/foto42.webp", "akoestische%20wandpanelen/foto.webp", "akoestische%20wandpanelen/foto1.webp", "akoestische%20wandpanelen/foto2.webp", "akoestische%20wandpanelen/foto3.webp", "akoestische%20wandpanelen/foto4.webp", "akoestische%20wandpanelen/foto5.webp", "akoestische%20wandpanelen/foto6.webp", "akoestische%20wandpanelen/foto7.webp", "akoestische%20wandpanelen/foto8.webp", "akoestische%20wandpanelen/foto9.webp", "akoestische%20wandpanelen/foto10.webp", "akoestische%20wandpanelen/foto11.webp", "akoestische%20wandpanelen/foto12.webp", "akoestische%20wandpanelen/foto13.webp", "akoestische%20wandpanelen/foto14.webp", "akoestische%20wandpanelen/foto15.webp", "akoestische%20wandpanelen/foto16.webp", "akoestische%20wandpanelen/foto17.webp"];
var TITLES = {
'-1': 'Floors & Walls | Laminaat, PVC vloeren en wandpanelen in Amersfoort',
'0': 'Laminaat kopen in Amersfoort | Floors & Walls',
'1': 'Click PVC visgraat vloeren | Floors & Walls Amersfoort',
'2': 'Plak PVC visgraat vloeren | Floors & Walls Amersfoort',
'3': 'PVC marmerlook wandpanelen | Floors & Walls Amersfoort',
'4': 'Akoestische wandpanelen | Floors & Walls Amersfoort',
'10': 'Over Floors & Walls | Showroom, adres en openingstijden',
'11': 'Offerte aanvragen | Floors & Walls',
'12': 'Contact | Floors & Walls Amersfoort'
};
 
function initMapView(card) {
var view = card.querySelector('.mapview');
var img = card.querySelector('.mapimg');
if (!view || !img) return;
var IW = 703, IH = 679, PX = 407, PY = 316;
var s = 1, tx = 0, ty = 0, smin = 1, smax = 2, cw = 0, ch = 0, touched = false;
function clamp() {
tx = Math.min(0, Math.max(cw - IW * s, tx));
ty = Math.min(0, Math.max(ch - IH * s, ty));
}
function apply() { img.style.transform = 'translate(' + tx + 'px,' + ty + 'px) scale(' + s + ')'; }
function reset() { s = smin; tx = cw / 2 - PX * s; ty = ch / 2 - PY * s; clamp(); apply(); }
function measure() {
var r = view.getBoundingClientRect();
if (!r.width || !r.height) return;
var first = !cw;
cw = r.width; ch = r.height;
smin = Math.max(cw / IW, ch / IH, cw / (2 * (IW - PX)), ch / (2 * PY));
smax = smin * 2;
if (first || !touched) reset(); else { s = Math.min(smax, Math.max(smin, s)); clamp(); apply(); }
}
function zoomAt(f, ox, oy) {
var ns = Math.min(smax, Math.max(smin, s * f));
var k = ns / s;
tx = ox - (ox - tx) * k; ty = oy - (oy - ty) * k; s = ns;
clamp(); apply(); touched = true;
}
var drag = null;
view.addEventListener('pointerdown', function (e) {
if (e.pointerType === 'touch') return;
drag = { x: e.clientX, y: e.clientY, tx: tx, ty: ty };
try { view.setPointerCapture(e.pointerId); } catch (err) {}
view.style.cursor = 'grabbing';
});
view.addEventListener('pointermove', function (e) {
if (!drag) return;
tx = drag.tx + e.clientX - drag.x; ty = drag.ty + e.clientY - drag.y;
clamp(); apply(); touched = true;
});
var endDrag = function () { drag = null; view.style.cursor = 'grab'; };
view.addEventListener('pointerup', endDrag);
view.addEventListener('pointercancel', endDrag);
view.addEventListener('wheel', function (e) {
if (!e.ctrlKey && !e.metaKey) return;
e.preventDefault();
var r = view.getBoundingClientRect();
zoomAt(e.deltaY < 0 ? 1.15 : 1 / 1.15, e.clientX - r.left, e.clientY - r.top);
}, { passive: false });
var hint = card.querySelector('.maphint');
var hintTimer = null;
var showHint = function () {
if (!hint) return;
hint.style.opacity = '1';
clearTimeout(hintTimer);
hintTimer = setTimeout(function () { hint.style.opacity = '0'; }, 1400);
};
var two = function (e) {
var a = e.touches[0], b = e.touches[1];
return { x: (a.clientX + b.clientX) / 2, y: (a.clientY + b.clientY) / 2, d: Math.sqrt(Math.pow(a.clientX - b.clientX, 2) + Math.pow(a.clientY - b.clientY, 2)) };
};
var t0 = null;
view.addEventListener('touchstart', function (e) { t0 = e.touches.length === 2 ? two(e) : null; }, { passive: true });
view.addEventListener('touchmove', function (e) {
if (e.touches.length === 2) {
e.preventDefault();
var c = two(e);
if (!t0) { t0 = c; return; }
var r = view.getBoundingClientRect();
tx += c.x - t0.x; ty += c.y - t0.y;
if (t0.d > 0) zoomAt(c.d / t0.d, c.x - r.left, c.y - r.top); else { clamp(); apply(); }
t0 = c; touched = true;
} else {
showHint();
}
}, { passive: false });
view.addEventListener('touchend', function () { t0 = null; }, { passive: true });
each(card, '[data-zoom]', function (btn) {
btn.addEventListener('click', function () { zoomAt(btn.getAttribute('data-zoom') === 'in' ? 1.4 : 1 / 1.4, cw / 2, ch / 2); });
});
measure();
if (window.ResizeObserver) new ResizeObserver(measure).observe(view);
window.addEventListener('resize', measure);
}
function loadFavs() {
try { var v = JSON.parse(localStorage.getItem('fw-favs') || '[]'); return Array.isArray(v) ? v : []; } catch (err) { return []; }
}
function App() {
this.state = { favs: loadFavs(), quote: [], autoMsg: '', lb: -1, lbKeys: [], menuOpen: false, view: -1, searchOpen: false, query: '', sort: '', form: {}, soort: -1, tried: false, sent: false, calc: { 'calc-l': '', 'calc-b': '', extra: true } };
}
App.prototype.setState = function (u) {
var before = this.state.view;
for (var k in u) this.state[k] = u[k];
if (this.state.view !== before) {
var name = ROUTES[String(this.state.view)] || '';
try {
if (location.hash.replace('#', '') !== name) {
settingHash = true;
location.hash = name;
setTimeout(function () { settingHash = false; }, 0);
}
} catch (err) { settingHash = false; }
}
render();
};
App.prototype.renderVals = function () {
var self = this;
var st = this.state;
var view = st.view;
var WA = 'https://wa.me/31643542934';
var MAIL = 'mailto:mushgroep@gmail.com';
var enc = encodeURIComponent;
var euro = function (n) { return '€ ' + n.toFixed(2).replace('.', ','); };
var label = function (p) { return p.price == null ? '[PRIJS]' : euro(p.price); };
var real = function (name, price, cat) { return { photo: '[PRODUCTFOTO]', name: name, price: price, cat: cat }; };
var ph = function (n, cat) { return { photo: '[PRODUCTFOTO ' + n + ']', name: '[PRODUCTNAAM]', price: null, cat: cat }; };
var eight = function (cat) { return [1, 2, 3, 4, 5, 6, 7, 8].map(function (n) { return ph(n, cat); }); };
var tegel = real('Tegel laminaat zwart', 12.99, 0);
var visgraat = real('Visgraat laminaat houtlook', 11.99, 0);
var kunstgras = real('Kunstgras Rotterdam', 8.99, -1);
var clickLam = real('Laminaat', 7.95, 0);
var data = [
{ name: 'Laminaat', group: 'Vloeren', products: [18, 19, 20, 21, 22, 23, 24, 25, 26, 27].map(function (n, i) { return { name: 'Laminaat ' + (i + 1), price: 7.95, cat: 0, img: 'laminaat/foto' + n + '.webp' }; }) },
{ name: 'Click PVC visgraat', group: 'Vloeren', products: [43, 44, 45, 46, 47, 48].map(function (n, i) { return { name: 'Click PVC visgraat ' + (i + 1), price: 18.95, cat: 1, img: 'visgraat%20klik%20PVC/foto' + n + '.webp' }; }) },
{ name: 'Plak PVC visgraat', group: 'Vloeren', products: [49, 50, 51, 52].map(function (n, i) { return { name: 'Plak PVC visgraat ' + (i + 1), price: 23.95, cat: 2, img: 'visgraat%20plak%20PVC/foto' + n + '.webp' }; }) },
{ name: 'PVC marmerlook panelen', group: 'Wandpanelen', products: [28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42].map(function (n, i) { return { name: 'PVC marmerlook paneel ' + (i + 1), price: 35, cat: 3, img: 'PVC%20wandpanelen/foto' + n + '.webp' }; }) },
{ name: 'Akoestische panelen', group: 'Wandpanelen', products: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17].map(function (n, i) { return { name: 'Akoestisch paneel ' + (i + 1), price: 35, cat: 4, img: 'akoestische%20wandpanelen/foto' + (n === 0 ? '' : n) + '.webp' }; }) }
];
var sel = (view < 0 || view > 4) ? 0 : view;
var INTRO = [
'Laminaat met kliksysteem: zonder lijm te leggen en prima zelf te doen. Een slijtvaste, betaalbare vloer met een natuurlijke houtlook. Kom de dessins bekijken in onze showroom.',
'Visgraatvloeren in PVC met een kliksysteem: geen lijm nodig en snel gelegd. PVC is waterbestendig en makkelijk schoon te houden. Zo krijg je de uitstraling van een klassieke visgraatvloer.',
'Visgraat PVC die op de ondergrond wordt verlijmd. Dat geeft een stevige vloer zonder kliknaden. De ondergrond moet wel vlak en schoon zijn, vraag ons gerust om advies.',
'PVC wandpanelen met een marmerlook, voor een luxe uitstraling zonder echt steen. Ze zijn waterbestendig en makkelijk schoon te maken, ook handig in de keuken of badkamer. Bekijk de uitvoeringen in onze showroom.',
'Wandpanelen met houtlook latten op een geluiddempende laag. Ze dempen galm en geven een ruimte direct sfeer. Beschikbaar in meerdere kleuren, van licht eiken tot zwart, kom ze bekijken in de showroom.'
];
 
var jump = function (id, smooth) {
setTimeout(function () {
var el = document.getElementById(id);
if (el && el.scrollIntoView) el.scrollIntoView({ behavior: smooth ? 'smooth' : 'instant', block: 'start' });
}, smooth ? 80 : 0);
};
var stop = function (e) { if (e && e.preventDefault) e.preventDefault(); };
var go = function (i) {
return function (e) {
stop(e);
self.setState({ view: i, menuOpen: false, searchOpen: false });
jump('top', false);
};
};
var nav = function (id) {
return function (e) {
stop(e);
var wasHome = self.state.view < 0;
self.setState({ view: -1, menuOpen: false, searchOpen: false });
jump(id, wasHome);
};
};
var th = function (u) { return u; };
var byKey = {};
data.forEach(function (c) { c.products.forEach(function (p) { if (p.img) byKey[p.img] = p; }); });
var favs = (st.favs || []).filter(function (k) { return byKey[k]; });
var quote = (st.quote || []).filter(function (k) { return byKey[k]; });
var isFav = function (k) { return favs.indexOf(k) >= 0; };
var setFavs = function (list) {
try { localStorage.setItem('fw-favs', JSON.stringify(list)); } catch (err) {}
self.setState({ favs: list });
};
var toggleFav = function (k) {
var l = favs.slice();
var i = l.indexOf(k);
if (i >= 0) l.splice(i, 1); else l.push(k);
setFavs(l);
};
var quoteMsg = function (keys) {
return keys.length ? 'Ik wil graag een offerte voor: ' + keys.map(function (k) { return byKey[k].name; }).join(', ') + '.' : '';
};
var openQuote = function (keys) {
var form = {};
for (var k in self.state.form) form[k] = self.state.form[k];
var msg = quoteMsg(keys);
form['of-bericht'] = msg;
self.setState({ view: 11, menuOpen: false, searchOpen: false, lb: -1, form: form, quote: keys, autoMsg: msg, soort: -1, soortOpen: false });
var box = document.getElementById('of-bericht');
if (box) box.value = msg;
jump('top', false);
};
var ask = function (p) {
return function (e) {
stop(e);
if (p.img) { openQuote([p.img]); return; }
var form = {};
for (var k in self.state.form) form[k] = self.state.form[k];
var known = p.name.charAt(0) !== '[';
var msg = known ? 'Ik wil graag een offerte voor: ' + p.name + '.' : (form['of-bericht'] || '');
form['of-bericht'] = msg;
var next = { view: 11, menuOpen: false, searchOpen: false, form: form, quote: [], autoMsg: '', lb: -1 };
if (p.cat >= 0) next.soort = p.cat;
self.setState(next);
var box = document.getElementById('of-bericht');
if (box) box.value = msg;
jump('top', false);
};
};
var show = function (p, idx) {
var known = p.name.charAt(0) !== '[';
var text = known ? 'Hallo, ik heb interesse in ' + p.name + '. Kunnen jullie mij meer vertellen?' : 'Hallo, ik heb een vraag over jullie producten.';
var out = { thumb: p.img ? th(p.img) : '', photo: p.photo, name: p.name, price: p.priceText || label(p), ask: ask(p), wa: WA + '?text=' + enc(text), img: p.img || '', hasImg: !!p.img, noImg: !p.img };
if (p.img) {
var on = isFav(p.img);
out.heartFill = on ? '#E5484D' : 'none';
out.heartStroke = on ? '#E5484D' : '#13244A';
out.favPressed = on ? 'true' : 'false';
out.favLabel = (on ? 'Uit selectie halen: ' : 'Zet in selectie: ') + p.name;
out.fav = function (e) { stop(e); toggleFav(p.img); };
out.open = function (e) {
stop(e);
self.setState({ lb: idx, lbKeys: products.map(function (x) { return x.img; }) });
setTimeout(function () { var c = document.getElementById('lb-close'); if (c && c.focus) c.focus(); }, 0);
};
}
return out;
};
 
var products = data[sel].products.slice();
if (st.sort === 'asc' || st.sort === 'desc') {
var dir = st.sort === 'asc' ? 1 : -1;
products.sort(function (a, b) {
if (a.price == null && b.price == null) return 0;
if (a.price == null) return 1;
if (b.price == null) return -1;
return (a.price - b.price) * dir;
});
}
 
var pad = function (n) { return (n < 10 ? '0' : '') + n; };
var hm = function (m) { return pad(Math.floor(m / 60)) + ':' + pad(m % 60); };
var now = new Date();
var wd = now.getDay();
var mins = now.getHours() * 60 + now.getMinutes();
try {
var fmt = new Intl.DateTimeFormat('en-GB', { timeZone: 'Europe/Amsterdam', weekday: 'short', hour: '2-digit', minute: '2-digit', hour12: false });
var got = {};
fmt.formatToParts(now).forEach(function (p) { got[p.type] = p.value; });
var idx = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'].indexOf(got.weekday);
if (idx >= 0) { wd = idx; mins = (Number(got.hour) % 24) * 60 + Number(got.minute); }
} catch (err) {}
var sched = [[720, 960], null, [600, 1080], [600, 1080], [600, 1080], [600, 1080], [600, 1080]];
var dayNames = ['zondag', 'maandag', 'dinsdag', 'woensdag', 'donderdag', 'vrijdag', 'zaterdag'];
var todaySched = sched[wd];
var isOpenNow = !!todaySched && mins >= todaySched[0] && mins < todaySched[1];
var openText = '';
if (isOpenNow) openText = 'Sluit vandaag om ' + hm(todaySched[1]);
else if (todaySched && mins < todaySched[0]) openText = 'Opent vandaag om ' + hm(todaySched[0]);
else {
for (var step = 1; step <= 7 && !openText; step++) {
var nd = (wd + step) % 7;
if (sched[nd]) openText = 'Opent ' + (step === 1 ? 'morgen' : dayNames[nd]) + ' om ' + hm(sched[nd][0]);
}
}
var num = function (v) { var n = parseFloat(String(v || '').replace(',', '.')); return n > 0 ? n : 0; };
var cl = num(st.calc['calc-l']);
var cb = num(st.calc['calc-b']);
var area = cl * cb;
var need = area > 0 ? Math.ceil(area * (st.calc.extra ? 1.1 : 1)) : 0;
var nl = function (n) { return (Math.round(n * 10) / 10).toString().replace('.', ','); };
 
var shortNames = ['Laminaat', 'Click PVC', 'Plak PVC', 'PVC marmerlook', 'Akoestisch'];
var cats = data.map(function (c, i) { return { name: c.name, short: shortNames[i], thumb: th(c.products[0].img), group: c.group, current: view === i, other: view !== i, go: go(i) }; });
var groupTabs = ['Vloeren', 'Wandpanelen'].map(function (g) {
var first = 0;
for (var gi = 0; gi < data.length; gi++) { if (data[gi].group === g) { first = gi; break; } }
var cur = view >= 0 && view <= 4 && data[sel].group === g;
return { name: g, current: cur, other: !cur, go: go(first) };
});
var subCats = cats.filter(function (c) { return c.group === data[sel].group; });
var soorten = data.map(function (c, i) {
return {
name: c.name,
group: c.group,
head: i === 0 || data[i - 1].group !== c.group,
selected: st.soort === i,
sel: st.soort === i ? 'true' : 'false',
pick: function () { self.setState({ soort: i, soortOpen: false }); }
};
});
 
var f = st.form;
var val = function (k) { return (f[k] || '').trim(); };
var adres = (val('of-straat') + ' ' + val('of-huisnr') + ' ' + val('of-toev')).trim() + ', ' + val('of-postcode') + ' ' + val('of-plaats');
var quoteCats = [];
quote.forEach(function (k) { var c = byKey[k].cat; if (quoteCats.indexOf(c) < 0) quoteCats.push(c); });
var productLine = quote.length ? quoteCats.map(function (c) { return data[c].name; }).join(' + ') : (st.soort < 0 ? '' : data[st.soort].name);
var offerteText = ['Offerteaanvraag via de website', '', 'Product: ' + productLine, 'Aantal m2: ' + val('of-m2'), '', 'Naam: ' + (val('of-voornaam') + ' ' + val('of-achternaam')).trim(), 'Telefoon: ' + val('of-tel'), 'E-mail: ' + val('of-mail'), 'Adres: ' + adres, '', 'Bericht: ' + val('of-bericht')].join('\n');
var errors = {};
var order = ['of-voornaam', 'of-achternaam', 'of-tel', 'of-mail', 'of-straat', 'of-huisnr', 'of-postcode', 'of-plaats', 'soort', 'of-m2'];
if (!quote.length && st.soort < 0) errors['soort'] = 'Kies een product.';
if (!val('of-voornaam')) errors['of-voornaam'] = 'Vul je voornaam in.';
if (!val('of-achternaam')) errors['of-achternaam'] = 'Vul je achternaam in.';
var digits = val('of-tel').replace(/\D/g, '');
if (digits.length < 10 || digits.length > 13) errors['of-tel'] = 'Vul een geldig telefoonnummer in.';
if (!/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(val('of-mail'))) errors['of-mail'] = 'Vul een geldig e-mailadres in.';
if (!(parseFloat(val('of-m2').replace(',', '.')) > 0)) errors['of-m2'] = 'Vul het aantal m² in.';
if (!val('of-straat')) errors['of-straat'] = 'Vul je straat in.';
if (!/^\d+/.test(val('of-huisnr'))) errors['of-huisnr'] = 'Vul je huisnummer in.';
if (!/^\d{4}\s?[A-Za-z]{2}$/.test(val('of-postcode'))) errors['of-postcode'] = 'Vul een geldige postcode in, bijvoorbeeld 1234 AB.';
if (!val('of-plaats')) errors['of-plaats'] = 'Vul je woonplaats in.';
var firstBad = null;
order.forEach(function (k) { if (firstBad === null && errors[k]) firstBad = k; });
 
var cerrors = {};
var cOrder = ['cf-voornaam', 'cf-achternaam', 'cf-mail', 'cf-tel', 'cf-vraag'];
if (!val('cf-voornaam')) cerrors['cf-voornaam'] = 'Vul je voornaam in.';
if (!val('cf-achternaam')) cerrors['cf-achternaam'] = 'Vul je achternaam in.';
if (!/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(val('cf-mail'))) cerrors['cf-mail'] = 'Vul een geldig e-mailadres in.';
var cdigits = val('cf-tel').replace(/\D/g, '');
if (val('cf-tel') && (cdigits.length < 10 || cdigits.length > 13)) cerrors['cf-tel'] = 'Vul een geldig telefoonnummer in of laat het leeg.';
if (!val('cf-vraag')) cerrors['cf-vraag'] = 'Vul je vraag in.';
var cFirstBad = null;
cOrder.forEach(function (k) { if (cFirstBad === null && cerrors[k]) cFirstBad = k; });
var contactLines = ['Vraag via de website', '', 'Naam: ' + (val('cf-voornaam') + ' ' + val('cf-achternaam')).trim(), 'E-mail: ' + val('cf-mail')];
if (val('cf-tel')) contactLines.push('Telefoon: ' + val('cf-tel'));
if (val('cf-onderwerp')) contactLines.push('Onderwerp: ' + val('cf-onderwerp'));
contactLines.push('', 'Vraag: ' + val('cf-vraag'));
var contactText = contactLines.join('\n');
var allErrors = {};
if (st.tried) for (var ek in errors) allErrors[ek] = errors[ek];
if (st.cTried) for (var ck in cerrors) allErrors[ck] = cerrors[ck];
 
var allReal = [clickLam, tegel, visgraat, kunstgras];
var q = st.query.trim().toLowerCase();
var results = allReal.filter(function (p) { return !q || p.name.toLowerCase().indexOf(q) >= 0; }).map(show);
 
var lbKeys = st.lbKeys || [];
var lbN = lbKeys.length;
var lbKey = (st.lb >= 0 && st.lb < lbN) ? lbKeys[st.lb] : null;
var lbP = lbKey ? byKey[lbKey] : null;
var lbGo = function (d) { return function (e) { stop(e); if (lbN > 1) self.setState({ lb: (st.lb + d + lbN) % lbN }); }; };
var selNames = favs.map(function (k) { return byKey[k].name; });
return {
lbOpen: !!lbP,
lbName: lbP ? lbP.name : '',
lbCount: lbP ? (st.lb + 1) + ' / ' + lbN : '',
lbSrc: lbKey || '',
lbPreload: lbP && lbN > 1 ? [lbKeys[(st.lb + 1) % lbN], lbKeys[(st.lb - 1 + lbN) % lbN]] : [],
lbMulti: lbN > 1,
lbFavOn: lbP ? isFav(lbKey) : false,
lbFavText: lbP && isFav(lbKey) ? 'In selectie' : 'Zet in selectie',
lbClose: function (e) { stop(e); self.setState({ lb: -1 }); },
lbPrev: lbGo(-1),
lbNext: lbGo(1),
lbFav: function (e) { stop(e); if (lbKey) toggleFav(lbKey); },
lbAsk: function (e) { stop(e); if (lbKey) openQuote([lbKey]); },
lbBackdrop: function (e) { if (e && e.target === e.currentTarget) self.setState({ lb: -1 }); },
selOpen: favs.length > 0 && view !== 11,
selText: favs.length === 1 ? '1 product gekozen' : favs.length + ' producten gekozen',
selThumbs: favs.slice(0, 3).map(function (k) { return { img: th(k), name: byKey[k].name }; }),
selWa: favs.length ? WA + '?text=' + enc('Hallo, ik heb interesse in: ' + selNames.join(', ') + '. Kunnen jullie mij meer vertellen?') : '',
selAsk: function (e) { stop(e); if (favs.length) openQuote(favs.slice()); },
selClear: function (e) { stop(e); setFavs([]); },
hasQuote: view === 11 && quote.length > 0,
noQuote: !(view === 11 && quote.length > 0),
quoteCatsText: quoteCats.map(function (c) { return data[c].name; }).join(' + '),
quoteItems: quote.map(function (k) {
return { name: byKey[k].name, img: th(k), remove: function (e) {
stop(e);
var l = quote.filter(function (x) { return x !== k; });
var next = { quote: l, soort: -1 };
var nf = favs.filter(function (x) { return x !== k; });
try { localStorage.setItem('fw-favs', JSON.stringify(nf)); } catch (err) {}
next.favs = nf;
var cur = (self.state.form['of-bericht'] || '').trim();
if (!cur || cur === self.state.autoMsg) {
var msg = quoteMsg(l);
var form = {};
for (var f in self.state.form) form[f] = self.state.form[f];
form['of-bericht'] = msg;
next.form = form;
next.autoMsg = msg;
var box = document.getElementById('of-bericht');
if (box) box.value = msg;
}
self.setState(next);
} };
}),
isHome: view < 0,
isCat: view >= 0 && view <= 4,
isOver: view === 10,
isOfferte: view === 11,
isContact: view === 12,
cats: cats,
groupTabs: groupTabs,
subCats: subCats,
soorten: soorten,
floors: cats.filter(function (c) { return c.group === 'Vloeren'; }),
walls: cats.filter(function (c) { return c.group === 'Wandpanelen'; }),
catName: data[sel].name,
catIntro: INTRO[sel],
catGroup: data[sel].group,
catCount: data[sel].products.length + ' producten',
examples: products.map(show),
usps: ['Alleen A-merken', 'Laagste prijs', 'Altijd garantie', 'Showroom van 3.000 m²', 'Beste service'],
hours: [
{ day: 'Maandag', time: 'Gesloten', cls: wd === 1 ? 'hrow closed today' : 'hrow closed', today: wd === 1 },
{ day: 'Dinsdag', time: '10:00 – 18:00', cls: wd === 2 ? 'hrow today' : 'hrow', today: wd === 2 },
{ day: 'Woensdag', time: '10:00 – 18:00', cls: wd === 3 ? 'hrow today' : 'hrow', today: wd === 3 },
{ day: 'Donderdag', time: '10:00 – 18:00', cls: wd === 4 ? 'hrow today' : 'hrow', today: wd === 4 },
{ day: 'Vrijdag', time: '10:00 – 18:00', cls: wd === 5 ? 'hrow today' : 'hrow', today: wd === 5 },
{ day: 'Zaterdag', time: '10:00 – 18:00', cls: wd === 6 ? 'hrow today' : 'hrow', today: wd === 6 },
{ day: 'Zondag', time: '12:00 – 16:00', cls: wd === 0 ? 'hrow today' : 'hrow', today: wd === 0 }
],
go0: cats[0].go,
go1: cats[1].go,
go2: cats[2].go,
go3: cats[3].go,
go4: cats[4].go,
goHome: nav('top'),
navOver: go(10),
navOfferte: go(11),
navContact: go(12),
askTegel: ask(tegel),
askVisgraat: ask(visgraat),
askKunstgras: ask(kunstgras),
offerteWa: firstBad === null ? WA + '?text=' + enc(offerteText) : '',
offerteMail: firstBad === null ? MAIL + '?subject=' + enc('Offerteaanvraag via de website') + '&body=' + enc(offerteText) : '',
setField: function (e) {
var t = e && e.target;
if (!t || !t.id) return;
var form = {};
for (var k in self.state.form) form[k] = self.state.form[k];
form[t.id] = t.value;
self.setState({ form: form });
},
setSort: function (e) { self.setState({ sort: e.target.value }); },
soortName: st.soort < 0 ? 'Kies een product' : data[st.soort].name,
soortOpen: !!st.soortOpen,
sent: !!st.sent,
resetForm: function () {
['of-voornaam', 'of-achternaam', 'of-tel', 'of-mail', 'of-m2', 'of-straat', 'of-huisnr', 'of-toev', 'of-postcode', 'of-plaats', 'of-bericht'].forEach(function (id) {
var el = document.getElementById(id);
if (el) el.value = '';
});
self.setState({ form: {}, soort: -1, tried: false, sent: false, soortOpen: false, quote: [], autoMsg: '' });
},
isOpenNow: isOpenNow,
isClosedNow: !isOpenNow,
openDetail: openText,
calcResult: need > 0 ? need + ' m²' : '– m²',
calcSub: need > 0 ? ('Kamer van ' + nl(area) + ' m²' + (st.calc.extra ? ', plus 10% extra voor snijverlies' : ', zonder extra')) : 'Vul de lengte en breedte van de kamer in.',
setCalc: function (e) {
var t = e && e.target;
if (!t || !t.id) return;
var calc = {};
for (var k in self.state.calc) calc[k] = self.state.calc[k];
if (t.id === 'calc-extra') calc.extra = !!t.checked; else calc[t.id] = t.value;
self.setState({ calc: calc });
},
calcToOfferte: function (e) {
stop(e);
if (!(need > 0)) {
var miss = document.getElementById(cl > 0 ? 'calc-b' : 'calc-l');
if (miss && miss.focus) miss.focus();
return;
}
var form = {};
for (var k in self.state.form) form[k] = self.state.form[k];
form['of-m2'] = String(need);
self.setState({ view: 11, menuOpen: false, searchOpen: false, form: form });
var box = document.getElementById('of-m2');
if (box) box.value = String(need);
jump('top', false);
},
errors: allErrors,
formInvalid: st.tried && firstBad !== null,
cSent: !!st.cSent,
cInvalid: !!st.cTried && cFirstBad !== null,
contactWa: cFirstBad === null ? WA + '?text=' + enc(contactText) : '',
contactMail: cFirstBad === null ? MAIL + '?subject=' + enc(val('cf-onderwerp') || 'Vraag via de website') + '&body=' + enc(contactText) : '',
cSubmit: function (e) {
if (cFirstBad === null) {
setTimeout(function () { self.setState({ cSent: true }); }, 400);
return;
}
stop(e);
self.setState({ cTried: true });
var el = document.getElementById(cFirstBad);
if (el) {
if (el.focus) el.focus();
if (el.scrollIntoView) el.scrollIntoView({ behavior: 'smooth', block: 'center' });
}
},
cReset: function () {
var next = {};
for (var k in self.state.form) if (k.indexOf('cf-') !== 0) next[k] = self.state.form[k];
cOrder.concat(['cf-onderwerp']).forEach(function (id) {
var el = document.getElementById(id);
if (el) el.value = '';
});
self.setState({ form: next, cTried: false, cSent: false });
},
submitCheck: function (e) {
if (firstBad === null) {
setTimeout(function () { self.setState({ sent: true }); }, 400);
return;
}
stop(e);
self.setState({ tried: true, soortOpen: false });
var el = document.getElementById(firstBad === 'soort' ? 'soort-btn' : firstBad);
if (el) {
if (el.focus) el.focus();
if (el.scrollIntoView) el.scrollIntoView({ behavior: 'smooth', block: 'center' });
}
},
toggleSoort: function () { self.setState({ soortOpen: !self.state.soortOpen }); },
searchOpen: st.searchOpen,
toggleSearch: function (e) {
stop(e);
self.setState({ searchOpen: !self.state.searchOpen, menuOpen: false, query: '' });
var box = document.getElementById('zoek');
if (box) { box.value = ''; if (self.state.searchOpen && box.focus) box.focus(); }
},
setQuery: function (e) { self.setState({ query: e.target.value }); },
results: results,
noResults: results.length === 0,
closeMenu: function () { self.setState({ menuOpen: false }); },
menuOpen: st.menuOpen,
menuClosed: !st.menuOpen,
toggleMenu: function () { self.setState({ menuOpen: !self.state.menuOpen, searchOpen: false }); }
};
};
 
var app = new App();
 
function esc(v) {
return String(v == null ? '' : v).replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
}
function resolve(path, scope) {
var parts = path.split('.');
var v = (scope && Object.prototype.hasOwnProperty.call(scope, parts[0])) ? scope[parts[0]] : vals[parts[0]];
for (var i = 1; i < parts.length && v != null; i++) v = v[parts[i]];
return v;
}
function each(root, sel, fn) { Array.prototype.forEach.call(root.querySelectorAll(sel), fn); }
 
var lastView = null;
function render() {
var keepY = window.pageYOffset || 0;
var sameView = lastView === app.state.view;
if (sameView) document.body.style.minHeight = document.documentElement.scrollHeight + 'px';
vals = app.renderVals();
each(document, '[data-for]', function (host) {
var tpl = host.querySelector('template');
if (!tpl) return;
Array.prototype.slice.call(host.children).forEach(function (ch) { if (ch !== tpl) host.removeChild(ch); });
var list = vals[host.getAttribute('data-for')] || [];
var as = host.getAttribute('data-as');
var src = tpl.innerHTML;
list.forEach(function (item) {
var scope = {};
scope[as] = item;
var html = src.replace(/\{\{\s*([\w.$]+)\s*\}\}/g, function (m, p) { return esc(resolve(p, scope)); });
var box = document.createElement('template');
box.innerHTML = html;
var frag = box.content;
each(frag, '[data-if]', function (el) {
if (!resolve(el.getAttribute('data-if'), scope)) { if (el.parentNode) el.parentNode.removeChild(el); }
else el.removeAttribute('data-if');
});
each(frag, '[data-click]', function (el) {
var fn = resolve(el.getAttribute('data-click'), scope);
el.removeAttribute('data-click');
if (typeof fn === 'function') el.addEventListener('click', fn);
});
host.appendChild(frag);
});
});
each(document, '[data-if]', function (el) { el.hidden = !resolve(el.getAttribute('data-if')); });
each(document, '[data-text]', function (el) {
var t = String(resolve(el.getAttribute('data-text')));
if (el.textContent !== t) el.textContent = t;
});
each(document, '[data-err]', function (el) {
var id = el.getAttribute('data-err');
var msg = vals.errors[id] || '';
if (el.textContent !== msg) el.textContent = msg;
var field = document.getElementById(id);
if (field) {
field.classList.toggle('invalid', !!msg);
if (msg) field.setAttribute('aria-invalid', 'true'); else field.removeAttribute('aria-invalid');
}
});
each(document, '[data-href]', function (el) {
var url = resolve(el.getAttribute('data-href'));
if (url) {
el.setAttribute('href', url);
el.removeAttribute('role');
el.removeAttribute('tabindex');
} else {
el.removeAttribute('href');
el.setAttribute('role', 'button');
el.setAttribute('tabindex', '0');
}
});
var soortBtn = document.getElementById('soort-btn');
if (soortBtn) {
soortBtn.setAttribute('aria-expanded', app.state.soortOpen ? 'true' : 'false');
soortBtn.classList.toggle('dd-empty', app.state.soort < 0);
soortBtn.classList.toggle('invalid', !!vals.errors.soort);
}
var lbImg = document.getElementById('lb-img');
if (lbImg) {
if (vals.lbOpen) {
if (lbImg.getAttribute('src') !== vals.lbSrc) lbImg.setAttribute('src', vals.lbSrc);
lbImg.setAttribute('alt', vals.lbName);
(vals.lbPreload || []).forEach(function (u) { var im = new Image(); im.src = u; });
} else if (lbImg.getAttribute('src')) {
lbImg.removeAttribute('src');
}
}
var lbFavBtn = document.getElementById('lb-fav');
if (lbFavBtn) {
lbFavBtn.classList.toggle('on', !!vals.lbFavOn);
lbFavBtn.setAttribute('aria-pressed', vals.lbFavOn ? 'true' : 'false');
}
var ttl = TITLES[String(app.state.view)];
if (ttl && document.title !== ttl) document.title = ttl;
document.body.style.overflow = vals.lbOpen ? 'hidden' : '';
document.body.classList.toggle('has-bar', !!vals.selOpen);
lastView = app.state.view;
if (!sameView) {
var onChip = document.querySelector('.subnav .chip.on');
var navBox = onChip && onChip.parentNode ? onChip.closest('.subnav') : null;
if (navBox) navBox.scrollLeft = Math.max(0, onChip.offsetLeft - (navBox.clientWidth - onChip.offsetWidth) / 2);
}
if (sameView) {
document.body.style.minHeight = '';
if (Math.abs((window.pageYOffset || 0) - keepY) > 1) window.scrollTo(0, keepY);
}
}
 
function route() {
if (settingHash) return;
var name = '';
try { name = location.hash.replace('#', ''); } catch (err) { name = ''; }
var view = null;
for (var k in ROUTES) if (ROUTES[k] === name && name !== '') view = Number(k);
if (view === null) {
if (app.state.view === -1) return;
if (name !== '') return;
view = -1;
}
if (view !== app.state.view) {
app.state.view = view;
app.state.menuOpen = false;
app.state.searchOpen = false;
render();
var top = document.getElementById('top');
if (top && top.scrollIntoView) top.scrollIntoView({ behavior: 'instant', block: 'start' });
}
}
 
each(document, '[data-click]', function (el) {
var path = el.getAttribute('data-click');
el.addEventListener('click', function (e) {
var fn = resolve(path);
if (typeof fn === 'function') fn(e);
});
});
each(document, '[data-change]', function (el) {
var path = el.getAttribute('data-change');
var handler = function (e) {
var fn = resolve(path);
if (typeof fn === 'function') fn(e);
};
el.addEventListener('input', handler);
el.addEventListener('change', handler);
});
var form = document.getElementById('offerte-form');
if (form) form.addEventListener('submit', function (e) { e.preventDefault(); });
document.addEventListener('click', function (e) {
if (!app.state.soortOpen) return;
var t = e.target;
if (t && t.closest && t.closest('.dd')) return;
app.setState({ soortOpen: false });
});
document.addEventListener('keydown', function (e) {
if (app.state.lb >= 0) {
if (e.key === 'Escape') vals.lbClose();
else if (e.key === 'ArrowLeft') vals.lbPrev();
else if (e.key === 'ArrowRight') vals.lbNext();
return;
}
if (e.key === 'Escape' && app.state.soortOpen) app.setState({ soortOpen: false });
});
each(document, '[data-href]', function (el) {
el.addEventListener('keydown', function (e) {
if (el.hasAttribute('href')) return;
if (e.key === 'Enter' || e.key === ' ') { e.preventDefault(); el.click(); }
});
});
var lbEl = document.getElementById('lb');
if (lbEl) {
var swipeX = null;
lbEl.addEventListener('touchstart', function (e) { swipeX = e.touches[0].clientX; }, { passive: true });
lbEl.addEventListener('touchend', function (e) {
if (swipeX === null) return;
var dx = e.changedTouches[0].clientX - swipeX;
swipeX = null;
if (Math.abs(dx) > 50) { if (dx < 0) vals.lbNext(); else vals.lbPrev(); }
}, { passive: true });
}
if ('IntersectionObserver' in window && !(window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches)) {
var io = new IntersectionObserver(function (entries) {
entries.forEach(function (en) { if (en.isIntersecting) { en.target.classList.add('in'); io.unobserve(en.target); } });
}, { threshold: 0.08, rootMargin: '0px 0px -20px 0px' });
document.documentElement.classList.add('js-rv');
var homeEl = document.querySelector('[data-if="isHome"]');
each(homeEl || document, '.view', function (v) {
if (!homeEl) return;
Array.prototype.slice.call(v.children).forEach(function (el, i) {
if (i === 0 || el.tagName !== 'SECTION') return;
el.classList.add('rv');
io.observe(el);
});
});
}
var warm = [];
var warmList = [];
for (var wk in PRELOAD) warmList.push(PRELOAD[wk]);
var warmStep = function () {
warmList.splice(0, 6).forEach(function (u) { var im = new Image(); im.src = u; warm.push(im); });
if (warmList.length) setTimeout(warmStep, 120);
};
setTimeout(warmStep, 200);
window.addEventListener('hashchange', route);
render();
route();
setInterval(render, 60000);
})();
