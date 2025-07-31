# ACAPULCO-POST-OTIS
pagina web Acapulco
import { useState, useEffect } from "react";

export default function App() {
  const [visitas, setVisitas] = useState(0);
  const [proyectosRecibidos, setProyectosRecibidos] = useState([]);
  const [sugerenciasRecibidas, setSugerenciasRecibidas] = useState([]);

  // Contador de visitas (simulado)
  useEffect(() => {
    const visitasGuardadas = localStorage.getItem("visitasAcapulcoFuturo");
    const nuevasVisitas = visitasGuardadas ? parseInt(visitasGuardadas) + 1 : 1;
    setVisitas(nuevasVisitas);
    localStorage.setItem("visitasAcapulcoFuturo", nuevasVisitas);
  }, []);

  // Manejo de formularios
  const handleSubmitProyecto = (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    const proyecto = {
      nombre: formData.get("nombre"),
      correo: formData.get("correo"),
      titulo: formData.get("titulo"),
      descripcion: formData.get("descripcion"),
      fecha: new Date().toLocaleDateString(),
    };
    setProyectosRecibidos((prev) => [proyecto, ...prev]);
    alert("¡Gracias por tu proyecto! Lo revisaremos pronto.");
    e.target.reset();
  };

  const handleSubmitSugerencia = (e) => {
    e.preventDefault();
    const formData = new FormData(e.target);
    const sugerencia = {
      nombre: formData.get("nombre"),
      tema: formData.get("tema"),
      mensaje: formData.get("mensaje"),
      fecha: new Date().toLocaleDateString(),
    };
    setSugerenciasRecibidas((prev) => [sugerencia, ...prev]);
    alert("¡Gracias por tu sugerencia! Nos ayuda a mejorar.");
    e.target.reset();
  };

  return (
    <div className="min-h-screen bg-gradient-to-br from-blue-50 via-teal-50 to-green-50">
      {/* Header */}
      <header className="bg-white shadow-lg border-b-4 border-teal-500">
        <div className="max-w-7xl mx-auto px-4 py-6 text-center">
          <h1 className="text-4xl font-bold text-gray-800">
            Acapulco Futuro
          </h1>
          <p className="text-xl text-teal-600 mt-2">
            Reconstrucción Participativa tras el Huracán Otis
          </p>
          <div className="mt-4 bg-teal-100 text-teal-800 px-6 py-2 rounded-full inline-block text-lg font-medium">
            👋 ¡Bienvenido! Visitante #{visitas}
          </div>
        </div>
      </header>

      {/* Navigation */}
      <nav className="bg-white shadow-md sticky top-0 z-10">
        <div className="max-w-7xl mx-auto px-4">
          <div className="flex justify-center space-x-8 py-4">
            {["Inicio", "Bibliografía", "Mapas", "Proyectos", "Envía tu Proyecto", "Sugerencias"].map((item) => (
              <a
                key={item}
                href={`#${item}`}
                className="text-gray-700 hover:text-teal-600 font-medium transition-colors duration-200 px-3 py-2 rounded hover:bg-gray-100"
              >
                {item}
              </a>
            )}
          </div>
        </div>
      </nav>

      <main className="max-w-7xl mx-auto px-4 py-12 space-y-20">
        {/* Sección: Inicio */}
        <section id="Inicio" className="text-center">
          <h2 className="text-3xl font-bold text-gray-800 mb-6">Construyamos Acapulco juntos</h2>
          <p className="text-lg text-gray-600 max-w-4xl mx-auto leading-relaxed">
            Esta plataforma es un espacio abierto para la <strong>reconstrucción participativa</strong> de Acapulco después del paso del huracán Otis. 
            Aquí encontrarás información, mapas, proyectos y, lo más importante, <strong>tu voz cuenta</strong>. 
            Comparte tus ideas, proyectos o sugerencias para construir una ciudad más <strong>resiliente, inclusiva y sostenible</strong>.
          </p>
          <div className="mt-10 grid grid-cols-1 md:grid-cols-3 gap-8">
            <div className="bg-white p-6 rounded-xl shadow-md hover:shadow-lg transition-shadow">
              <div className="text-4xl mb-4">📚</div>
              <h3 className="text-xl font-semibold text-gray-800">Biblioteca Urbana</h3>
              <p className="text-gray-600 mt-2">Accede a estudios, informes y documentos clave sobre urbanismo, resiliencia y desarrollo sostenible.</p>
            </div>
            <div className="bg-white p-6 rounded-xl shadow-md hover:shadow-lg transition-shadow">
              <div className="text-4xl mb-4">🗺️</div>
              <h3 className="text-xl font-semibold text-gray-800">Mapas Interactivos</h3>
              <p className="text-gray-600 mt-2">Visualiza el crecimiento urbano, zonas de riesgo y propuestas de intervención con datos del GHSL.</p>
            </div>
            <div className="bg-white p-6 rounded-xl shadow-md hover:shadow-lg transition-shadow">
              <div className="text-4xl mb-4">💡</div>
              <h3 className="text-xl font-semibold text-gray-800">Tu Idea Importa</h3>
              <p className="text-gray-600 mt-2">Envía tu proyecto o sugerencia. ¡La ciudad se construye con todos!</p>
            </div>
          </div>
        </section>

        {/* Bibliografía */}
        <section id="Bibliografía" className="bg-white p-8 rounded-2xl shadow-lg">
          <h2 className="text-3xl font-bold text-gray-800 mb-6 text-center">Material Bibliográfico</h2>
          <div className="space-y-4 max-w-4xl mx-auto">
            {[
              "Naciones Unidas. (2016). Nueva Agenda Urbana.",
              "ONU-Hábitat. Manual de Calles: Diseño para ciudades humanas.",
              "Ortiz Ramírez, A. Manual práctico para comprender el urbanismo.",
              "INEGI. Censo de Población y Vivienda 2020.",
              "Banco Mundial. Evaluación de daños posteriores al huracán Otis (2023).",
              "JRC. Global Human Settlement Layer (GHSL), 2023.",
              "Documento: 'Ciudades y Desarrollo Urbano que dice la IA'",
            ].map((item, i) => (
              <div key={i} className="p-4 bg-gray-50 rounded-lg border-l-4 border-teal-500">
                <p className="text-gray-700">{item}</p>
              </div>
            ))}
          </div>
        </section>

        {/* Mapas */}
        <section id="Mapas" className="bg-white p-8 rounded-2xl shadow-lg">
          <h2 className="text-3xl font-bold text-gray-800 mb-6 text-center">Material Cartográfico</h2>
          <div className="grid grid-cols-1 lg:grid-cols-2 gap-8 items-center">
            <div>
              <h3 className="text-xl font-semibold text-gray-800 mb-4">Crecimiento urbano de Acapulco (1975–2020)</h3>
              <p className="text-gray-600 mb-4">
                Basado en datos del Global Human Settlement Layer (GHSL), el área construida pasó de 66.58 km² a 185.16 km². 
                Este crecimiento descontrolado aumentó la exposición al riesgo.
              </p>
              <ul className="text-gray-700 space-y-2">
                <li>📍 <strong>1975:</strong> 66.58 km²</li>
                <li>📍 <strong>1990:</strong> 98.34 km²</li>
                <li>📍 <strong>2000:</strong> 125.72 km²</li>
                <li>📍 <strong>2020:</strong> 185.16 km²</li>
              </ul>
            </div>
            <div className="bg-gradient-to-br from-blue-100 to-green-100 p-6 rounded-xl border-2 border-dashed border-teal-300 text-center">
              <div className="text-6xl mb-4">🗺️</div>
              <p className="text-gray-600">
                <strong>Mapa interactivo en desarrollo.</strong><br />
                Próximamente: visualización con Google Earth Engine y capas de riesgo, suelo y propuestas.
              </p>
            </div>
          </div>
        </section>

        {/* Proyectos Propuestos */}
        <section id="Proyectos" className="bg-white p-8 rounded-2xl shadow-lg">
          <h2 className="text-3xl font-bold text-gray-800 mb-6 text-center">Proyectos Propuestos</h2>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
            {[
              {
                titulo: "Urbanismo Táctico en La Sabana",
                desc: "Intervenciones temporales para probar rediseños viales, priorizando peatones y ciclistas.",
                icono: "🛠️",
              },
              {
                titulo: "Reubicación Segura de Asentamientos",
                desc: "Vivienda digna en zonas seguras para familias en laderas y cauces de río.",
                icono: "🏠",
              },
              {
                titulo: "Infraestructura Verde",
                desc: "Jardines de lluvia, pavimentos permeables y restauración de manglares.",
                icono: "🌱",
              },
              {
                titulo: "Presupuesto Participativo",
                desc: "Los ciudadanos deciden cómo se usan recursos públicos en sus colonias.",
                icono: "🗳️",
              },
            ].map((proyecto, i) => (
              <div key={i} className="p-6 bg-teal-50 rounded-xl border border-teal-200 hover:shadow-md transition-shadow">
                <div className="text-4xl mb-3">{proyecto.icono}</div>
                <h3 className="text-xl font-bold text-teal-800">{proyecto.titulo}</h3>
                <p className="text-gray-700 mt-2">{proyecto.desc}</p>
              </div>
            ))}
          </div>
        </section>

        {/* Envía tu Proyecto */}
        <section id="Envía tu Proyecto" className="bg-gradient-to-r from-teal-600 to-green-600 text-white p-8 rounded-2xl shadow-lg">
          <h2 className="text-3xl font-bold mb-6 text-center">Envía tu Proyecto</h2>
          <p className="text-center mb-8 text-teal-100">
            ¿Tienes una idea para mejorar Acapulco? ¡Compártela con nosotros!
          </p>
          <form onSubmit={handleSubmitProyecto} className="max-w-2xl mx-auto bg-white rounded-xl p-6 text-gray-800 shadow-md">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
              <input name="nombre" placeholder="Tu nombre" className="p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-teal-500 outline-none" required />
              <input name="correo" type="email" placeholder="Tu correo" className="p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-teal-500 outline-none" required />
            </div>
            <input name="titulo" placeholder="Título del proyecto" className="w-full p-3 border border-gray-300 rounded-lg mb-4 focus:ring-2 focus:ring-teal-500 outline-none" required />
            <textarea name="descripcion" placeholder="Describe tu proyecto (máx. 300 palabras)" rows="5" className="w-full p-3 border border-gray-300 rounded-lg mb-4 focus:ring-2 focus:ring-teal-500 outline-none" maxLength="500" required></textarea>
            <button type="submit" className="w-full bg-teal-600 hover:bg-teal-700 text-white font-bold py-3 px-6 rounded-lg transition-colors">
              Enviar Proyecto
            </button>
          </form>
        </section>

        {/* Sugerencias */}
        <section id="Sugerencias" className="bg-white p-8 rounded-2xl shadow-lg">
          <h2 className="text-3xl font-bold text-gray-800 mb-6 text-center">Sugerencias Ciudadanas</h2>
          <p className="text-center text-gray-600 mb-8">
            ¿Cómo mejorarías tu colonia, calle o parque? ¡Tu opinión nos importa!
          </p>
          <form onSubmit={handleSubmitSugerencia} className="max-w-2xl mx-auto bg-gray-50 p-6 rounded-xl border">
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
              <input name="nombre" placeholder="Tu nombre" className="p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-teal-500 outline-none" required />
              <select name="tema" className="p-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-teal-500 outline-none" required>
                <option value="">Selecciona un tema</option>
                <option value="movilidad">Movilidad y calles</option>
                <option value="espacios">Espacios públicos</option>
                <option value="vivienda">Vivienda y asentamientos</option>
                <option value="medio">Medio ambiente</option>
                <option value="otros">Otros</option>
              </select>
            </div>
            <textarea name="mensaje" placeholder="Tu sugerencia (máx. 200 palabras)" rows="4" className="w-full p-3 border border-gray-300 rounded-lg mb-4 focus:ring-2 focus:ring-teal-500 outline-none" maxLength="300" required></textarea>
            <button type="submit" className="w-full bg-green-600 hover:bg-green-700 text-white font-bold py-3 px-6 rounded-lg transition-colors">
              Enviar Sugerencia
            </button>
          </form>

          {/* Sugerencias recibidas (solo ejemplos visibles) */}
          {sugerenciasRecibidas.length > 0 && (
            <div className="mt-10">
              <h3 className="text-xl font-semibold text-gray-800 mb-4">Sugerencias recientes (ejemplos):</h3>
              <div className="space-y-2">
                {sugerenciasRecibidas.slice(0, 3).map((s, i) => (
                  <div key={i} className="p-3 bg-gray-100 rounded-lg text-sm">
                    <strong>{s.nombre}</strong> ({s.tema}): "{s.mensaje.substring(0, 80)}..."
                  </div>
                ))}
              </div>
            </div>
          )}
        </section>
      </main>

      {/* Footer */}
      <footer className="bg-gray-800 text-white py-8 mt-20">
        <div className="max-w-7xl mx-auto px-4 text-center">
          <h3 className="text-2xl font-bold">Acapulco Futuro</h3>
          <p className="mt-2 text-gray-300">
            Una iniciativa ciudadana para la reconstrucción participativa, sostenible y resiliente de Acapulco.
          </p>
          <p className="mt-4 text-sm text-gray-400">
            © {new Date().getFullYear()} Acapulco Futuro. Hecho con ❤️ por la comunidad.
          </p>
        </div>
      </footer>
    </div>
  );
}
