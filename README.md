# DIOSAPROHIBIDADEANS
## 🌐 Conéctate conmigo
- 📸 [Instagram](https://instagram.com/tuusuario)
- 🎵 [TikTok](https://tiktok.com/@tuusuario)
- 🎥 [Streamlabs](https://streamlabs.com/tuusuario)
- 🎨 [Pixiv](https://pixiv.me/tuusuario)
## 🌐 Conéctate con DIOSAPROHIBIDA
- 📸 [Instagram](https://instagram.com/tuusuario)
- 🎵 [TikTok](https://tiktok.com/@tuusuario)
- 💬 [Telegram](https://t.me/tuusuario)
- 🌍 [Mi página web](https://tusitio.com)
app.py
python app.py
python "destreamointe,flask.py codigo.py"
Markdown Preview Enhanced

<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>💜 DIOSA PROHIBIDA — Espacio</title>
<style>
  /* pega aquí tu CSS (usa el estilo que prefieras) */
  :root{--neon1:#ff00ff;--neon2:#00ccff;--neon3:#ff66cc;--bg1:#050006;--bg2:#1a001a}
  *{box-sizing:border-box} body{margin:0;font-family:Segoe UI, Roboto, Arial;color:#fff;background:linear-gradient(120deg,var(--bg1),var(--bg2));}
  .menu{position:fixed;top:10px;left:50%;transform:translateX(-50%);width:calc(100% - 40px);max-width:1200px;background:rgba(0,0,0,0.35);backdrop-filter:blur(6px);border-radius:14px;padding:10px 18px;display:flex;gap:12px;align-items:center;justify-content:center;z-index:1000}
  .menu a{color:#fff;text-decoration:none;padding:8px 12px;border-radius:8px;font-weight:600}
  main{padding-top:110px;max-width:1100px;margin:0 auto}
  section{margin:40px 18px;padding:32px;border-radius:14px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(0,0,0,0.06));border:1px solid rgba(255,255,255,0.03)}
  h1,h2{font-family:Orbitron, sans-serif;text-align:center;color:#fff}
  .lead{max-width:900px;margin:14px auto 0;font-size:18px;line-height:1.8;text-align:justify;color:#f3eefe}
  .preview{display:flex;gap:12px;flex-wrap:wrap;justify-content:center;margin-top:12px}
  .preview img,.preview video{max-width:220px;border-radius:10px;border:3px solid rgba(255,255,255,0.04)}
  .tokens{display:flex;gap:10px;justify-content:center;margin-top:12px;flex-wrap:wrap}
  .tokens button{background:transparent;border:2px solid rgba(255,255,255,0.06);padding:12px 18px;border-radius:10px;color:#fff;font-weight:700;cursor:pointer}
  .privado{ text-align:center;padding:20px;border-radius:12px;border:2px dashed rgba(255,255,255,0.04);background: rgba(0,0,0,0.2);}
</style>
</head>
<body>

<nav class="menu">
  <a href="#romantica">💖 Romántica</a>
  <a href="#caliente">🔥 Caliente</a>
  <a href="#media">📤 Subir</a>
  <a href="#tokens">💳 Créditos</a>
  <a href="#privado">🔒 Privado</a>
</nav>

<main>
  <section id="romantica"><h1>🌹 Sección Romántica</h1>
    <p class="lead">... (texto romántico extenso, pega el que quieras aquí) ...</p>
  </section>

  <section id="caliente"><h1>🔥 Sección Caliente</h1>
    <div class="lead" style="text-align:center;">
      <p>... (frases cortas y directas) ...</p>
    </div>
  </section>

  <section id="media">
    <h2>📤 Subir Imágenes y Videos</h2>
    <p class="lead" style="text-align:center">Selecciona archivos; se guardarán en el servidor y los verás en la galería.</p>

    <form action="{{ url_for('upload') }}" method="post" enctype="multipart/form-data" style="text-align:center;">
      <input type="file" name="archivo" accept="image/*,video/*" multiple>
      <br><br>
      <button type="submit">Subir</button>
    </form>

    <div class="preview" id="preview">
      {% for archivo in archivos %}
        {% set lower = archivo.lower() %}
        {% if lower.endswith('.jpg') or lower.endswith('.jpeg') or lower.endswith('.png') or lower.endswith('.gif') %}
          <img src="{{ url_for('uploaded_file', filename=archivo) }}" alt="{{ archivo }}">
        {% elif lower.endswith('.mp4') or lower.endswith('.webm') or lower.endswith('.mov') %}
          <video controls src="{{ url_for('uploaded_file', filename=archivo) }}"></video>
        {% endif %}
      {% endfor %}
    </div>
  </section>

  <section id="tokens">
    <h2>💳 Enviar Créditos / Tokens</h2>
    <p class="lead" style="text-align:center">Botones de ejemplo. Si quieres PayPal real, configura PAYPAL_CLIENT_ID y PAYPAL_SECRET en .env y sigue los pasos.</p>

    <!-- Botones PayPal client-side ejemplo (necesita PAYPAL_CLIENT_ID en el template) -->
    <div style="text-align:center; margin-top:12px;">
      {% if paypal_client %}
        <!-- Carga SDK de PayPal (cliente sandbox/prod según ID) -->
        <script src="https://www.paypal.com/sdk/js?client-id={{ paypal_client }}&currency=USD"></script>
        <div id="paypal-button-container"></div>
        <script>
          paypal.Buttons({
            createOrder: function(data, actions){
              return fetch('/create-paypal-order', { method:'post' }).then(res=>res.json()).then(order => order.id);
            },
            onApprove: function(data, actions){
              return fetch('/capture-paypal-order/' + data.orderID, { method:'post' }).then(res=>res.json()).then(details => {
                alert('Pago completado (demo): ' + JSON.stringify(details));
                window.location.reload();
              });
            }
          }).render('#paypal-button-container');
        </script>
      {% else %}
        <div class="tokens">
          <button onclick="alert('Demo token 10')">Enviar 10</button>
          <button onclick="alert('Demo token 25')">Enviar 25</button>
          <button onclick="alert('Demo token 50')">Enviar 50</button>
        </div>
      {% endif %}
    </div>
  </section>

  <section id="privado">
    <h2>🔒 Zona Privada</h2>
    <div class="privado">
      <p>Contenido exclusivo. Para desbloquear, realiza un pago real o usa el botón demo.</p>
      <button onclick="document.getElementById('privateContent').style.display='block'">Desbloquear (demo)</button>
      <div id="privateContent" style="margin-top:12px; display:none;">
        <p><strong>Contenido privado:</strong> aquí iría tu vídeo o enlaces especiales.</p>
      </div>
    </div>
  </section>

</main>

</body>
</html>

