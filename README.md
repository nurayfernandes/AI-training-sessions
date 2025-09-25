<!DOCTYPE html>

<html lang="pt-BR">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Capacitação em Inteligência Artificial</title>

    <script src="https://cdn.tailwindcss.com"></script>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <!-- Chosen Palette: Nubank Inspired (Purple, Gray, White) -->

    <!-- Application Structure Plan: A single-page application with a tab-based navigation. The user starts at an introduction page (Início) and can click on tabs (NotebookLM, Gemini, Cursor, Comparativo) to dynamically display the content for each section without reloading the page. This structure was chosen for its intuitive user experience, allowing for easy comparison between the different AI tools. A dedicated "Comparativo" section with a radar chart provides a quick visual summary of the tools' strengths, which is more effective for synthesis than text alone. The flow is non-linear, empowering the user to explore the content in any order. This version adds a Gemini API-powered use-case generator in each tool's section to provide contextual, dynamic content. -->

    <!-- Visualization & Content Choices: 

        - Report Info: Overview of 3 AI tools. Goal: Inform & Compare. Viz/Method: Tabbed content sections for detailed info. Interaction: Clickable navigation tabs to switch views. Justification: Familiar and efficient for comparing distinct items.

        - Report Info: Strengths of each tool. Goal: Synthesize & Compare. Viz/Method: Radar Chart (Chart.js/Canvas). Interaction: Tooltips on hover provide specific data points. Justification: A radar chart is excellent for visually comparing multiple subjects across multiple quantitative or qualitative dimensions, offering an immediate high-level understanding of their profiles.

        - Report Info: "Pontos Positivos". Goal: Inform clearly. Viz/Method: Styled lists with icons (HTML/Tailwind). Interaction: Subtle hover effects. Justification: More visually engaging than standard bullet points.

        - Report Info: Tool Applicability. Goal: Brainstorm & Inspire. Viz/Method: Button-triggered content generation via Gemini API. Interaction: User clicks a button to get tailored use cases. Justification: Adds a dynamic, "wow" factor and provides real-world, context-specific value beyond the static report content.

    -->

    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <style>

        body {

            font-family: 'Nunito', sans-serif;

        }

        .content-section {

            display: none;

        }

        .content-section.active {

            display: block;

            animation: fadeIn 0.5s ease-in-out;

        }

        @keyframes fadeIn {

            from { opacity: 0; transform: translateY(10px); }

            to { opacity: 1; transform: translateY(0); }

        }

        .nav-btn.active {

            background-color: #820AD1; 

            color: #ffffff;

        }

        .chart-container {

            position: relative; 

            width: 100%; 

            max-width: 700px; 

            margin-left: auto; 

            margin-right: auto; 

            height: 60vh;

            max-height: 500px;

        }

        .loader {

            display: none; /* Initially hidden */

        }

        .gemini-results ul {

            list-style-type: none;

            padding-left: 0;

        }

        .gemini-results li {

            background-color: #f9f5ff;

            padding: 12px;

            border-radius: 8px;

            margin-bottom: 12px;

            border-left: 4px solid #a855f7;

        }

         .gemini-results strong {

            color: #6b21a8;

        }

        @media (min-width: 768px) {

            .chart-container {

                height: 450px;

            }

        }

    </style>

    <link rel="preconnect" href="https://fonts.googleapis.com">

    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;700;800&display=swap" rel="stylesheet">

</head>

