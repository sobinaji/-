# -<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CV Builder IA Pro - ¡Genera tu CV en 30 Segundos! (€4.99 Premium)</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 800px; margin: 0 auto; padding: 20px; background: #f4f4f4; }
        .form-group { margin: 10px 0; }
        input, textarea, select { width: 100%; padding: 10px; border: 1px solid #ddd; border-radius: 5px; }
        button { background: #ff6b35; color: white; padding: 15px; border: none; border-radius: 5px; font-size: 18px; cursor: pointer; width: 100%; }
        button:hover { background: #e55a2b; }
        #cv-output { margin-top: 20px; background: white; padding: 20px; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); white-space: pre-wrap; }
        .premium { color: #ff6b35; font-weight: bold; background: #fff3e0; padding: 10px; border-radius: 5px; }
        .stripe-btn { background: #6772e5; margin-top: 10px; }
    </style>
</head>
<body>
    <h1>🧠 CV Builder IA Pro - ¡Tu CV Perfecto en Segundos! (España/Europa)</h1>
    <p>Ingresa datos, IA genera CV pro optimizado ATS. <span class="premium">Premium: PDF + Plantillas por **€4.99/mes** (Stripe).</span></p>
    
    <form id="cvForm">
        <div class="form-group">
            <label>Nombre Completo:</label>
            <input type="text" id="nombre" required>
        </div>
        <div class="form-group">
            <label>Email / Teléfono:</label>
            <input type="text" id="contacto" required>
        </div>
        <div class="form-group">
            <label>Experiencia (lista):</label>
            <textarea id="experiencia" rows="4" placeholder="Ej: Dev en Google, 2020-2023..."></textarea>
        </div>
        <div class="form-group">
            <label>Educación:</label>
            <textarea id="educacion" rows="3" placeholder="Ej: Ingeniería Informática, UCM..."></textarea>
        </div>
        <div class="form-group">
            <label>Habilidades:</label>
            <input type="text" id="habilidades" placeholder="Ej: Python, React, IA">
        </div>
        <div class="form-group">
            <label>Puesto Deseado:</label>
            <input type="text" id="puesto" placeholder="Ej: Desarrollador Senior">
        </div>
        <button type="submit">¡GENERAR CV CON IA GRATIS! 🚀</button>
    </form>
    
    <div id="cv-output"></div>

    <script>
        const form = document.getElementById('cvForm');
        const output = document.getElementById('cv-output');
        
        form.addEventListener('submit', async (e) => {
            e.preventDefault();
            const data = {
                nombre: document.getElementById('nombre').value,
                contacto: document.getElementById('contacto').value,
                experiencia: document.getElementById('experiencia').value,
                educacion: document.getElementById('educacion').value,
                habilidades: document.getElementById('habilidades').value,
                puesto: document.getElementById('puesto').value
            };
            
            const prompt = `Genera CV profesional en Markdown para ${data.nombre} (${data.contacto}). Puesto: ${data.puesto}. 
            Experiencia: ${data.experiencia}. Educación: ${data.educacion}. Habilidades: ${data.habilidades}. 
            Optimizado ATS/Europa, atractivo, 1 página. Solo CV limpio.`;
            
            try {
                const response = await fetch('https://api.groq.com/openai/v1/chat/completions', {
                    method: 'POST',
                    headers: {
                        'Authorization': 'Bearer TU_CLAVE_GROQ_GRATIS',  // groq.com free
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        model: 'llama3-8b-8192',
                        messages: [{ role: 'user', content: prompt }],
                        max_tokens: 1000
                    })
                });
                const result = await response.json();
                const cv = result.choices[0].message.content;
                output.innerHTML = `<h2>¡CV IA Listo! 📄 Copia y pega en Word/PDF.</h2>
                <div style="background:#f9f9f9;padding:20px;border-left:5px solid #ff6b35;">${cv}</div>
                <button class="stripe-btn" onclick="upgradePremium()">🔥 PREMIUM €4.99/mes - PDF + Cover Letter</button>
                <p><em>Comparte en LinkedIn/InfoJobs para viralidad.</em></p>`;
            } catch (error) {
                output.innerHTML = `<p>Error: Regístrate en <a href="https://groq.com">groq.com</a> para clave gratis. Prompt: ${prompt}</p>`;
            }
        });
        
        function upgradePremium() {
            alert('¡Integra Stripe! Ve stripe.com, crea checkout €4.99. Código fácil: stripe.com/docs. ¡Gana €€€!');
        }
    </script>
</body>
</html>
