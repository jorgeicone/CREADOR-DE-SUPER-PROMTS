<!DOCTYPE html>
<html lang="es" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SuperPrompter - Creador de Prompts Inteligente</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght=300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f5f3ff',
                            100: '#ede9fe',
                            200: '#ddd6fe',
                            300: '#c4b5fd',
                            400: '#a78bfa',
                            500: '#8b5cf6',
                            600: '#7c3aed',
                            700: '#6d28d9',
                            800: '#5b21b6',
                            900: '#4c1d95',
                            950: '#020617',
                        }
                    }
                }
            }
        }
    </script>
    <style>
        body {
            background-color: #020617;
            background-image: 
                radial-gradient(at 0% 0%, rgba(139, 92, 246, 0.15) 0px, transparent 50%),
                radial-gradient(at 100% 100%, rgba(217, 70, 239, 0.1) 0px, transparent 50%),
                radial-gradient(at 50% 50%, rgba(6, 182, 212, 0.05) 0px, transparent 50%);
            background-attachment: fixed;
        }
        .glass-panel {
            background: rgba(15, 23, 42, 0.65);
            backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .pulsing-glow {
            animation: pulseGlow 4s infinite alternate;
        }
        @keyframes pulseGlow {
            0% { opacity: 0.3; transform: scale(0.98); }
            100% { opacity: 0.6; transform: scale(1.02); }
        }
    </style>
</head>
<body class="text-slate-100 min-h-full flex flex-col font-sans antialiased">

    <!-- Header Navigation -->
    <header class="border-b border-slate-800 bg-slate-950/80 backdrop-blur-md sticky top-0 z-50 transition-all">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="h-10 w-10 rounded-xl bg-gradient-to-tr from-brand-600 via-purple-500 to-pink-500 flex items-center justify-center shadow-lg shadow-brand-500/20">
                    <i class="fa-solid fa-wand-magic-sparkles text-white text-lg animate-pulse"></i>
                </div>
                <div>
                    <span class="text-lg font-extrabold tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-white via-slate-100 to-slate-400">SuperPrompter</span>
                    <span class="text-xs block text-brand-400 font-medium tracking-wider uppercase -mt-1">Laboratorio de Prompts</span>
                </div>
            </div>
            <div class="flex items-center space-x-4">
                <button onclick="showHelpModal()" class="text-sm text-slate-400 hover:text-white transition flex items-center space-x-1.5 px-3 py-1.5 rounded-lg hover:bg-slate-800/50">
                    <i class="fa-regular fa-circle-question"></i>
                    <span class="hidden sm:inline">Guía de Uso</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content Grid -->
    <main class="flex-grow max-w-5xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 flex flex-col justify-center">
        
        <!-- STEP 1: IDEA INICIAL & CATEGORÍA -->
        <section id="step-1" class="transition-all duration-300 transform">
            <div class="text-center max-w-2xl mx-auto mb-10">
                <h1 class="text-4xl sm:text-5xl font-black tracking-tight mb-4 text-white">
                    Transforma tus ideas en <span class="bg-clip-text text-transparent bg-gradient-to-r from-brand-400 via-purple-400 to-pink-400">prompts profesionales</span>
                </h1>
                <p class="text-slate-400 text-base sm:text-lg">
                    No importa si es una idea vaga o un problema complejo. Defínelo aquí y nuestra IA te guiará paso a paso para construir la instrucción perfecta.
                </p>
            </div>

            <div class="glass-panel rounded-3xl p-6 sm:p-8 shadow-2xl relative overflow-hidden">
                <div class="absolute -top-24 -right-24 w-48 h-48 bg-brand-500/10 rounded-full blur-3xl pointer-events-none"></div>
                <div class="absolute -bottom-24 -left-24 w-48 h-48 bg-pink-500/10 rounded-full blur-3xl pointer-events-none"></div>

                <!-- Formulario -->
                <div class="space-y-6">
                    <div>
                        <label class="block text-sm font-semibold text-slate-300 mb-3 flex items-center justify-between">
                            <span>1. Selecciona la categoría de tu prompt</span>
                            <span class="text-xs text-slate-500 font-normal">Ayuda a ajustar el enfoque del modelo</span>
                        </label>
                        <div class="grid grid-cols-2 md:grid-cols-4 gap-3" id="category-selector">
                            <button onclick="selectCategory('text', this)" class="category-btn p-4 rounded-xl border border-slate-800 bg-slate-900/50 text-slate-300 hover:border-brand-500 hover:bg-brand-500/5 transition flex flex-col items-center justify-center text-center group active">
                                <i class="fa-solid fa-pen-fancy text-xl mb-2 text-brand-400 group-hover:scale-110 transition"></i>
                                <span class="text-sm font-semibold">Redacción y Texto</span>
                            </button>
                            <button onclick="selectCategory('code', this)" class="category-btn p-4 rounded-xl border border-slate-800 bg-slate-900/50 text-slate-300 hover:border-brand-500 hover:bg-brand-500/5 transition flex flex-col items-center justify-center text-center group">
                                <i class="fa-solid fa-code text-xl mb-2 text-cyan-400 group-hover:scale-110 transition"></i>
                                <span class="text-sm font-semibold">Programación</span>
                            </button>
                            <button onclick="selectCategory('analysis', this)" class="category-btn p-4 rounded-xl border border-slate-800 bg-slate-900/50 text-slate-300 hover:border-brand-500 hover:bg-brand-500/5 transition flex flex-col items-center justify-center text-center group">
                                <i class="fa-solid fa-chart-pie text-xl mb-2 text-emerald-400 group-hover:scale-110 transition"></i>
                                <span class="text-sm font-semibold">Análisis y Datos</span>
                            </button>
                            <button onclick="selectCategory('general', this)" class="category-btn p-4 rounded-xl border border-slate-800 bg-slate-900/50 text-slate-300 hover:border-brand-500 hover:bg-brand-500/5 transition flex flex-col items-center justify-center text-center group">
                                <i class="fa-solid fa-brain text-xl mb-2 text-pink-400 group-hover:scale-110 transition"></i>
                                <span class="text-sm font-semibold">General / Chatbot</span>
                            </button>
                        </div>
                    </div>

                    <div>
                        <label for="raw-idea" class="block text-sm font-semibold text-slate-300 mb-3 flex items-center justify-between">
                            <span>2. Describe tu idea, problema o necesidad</span>
                            <span class="text-xs text-brand-400 font-medium cursor-pointer hover:underline" onclick="loadExample()">Ver un ejemplo</span>
                        </label>
                        <div class="relative">
                            <textarea id="raw-idea" rows="5" 
                                class="w-full rounded-2xl bg-slate-950/80 border border-slate-800 focus:border-brand-500 focus:ring-1 focus:ring-brand-500 text-white placeholder-slate-500 p-4 transition text-base resize-none"
                                placeholder="Ej: Necesito crear un plan de alimentación saludable para un mes, pero tengo poco tiempo para cocinar y no me gusta el brócoli..."></textarea>
                            <div class="absolute bottom-3 right-3 text-xs text-slate-500" id="char-counter">0 / 1000</div>
                        </div>
                    </div>

                    <div class="pt-2">
                        <button onclick="generateQuestions()" id="btn-start-refinement" 
                            class="w-full py-4 px-6 bg-gradient-to-r from-brand-600 to-purple-600 hover:from-brand-500 hover:to-purple-500 text-white font-bold rounded-2xl shadow-lg shadow-brand-500/20 hover:shadow-brand-500/35 transition flex items-center justify-center space-x-2 text-lg active:scale-95 duration-100">
                            <span>Siguiente: Estructurar Preguntas</span>
                            <i class="fa-solid fa-arrow-right text-sm"></i>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- STEP 2: FORMULARIO DE REFINAMIENTO (PREGUNTAS DINÁMICAS) -->
        <section id="step-2" class="hidden transition-all duration-300 transform">
            <div class="mb-8">
                <button onclick="goToStep(1)" class="text-slate-400 hover:text-white transition flex items-center space-x-1.5 text-sm mb-4">
                    <i class="fa-solid fa-arrow-left"></i>
                    <span>Volver a la idea inicial</span>
                </button>
                <h2 class="text-3xl font-extrabold text-white flex items-center gap-2">
                    <i class="fa-solid fa-circle-question text-brand-400 text-2xl"></i>
                    Ajustando detalles con la IA
                </h2>
                <p class="text-slate-400 mt-1">
                    Para diseñar el prompt perfecto, responde a estas preguntas sugeridas específicamente para tu caso.
                </p>
            </div>

            <!-- Idea original en formato reducido -->
            <div class="bg-slate-900/40 border border-slate-800 rounded-2xl p-4 mb-6">
                <span class="text-xs text-brand-400 uppercase tracking-wider font-bold">Tu idea original:</span>
                <p class="text-slate-300 text-sm italic mt-1" id="display-raw-idea"></p>
            </div>

            <!-- Contenedor de preguntas dinámicas -->
            <div class="glass-panel rounded-3xl p-6 sm:p-8 shadow-2xl space-y-6">
                <div id="dynamic-questions-container" class="space-y-6">
                    <!-- Se inyectarán dinámicamente -->
                </div>

                <div class="pt-4 flex flex-col sm:flex-row gap-3">
                    <button onclick="generatePrompt()" 
                        class="flex-grow py-4 px-6 bg-gradient-to-r from-brand-600 to-purple-600 hover:from-brand-500 hover:to-purple-500 text-white font-bold rounded-2xl shadow-lg shadow-brand-500/20 transition flex items-center justify-center space-x-2 text-base active:scale-95 duration-100">
                        <i class="fa-solid fa-wand-magic-sparkles"></i>
                        <span>¡Construir Prompt Perfecto!</span>
                    </button>
                    <button onclick="skipQuestions()" 
                        class="py-4 px-6 bg-slate-800 hover:bg-slate-700 text-slate-300 font-medium rounded-2xl transition text-base active:scale-95 duration-100">
                        Omitir y generar con lo que tengo
                    </button>
                </div>
            </div>
        </section>

        <!-- STEP 3: PANTALLA DE CARGA / ANIMACIÓN IA -->
        <section id="step-3" class="hidden text-center py-12 transition-all duration-300 transform">
            <div class="relative w-32 h-32 mx-auto mb-8">
                <!-- Anillos orbitales giratorios -->
                <div class="absolute inset-0 rounded-full border-4 border-dashed border-brand-500/30 animate-[spin_8s_linear_infinite]"></div>
                <div class="absolute inset-2 rounded-full border-4 border-dashed border-purple-500/40 animate-[spin_4s_linear_infinite_reverse]"></div>
                <!-- Círculo interior brillante -->
                <div class="absolute inset-4 rounded-full bg-slate-900 flex items-center justify-center shadow-inner">
                    <i class="fa-solid fa-brain text-4xl text-brand-400 animate-pulse"></i>
                </div>
            </div>
            
            <h3 class="text-2xl font-bold text-white mb-2" id="loading-title">Analizando parámetros...</h3>
            <p class="text-slate-400 max-w-sm mx-auto text-sm" id="loading-subtitle">
                Nuestro motor de ingeniería estructurando el rol óptimo, contexto y delimitadores de salida.
            </p>
        </section>

        <!-- STEP 4: PANTALLA DE RESULTADOS (PROMPT FINAL) -->
        <section id="step-4" class="hidden transition-all duration-300 transform">
            <div class="mb-6 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
                <div>
                    <h2 class="text-3xl font-black text-white flex items-center gap-2">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i>
                        ¡Tu Prompt está Listo!
                    </h2>
                    <p class="text-slate-400 text-sm mt-1">
                        Copia la instrucción optimizada de abajo y úsala en cualquier inteligencia artificial.
                    </p>
                </div>
                <div class="flex gap-2">
                    <button onclick="goToStep(1)" class="px-4 py-2.5 bg-slate-800 hover:bg-slate-700 text-slate-300 rounded-xl transition text-sm font-semibold flex items-center gap-1.5">
                        <i class="fa-solid fa-rotate-left"></i>
                        <span>Nueva Idea</span>
                    </button>
                </div>
            </div>

            <!-- Contenedor Principal de Resultados -->
            <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
                <!-- Columna Izquierda: El Prompt (8 columnas) -->
                <div class="lg:col-span-8 flex flex-col">
                    <div class="glass-panel rounded-3xl shadow-xl overflow-hidden flex flex-col flex-grow">
                        <!-- Cabecera del panel de Prompt -->
                        <div class="bg-slate-900/60 px-6 py-4 border-b border-slate-800 flex justify-between items-center">
                            <span class="text-xs font-bold uppercase tracking-widest text-slate-400 flex items-center gap-1.5">
                                <i class="fa-solid fa-terminal text-brand-400"></i>
                                Prompt Estructurado
                            </span>
                            <button onclick="copyToClipboard()" id="btn-copy" 
                                class="px-3 py-1.5 bg-brand-600 hover:bg-brand-500 text-white rounded-lg transition text-xs font-bold flex items-center gap-1.5 shadow-lg shadow-brand-500/20">
                                <i class="fa-regular fa-copy"></i>
                                <span id="copy-text">Copiar Prompt</span>
                            </button>
                        </div>
                        <!-- Area de visualización del prompt -->
                        <div class="p-6 bg-slate-950/40 relative group flex-grow">
                            <pre id="output-prompt" class="whitespace-pre-wrap font-mono text-sm leading-relaxed text-slate-100 selection:bg-brand-500/30 overflow-auto max-h-[480px] pr-2"></pre>
                        </div>
                    </div>
                </div>

                <!-- Columna Derecha: Explicación y Tips (4 columnas) -->
                <div class="lg:col-span-4 space-y-6 flex flex-col justify-between">
                    <!-- Panel de Explicación -->
                    <div class="glass-panel rounded-3xl p-6 shadow-xl space-y-4">
                        <h4 class="text-sm font-extrabold uppercase tracking-widest text-slate-400 flex items-center gap-1.5 border-b border-slate-800 pb-3">
                            <i class="fa-solid fa-gears text-purple-400"></i>
                            ¿Por qué funciona?
                        </h4>
                        <p id="output-explanation" class="text-slate-300 text-sm leading-relaxed">
                            Aquí se mostrará por qué se estructuró de esta manera.
                        </p>
                    </div>

                    <!-- Panel de Tips -->
                    <div class="glass-panel rounded-3xl p-6 shadow-xl space-y-4">
                        <h4 class="text-sm font-extrabold uppercase tracking-widest text-slate-400 flex items-center gap-1.5 border-b border-slate-800 pb-3">
                            <i class="fa-solid fa-lightbulb text-amber-400"></i>
                            Consejo Pro
                        </h4>
                        <div class="text-slate-300 text-sm leading-relaxed flex gap-2">
                            <p id="output-tips"></p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- SECCIÓN: CHAT DE AJUSTE / REFINAMIENTO EXTRA -->
            <div class="mt-8 glass-panel rounded-3xl p-6 shadow-xl">
                <h4 class="text-base font-bold text-white mb-3 flex items-center gap-2">
                    <i class="fa-solid fa-wand-magic-sparkles text-brand-400"></i>
                    ¿Quieres refinarlo o cambiar algo?
                </h4>
                <p class="text-slate-400 text-sm mb-4">
                    Pídele ajustes directos a la IA sin reiniciar (Ej. *"hazlo más corto"*, *"añade una sección de preguntas frecuentes"*, *"cambia el tono a formal"*).
                </p>
                <div class="flex gap-2">
                    <input type="text" id="refinement-command" 
                        class="flex-grow rounded-xl bg-slate-950 border border-slate-800 focus:border-brand-500 focus:ring-1 focus:ring-brand-500 text-white placeholder-slate-500 px-4 py-3 transition text-sm"
                        placeholder="Ej: Haz que el tono sea más humorístico y agrega una restricción de longitud...">
                    <button onclick="applyRefinement()" id="btn-refine" 
                        class="px-5 py-3 bg-brand-600 hover:bg-brand-500 text-white font-semibold rounded-xl transition text-sm flex items-center gap-1.5 active:scale-95">
                        <span>Ajustar Prompt</span>
                        <i class="fa-solid fa-circle-arrow-up"></i>
                    </button>
                </div>
            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="border-t border-slate-900 bg-slate-950/40 py-6 mt-12">
        <div class="max-w-6xl mx-auto px-4 text-center text-xs text-slate-500 space-y-1">
            <p>SuperPrompter utiliza Inteligencia Artificial avanzada (Gemini 2.5 Flash) para formular las instrucciones.</p>
            <p>© 2026 SuperPrompter • Creado con ❤️ para ingenieros de prompts y entusiastas.</p>
        </div>
    </footer>

    <!-- MODAL DE AYUDA / GUÍA -->
    <div id="help-modal" class="fixed inset-0 bg-black/80 backdrop-blur-sm flex items-center justify-center p-4 z-[100] hidden">
        <div class="glass-panel max-w-lg w-full rounded-3xl p-6 sm:p-8 space-y-4 relative">
            <button onclick="hideHelpModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white transition">
                <i class="fa-solid fa-xmark text-lg"></i>
            </button>
            <h3 class="text-xl font-bold text-white flex items-center gap-2">
                <i class="fa-solid fa-circle-info text-brand-400"></i>
                Guía del Ingeniero de Prompts
            </h3>
            <div class="text-slate-300 text-sm space-y-3 leading-relaxed">
                <p>
                    Un buen prompt define la calidad de la respuesta de cualquier IA. Para lograrlo, **SuperPrompter** aplica la metodología estructural clásica:
                </p>
                <ul class="space-y-2 pl-4 list-disc text-slate-400">
                    <li><strong class="text-slate-200">Rol & Persona:</strong> Le asignamos una identidad experta al modelo.</li>
                    <li><strong class="text-slate-200">Contexto & Objetivo:</strong> Explicamos claramente la situación real.</li>
                    <li><strong class="text-slate-200">Delimitadores:</strong> Usamos marcas claras para separar la información de las instrucciones.</li>
                    <li><strong class="text-slate-200">Restricciones:</strong> Bloqueamos respuestas ambiguas u ofensivas.</li>
                    <li><strong class="text-slate-200">Formato de Salida:</strong> Pedimos tablas, código, markdown o viñetas según sea óptimo.</li>
                </ul>
                <p class="text-xs text-brand-400 italic">
                    ¡Responde con libertad en el cuestionario intermedio! Mientras más detallada sea tu respuesta, más refinada e instructiva será la salida.
                </p>
            </div>
            <div class="pt-2 text-right">
                <button onclick="hideHelpModal()" class="px-5 py-2.5 bg-brand-600 hover:bg-brand-500 text-white font-semibold rounded-xl text-sm transition">
                    Entendido
                </button>
            </div>
        </div>
    </div>

    <!-- NOTIFICACIONES CUSTOM (TOASTS) -->
    <div id="toast-container" class="fixed bottom-4 right-4 z-[200] space-y-2"></div>

    <script>
        // Configuración de API e Inicializaciones
        const apiKey = ""; // La plataforma inyectará el API key en tiempo de ejecución o puedes colocar tu propia clave
        const modelName = "gemini-2.5-flash-preview-09-2025";
        
        let currentStep = 1;
        let selectedCategory = 'text';
        let rawIdea = '';
        let dynamicQuestions = [];
        let generatedPromptData = {
            prompt: '',
            explanation: '',
            tips: ''
        };

        // Ejemplos por defecto para ayudar al usuario
        const examples = {
            text: "Necesito redactar una carta formal de renuncia para mi trabajo actual de desarrollador de software. Quiero irme en buenos términos, dar un preaviso de 15 días, y agradecer las oportunidades de crecimiento.",
            code: "Quiero una función en Javascript que reciba una lista de objetos de compras, filtre los que tienen un precio mayor a 50 dólares, sume el total aplicando un 15% de IVA y retorne el desglose completo.",
            analysis: "Tengo datos de ventas trimestrales donde notamos que en mayo bajan mucho las compras de helados. Necesito estructurar un análisis paso a paso para encontrar causas y proponer soluciones creativas.",
            general: "Quiero crear un juego interactivo de adivinanzas de texto sobre historia universal, donde la IA actúe como un viajero del tiempo que me va dando pistas crípticas."
        };

        // Contador de caracteres para textarea
        document.getElementById('raw-idea').addEventListener('input', function() {
            const count = this.value.length;
            document.getElementById('char-counter').textContent = `${count} / 1000`;
        });

        // Selección de categoría
        function selectCategory(category, button) {
            selectedCategory = category;
            document.querySelectorAll('.category-btn').forEach(btn => {
                btn.classList.remove('border-brand-500', 'bg-brand-500/5', 'text-white');
                btn.classList.add('border-slate-800', 'bg-slate-900/50', 'text-slate-300');
            });
            button.classList.add('border-brand-500', 'bg-brand-500/5', 'text-white');
            button.classList.remove('border-slate-800', 'bg-slate-900/50', 'text-slate-300');
        }

        // Carga un ejemplo basado en la categoría seleccionada
        function loadExample() {
            const ideaInput = document.getElementById('raw-idea');
            ideaInput.value = examples[selectedCategory] || examples.text;
            ideaInput.dispatchEvent(new Event('input'));
            showToast("Ejemplo cargado", "info");
        }

        // Manejo de Pasos del Flujo
        function goToStep(step) {
            document.querySelectorAll('section').forEach(sec => sec.classList.add('hidden'));
            document.getElementById(`step-${step}`).classList.remove('hidden');
            currentStep = step;
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // --- SISTEMA DE TOASTS CUSTOM (Sustituye alert) ---
        function showToast(message, type = "success") {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = `p-4 rounded-xl shadow-lg border text-sm font-semibold transition-all duration-300 transform translate-y-2 opacity-0 flex items-center space-x-2 w-72 ${
                type === 'success' ? 'bg-emerald-950/90 border-emerald-500/30 text-emerald-400' :
                type === 'error' ? 'bg-rose-950/90 border-rose-500/30 text-rose-400' :
                'bg-slate-900/90 border-slate-700 text-slate-300'
            }`;
            
            const icon = type === 'success' ? '<i class="fa-solid fa-circle-check"></i>' :
                         type === 'error' ? '<i class="fa-solid fa-circle-exclamation"></i>' :
                                            '<i class="fa-solid fa-circle-info"></i>';

            toast.innerHTML = `${icon} <span>${message}</span>`;
            container.appendChild(toast);

            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 50);

            setTimeout(() => {
                toast.classList.add('translate-y-2', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 3500);
        }

        // Helpers de Modales
        function showHelpModal() { document.getElementById('help-modal').classList.remove('hidden'); }
        function hideHelpModal() { document.getElementById('help-modal').classList.add('hidden'); }

        // --- CONSUMO DE LA API DE GEMINI CON EXPONENTIAL BACKOFF ---
        async function queryGemini(payload, maxRetries = 5) {
            const endpoint = `https://generativelanguage.googleapis.com/v1beta/models/${modelName}:generateContent?key=${apiKey}`;
            let delay = 1000;
            
            for (let i = 0; i < maxRetries; i++) {
                try {
                    const response = await fetch(endpoint, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });
                    
                    if (response.ok) {
                        return await response.json();
                    }
                } catch (error) {
                    if (i === maxRetries - 1) throw error;
                }
                // Backoff exponencial
                await new Promise(resolve => setTimeout(resolve, delay));
                delay *= 2;
            }
            throw new Error("No pudimos conectarnos con la inteligencia artificial. Inténtalo de nuevo.");
        }

        // --- STEP 1 -> STEP 2: GENERACIÓN DE PREGUNTAS CLAVE ---
        async function generateQuestions() {
            rawIdea = document.getElementById('raw-idea').value.trim();
            if (!rawIdea) {
                showToast("Por favor describe brevemente tu idea o necesidad.", "error");
                return;
            }

            // Cambiar a carga
            goToStep(3);
            document.getElementById('loading-title').innerText = "Analizando tu idea...";
            document.getElementById('loading-subtitle').innerText = "Detectando el mejor enfoque estructural para formular tus preguntas de precisión.";

            // Prompt del sistema para generar preguntas
            const systemPrompt = "Eres un refinado consultor en ingeniería de prompts. Tu tarea es analizar la idea inicial de un usuario y formular exactamente 3 preguntas clave y altamente específicas que ayuden a estructurar el prompt perfecto. No hagas preguntas genéricas, haz preguntas precisas de acuerdo con el contexto entregado (por ejemplo, limitaciones técnicas, tipo de tono, estilo, nivel de detalle). Retorna la respuesta estrictamente en un objeto JSON que contenga un arreglo 'questions' con 3 elementos de texto en español.";

            const userQuery = `Idea Inicial: "${rawIdea}". Categoría del Prompt: "${selectedCategory}". Genera 3 preguntas de refinamiento específicas en un arreglo JSON.`;

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            questions: {
                                type: "ARRAY",
                                items: { type: "STRING" }
                            }
                        },
                        required: ["questions"]
                    }
                }
            };

            try {
                const responseData = await queryGemini(payload);
                const rawText = responseData.candidates?.[0]?.content?.parts?.[0]?.text;
                const parsed = JSON.parse(rawText);
                dynamicQuestions = parsed.questions || [];

                // Renderizar preguntas en el paso 2
                renderQuestionsForm();
                document.getElementById('display-raw-idea').innerText = rawIdea;
                goToStep(2);
            } catch (err) {
                goToStep(1);
                showToast("Error generando preguntas. Inténtalo de nuevo.", "error");
            }
        }

        function renderQuestionsForm() {
            const container = document.getElementById('dynamic-questions-container');
            container.innerHTML = '';

            dynamicQuestions.forEach((q, index) => {
                const questionBlock = document.createElement('div');
                questionBlock.className = 'space-y-2';
                questionBlock.innerHTML = `
                    <label class="block text-sm font-semibold text-slate-300">
                        Pregunta ${index + 1}: <span class="text-slate-100">${q}</span>
                    </label>
                    <input type="text" id="answer-${index}" 
                        class="w-full rounded-xl bg-slate-950 border border-slate-800 focus:border-brand-500 focus:ring-1 focus:ring-brand-500 text-white placeholder-slate-500 px-4 py-3 text-sm transition"
                        placeholder="Escribe tu respuesta aquí para afinar los detalles...">
                `;
                container.appendChild(questionBlock);
            });
        }

        // --- STEP 2 -> STEP 4: CONSTRUCCIÓN DEL PROMPT FINAL ---
        async function generatePrompt() {
            // Recoger respuestas del cuestionario
            const answers = [];
            dynamicQuestions.forEach((q, index) => {
                const val = document.getElementById(`answer-${index}`).value.trim() || "(No especificado por el usuario)";
                answers.push({ question: q, answer: val });
            });

            await triggerPromptBuilder(answers);
        }

        async function skipQuestions() {
            showToast("Generando con parámetros por defecto", "info");
            await triggerPromptBuilder([]);
        }

        async function triggerPromptBuilder(answersArray) {
            goToStep(3);
            document.getElementById('loading-title').innerText = "Construyendo tu Prompt...";
            document.getElementById('loading-subtitle').innerText = "Estamos estructurando el Rol, Delimitadores, Restricciones y el Formato de Salida ideal para ti.";

            const systemPrompt = `Eres un ingeniero experto de prompts de nivel mundial. Tu labor es construir un prompt profesional, estructurado y altamente eficiente usando técnicas avanzadas de prompting (ej. asignación de rol de experto, definición clara de objetivo, delimitadores XML o Markdown para aislar entradas, restricciones para evitar alucinaciones, formato de salida deseado, y un tono específico). Tu salida debe ser un JSON plano con tres propiedades principales en español:
1. 'prompt': El prompt final optimizado, que comienza con un rol imponente, asigna tareas paso a paso claras y describe detalladamente el formato esperado.
2. 'explanation': Explicación de las mejores prácticas y técnicas de prompt aplicadas en el diseño (máximo 120 palabras).
3. 'tips': Un truco de oro rápido para exprimir el rendimiento de este prompt específico.

No agregues markdown exterior adicional al JSON.`;

            let userQuery = `Idea original: "${rawIdea}". Categoría seleccionada: "${selectedCategory}".`;
            if (answersArray.length > 0) {
                userQuery += `\nRespuestas adicionales de refinamiento:\n`;
                answersArray.forEach((item, i) => {
                    userQuery += `${i+1}. Pregunta: "${item.question}" -> Respuesta: "${item.answer}"\n`;
                });
            }

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            prompt: { type: "STRING" },
                            explanation: { type: "STRING" },
                            tips: { type: "STRING" }
                        },
                        required: ["prompt", "explanation", "tips"]
                    }
                }
            };

            try {
                const responseData = await queryGemini(payload);
                const rawText = responseData.candidates?.[0]?.content?.parts?.[0]?.text;
                generatedPromptData = JSON.parse(rawText);

                // Renderizar salida
                displayResult();
                goToStep(4);
            } catch (err) {
                goToStep(2);
                showToast("Error construyendo el prompt. Reinténtalo.", "error");
            }
        }

        function displayResult() {
            document.getElementById('output-prompt').innerText = generatedPromptData.prompt;
            document.getElementById('output-explanation').innerText = generatedPromptData.explanation;
            document.getElementById('output-tips').innerText = generatedPromptData.tips;
        }

        // --- SISTEMA DE REFINAMIENTO ADICIONAL (CHAT INTERACTIVO) ---
        async function applyRefinement() {
            const command = document.getElementById('refinement-command').value.trim();
            if (!command) {
                showToast("Ingresa un ajuste para modificar el prompt.", "error");
                return;
            }

            const btnRefine = document.getElementById('btn-refine');
            btnRefine.disabled = true;
            btnRefine.innerHTML = `<i class="fa-solid fa-circle-notch animate-spin"></i> <span>Ajustando...</span>`;

            const systemPrompt = `Eres un ingeniero experto en optimización de prompts. El usuario tiene un prompt estructurado y desea realizarle una modificación específica. Debes actualizar el prompt conservando la estructura técnica avanzada (Rol, Contexto, Instrucciones claras, Restricciones), pero acomodándolo exactamente al nuevo requisito del usuario. Responde estrictamente con un JSON que tenga las mismas claves: 'prompt', 'explanation' y 'tips'.`;

            const userQuery = `Prompt Actual:\n"""\n${generatedPromptData.prompt}\n"""\n\nModificación o Ajuste solicitado por el usuario:\n"${command}"`;

            const payload = {
                contents: [{ parts: [{ text: userQuery }] }],
                systemInstruction: { parts: [{ text: systemPrompt }] },
                generationConfig: {
                    responseMimeType: "application/json",
                    responseSchema: {
                        type: "OBJECT",
                        properties: {
                            prompt: { type: "STRING" },
                            explanation: { type: "STRING" },
                            tips: { type: "STRING" }
                        },
                        required: ["prompt", "explanation", "tips"]
                    }
                }
            };

            try {
                const responseData = await queryGemini(payload);
                const rawText = responseData.candidates?.[0]?.content?.parts?.[0]?.text;
                generatedPromptData = JSON.parse(rawText);

                // Actualizar la interfaz
                displayResult();
                document.getElementById('refinement-command').value = '';
                showToast("¡Prompt re-estructurado con éxito!");
            } catch (err) {
                showToast("Ocurrió un error al procesar el ajuste.", "error");
            } finally {
                btnRefine.disabled = false;
                btnRefine.innerHTML = `<span>Ajustar Prompt</span> <i class="fa-solid fa-circle-arrow-up"></i>`;
            }
        }

        // --- COPIADO AL PORTAPAPELES COMPATIBLE CON IFRAME ---
        function copyToClipboard() {
            const textToCopy = document.getElementById('output-prompt').innerText;
            
            // Creamos un textarea invisible
            const tempTextArea = document.createElement("textarea");
            tempTextArea.value = textToCopy;
            tempTextArea.style.position = "absolute";
            tempTextArea.style.left = "-9999px";
            document.body.appendChild(tempTextArea);
            
            tempTextArea.select();
            tempTextArea.setSelectionRange(0, 99999); // Para móviles

            try {
                const successful = document.execCommand('copy');
                if (successful) {
                    const copyBtn = document.getElementById('btn-copy');
                    const copyText = document.getElementById('copy-text');
                    
                    copyBtn.className = "px-3 py-1.5 bg-emerald-600 hover:bg-emerald-500 text-white rounded-lg transition text-xs font-bold flex items-center gap-1.5 shadow-lg shadow-emerald-500/20";
                    copyText.innerText = "¡Copiado!";
                    
                    setTimeout(() => {
                        copyBtn.className = "px-3 py-1.5 bg-brand-600 hover:bg-brand-500 text-white rounded-lg transition text-xs font-bold flex items-center gap-1.5 shadow-lg shadow-brand-500/20";
                        copyText.innerText = "Copiar Prompt";
                    }, 2000);

                    showToast("Prompt copiado al portapapeles.");
                } else {
                    showToast("No se pudo copiar de forma automática.", "error");
                }
            } catch (err) {
                showToast("No se pudo copiar al portapapeles.", "error");
            } finally {
                document.body.removeChild(tempTextArea);
            }
        }
    </script>
</body>
</html>
