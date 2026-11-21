# ATN_music
Música 
const tracks=[
 {title:"Luz de Medianoche",artist:"ATN Sessions",kind:"popular",symbol:"✦",duration:"3:42"},
 {title:"Ritmo del Cielo",artist:"Sonidos del Norte",kind:"energy",symbol:"◈",duration:"3:18"},
 {title:"Ecos de la Luna",artist:"Frecuencia Violeta",kind:"chill",symbol:"☾",duration:"4:05"},
 {title:"Ciudad Eléctrica",artist:"Neón Club",kind:"energy",symbol:"⚡",duration:"3:51"},
 {title:"Amanecer Suave",artist:"Nube Azul",kind:"chill",symbol:"☁",duration:"2:59"}
];
const list=document.querySelector('#trackList'), search=document.querySelector('#searchInput');
let current=null,playing=false;
function render(items){list.innerHTML='';items.forEach(t=>{const b=document.createElement('button');b.className='track';b.innerHTML=`<span class="cover">${t.symbol}</span><span class="track-copy"><b>${t.title}</b><span>${t.artist}</span></span><small>${t.duration}</small>`;b.addEventListener('click',()=>selectTrack(t));list.appendChild(b)});document.querySelector('#emptyState').classList.toggle('hidden',items.length>0)}
function selectTrack(t){current=t;playing=true;document.querySelector('#nowTitle').textContent=t.title;document.querySelector('#nowArtist').textContent=t.artist;document.querySelector('#playerArt').textContent=t.symbol;document.querySelector('#playButton').textContent='Ⅱ';document.querySelector('#progressFill').style.width='18%';document.querySelector('#playerNote').textContent='Vista previa visual · reproducción Apple Music pendiente'}
search.addEventListener('input',()=>{const q=search.value.toLowerCase();render(tracks.filter(t=>(t.title+' '+t.artist).toLowerCase().includes(q)))});
document.querySelectorAll('[data-filter]').forEach(b=>b.addEventListener('click',()=>render(tracks.filter(t=>t.kind===b.dataset.filter))));
document.querySelector('#playButton').addEventListener('click',()=>{if(!current){selectTrack(tracks[0]);return}playing=!playing;document.querySelector('#playButton').textContent=playing?'Ⅱ':'▶'});
document.querySelector('#searchNav').addEventListener('click',()=>search.focus());
document.querySelector('#libraryNav').addEventListener('click',()=>alert('Tu biblioteca personal se habilitará en la siguiente etapa.'));
render(tracks);
if('serviceWorker' in navigator)window.addEventListener('load',()=>navigator.serviceWorker.register('/sw.js').catch(()=>{}));
