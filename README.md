<!doctype html>
<html lang="fr">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Tags approuves - Hell in Paradise</title>
<style>
  :root{
    --bg:#0e0f13; --card:#171922; --line:#272a36;
    --txt:#e7e9ef; --dim:#9aa0b0; --accent:#c0392b; --ok:#2e8b57;
  }
  *{box-sizing:border-box}
  body{
    margin:0; padding:32px 16px 64px;
    background:var(--bg); color:var(--txt);
    font:16px/1.55 system-ui,-apple-system,Segoe UI,Roboto,sans-serif;
  }
  .wrap{max-width:960px;margin:0 auto}
  h1{margin:0 0 6px;font-size:28px;letter-spacing:.5px}
  .sub{color:var(--dim);margin:0 0 28px}
  .howto{
    background:var(--card);border:1px solid var(--line);border-radius:10px;
    padding:16px 18px;margin-bottom:32px
  }
  .howto h2{margin:0 0 8px;font-size:15px;text-transform:uppercase;letter-spacing:1px;color:var(--dim)}
  .howto ol{margin:0;padding-left:20px}
  .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:20px}
  .card{background:var(--card);border:1px solid var(--line);border-radius:10px;overflow:hidden;display:flex;flex-direction:column}
  .thumb{
    aspect-ratio:1/1;display:flex;align-items:center;justify-content:center;
    background:repeating-conic-gradient(#20222c 0 25%,#191b24 0 50%) 50%/20px 20px;
    padding:14px
  }
  .thumb img{max-width:100%;max-height:100%;object-fit:contain}
  .meta{padding:14px;border-top:1px solid var(--line)}
  .name{font-weight:600;margin:0 0 8px}
  .url{
    display:block;width:100%;font:12px/1.4 ui-monospace,Consolas,monospace;
    color:var(--dim);background:#0f111a;border:1px solid var(--line);
    border-radius:6px;padding:8px;word-break:break-all;margin-bottom:10px
  }
  button{
    width:100%;padding:9px;border:0;border-radius:6px;cursor:pointer;
    background:var(--accent);color:#fff;font-weight:600;font-size:14px
  }
  button.copied{background:var(--ok)}
  footer{margin-top:40px;color:var(--dim);font-size:13px;text-align:center}
</style>
</head>
<body>
<div class="wrap">
  <h1>Tags approuves</h1>
  <p class="sub">Les seules images utilisables pour les graffitis sur Hell in Paradise.</p>

  <div class="howto">
    <h2>Comment s'en servir</h2>
    <ol>
      <li>Copie l'adresse du tag que tu veux.</li>
      <li>En jeu, prends une bombe de peinture et vise un mur.</li>
      <li>Choisis le mode image et colle l'adresse.</li>
    </ol>
  </div>

  <div class="grid" id="grid"></div>

  <footer>Aucune autre adresse ne fonctionne. Demande a un admin pour faire ajouter un tag.</footer>
</div>

<script>
const BASE = location.origin + "/";
const TAGS = [
  { file: "cartel.png", name: "Cartel" }
];

const grid = document.getElementById("grid");

for (const tag of TAGS) {
  const url = BASE + tag.file;
  const card = document.createElement("div");
  card.className = "card";
  card.innerHTML =
    '<div class="thumb"><img alt="" loading="lazy"></div>' +
    '<div class="meta"><p class="name"></p><code class="url"></code>' +
    '<button type="button">Copier l\'adresse</button></div>';
  card.querySelector("img").src = url;
  card.querySelector(".name").textContent = tag.name;
  card.querySelector(".url").textContent = url;
  const btn = card.querySelector("button");
  btn.addEventListener("click", async () => {
    try { await navigator.clipboard.writeText(url); }
    catch (e) {
      const t = document.createElement("textarea");
      t.value = url; document.body.appendChild(t); t.select();
      document.execCommand("copy"); t.remove();
    }
    btn.textContent = "Copie !";
    btn.classList.add("copied");
    setTimeout(() => { btn.textContent = "Copier l'adresse"; btn.classList.remove("copied"); }, 1600);
  });
  grid.appendChild(card);
}
</script>
</body>
</html>
