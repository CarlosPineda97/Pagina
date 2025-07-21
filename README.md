<html lang="es">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Fuerza de Seguridad Privada</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet" />
    <style>
      /* Estilos generales del cuerpo de la página */
      body {
        font-family: 'Poppins', sans-serif; /* Fuente moderna */
        background-color: #ffffff;          /* Fondo blanco */
        margin: 0;                          /* Elimina márgenes por defecto */
        padding: 0;                         /* Elimina relleno por defecto */
        display: flex;                      /* Usa flexbox para organizar verticalmente */
        flex-direction: column;            /* Coloca elementos en columna */
        align-items: center;               /* Centra horizontalmente los hijos */
      }

      /* Barra de navegación fija en la parte superior */
      .navbar {
        width: 100%;                       /* Ocupa todo el ancho */
        background: #000;                  /* Fondo negro */
        padding: 12px 0;                   /* Espaciado vertical */
        display: flex;                     /* Flexbox para organizar los botones */
        justify-content: center;          /* Centra los botones */
        flex-wrap: wrap;                  /* Permite que los botones se acomoden en varias líneas si es necesario */
        gap: 12px;                         /* Espacio entre botones */
        position: fixed;                  /* Fija la barra arriba */
        top: 0;                            /* Pegado al borde superior */
        z-index: 1000;                     /* Superposición para que no lo tapen otros elementos */
      }

      /* Estilo de los botones en la barra */
      .navbar button {
        background: transparent;          /* Fondo transparente */
        color: white;                     /* Texto blanco */
        border: none;                     /* Sin bordes */
        font-weight: 600;                 /* Texto en negrita */
        font-size: 18px;                  /* Tamaño de letra */
        cursor: pointer;                  /* Cursor de mano al pasar */
        padding: 5px 3px;                /* Espacio interno */
        border-radius: 6px;               /* Bordes redondeados */
      }

      /* Cambios al pasar el mouse o cuando el botón está activo */
      .navbar button:hover,
      .navbar button.active {
        background-color: #ccc;           /* Fondo gris claro */
        color: #000;                      /* Texto negro */
      }

      /* Contenedor principal del contenido (formularios) */
      main {
        padding-top: 100px;                /* Espacio arriba para que no quede pegado al logo */
        width: 90%;                       /* Ancho del 90% del viewport */
        max-width: 850px;                 /* Máximo 800px de ancho */
        scroll-margin-top: 100px;         /* Al hacer scroll, deja espacio por el navbar fijo */
      }

      /* Contenedor del logo */
      #logo-container {
        text-align: center;               /* Centra el logo */
        margin-bottom: 5px;               /* Espacio inferior */
        transition: opacity 0.4s ease;    /* Transición suave al ocultarlo/mostrarlo */
      }

      /* Imagen del logo */
      #logo-container img {
        max-width: 50%;                   /* El logo puede ocupar hasta el 50% del ancho */
        height: 55%;                      /* Altura relativa (se puede ajustar según necesidad) */
      }

      #logo-container.hide {
        opacity: 0;                           /* Se vuelve invisible */
        transform: translateY(-30px);         /* Se desplaza hacia arriba */
        height: 0;                            /* Quita el espacio vertical */
        margin: 0;                            /* Sin márgenes */
        padding: 0;                           /* Sin relleno */
        overflow: hidden;                     /* Oculta cualquier parte que sobresalga */
      }

      /* Estilos base para todos los formularios (inicialmente ocultos) */
      form {
        display: none;                    /* Ocultos por defecto */
        background-color: #fff;           /* Fondo blanco */
        padding: 20px;                    /* Espaciado interno */
        border-radius: 12px;              /* Bordes redondeados */
        box-shadow: 0 4px 10px rgba(0,0,0,0.1); /* Sombra suave */
        margin-bottom: 30px;              /* Espacio debajo */
        opacity: 0;                       /* Invisibles al principio */
        transform: translateY(15px);      /* Desplazados hacia abajo (para animación) */
        transition: opacity 0.5s ease, transform 0.5s ease; /* Animación suave al mostrar */
      }

      /* Cuando el formulario está activo (visible) */
      form.active {
        display: block;                   /* Se muestra */
        background-color: #000;           /* Fondo negro */
        color: white;                     /* Texto blanco */
        opacity: 1;                       /* Totalmente visible */
        transform: translateY(0);         /* Vuelve a su posición original */
      }

      /* Estilo de campos dentro de formularios activos */
      form.active label,
      form.active input,
      form.active select,
      form.active textarea {
        color: white;                     /* Texto blanco */
      }

      form.active input,
      form.active select,
      form.active textarea {
        background-color: #222;           /* Fondo gris oscuro */
        border: 1px solid #555;           /* Bordes gris medio */
      }

      /* Color del placeholder cuando el formulario está activo */
      form.active input::placeholder,
      form.active textarea::placeholder {
        color: #ccc;                      /* Color más tenue para texto de ayuda */
      }

      /* Estilo general para etiquetas */
      label {
        font-weight: bold;                /* Texto en negrita */
        display: block;                   /* Ocupan toda la línea */
        margin-top: 10px;                 /* Espacio superior */
      }

      /* Estilo general para inputs, selects y textareas */
      input, select, textarea {
        width: 100%;                      /* Ocupan todo el ancho disponible */
        padding: 10px;                    /* Espacio interno */
        margin-top: 6px;                  /* Espacio superior */
        margin-bottom: 15px;              /* Espacio inferior */
        border: 1px solid #ccc;           /* Borde gris claro */
        border-radius: 6px;               /* Bordes redondeados */
      }

      /* Estilo para los botones de enviar */
      button[type="submit"] {
        background-color: #ffffff;           /* Fondo negro */
        color: rgb(0, 0, 0);                     /* Texto blanco */
        font-weight: bold;                /* Negrita */
        border: none;                     /* Sin borde */
        padding: 10px;                    /* Espaciado */
        border-radius: 6px;               /* Bordes redondeados */
        cursor: pointer;                  /* Cursor de mano */
      }

      /* Efecto al pasar el mouse sobre el botón de enviar */
      button[type="submit"]:hover {
        background-color: #898989;           /* Fondo más claro al pasar el mouse */
      }

      /* Estilo para el título que aparece encima de cada formulario */
      .form-title {
        font-size: 22px;                  /* Tamaño grande de letra */
        font-weight: bold;               /* Negrita */
        margin-bottom: 20px;             /* Espacio debajo */
        color: white;                    /* Texto blanco */
        text-align: center;              /* Centrado */
      }
    </style>
  </head>
  <body>

    <nav class="navbar">
      <button onclick="showSection(null)">Inicio</button>
       <button onclick="window.open('https://docs.google.com/spreadsheets/d/e/2PACX-1vQRvRyuvWKYjDkWYnartnxSPhz91oqEtguU73bPzIeVid2rKR61O7Vsr1p1dDT869Tk5yFFpEibIx7B/pubhtml', '_blank')">Listados📋</button>
      <button onclick="showSection('guardias', 'Altas')">Altas✅</button>
      <button onclick="showSection('bajas', 'Bajas')">Bajas❌</button>
      <button onclick="showSection('armas', 'Armas')">Armas🔫</button>
      <button onclick="showSection('papeleria', 'Papelería')">Papelería📄</button>
      <button onclick="showSection('vale', 'Vale')">Vales💵</button>
      <button onclick="showSection('caja', 'caja')">Caja Chica💰</button>
      <button onclick="showSection('carro', 'carro')">Carros🚓</button>
          
    </nav>

    <div id="logo-container">
      <img src="img-FUSEPRI.jpg" alt="Logo Seguridad" />
    </div>

    <main>
      
      <form id="guardias" class="form" method="post" action="https://script.google.com/macros/s/AKfycbyqMu4YXcAzz10VVVD70Rx7wwuWX0YmbMs5J7umWJPgNUkjTNwbOkfj1dPYRMJxknoofA/exec">
        <div class="form-title">formulario de Altas</div>
        <input type="hidden" name="formulario" value="personas" />
        <label>Nombre completo:</label>
        <input type="text" name="nombre" required placeholder="Ej: Juan Pérez" />
        <label>ID:</label>
        <input type="number" name="cedula" required />
        <label>Teléfono:</label>
        <input type="number" name="telefono" required />
        <label>Dirección:</label>
        <input type="text" name="direccion" required />
        <label>Fecha de ingreso:</label>
        <input type="date" name="fecha" required />
        <label>Puesto asignado:</label>
        <select name="puesto" required>
          <option disabled selected>Seleccione el puesto</option>
          <option>Halcón 1</option>
          <option>Halcón 2</option>
          <option>Halcón 3</option>
          <option>Alhambra</option>
          <option>Comision</option>
          <option>Edificio</option>
          <option>Muralla China</option>
          <option>Aguila 1</option>
          <option>Aguila 2</option>
          <option>Aguila 3</option>
          <option>Aguila 4</option>
          <option>Halcón 3</option>
        </select>
        <label>Número de emergencia:</label>
        <input type="number" name="emergencia" />
        <input type="text" name="pertenece" placeholder="Pertenece a" />
        <label>Papeles pendientes:</label>
        <select name="papeles" required>
          <option disabled selected>Pendientes</option>
          <option>Ninguno</option>
          <option>Policiales</option>
          <option>Penales</option>
          <option>Ambos</option>
        </select>
        <label>Licencia:</label>
        <select name="licencia">
          <option disabled selected>Licencia</option>
          <option>Ninguno</option>
          <option>Motocicleta</option>
          <option>Carro</option>
          <option>Ambas</option>
        </select>
        <label>Registrado Por:</label>
        <select name="ingresado" required>
          <option disabled selected>Ingresado</option>
          <option>Oficina</option>
          <option>Christian</option>
          <option>Steven</option>
          <option>Don Ivan</option>
        </select>
        <label>Descripción adicional:</label>
        <textarea name="descripcion" rows="3" placeholder="Observaciones, condiciones, etc."></textarea>
        <button type="submit">Guardar Información</button>
      </form>

      <form id="bajas" class="form" method="post" action="https://script.google.com/macros/s/AKfycbyqMu4YXcAzz10VVVD70Rx7wwuWX0YmbMs5J7umWJPgNUkjTNwbOkfj1dPYRMJxknoofA/exec">
        <div class="form-title">Formulario de Bajas</div>
        <input type="hidden" name="formulario" value="bajas" />
        <label>Nombre del Guardia:</label>
        <input type="text" name="nombre" required />
        <label>Puesto asignado:</label>
        <select name="puesto" required>
          <option disabled selected>Seleccion de Puesto</option>
          <option>Halcón 1</option>
          <option>Halcón 2</option>
          <option>Halcón 3</option>
        </select>
        <label>Motivo de Baja</label>
        <input type="text" name="baja" required />
        <button type="submit">Guardar Información</button>
      </form>

      <form id="armas" class="form" method="post" action="https://script.google.com/macros/s/AKfycbyqMu4YXcAzz10VVVD70Rx7wwuWX0YmbMs5J7umWJPgNUkjTNwbOkfj1dPYRMJxknoofA/exec">
        <div class="form-title">Formulario de Armas</div>
        <input type="hidden" name="formulario" value="armas" />
        <label>Tipo de Arma:</label>
        <select name="arma" required>
          <option disabled selected>Seleccion de Arma</option>
          <option>Escopeta</option>
          <option>Revolver</option>
          <option>38</option>
          <option>39</option>
        </select>
        <label>Puesto asignado:</label>
        <select name="puesto" required>
          <option disabled selected>Seleccion de Puesto</option>
          <option>Halcón 1</option>
          <option>Halcón 2</option>
          <option>Halcón 3</option>
        </select>
        <label>Número de serie:</label>
        <input type="text" name="serie" required />
        <label>Permiso Emitido:</label>
        <input type="date" name="fechaEmitida" required />
        <label>Expiración del permiso:</label>
        <input type="date" name="fecha" required />
        <button type="submit">Guardar Información</button>
      </form>

      <form id="papeleria" class="form" method="post" action="https://script.google.com/macros/s/AKfycbyqMu4YXcAzz10VVVD70Rx7wwuWX0YmbMs5J7umWJPgNUkjTNwbOkfj1dPYRMJxknoofA/exec">
        <div class="form-title">Formulario de Papelería</div>
        <input type="hidden" name="formulario" value="papeleria" />
        <label>Escritorio:</label>
        <select name="escritorio" required>
          <option disabled selected>Seleccione el escritorio</option>
          <option>Escritorio1</option>
          <option>Escritorio2</option>
          <option>Escritorio3</option>
        </select>
        <label>Gaveta:</label>
        <select name="gaveta" required>
          <option disabled selected>Seleccione la gaveta</option>
          <option>Gaveta1</option>
          <option>Gaveta2</option>
          <option>Gaveta3</option>
          <option>Gaveta4</option>
          <option>Gaveta5</option>
        </select>
        <label>Folder:</label>
        <input type="text" name="folder" required />
        <label>Contenido:</label>
        <input type="text" name="contenido" required />
        <button type="submit">Guardar</button>
      </form>

      <form id="vale" class="form" method="post" action="https://script.google.com/macros/s/AKfycbxnGB0bQaLkVM9N06pc8S-S6f4pBAhLpZuJ4gN-D_E4_7WUuvH2Or970cpFHkMsfd0Lkg/exec">
        <div class="form-title">Formulario de Vales</div>
        <input type="hidden" name="formulario" value="vale" />
         <label>Tipo de Vale:</label>
        <label>Nombre:</label>
        <input type="text" name="nombre" required />
         <select name="vales" required>
          <option disabled selected>Seleccione el Vale</option>
          <option>Anticipo</option>
          <option>Prestamo</option>          
        </select>
        <label>Puesto Asignado:</label>
        <select name="puesto" required>
          <option disabled selected>Seleccion de Puesto</option>
          <option>Halcón 1</option>
          <option>Halcón 2</option>
          <option>Halcón 3</option>
        </select>
        <label>Cantidad:</label>
        <input type="text" name="cantidad" required />
        <label>Fecha:</label>
        <input type="date" name="fecha" required />
        <label>Descripcion:</label>
        <input type="text" name="descripcion" required />
        <button type="submit">Guardar Información</button>
      </form>

      <form id="caja" action="">
        <section id="caja" class="form">
          <input type="hidden" name="formulario" value="cajaC" />
          <div class="form-title">Caja Chica</div>
          <div style="display: flex; gap: 10px; justify-content: center;">
            <button type="button" onclick="showSection('ingreso')">💰 Ingreso</button>
            <button type="button" onclick="showSection('egreso')">🧾 Egreso</button>
          </div>
        </section>

      </form>
      
      <form id="ingreso" class="form" method="post" action="https://script.google.com/macros/s/AKfycbwZ9y5SXQ4-TuopA_GrmkYS8RkRvHMr7s84tCBsSULCbK-oHXstwmHP43eojPPSaH00rg/exec">
        <input type="hidden" name="formulario" value="ingreso" />
        <label>Cantidad:</label>
        <input type="text" name="cantidad" required />
        <label>Fecha:</label>
        <input type="date" name="fecha" required />
        <button type="submit">Guardar Información</button>
      </form>

      <form id="egreso" class="form" method="post" action="https://script.google.com/macros/s/AKfycbwc4V4bjuJaV4-flDL0c5thPlMHZ35PKdArMv2v5mfs_KjsebFafapIbjubyU2CDJ_8Kg/exec" >
        <input type="hidden" name="formulario" value="egreso" />
        <label>Cantidad:</label>
        <input type="text" name="cantidad" required />
        <label>Fecha:</label>
        <input type="date" name="fecha" required />
        <label>Descripcion:</label>
        <input type="text" name="descripcion" required />
        <button type="submit">Guardar Información</button>
      </form>
      
      <form id="carro" action="">
         <section id="carro" class="form">
        <input type="hidden" name="formulario" value="carro" />
        <div class="form-title">Carro</div>
        <div style="display: flex; gap: 10px; justify-content: center;">
          <button type="button" onclick="showSection('gasolina')">Gasolina⛽</button>
          <button type="button" onclick="showSection('mantenimiento')">Mantenimeinto🧰</button>
        </div>
      </section>


      </form>
     
      <form id="mantenimiento" class="form" method="post" action="https://script.google.com/macros/s/AKfycbzgRu2_TOvBeAvRIN9DPT4tQYOn6XjIXulUB5bjt0fMteADm5MlyOMxEAG6AaG8lwHzEQ/exec">
        <div class="form-title">Registro de Mantenimiento</div>
        <input type="hidden" name="formulario" value="mantenimiento" />
        <label>Gasto en mantenimiento:</label>
        <input type="number" name="monto" required />
        <label>Detalle:</label>
        <input type="text" name="detalle" />
        <label>Fecha:</label>
        <input type="date" name="fecha" required />
        <label>Carro:</label>
        <select name="automotor" required>
          <option disabled selected>Seleccione Carro</option>
          <option>Patrulla</option>
          <option>Moto 150</option>
        </select>
        <button type="submit">Guardar mantenimiento</button>
      </form>

      <form id="gasolina" class="form" method="post" action="https://script.google.com/macros/s/AKfycbxerwE73KLCDPxqxYXbG2HwiwjKnqICn6E0EtHnZKb3mIJTwj5UUH1kdz_DMGi5WTUJYA/exec">
        <div class="form-title">Registro de Combustible</div>
        <input type="hidden" name="formulario" value="gasolina" />
        <label>Cantidad Tranferida:</label>
        <input type="number" name="transferencia" required />
        <label>Cantidad:</label>
        <input type="number" name="gastos" required />
        <label>Fecha:</label>
        <input type="date" name="fecha" required />
        <label>Carro:</label>
        <select name="automotor" required>
          <option disabled selected>Seleccione Carro</option>
          <option>Patrulla</option>
          <option>Moto 150</option>
        </select>
        <button type="submit">Guardar combustible</button>
      </form>

    </main>

    <script>
        // Función de búsqueda
        document.getElementById("buscarForm").addEventListener("submit", function(e) {
        e.preventDefault();
        const nombre = document.getElementById("nombreBuscar").value;
        const hoja = document.getElementById("hojaBuscar").value;

        const url = `https://script.google.com/macros/s/AKfycbxXL8eMmWB9--GsETVRB_GIfFuH3dxj4bZKNd_JCqNlKdhVoSmuXD6IlgnE9byn8V6bPA/exec?nombre=${encodeURIComponent(nombre)}&hoja=${encodeURIComponent(hoja)}`;

        fetch(url)
          .then(res => res.json())
          .then(data => {
            const contenedor = document.getElementById("resultadoBusqueda");
            if (data.length > 0) {
              contenedor.innerHTML = "<strong>Resultados encontrados:</strong><br><br>" +
                data.map(fila => fila.join(" | ")).join("<br>");
            } else {
              contenedor.innerHTML = "No se encontraron resultados.";
            }
          })
          .catch(error => {
            console.error("Error en búsqueda:", error);
            document.getElementById("resultadoBusqueda").innerText = "Ocurrió un error en la búsqueda.";
          });
      });

      // ✅ Función única y correcta para mostrar formularios
      function showSection(id) {
        document.querySelectorAll("form").forEach(f => f.classList.remove("active"));
        document.getElementById("logo-container").classList.add("hide");

        const form = document.getElementById(id);
        if (form) {
          form.classList.add("active");
          setTimeout(() => {
            form.scrollIntoView({ behavior: "smooth", block: "start" });
          }, 15);
        } else {
          document.getElementById("logo-container").classList.remove("hide");
        }
      }
    </script>

    
  </body>
</html>