<body class="bg-gray-50 text-gray-800">



    <div class="container mx-auto p-4 md:p-8">



        <header class="text-center mb-8">

            <h1 class="text-4xl md:text-5xl font-extrabold text-gray-900">Capacitação em Inteligência Artificial</h1>

            <p class="mt-2 text-lg text-gray-600">Ferramentas para otimizar o time de Gestão de Treinamento</p>

        </header>



        <nav class="flex flex-wrap justify-center gap-2 md:gap-4 mb-8 bg-white p-3 rounded-xl shadow-sm sticky top-4 z-10">

            <button data-target="inicio" class="nav-btn active px-4 py-2 font-bold text-gray-700 rounded-lg hover:bg-purple-100 transition-colors">Início</button>

            <button data-target="notebooklm" class="nav-btn px-4 py-2 font-bold text-gray-700 rounded-lg hover:bg-purple-100 transition-colors">NotebookLM</button>

            <button data-target="gemini" class="nav-btn px-4 py-2 font-bold text-gray-700 rounded-lg hover:bg-purple-100 transition-colors">Gemini</button>

            <button data-target="cursor" class="nav-btn px-4 py-2 font-bold text-gray-700 rounded-lg hover:bg-purple-100 transition-colors">Cursor</button>

            <button data-target="comparativo" class="nav-btn px-4 py-2 font-bold text-gray-700 rounded-lg hover:bg-purple-100 transition-colors">Comparativo</button>

        </nav>



        <main id="main-content">

            <section id="inicio" class="content-section active p-6 md:p-8 bg-white rounded-2xl shadow-lg">

                <h2 class="text-3xl font-bold text-purple-700 mb-4">Bem-vindo(a) ao Treinamento!</h2>

                <p class="text-lg text-gray-600 mb-6">Esta é uma guia interativa para explorar o potencial de ferramentas de Inteligência Artificial Generativa que podem transformar nosso fluxo de trabalho. Navegue pelas seções para conhecer cada plataforma, entender seus diferenciais e comparar seus pontos fortes.</p>

                <div class="bg-purple-50 border-l-4 border-purple-400 p-4 rounded-r-lg">

                    <h3 class="text-xl font-semibold text-gray-800 mb-2">Agenda de Exploração:</h3>

                    <ol class="list-decimal list-inside text-gray-700 space-y-1">

                        <li>Introdução ao Potencial da IA Generativa</li>

                        <li><strong>NotebookLM:</strong> Sua IA de pesquisa pessoal</li>

                        <li><strong>Gemini:</strong> O assistente criativo e multimodal</li>

                        <li><strong>Cursor:</strong> O futuro da edição de código com IA</li>

                        <li><strong>Comparativo:</strong> Análise visual das ferramentas</li>

                    </ol>

                </div>

            </section>



            <section id="notebooklm" class="content-section p-6 md:p-8 bg-white rounded-2xl shadow-lg">

                <h2 class="text-3xl font-bold text-purple-700 mb-4">NotebookLM</h2>

                <div class="grid md:grid-cols-2 gap-8">

                    <div>

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Diferencial</h3>

                        <p class="text-gray-600 leading-relaxed">O NotebookLM transforma seus documentos em um especialista personalizado. Diferente de outras IAs que buscam informações na internet inteira, ele se baseia exclusivamente nas fontes que você fornece (PDFs, Docs, notas). Isso o torna uma ferramenta de pesquisa e análise extremamente precisa e segura, ideal para resumir relatórios, analisar documentação interna e extrair insights de materiais específicos do banco, garantindo que as respostas sejam sempre baseadas nos seus dados.</p>

                    </div>

                    <div class="space-y-4">

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Pontos Positivos</h3>

                        <ul class="space-y-3">

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Respostas 100% baseadas em suas fontes.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Excelente para resumir e extrair informações-chave de documentos longos.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Cria automaticamente guias de estudo, glossários e FAQs.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Privacidade e controle total sobre o contexto da informação.</span></li>

                        </ul>

                    </div>

                </div>

                <div class="mt-8 border-t pt-6">

                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Ideias de Aplicação Prática</h3>

                    <ul class="space-y-3 mb-6">

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Criação de Treinamentos de Produtos/Features:</strong> Analise a documentação de um novo produto e gere rascunhos de materiais de treinamento, quizzes e guias rápidos.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Revisão de Macros e FAQs:</strong> Carregue as macros existentes e peça para a IA identificar redundâncias, sugerir melhorias de clareza e criar novas FAQs com base no conteúdo.</span></li>

                    </ul>

                    <p class="text-gray-600 mb-4 text-sm">Para mais ideias, clique no botão e a IA irá gerar outros casos de uso com base nas características da ferramenta.</p>

                    <button class="gemini-btn bg-[#820AD1] text-white font-bold py-2 px-4 rounded-lg hover:bg-purple-800 transition-colors" data-tool="notebooklm">✨ Gerar Mais Ideias</button>

                    <div class="loader mt-4 items-center" id="loader-notebooklm">

                        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-purple-700"></div>

                        <p class="text-gray-500 ml-3">Gerando ideias com Gemini...</p>

                    </div>

                    <div class="gemini-results mt-4" id="results-notebooklm"></div>

                </div>

            </section>



            <section id="gemini" class="content-section p-6 md:p-8 bg-white rounded-2xl shadow-lg">

                <h2 class="text-3xl font-bold text-purple-700 mb-4">Gemini</h2>

                <div class="grid md:grid-cols-2 gap-8">

                    <div>

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Diferencial</h3>

                        <p class="text-gray-600 leading-relaxed">O Gemini é a IA multimodal do Google, projetada para entender, combinar e raciocinar sobre diferentes tipos de informação de forma nativa. Seu grande diferencial é a capacidade de processar não apenas texto, mas também imagens, áudio e código simultaneamente. Ele funciona como um parceiro criativo e analítico, capaz de gerar desde um e-mail complexo até analisar o sentimento em um feedback de cliente ou criar um roteiro de treinamento a partir de alguns tópicos.</p>

                    </div>

                    <div>

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Pontos Positivos</h3>

                        <ul class="space-y-3">

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Capacidade de entender e gerar conteúdo em múltiplos formatos.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Fortes habilidades de raciocínio e resolução de problemas complexos.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Acesso a informações em tempo real da internet.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Extremamente versátil para tarefas criativas e de brainstorming.</span></li>

                        </ul>

                    </div>

                </div>

                <div class="mt-8 border-t pt-6">

                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Ideias de Aplicação Prática</h3>

                     <ul class="space-y-3 mb-6">

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Análise de Tickets e Proposição de Melhorias:</strong> Cole uma amostra de tickets de suporte e peça para a IA identificar temas recorrentes, analisando o sentimento e sugerindo melhorias para os treinamentos.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Criação de Documentações como PRDs:</strong> Forneça um briefing sobre uma nova feature e peça ao Gemini para rascunhar um Documento de Requisitos de Produto (PRD) inicial.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Revisão de Macros e FAQs:</strong> Peça para a IA reescrever macros existentes em um tom de voz diferente ou expandir FAQs com base em dúvidas comuns de clientes.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Suporte:</strong> Use como um "copiloto" para ajudar a encontrar respostas e formular explicações claras durante o suporte a outras equipes internas.</span></li>

                    </ul>

                    <p class="text-gray-600 mb-4 text-sm">Para mais ideias, clique no botão e a IA irá gerar outros casos de uso com base nas características da ferramenta.</p>

                    <button class="gemini-btn bg-[#820AD1] text-white font-bold py-2 px-4 rounded-lg hover:bg-purple-800 transition-colors" data-tool="gemini">✨ Gerar Mais Ideias</button>

                    <div class="loader mt-4 items-center" id="loader-gemini">

                        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-purple-700"></div>

                        <p class="text-gray-500 ml-3">Gerando ideias com Gemini...</p>

                    </div>

                    <div class="gemini-results mt-4" id="results-gemini"></div>

                </div>

            </section>



            <section id="cursor" class="content-section p-6 md:p-8 bg-white rounded-2xl shadow-lg">

                <h2 class="text-3xl font-bold text-purple-700 mb-4">Cursor: Uma Prévia do Futuro</h2>

                <div class="grid md:grid-cols-2 gap-8">

                    <div>

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Diferencial</h3>

                        <p class="text-gray-600 leading-relaxed">O Cursor representa a próxima fronteira da IA, mas focada em um nicho específico: o desenvolvimento de software. Ele não é apenas um assistente, mas um ambiente de programação construído do zero com a IA em seu núcleo. Sua capacidade de entender todo o contexto de um projeto de código para sugerir, corrigir e até mesmo escrever blocos inteiros de lógica o posiciona como uma ferramenta que irá revolucionar a produtividade técnica. Para nós, conhecê-lo é entender o tipo de tecnologia que em breve poderá estar presente em outras áreas.</p>

                    </div>

                    <div>

                        <h3 class="text-2xl font-semibold text-gray-800 mb-3">Pontos Positivos</h3>

                        <ul class="space-y-3">

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Visão do futuro da interação entre humanos e IA em ambientes de trabalho.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Integração profunda com o contexto de um projeto.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Capacidade de acelerar fluxos de trabalho técnicos drasticamente.</span></li>

                            <li class="flex items-start"><span class="text-purple-600 font-bold mr-3 mt-1">✓</span><span>Demonstra o potencial de IAs especializadas em nichos.</span></li>

                        </ul>

                    </div>

                </div>

                 <div class="mt-8 border-t pt-6">

                    <h3 class="text-2xl font-semibold text-gray-800 mb-3">Ideias de Aplicação Prática</h3>

                    <ul class="space-y-3 mb-6">

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Construção de Querys:</strong> Descreva em linguagem natural a informação que você precisa (ex: "usuários que usaram a feature X no último mês") e peça para o Cursor escrever a query SQL.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Análises via Notebooks:</strong> Agilize a criação de notebooks de análise de dados (Python/Pandas) para investigar o impacto de um treinamento ou o comportamento de um produto.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Análises de Shuffle:</strong> Ajuda a construir e depurar scripts para analisar resultados de testes A/B (shuffle) em produtos, traduzindo hipóteses em código de análise.</span></li>

                        <li class="flex items-start"><span class="text-purple-500 mr-3 mt-1.5">◆</span><span class="text-gray-700"><strong>Desenvolvimento de Softwares:</strong> Para equipes com desenvolvedores, acelera drasticamente a criação de ferramentas internas, automações e pequenos aplicativos.</span></li>

                    </ul>

                    <p class="text-gray-600 mb-4 text-sm">Para mais ideias, clique no botão e a IA irá gerar outros casos de uso com base nas características da ferramenta.</p>

                    <button class="gemini-btn bg-[#820AD1] text-white font-bold py-2 px-4 rounded-lg hover:bg-purple-800 transition-colors" data-tool="cursor">✨ Gerar Mais Ideias</button>

                    <div class="loader mt-4 items-center" id="loader-cursor">

                        <div class="animate-spin rounded-full h-8 w-8 border-b-2 border-purple-700"></div>

                        <p class="text-gray-500 ml-3">Gerando ideias com Gemini...</p>

                    </div>

                    <div class="gemini-results mt-4" id="results-cursor"></div>

                </div>

            </section>

            

            <section id="comparativo" class="content-section p-6 md:p-8 bg-white rounded-2xl shadow-lg">

                <h2 class="text-3xl font-bold text-purple-700 mb-4 text-center">Comparativo Visual</h2>

                <p class="text-center text-gray-600 mb-6 max-w-3xl mx-auto">Este gráfico compara as três ferramentas em cinco dimensões-chave. Passe o mouse sobre os pontos para ver os detalhes. Use-o para identificar rapidamente qual ferramenta se alinha melhor com uma necessidade específica.</p>

                <div class="chart-container">

                    <canvas id="radarChart"></canvas>

                </div>

            </section>

        </main>

    </div>



    <script>

        document.addEventListener('DOMContentLoaded', () => {

            const navButtons = document.querySelectorAll('.nav-btn');

            const contentSections = document.querySelectorAll('.content-section');

            const geminiButtons = document.querySelectorAll('.gemini-btn');



            const setActiveTab = (targetId) => {

                navButtons.forEach(btn => btn.classList.toggle('active', btn.dataset.target === targetId));

                contentSections.forEach(section => section.classList.toggle('active', section.id === targetId));

            };

            

            navButtons.forEach(button => {

                button.addEventListener('click', () => setActiveTab(button.dataset.target));

            });



            async function callGeminiAPI(payload, retries = 3, delay = 1000) {

                const apiKey = "";

                const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-05-20:generateContent?key=${apiKey}`;



                try {

                    const response = await fetch(apiUrl, {

                        method: 'POST',

                        headers: { 'Content-Type': 'application/json' },

                        body: JSON.stringify(payload)

                    });



                    if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);

                    

                    const result = await response.json();

                    const candidate = result.candidates?.[0];



                    if (candidate && candidate.content?.parts?.[0]?.text) {

                        return candidate.content.parts[0].text;

                    } else {

                        throw new Error("Resposta da API inválida ou vazia.");

                    }

                } catch (error) {

                    console.error(`API call failed: ${error.message}`);

                    if (retries > 0) {

                        await new Promise(res => setTimeout(res, delay));

                        return callGeminiAPI(payload, retries - 1, delay * 2);

                    } else {

                        return "<p class='text-red-600'>Desculpe, não foi possível gerar as ideias no momento. Tente novamente mais tarde.</p>";

                    }

                }

            }



            async function generateUseCases(tool) {

                const loader = document.getElementById(`loader-${tool}`);

                const resultsContainer = document.getElementById(`results-${tool}`);

                const toolSection = document.getElementById(tool);

                const toolName = toolSection.querySelector('h2').textContent;

                const differential = toolSection.querySelector('p.leading-relaxed').textContent;



                loader.style.display = 'flex';

                resultsContainer.innerHTML = '';



                const systemPrompt = "Aja como um especialista em inovação e treinamento para o setor bancário. Você é criativo, prático e focado em resultados. Suas sugestões devem ser diretamente aplicáveis por um time de Gestão de Treinamento.";

                const userQuery = `Para a ferramenta de IA chamada "${toolName}", cujo principal diferencial é: "${differential}". Gere 3 casos de uso práticos para um time de 'Gestão de Treinamento' em um grande banco. Para cada caso de uso, inclua um título em negrito e uma breve descrição. Formate a resposta inteira como uma lista HTML (<ul>...</ul>), sem nenhum texto introdutório ou conclusivo fora da lista.`;

                

                const payload = {

                    contents: [{ parts: [{ text: userQuery }] }],

                    systemInstruction: { parts: [{ text: systemPrompt }] },

                };



                const generatedHtml = await callGeminiAPI(payload);

                

                resultsContainer.innerHTML = generatedHtml;

                loader.style.display = 'none';

            }



            geminiButtons.forEach(button => {

                button.addEventListener('click', () => {

                    const tool = button.dataset.tool;

                    generateUseCases(tool);

                });

            });



            const ctx = document.getElementById('radarChart').getContext('2d');

            const radarChart = new Chart(ctx, {

                type: 'radar',

                data: {

                    labels: ['Foco em Dados Internos', 'Criatividade Multimodal', 'Especialização Técnica', 'Versatilidade Geral', 'Segurança (Contexto Fechado)'],

                    datasets: [{

                        label: 'NotebookLM',

                        data: [5, 2, 1, 3, 5],

                        backgroundColor: 'rgba(130, 10, 209, 0.2)',

                        borderColor: 'rgba(130, 10, 209, 1)',

                        borderWidth: 2,

                        pointBackgroundColor: 'rgba(130, 10, 209, 1)',

                        pointBorderColor: '#fff',

                        pointHoverBackgroundColor: '#fff',

                        pointHoverBorderColor: 'rgba(130, 10, 209, 1)'

                    }, {

                        label: 'Gemini',

                        data: [3, 5, 3, 5, 2],

                        backgroundColor: 'rgba(0, 180, 150, 0.2)',

                        borderColor: 'rgba(0, 180, 150, 1)',

                        borderWidth: 2,

                        pointBackgroundColor: 'rgba(0, 180, 150, 1)',

                        pointBorderColor: '#fff',

                        pointHoverBackgroundColor: '#fff',

                        pointHoverBorderColor: 'rgba(0, 180, 150, 1)'

                    }, {

                        label: 'Cursor',

                        data: [2, 2, 5, 2, 4],

                        backgroundColor: 'rgba(30, 41, 59, 0.2)',

                        borderColor: 'rgba(30, 41, 59, 1)',

                        borderWidth: 2,

                        pointBackgroundColor: 'rgba(30, 41, 59, 1)',

                        pointBorderColor: '#fff',

                        pointHoverBackgroundColor: '#fff',

                        pointHoverBorderColor: 'rgba(30, 41, 59, 1)'

                    }]

                },

                options: {

                    maintainAspectRatio: false,

                    responsive: true,

                    scales: { r: { angleLines: { color: 'rgba(0, 0, 0, 0.05)' }, grid: { color: 'rgba(0, 0, 0, 0.08)' }, pointLabels: { font: { size: 13, weight: 'bold' }, color: '#1e293b' }, ticks: { backdropColor: 'rgba(249, 245, 255, 0.75)', color: '#64748b', stepSize: 1, max: 5, min: 0 } } },

                    plugins: { legend: { position: 'top', labels: { font: { size: 14 } } }, tooltip: { callbacks: { label: (c) => `${c.dataset.label||''}: ${c.parsed.r!==null?c.parsed.r:''}` } } }

                }

            });

            

            setActiveTab('inicio');

        });

    </script>

</body>

</html>

