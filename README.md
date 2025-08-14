<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PontoTech - Sistema Completo de Ponto Eletrônico</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
        }
        
        .phone-mockup {
            width: 320px;
            height: 640px;
            background: linear-gradient(145deg, #2a2a2a, #1a1a1a);
            border-radius: 35px;
            padding: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3), inset 0 2px 4px rgba(255,255,255,0.1);
            position: relative;
            margin: 0 auto;
        }
        
        .phone-screen {
            width: 100%;
            height: 100%;
            background: #000;
            border-radius: 25px;
            overflow: hidden;
            position: relative;
        }
        
        .notch {
            position: absolute;
            top: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 120px;
            height: 25px;
            background: #000;
            border-radius: 0 0 15px 15px;
            z-index: 10;
        }
        
        .orange-btn {
            background: linear-gradient(135deg, #ff6b35, #ff8c42);
            transition: all 0.3s ease;
        }
        
        .orange-btn:hover {
            background: linear-gradient(135deg, #e55a2b, #e67a35);
            transform: translateY(-2px);
        }
        
        .digital-clock {
            font-family: 'Courier New', monospace;
            font-size: 2.5rem;
            font-weight: bold;
            color: white;
            text-shadow: 0 0 20px rgba(255,255,255,0.3);
        }
        
        .employee-photo {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background: linear-gradient(135deg, #ff6b35, #ff8c42);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        .screen {
            display: none;
            height: 100%;
            overflow-y: auto;
        }
        
        .screen.active {
            display: block;
        }
        
        .nav-btn {
            padding: 8px 16px;
            margin: 4px;
            border-radius: 20px;
            background: #333;
            color: white;
            border: none;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .nav-btn.active {
            background: linear-gradient(135deg, #ff6b35, #ff8c42);
        }
        
        .status-present { color: #10b981; }
        .status-absent { color: #6b7280; }
        .status-late { color: #f59e0b; }
        
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.8);
            z-index: 1000;
        }
        
        .modal.active {
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .modal-content {
            background: #1a1a1a;
            padding: 30px;
            border-radius: 15px;
            max-width: 90%;
            max-height: 90%;
            overflow-y: auto;
            color: white;
        }
        
        .report-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        
        .report-table th,
        .report-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #333;
        }
        
        .report-table th {
            background: #333;
            color: #ff6b35;
        }
        
        .control-panel {
            background: #1a1a1a;
            padding: 30px;
            border-radius: 15px;
            margin: 20px;
            color: white;
        }
    </style>
</head>
<body class="bg-gray-100 min-h-screen">
    <!-- Painel de Controle Principal -->
    <div class="control-panel">
        <h1 class="text-4xl font-bold text-center mb-8 text-orange-500">PontoTech - Sistema Completo</h1>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
            <div class="bg-gray-800 p-6 rounded-lg text-center">
                <h3 class="text-xl font-semibold mb-4 text-orange-500">📱 Simulador do App</h3>
                <p class="text-gray-300 mb-4">Teste todas as funcionalidades do aplicativo</p>
                <button onclick="showApp()" class="orange-btn text-white px-6 py-3 rounded-lg font-semibold">Abrir App</button>
            </div>
            
            <div class="bg-gray-800 p-6 rounded-lg text-center">
                <h3 class="text-xl font-semibold mb-4 text-orange-500">📊 Relatórios Gerenciais</h3>
                <p class="text-gray-300 mb-4">Visualize relatórios detalhados de ponto</p>
                <button onclick="showReports()" class="orange-btn text-white px-6 py-3 rounded-lg font-semibold">Ver Relatórios</button>
            </div>
            
            <div class="bg-gray-800 p-6 rounded-lg text-center">
                <h3 class="text-xl font-semibold mb-4 text-orange-500">📖 Manual de Uso</h3>
                <p class="text-gray-300 mb-4">Aprenda a usar todas as funcionalidades</p>
                <button onclick="showManual()" class="orange-btn text-white px-6 py-3 rounded-lg font-semibold">Ver Manual</button>
            </div>
        </div>
        
        <div class="text-center">
            <h3 class="text-2xl font-semibold mb-4 text-orange-500">🔧 Como Implementar</h3>
            <div class="bg-gray-800 p-6 rounded-lg text-left">
                <h4 class="font-semibold mb-3 text-orange-400">Para usar este sistema:</h4>
                <ol class="list-decimal list-inside space-y-2 text-gray-300">
                    <li><strong>Salvar o arquivo:</strong> Copie todo este código e salve como "pontotech.html"</li>
                    <li><strong>Hospedar online:</strong> Use serviços como Netlify, Vercel ou GitHub Pages (gratuitos)</li>
                    <li><strong>Compartilhar com funcionários:</strong> Envie o link gerado para os dispositivos móveis</li>
                    <li><strong>Acesso móvel:</strong> Funcionários acessam pelo navegador do celular</li>
                    <li><strong>Dados salvos:</strong> Informações ficam armazenadas no navegador de cada dispositivo</li>
                </ol>
                <div class="mt-4 p-4 bg-orange-900 rounded-lg">
                    <p class="text-orange-200"><strong>💡 Dica:</strong> Para uso empresarial real, recomenda-se integração com banco de dados e servidor próprio.</p>
                </div>
            </div>
        </div>
    </div>

    <!-- Simulador do App Mobile -->
    <div id="appModal" class="modal">
        <div class="modal-content" style="max-width: 400px;">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-semibold text-orange-500">📱 Simulador PontoTech</h3>
                <button onclick="closeApp()" class="text-white hover:text-orange-500 text-2xl">&times;</button>
            </div>
            
            <!-- Navegação do App -->
            <div class="flex flex-wrap justify-center mb-4">
                <button class="nav-btn active" onclick="showScreen('login')">Login</button>
                <button class="nav-btn" onclick="showScreen('ponto')">Ponto</button>
                <button class="nav-btn" onclick="showScreen('historico')">Histórico</button>
                <button class="nav-btn" onclick="showScreen('gestor')">Gestor</button>
                <button class="nav-btn" onclick="showScreen('cadastro')">Cadastro</button>
            </div>
            
            <div class="phone-mockup">
                <div class="notch"></div>
                
                <!-- Tela de Login -->
                <div id="loginScreen" class="screen active phone-screen p-6 flex flex-col">
                    <div class="text-center mb-8 mt-6">
                        <div class="w-16 h-16 mx-auto mb-4 bg-gradient-to-r from-orange-500 to-orange-600 rounded-full flex items-center justify-center">
                            <span class="text-white font-bold text-xl">PT</span>
                        </div>
                        <h2 class="text-white text-xl font-semibold">PontoTech</h2>
                        <p class="text-gray-400 text-sm">Sistema de Ponto Digital</p>
                    </div>
                    
                    <div class="flex-1 flex flex-col justify-center space-y-4">
                        <div>
                            <input type="text" id="loginUser" placeholder="CPF ou E-mail" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div class="relative">
                            <input type="password" id="loginPass" placeholder="Senha" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none pr-10">
                            <div class="absolute right-3 top-3 text-gray-400">🔒</div>
                        </div>
                        
                        <button onclick="doLogin()" class="orange-btn text-white font-semibold py-3 rounded-lg mt-6">
                            Entrar
                        </button>
                        
                        <div class="text-center mt-4">
                            <a href="#" class="text-white text-sm hover:text-orange-500">Esqueci minha senha</a>
                        </div>
                    </div>
                </div>
                
                <!-- Tela de Registro de Ponto -->
                <div id="pontoScreen" class="screen phone-screen p-6">
                    <div class="flex items-center justify-between mb-6 mt-6">
                        <div class="flex items-center">
                            <div class="employee-photo mr-3" id="userPhoto">JS</div>
                            <div>
                                <h3 class="text-white font-semibold" id="userName">Josciele Silva</h3>
                                <p class="text-gray-400 text-sm" id="userRole">Desenvolvedor</p>
                            </div>
                        </div>
                        <button onclick="logout()" class="text-orange-500 text-sm">Sair</button>
                    </div>
                    
                    <div class="text-center mb-8">
                        <div class="digital-clock mb-2" id="clock">14:32:45</div>
                        <p class="text-gray-400" id="currentDate">Quinta-feira, 21 de Dezembro</p>
                    </div>
                    
                    <div class="space-y-3">
                        <button onclick="registrarPonto('entrada')" class="w-full bg-gradient-to-r from-orange-500 to-orange-600 text-white font-semibold py-3 rounded-lg hover:from-orange-600 hover:to-orange-700">
                            🚪 Bater Entrada
                        </button>
                        
                        <button onclick="registrarPonto('inicio_intervalo')" class="w-full bg-gradient-to-r from-yellow-500 to-yellow-600 text-white font-semibold py-3 rounded-lg hover:from-yellow-600 hover:to-yellow-700">
                            ☕ Início Intervalo
                        </button>
                        
                        <button onclick="registrarPonto('fim_intervalo')" class="w-full bg-gradient-to-r from-blue-500 to-blue-600 text-white font-semibold py-3 rounded-lg hover:from-blue-600 hover:to-blue-700">
                            🔄 Fim Intervalo
                        </button>
                        
                        <button onclick="registrarPonto('saida')" class="w-full bg-gradient-to-r from-red-500 to-red-600 text-white font-semibold py-3 rounded-lg hover:from-red-600 hover:to-red-700">
                            🚪 Bater Saída
                        </button>
                    </div>
                    
                    <div class="mt-6 p-3 bg-gray-900 rounded-lg">
                        <p class="text-gray-400 text-xs">📍 Localização: <span id="location">Carregando...</span></p>
                        <p class="text-gray-400 text-xs">🌐 IP: <span id="userIP">Detectando...</span></p>
                    </div>
                    
                    <div id="pontoStatus" class="mt-4 p-3 bg-green-900 rounded-lg hidden">
                        <p class="text-green-400 text-sm font-semibold">✅ Ponto registrado com sucesso!</p>
                    </div>
                </div>
                
                <!-- Tela de Histórico -->
                <div id="historicoScreen" class="screen phone-screen p-6">
                    <div class="flex justify-between items-center mb-6 mt-6">
                        <h3 class="text-white font-semibold text-lg">Histórico</h3>
                        <select id="mesFilter" onchange="filterHistorico()" class="bg-gray-900 text-white p-2 rounded border border-gray-700 text-sm">
                            <option value="2023-12">Dezembro 2023</option>
                            <option value="2023-11">Novembro 2023</option>
                            <option value="2023-10">Outubro 2023</option>
                        </select>
                    </div>
                    
                    <div id="historicoList" class="space-y-3">
                        <!-- Histórico será carregado dinamicamente -->
                    </div>
                    
                    <div class="mt-6">
                        <button onclick="exportarHistorico()" class="w-full orange-btn text-white font-semibold py-3 rounded-lg">
                            📄 Exportar Histórico
                        </button>
                    </div>
                </div>
                
                <!-- Tela do Gestor -->
                <div id="gestorScreen" class="screen phone-screen p-6">
                    <div class="flex justify-between items-center mb-6 mt-6">
                        <h3 class="text-white font-semibold text-lg">Painel Gestor</h3>
                        <div class="text-orange-500 text-sm" id="totalFuncionarios">👥 8 funcionários</div>
                    </div>
                    
                    <div id="funcionariosList" class="space-y-2 mb-6">
                        <!-- Lista será carregada dinamicamente -->
                    </div>
                    
                    <div class="grid grid-cols-3 gap-2 mb-4 text-center text-xs">
                        <div class="bg-green-900 p-2 rounded">
                            <div class="text-green-400 font-bold" id="presentesCount">5</div>
                            <div class="text-gray-400">Presentes</div>
                        </div>
                        <div class="bg-yellow-900 p-2 rounded">
                            <div class="text-yellow-400 font-bold" id="atrasosCount">1</div>
                            <div class="text-gray-400">Atrasos</div>
                        </div>
                        <div class="bg-red-900 p-2 rounded">
                            <div class="text-red-400 font-bold" id="ausentesCount">2</div>
                            <div class="text-gray-400">Ausentes</div>
                        </div>
                    </div>
                    
                    <div class="space-y-2">
                        <button onclick="gerarRelatorioCompleto()" class="w-full orange-btn text-white font-semibold py-2 rounded-lg text-sm">
                            📊 Relatório Completo
                        </button>
                        <button onclick="showScreen('cadastro')" class="w-full bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 rounded-lg text-sm">
                            👤 Cadastrar Funcionário
                        </button>
                    </div>
                </div>
                
                <!-- Tela de Cadastro -->
                <div id="cadastroScreen" class="screen phone-screen p-6">
                    <div class="flex justify-between items-center mb-6 mt-6">
                        <h3 class="text-white font-semibold text-lg">Novo Funcionário</h3>
                        <button onclick="showScreen('gestor')" class="text-orange-500 text-sm">Voltar</button>
                    </div>
                    
                    <div class="space-y-4">
                        <div>
                            <label class="text-gray-400 text-sm">Nome Completo</label>
                            <input type="text" id="novoNome" placeholder="Ex: João Silva" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div>
                            <label class="text-gray-400 text-sm">CPF</label>
                            <input type="text" id="novoCPF" placeholder="000.000.000-00" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div>
                            <label class="text-gray-400 text-sm">E-mail</label>
                            <input type="email" id="novoEmail" placeholder="joao@empresa.com" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div>
                            <label class="text-gray-400 text-sm">Cargo</label>
                            <input type="text" id="novoCargo" placeholder="Ex: Desenvolvedor" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div>
                            <label class="text-gray-400 text-sm">Senha Inicial</label>
                            <input type="password" id="novaSenha" placeholder="Senha temporária" 
                                   class="w-full bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                        </div>
                        
                        <div>
                            <label class="text-gray-400 text-sm">Horário de Trabalho</label>
                            <div class="grid grid-cols-2 gap-2">
                                <input type="time" id="horarioEntrada" value="08:00" 
                                       class="bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                                <input type="time" id="horarioSaida" value="17:00" 
                                       class="bg-gray-900 text-white p-3 rounded-lg border border-gray-700 focus:border-orange-500 focus:outline-none">
                            </div>
                        </div>
                        
                        <button onclick="cadastrarFuncionario()" class="w-full orange-btn text-white font-semibold py-3 rounded-lg mt-6">
                            ✅ Cadastrar Funcionário
                        </button>
                    </div>
                    
                    <div id="cadastroStatus" class="mt-4 p-3 rounded-lg hidden">
                        <p class="text-sm font-semibold"></p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Relatórios -->
    <div id="reportsModal" class="modal">
        <div class="modal-content" style="max-width: 1200px;">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-2xl font-semibold text-orange-500">📊 Relatórios Gerenciais</h3>
                <button onclick="closeReports()" class="text-white hover:text-orange-500 text-2xl">&times;</button>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                <button onclick="showReport('diario')" class="bg-gray-800 p-4 rounded-lg hover:bg-gray-700 text-center">
                    <div class="text-3xl mb-2">📅</div>
                    <div class="text-white font-semibold">Relatório Diário</div>
                </button>
                <button onclick="showReport('mensal')" class="bg-gray-800 p-4 rounded-lg hover:bg-gray-700 text-center">
                    <div class="text-3xl mb-2">📊</div>
                    <div class="text-white font-semibold">Relatório Mensal</div>
                </button>
                <button onclick="showReport('funcionario')" class="bg-gray-800 p-4 rounded-lg hover:bg-gray-700 text-center">
                    <div class="text-3xl mb-2">👤</div>
                    <div class="text-white font-semibold">Por Funcionário</div>
                </button>
            </div>
            
            <div id="reportContent" class="bg-gray-800 p-6 rounded-lg">
                <p class="text-gray-400 text-center">Selecione um tipo de relatório acima</p>
            </div>
        </div>
    </div>

    <!-- Modal do Manual -->
    <div id="manualModal" class="modal">
        <div class="modal-content" style="max-width: 800px;">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-2xl font-semibold text-orange-500">📖 Manual de Uso - PontoTech</h3>
                <button onclick="closeManual()" class="text-white hover:text-orange-500 text-2xl">&times;</button>
            </div>
            
            <div class="space-y-6">
                <div class="bg-gray-800 p-6 rounded-lg">
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">🚀 Como Começar</h4>
                    <ol class="list-decimal list-inside space-y-2 text-gray-300">
                        <li><strong>Acesso Inicial:</strong> Use login "admin" e senha "123456" para acesso de gestor</li>
                        <li><strong>Cadastro de Funcionários:</strong> Vá em "Gestor" → "Cadastrar Funcionário"</li>
                        <li><strong>Login de Funcionário:</strong> Use CPF ou e-mail cadastrado</li>
                        <li><strong>Registro de Ponto:</strong> Clique nos botões coloridos na tela principal</li>
                    </ol>
                </div>
                
                <div class="bg-gray-800 p-6 rounded-lg">
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">👤 Para Funcionários</h4>
                    <ul class="list-disc list-inside space-y-2 text-gray-300">
                        <li><strong>Entrada:</strong> Botão laranja - registra chegada ao trabalho</li>
                        <li><strong>Início Intervalo:</strong> Botão amarelo - marca início do almoço/pausa</li>
                        <li><strong>Fim Intervalo:</strong> Botão azul - marca retorno do intervalo</li>
                        <li><strong>Saída:</strong> Botão vermelho - registra fim do expediente</li>
                        <li><strong>Histórico:</strong> Visualize todos os pontos batidos</li>
                    </ul>
                </div>
                
                <div class="bg-gray-800 p-6 rounded-lg">
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">👨‍💼 Para Gestores</h4>
                    <ul class="list-disc list-inside space-y-2 text-gray-300">
                        <li><strong>Painel Gestor:</strong> Visualize status de todos os funcionários</li>
                        <li><strong>Cadastro:</strong> Adicione novos funcionários ao sistema</li>
                        <li><strong>Relatórios:</strong> Gere relatórios detalhados de ponto</li>
                        <li><strong>Monitoramento:</strong> Acompanhe presenças, atrasos e faltas</li>
                        <li><strong>Exportação:</strong> Baixe dados em formato de texto</li>
                    </ul>
                </div>
                
                <div class="bg-gray-800 p-6 rounded-lg">
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">🔧 Implementação Técnica</h4>
                    <div class="space-y-4">
                        <div>
                            <h5 class="font-semibold text-orange-300">1. Hospedagem Gratuita:</h5>
                            <ul class="list-disc list-inside ml-4 space-y-1 text-gray-300">
                                <li><strong>Netlify:</strong> Arraste o arquivo HTML para netlify.app</li>
                                <li><strong>Vercel:</strong> Conecte com GitHub e faça deploy automático</li>
                                <li><strong>GitHub Pages:</strong> Crie repositório e ative Pages</li>
                            </ul>
                        </div>
                        
                        <div>
                            <h5 class="font-semibold text-orange-300">2. Compartilhamento:</h5>
                            <ul class="list-disc list-inside ml-4 space-y-1 text-gray-300">
                                <li>Copie o link gerado pela hospedagem</li>
                                <li>Envie para os funcionários via WhatsApp/e-mail</li>
                                <li>Funcionários salvam como atalho na tela inicial</li>
                            </ul>
                        </div>
                        
                        <div>
                            <h5 class="font-semibold text-orange-300">3. Dados e Segurança:</h5>
                            <ul class="list-disc list-inside ml-4 space-y-1 text-gray-300">
                                <li>Dados salvos localmente no navegador (localStorage)</li>
                                <li>Para uso empresarial: integrar com banco de dados</li>
                                <li>Backup regular recomendado via exportação</li>
                            </ul>
                        </div>
                    </div>
                </div>
                
                <div class="bg-orange-900 p-6 rounded-lg">
                    <h4 class="text-xl font-semibold text-orange-200 mb-4">⚠️ Limitações Atuais</h4>
                    <ul class="list-disc list-inside space-y-2 text-orange-200">
                        <li>Dados armazenados apenas no dispositivo local</li>
                        <li>Não há sincronização automática entre dispositivos</li>
                        <li>Para uso empresarial real, requer servidor e banco de dados</li>
                        <li>Localização GPS simulada (requer permissões reais em produção)</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Dados simulados e sistema de armazenamento
        let currentUser = null;
        let funcionarios = JSON.parse(localStorage.getItem('funcionarios')) || [
            {
                id: 1,
                nome: 'Josciele Silva',
                cpf: '123.456.789-00',
                email: 'josciele@empresa.com',
                cargo: 'Desenvolvedor',
                senha: '123456',
                horarioEntrada: '08:00',
                horarioSaida: '17:00',
                iniciais: 'JS'
            },
            {
                id: 2,
                nome: 'João Fábio',
                cpf: '987.654.321-00',
                email: 'joao@empresa.com',
                cargo: 'Designer',
                senha: '123456',
                horarioEntrada: '08:00',
                horarioSaida: '17:00',
                iniciais: 'JF'
            }
        ];
        
        let registrosPonto = JSON.parse(localStorage.getItem('registrosPonto')) || [];
        
        // Adicionar usuário admin
        if (!funcionarios.find(f => f.email === 'admin')) {
            funcionarios.push({
                id: 999,
                nome: 'Administrador',
                cpf: 'admin',
                email: 'admin',
                cargo: 'Gestor',
                senha: '123456',
                horarioEntrada: '08:00',
                horarioSaida: '17:00',
                iniciais: 'AD',
                isAdmin: true
            });
        }
        
        // Funções principais
        function showApp() {
            document.getElementById('appModal').classList.add('active');
            updateClock();
            detectLocation();
            detectIP();
        }
        
        function closeApp() {
            document.getElementById('appModal').classList.remove('active');
        }
        
        function showReports() {
            document.getElementById('reportsModal').classList.add('active');
        }
        
        function closeReports() {
            document.getElementById('reportsModal').classList.remove('active');
        }
        
        function showManual() {
            document.getElementById('manualModal').classList.add('active');
        }
        
        function closeManual() {
            document.getElementById('manualModal').classList.remove('active');
        }
        
        function showScreen(screenName) {
            // Esconder todas as telas
            document.querySelectorAll('.screen').forEach(screen => {
                screen.classList.remove('active');
            });
            
            // Remover classe active de todos os botões
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Mostrar tela selecionada
            document.getElementById(screenName + 'Screen').classList.add('active');
            
            // Ativar botão correspondente
            event.target.classList.add('active');
            
            // Carregar dados específicos da tela
            if (screenName === 'historico') {
                loadHistorico();
            } else if (screenName === 'gestor') {
                loadGestorData();
            }
        }
        
        function doLogin() {
            const user = document.getElementById('loginUser').value;
            const pass = document.getElementById('loginPass').value;
            
            const funcionario = funcionarios.find(f => 
                (f.cpf === user || f.email === user) && f.senha === pass
            );
            
            if (funcionario) {
                currentUser = funcionario;
                document.getElementById('userName').textContent = funcionario.nome;
                document.getElementById('userRole').textContent = funcionario.cargo;
                document.getElementById('userPhoto').textContent = funcionario.iniciais;
                showScreen('ponto');
                
                // Limpar campos
                document.getElementById('loginUser').value = '';
                document.getElementById('loginPass').value = '';
            } else {
                alert('Usuário ou senha incorretos!');
            }
        }
        
        function logout() {
            currentUser = null;
            showScreen('login');
        }
        
        function registrarPonto(tipo) {
            if (!currentUser) return;
            
            const agora = new Date();
            const registro = {
                funcionarioId: currentUser.id,
                funcionarioNome: currentUser.nome,
                tipo: tipo,
                data: agora.toISOString().split('T')[0],
                hora: agora.toTimeString().split(' ')[0],
                timestamp: agora.getTime(),
                localizacao: document.getElementById('location').textContent,
                ip: document.getElementById('userIP').textContent
            };
            
            registrosPonto.push(registro);
            localStorage.setItem('registrosPonto', JSON.stringify(registrosPonto));
            
            // Mostrar confirmação
            const status = document.getElementById('pontoStatus');
            status.classList.remove('hidden');
            status.querySelector('p').textContent = `✅ ${getTipoLabel(tipo)} registrado às ${registro.hora}`;
            
            setTimeout(() => {
                status.classList.add('hidden');
            }, 3000);
        }
        
        function getTipoLabel(tipo) {
            const labels = {
                'entrada': 'Entrada',
                'inicio_intervalo': 'Início do Intervalo',
                'fim_intervalo': 'Fim do Intervalo',
                'saida': 'Saída'
            };
            return labels[tipo] || tipo;
        }
        
        function getTipoIcon(tipo) {
            const icons = {
                'entrada': '🚪',
                'inicio_intervalo': '☕',
                'fim_intervalo': '🔄',
                'saida': '🚪'
            };
            return icons[tipo] || '⏰';
        }
        
        function loadHistorico() {
            if (!currentUser) return;
            
            const mes = document.getElementById('mesFilter').value;
            const registrosUsuario = registrosPonto.filter(r => 
                r.funcionarioId === currentUser.id && r.data.startsWith(mes)
            );
            
            // Agrupar por data
            const registrosPorData = {};
            registrosUsuario.forEach(r => {
                if (!registrosPorData[r.data]) {
                    registrosPorData[r.data] = [];
                }
                registrosPorData[r.data].push(r);
            });
            
            const historicoList = document.getElementById('historicoList');
            historicoList.innerHTML = '';
            
            Object.keys(registrosPorData).sort().reverse().forEach(data => {
                const registros = registrosPorData[data];
                const dataFormatada = new Date(data + 'T00:00:00').toLocaleDateString('pt-BR');
                
                const div = document.createElement('div');
                div.className = 'bg-gray-900 p-3 rounded-lg';
                
                let status = 'Completo';
                let statusColor = 'text-green-500';
                
                const temEntrada = registros.some(r => r.tipo === 'entrada');
                const temSaida = registros.some(r => r.tipo === 'saida');
                
                if (!temEntrada && !temSaida) {
                    status = 'Falta';
                    statusColor = 'text-red-500';
                } else if (!temEntrada || !temSaida) {
                    status = 'Incompleto';
                    statusColor = 'text-yellow-500';
                }
                
                div.innerHTML = `
                    <div class="flex justify-between items-center mb-2">
                        <span class="text-white font-medium">${dataFormatada}</span>
                        <span class="${statusColor} text-sm">${status}</span>
                    </div>
                    <div class="grid grid-cols-2 gap-2 text-sm">
                        ${registros.map(r => `
                            <div class="text-gray-400">${getTipoIcon(r.tipo)} ${getTipoLabel(r.tipo)}: ${r.hora.substring(0,5)}</div>
                        `).join('')}
                    </div>
                `;
                
                historicoList.appendChild(div);
            });
        }
        
        function filterHistorico() {
            loadHistorico();
        }
        
        function exportarHistorico() {
            if (!currentUser) return;
            
            const registrosUsuario = registrosPonto.filter(r => r.funcionarioId === currentUser.id);
            
            let texto = `HISTÓRICO DE PONTO - ${currentUser.nome}\n`;
            texto += `Gerado em: ${new Date().toLocaleString('pt-BR')}\n\n`;
            
            registrosUsuario.forEach(r => {
                texto += `${new Date(r.data).toLocaleDateString('pt-BR')} - ${r.hora} - ${getTipoLabel(r.tipo)}\n`;
            });
            
            const blob = new Blob([texto], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `historico_${currentUser.nome.replace(' ', '_')}.txt`;
            a.click();
        }
        
        function loadGestorData() {
            const funcionariosList = document.getElementById('funcionariosList');
            funcionariosList.innerHTML = '';
            
            let presentes = 0, ausentes = 0, atrasos = 0;
            
            funcionarios.filter(f => !f.isAdmin).forEach(funcionario => {
                const hoje = new Date().toISOString().split('T')[0];
                const registrosHoje = registrosPonto.filter(r => 
                    r.funcionarioId === funcionario.id && r.data === hoje
                );
                
                let status = 'Ausente';
                let statusColor = 'status-absent';
                let statusIcon = '●';
                
                if (registrosHoje.length > 0) {
                    const entrada = registrosHoje.find(r => r.tipo === 'entrada');
                    if (entrada) {
                        const horaEntrada = entrada.hora;
                        const horaEsperada = funcionario.horarioEntrada;
                        
                        if (horaEntrada <= horaEsperada) {
                            status = 'Presente';
                            statusColor = 'status-present';
                            presentes++;
                        } else {
                            status = 'Atraso';
                            statusColor = 'status-late';
                            atrasos++;
                        }
                    }
                } else {
                    ausentes++;
                }
                
                const div = document.createElement('div');
                div.className = 'bg-gray-900 p-3 rounded-lg flex items-center justify-between';
                div.innerHTML = `
                    <div class="flex items-center">
                        <div class="w-8 h-8 bg-gradient-to-r from-orange-500 to-orange-600 rounded-full flex items-center justify-center text-white text-xs font-bold mr-3">
                            ${funcionario.iniciais}
                        </div>
                        <div>
                            <p class="text-white text-sm font-medium">${funcionario.nome}</p>
                            <p class="text-gray-400 text-xs">${status}</p>
                        </div>
                    </div>
                    <div class="${statusColor}">${statusIcon}</div>
                `;
                
                funcionariosList.appendChild(div);
            });
            
            document.getElementById('presentesCount').textContent = presentes;
            document.getElementById('atrasosCount').textContent = atrasos;
            document.getElementById('ausentesCount').textContent = ausentes;
            document.getElementById('totalFuncionarios').textContent = `👥 ${funcionarios.filter(f => !f.isAdmin).length} funcionários`;
        }
        
        function cadastrarFuncionario() {
            const nome = document.getElementById('novoNome').value;
            const cpf = document.getElementById('novoCPF').value;
            const email = document.getElementById('novoEmail').value;
            const cargo = document.getElementById('novoCargo').value;
            const senha = document.getElementById('novaSenha').value;
            const horarioEntrada = document.getElementById('horarioEntrada').value;
            const horarioSaida = document.getElementById('horarioSaida').value;
            
            if (!nome || !cpf || !email || !cargo || !senha) {
                showCadastroStatus('Preencha todos os campos obrigatórios!', 'error');
                return;
            }
            
            // Verificar se já existe
            if (funcionarios.find(f => f.cpf === cpf || f.email === email)) {
                showCadastroStatus('CPF ou e-mail já cadastrado!', 'error');
                return;
            }
            
            const novoFuncionario = {
                id: Date.now(),
                nome,
                cpf,
                email,
                cargo,
                senha,
                horarioEntrada,
                horarioSaida,
                iniciais: nome.split(' ').map(n => n[0]).join('').substring(0, 2).toUpperCase()
            };
            
            funcionarios.push(novoFuncionario);
            localStorage.setItem('funcionarios', JSON.stringify(funcionarios));
            
            showCadastroStatus('Funcionário cadastrado com sucesso!', 'success');
            
            // Limpar formulário
            document.getElementById('novoNome').value = '';
            document.getElementById('novoCPF').value = '';
            document.getElementById('novoEmail').value = '';
            document.getElementById('novoCargo').value = '';
            document.getElementById('novaSenha').value = '';
        }
        
        function showCadastroStatus(message, type) {
            const status = document.getElementById('cadastroStatus');
            const p = status.querySelector('p');
            
            status.className = `mt-4 p-3 rounded-lg ${type === 'success' ? 'bg-green-900' : 'bg-red-900'}`;
            p.className = `text-sm font-semibold ${type === 'success' ? 'text-green-400' : 'text-red-400'}`;
            p.textContent = message;
            
            status.classList.remove('hidden');
            
            setTimeout(() => {
                status.classList.add('hidden');
            }, 3000);
        }
        
        function gerarRelatorioCompleto() {
            const hoje = new Date();
            const mes = hoje.getMonth();
            const ano = hoje.getFullYear();
            
            let relatorio = `RELATÓRIO MENSAL - ${hoje.toLocaleDateString('pt-BR', {month: 'long', year: 'numeric'}).toUpperCase()}\n`;
            relatorio += `Gerado em: ${hoje.toLocaleString('pt-BR')}\n\n`;
            
            funcionarios.filter(f => !f.isAdmin).forEach(funcionario => {
                relatorio += `FUNCIONÁRIO: ${funcionario.nome}\n`;
                relatorio += `CARGO: ${funcionario.cargo}\n`;
                
                const registrosFuncionario = registrosPonto.filter(r => 
                    r.funcionarioId === funcionario.id && 
                    new Date(r.data).getMonth() === mes &&
                    new Date(r.data).getFullYear() === ano
                );
                
                const diasTrabalhados = [...new Set(registrosFuncionario.map(r => r.data))].length;
                const totalRegistros = registrosFuncionario.length;
                
                relatorio += `DIAS TRABALHADOS: ${diasTrabalhados}\n`;
                relatorio += `TOTAL DE REGISTROS: ${totalRegistros}\n`;
                relatorio += `${'='.repeat(50)}\n\n`;
            });
            
            const blob = new Blob([relatorio], { type: 'text/plain' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `relatorio_mensal_${hoje.getMonth() + 1}_${hoje.getFullYear()}.txt`;
            a.click();
        }
        
        function showReport(tipo) {
            const content = document.getElementById('reportContent');
            
            if (tipo === 'diario') {
                const hoje = new Date().toISOString().split('T')[0];
                const registrosHoje = registrosPonto.filter(r => r.data === hoje);
                
                content.innerHTML = `
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">📅 Relatório Diário - ${new Date().toLocaleDateString('pt-BR')}</h4>
                    <table class="report-table">
                        <thead>
                            <tr>
                                <th>Funcionário</th>
                                <th>Tipo</th>
                                <th>Horário</th>
                                <th>Localização</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${registrosHoje.map(r => `
                                <tr>
                                    <td>${r.funcionarioNome}</td>
                                    <td>${getTipoLabel(r.tipo)}</td>
                                    <td>${r.hora}</td>
                                    <td>${r.localizacao}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                `;
            } else if (tipo === 'mensal') {
                const mesAtual = new Date().toISOString().substring(0, 7);
                const registrosMes = registrosPonto.filter(r => r.data.startsWith(mesAtual));
                
                // Agrupar por funcionário
                const porFuncionario = {};
                registrosMes.forEach(r => {
                    if (!porFuncionario[r.funcionarioNome]) {
                        porFuncionario[r.funcionarioNome] = [];
                    }
                    porFuncionario[r.funcionarioNome].push(r);
                });
                
                content.innerHTML = `
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">📊 Relatório Mensal</h4>
                    <div class="space-y-4">
                        ${Object.keys(porFuncionario).map(nome => {
                            const registros = porFuncionario[nome];
                            const diasTrabalhados = [...new Set(registros.map(r => r.data))].length;
                            return `
                                <div class="bg-gray-700 p-4 rounded-lg">
                                    <h5 class="font-semibold text-white mb-2">${nome}</h5>
                                    <p class="text-gray-300">Dias trabalhados: ${diasTrabalhados}</p>
                                    <p class="text-gray-300">Total de registros: ${registros.length}</p>
                                </div>
                            `;
                        }).join('')}
                    </div>
                `;
            } else if (tipo === 'funcionario') {
                content.innerHTML = `
                    <h4 class="text-xl font-semibold text-orange-400 mb-4">👤 Relatório por Funcionário</h4>
                    <select onchange="loadFuncionarioReport(this.value)" class="bg-gray-700 text-white p-3 rounded-lg mb-4">
                        <option value="">Selecione um funcionário</option>
                        ${funcionarios.filter(f => !f.isAdmin).map(f => `
                            <option value="${f.id}">${f.nome}</option>
                        `).join('')}
                    </select>
                    <div id="funcionarioReportContent"></div>
                `;
            }
        }
        
        function loadFuncionarioReport(funcionarioId) {
            if (!funcionarioId) return;
            
            const funcionario = funcionarios.find(f => f.id == funcionarioId);
            const registrosFuncionario = registrosPonto.filter(r => r.funcionarioId == funcionarioId);
            
            const content = document.getElementById('funcionarioReportContent');
            content.innerHTML = `
                <div class="bg-gray-700 p-4 rounded-lg">
                    <h5 class="font-semibold text-white mb-4">${funcionario.nome} - ${funcionario.cargo}</h5>
                    <table class="report-table">
                        <thead>
                            <tr>
                                <th>Data</th>
                                <th>Tipo</th>
                                <th>Horário</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            ${registrosFuncionario.slice(-30).map(r => `
                                <tr>
                                    <td>${new Date(r.data).toLocaleDateString('pt-BR')}</td>
                                    <td>${getTipoLabel(r.tipo)}</td>
                                    <td>${r.hora}</td>
                                    <td>${r.tipo === 'entrada' && r.hora > funcionario.horarioEntrada ? 'Atraso' : 'Normal'}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                </div>
            `;
        }
        
        function updateClock() {
            const now = new Date();
            const timeString = now.toLocaleTimeString('pt-BR', {
                hour12: false,
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit'
            });
            
            const dateString = now.toLocaleDateString('pt-BR', {
                weekday: 'long',
                day: 'numeric',
                month: 'long'
            });
            
            const clockElement = document.getElementById('clock');
            const dateElement = document.getElementById('currentDate');
            
            if (clockElement) clockElement.textContent = timeString;
            if (dateElement) dateElement.textContent = dateString;
        }
        
        function detectLocation() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        document.getElementById('location').textContent = 'Confirmada';
                    },
                    () => {
                        document.getElementById('location').textContent = 'Não disponível';
                    }
                );
            } else {
                document.getElementById('location').textContent = 'Não suportada';
            }
        }
        
        function detectIP() {
            // Simulação de detecção de IP
            document.getElementById('userIP').textContent = '192.168.1.' + Math.floor(Math.random() * 255);
        }
        
        // Inicialização
        setInterval(updateClock, 1000);
        updateClock();
        
        // Salvar dados automaticamente
        window.addEventListener('beforeunload', () => {
            localStorage.setItem('funcionarios', JSON.stringify(funcionarios));
            localStorage.setItem('registrosPonto', JSON.stringify(registrosPonto));
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'96f3430f20bba672',t:'MTc1NTIwMzk3MC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
