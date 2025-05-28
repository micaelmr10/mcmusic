<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Melodia - Seu aplicativo de música</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #121212;
            color: #ffffff;
        }
        .sidebar {
            background-color: #000000;
        }
        .main-content {
            background: linear-gradient(180deg, #2D0B4F 0%, #121212 100%);
        }
        .card-musica:hover {
            transform: scale(1.05);
            transition: all 0.3s ease;
        }
        .player {
            background-color: #181818;
            border-top: 1px solid #282828;
        }
        .progresso-musica {
            -webkit-appearance: none;
            height: 4px;
            background: #4d4d4d;
            border-radius: 2px;
        }
        .progresso-musica::-webkit-slider-thumb {
            -webkit-appearance: none;
            width: 12px;
            height: 12px;
            background: #1db954;
            border-radius: 50%;
            cursor: pointer;
        }
        .btn-verde {
            background-color: #1db954;
        }
        .btn-verde:hover {
            background-color: #1ed760;
        }
        .texto-principal {
            color: #ffffff;
        }
        .texto-secundario {
            color: #b3b3b3;
        }
        .playlist-card {
            background: linear-gradient(149.46deg, #450af5, #8e8ee5 99.16%);
        }
    </style>
</head>
<body class="flex flex-col h-screen">
    <!-- Barra de navegação lateral -->
    <div class="flex flex-1 overflow-hidden">
        <div class="sidebar w-64 flex-shrink-0 hidden md:block p-6">
            <div class="mb-10">
                <h1 class="text-2xl font-bold texto-principal">Melodia</h1>
            </div>
            
            <nav>
                <ul class="space-y-4">
                    <li>
                        <a href="#" class="flex items-center space-x-3 texto-principal font-medium">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                            </svg>
                            <span>Início</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-3 texto-secundario hover:texto-principal">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                            </svg>
                            <span>Buscar</span>
                        </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-3 texto-secundario hover:texto-principal">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
                            </svg>
                            <span>Sua Biblioteca</span>
                        </a>
                    </li>
                </ul>
            </nav>
            
            <div class="mt-10">
                <h3 class="texto-secundario uppercase text-xs font-bold mb-4">Playlists</h3>
                <ul class="space-y-3" id="lista-playlists">
                    <!-- Playlists serão adicionadas dinamicamente aqui -->
                </ul>
                <button id="btn-nova-playlist" class="mt-4 flex items-center space-x-2 texto-secundario hover:texto-principal">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
                    </svg>
                    <span>Criar playlist</span>
                </button>
            </div>
        </div>
        
        <!-- Conteúdo principal -->
        <div class="main-content flex-1 overflow-y-auto p-6">
            <!-- Barra de busca -->
            <div class="flex justify-between items-center mb-8">
                <div class="relative w-full md:w-1/3">
                    <input type="text" id="campo-busca" placeholder="O que você quer ouvir?" class="w-full bg-white bg-opacity-10 rounded-full py-2 px-4 texto-principal placeholder:texto-secundario focus:outline-none focus:ring-2 focus:ring-green-500">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 absolute right-3 top-2.5 texto-secundario" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                    </svg>
                </div>
                <div class="hidden md:flex items-center space-x-4">
                    <span class="texto-principal font-medium">Bem-vindo, Usuário</span>
                    <div class="w-8 h-8 bg-purple-500 rounded-full flex items-center justify-center">
                        <span class="font-bold">U</span>
                    </div>
                </div>
            </div>
            
            <!-- Seção de playlists -->
            <div class="mb-10">
                <h2 class="text-2xl font-bold texto-principal mb-6">Suas playlists</h2>
                <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6" id="container-playlists">
                    <!-- Playlists serão adicionadas dinamicamente aqui -->
                </div>
            </div>
            
            <!-- Seção de músicas recomendadas -->
            <div class="mb-10">
                <h2 class="text-2xl font-bold texto-principal mb-6">Recomendadas para você</h2>
                <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6" id="container-musicas">
                    <!-- Músicas serão adicionadas dinamicamente aqui -->
                </div>
            </div>
            
            <!-- Seção de artistas populares -->
            <div>
                <h2 class="text-2xl font-bold texto-principal mb-6">Artistas populares</h2>
                <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-6" id="container-artistas">
                    <!-- Artistas serão adicionadas dinamicamente aqui -->
                </div>
            </div>
        </div>
    </div>
    
    <!-- Player de música -->
    <div class="player flex items-center justify-between px-4 py-3">
        <div class="flex items-center space-x-4 w-1/4">
            <img id="capa-musica-atual" src="https://via.placeholder.com/56" alt="Capa da música" class="w-14 h-14 rounded">
            <div>
                <p id="nome-musica-atual" class="texto-principal text-sm font-medium">Nenhuma música selecionada</p>
                <p id="artista-musica-atual" class="texto-secundario text-xs">Selecione uma música para começar</p>
            </div>
            <button class="texto-secundario hover:texto-principal">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd" />
                </svg>
            </button>
        </div>
        
        <div class="flex flex-col items-center w-2/4">
            <div class="flex items-center space-x-6 mb-2">
                <button class="texto-secundario hover:texto-principal">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" />
                    </svg>
                </button>
                <button id="btn-play" class="bg-white rounded-full p-2 hover:scale-105 transition-transform">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
                    </svg>
                </button>
                <button class="texto-secundario hover:texto-principal">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
                    </svg>
                </button>
            </div>
            <div class="w-full flex items-center space-x-3">
                <span class="text-xs texto-secundario" id="tempo-atual">0:00</span>
                <input type="range" min="0" max="100" value="0" class="progresso-musica w-full" id="barra-progresso">
                <span class="text-xs texto-secundario" id="tempo-total">0:30</span>
            </div>
        </div>
        
        <div class="flex items-center space-x-4 w-1/4 justify-end">
            <button class="texto-secundario hover:texto-principal">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M5 4a1 1 0 00-2 0v7.268a2 2 0 000 3.464V16a1 1 0 102 0v-1.268a2 2 0 000-3.464V4zM11 4a1 1 0 10-2 0v1.268a2 2 0 000 3.464V16a1 1 0 102 0V8.732a2 2 0 000-3.464V4zM16 3a1 1 0 011 1v7.268a2 2 0 010 3.464V16a1 1 0 11-2 0v-1.268a2 2 0 010-3.464V4a1 1 0 011-1z" />
                </svg>
            </button>
            <button class="texto-secundario hover:texto-principal">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path fill-rule="evenodd" d="M4 5a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V7a2 2 0 00-2-2h-1.586a1 1 0 01-.707-.293l-1.121-1.121A2 2 0 0011.172 3H8.828a2 2 0 00-1.414.586L6.293 4.707A1 1 0 015.586 5H4zm6 9a3 3 0 100-6 3 3 0 000 6z" clip-rule="evenodd" />
                </svg>
            </button>
            <div class="relative">
                <input type="range" min="0" max="100" value="80" class="w-24 h-1">
            </div>
        </div>
    </div>
    
    <!-- Modal para criar playlist -->
    <div id="modal-playlist" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 hidden">
        <div class="bg-gray-800 rounded-lg p-6 w-full max-w-md">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-bold texto-principal">Criar nova playlist</h3>
                <button id="fechar-modal" class="texto-secundario hover:texto-principal">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <input type="text" id="nome-playlist" placeholder="Nome da playlist" class="w-full bg-gray-700 rounded p-3 mb-4 texto-principal focus:outline-none focus:ring-2 focus:ring-green-500">
            <div class="flex justify-end space-x-3">
                <button id="cancelar-playlist" class="px-4 py-2 rounded-full texto-principal hover:bg-gray-700">Cancelar</button>
                <button id="salvar-playlist" class="px-4 py-2 rounded-full btn-verde texto-principal font-medium">Criar</button>
            </div>
        </div>
    </div>
    
    <!-- Modal para adicionar música à playlist -->
    <div id="modal-adicionar-playlist" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 hidden">
        <div class="bg-gray-800 rounded-lg p-6 w-full max-w-md">
            <div class="flex justify-between items-center mb-4">
                <h3 class="text-xl font-bold texto-principal">Adicionar à playlist</h3>
                <button id="fechar-modal-adicionar" class="texto-secundario hover:texto-principal">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                    </svg>
                </button>
            </div>
            <p id="musica-selecionada" class="texto-secundario mb-4">Selecione uma playlist:</p>
            <div id="lista-playlists-modal" class="mb-4 max-h-60 overflow-y-auto">
                <!-- Playlists para adicionar música serão listadas aqui -->
            </div>
            <div class="flex justify-end space-x-3">
                <button id="cancelar-adicionar" class="px-4 py-2 rounded-full texto-principal hover:bg-gray-700">Cancelar</button>
            </div>
        </div>
    </div>

    <script>
        // Dados iniciais do aplicativo
        const musicas = [
            { id: 1, nome: "Bohemian Rhapsody", artista: "Queen", duracao: "5:55", capa: "https://i.scdn.co/image/ab67616d00001e02e319baafd16e84f0408af2a0" },
            { id: 2, nome: "Imagine", artista: "John Lennon", duracao: "3:04", capa: "https://i.scdn.co/image/ab67616d00001e02b1c4b76e23414c9f20242268" },
            { id: 3, nome: "Billie Jean", artista: "Michael Jackson", duracao: "4:54", capa: "https://i.scdn.co/image/ab67616d00001e02e11a75a2f2ff39cec27a1d07" },
            { id: 4, nome: "Like a Rolling Stone", artista: "Bob Dylan", duracao: "6:13", capa: "https://i.scdn.co/image/ab67616d00001e02e8b907dcfb5e2c51785e7b03" },
            { id: 5, nome: "Smells Like Teen Spirit", artista: "Nirvana", duracao: "5:01", capa: "https://i.scdn.co/image/ab67616d00001e02d6fb1e2e2c2d4e9a3ca2f819" },
            { id: 6, nome: "One", artista: "U2", duracao: "4:36", capa: "https://i.scdn.co/image/ab67616d00001e02d29fe8c4ffa7e92ae56e38c2" },
            { id: 7, nome: "Yesterday", artista: "The Beatles", duracao: "2:05", capa: "https://i.scdn.co/image/ab67616d00001e02a4fce8b8352c7c0d19a10948" },
            { id: 8, nome: "Sweet Child O'Mine", artista: "Guns N' Roses", duracao: "5:56", capa: "https://i.scdn.co/image/ab67616d00001e02a4fce8b8352c7c0d19a10948" }
        ];

        const artistas = [
            { id: 1, nome: "Queen", foto: "https://i.scdn.co/image/ab67616100005174a1d2e2a6e481b34bb8e3a7e3" },
            { id: 2, nome: "The Beatles", foto: "https://i.scdn.co/image/ab67616100005174a1d2e2a6e481b34bb8e3a7e3" },
            { id: 3, nome: "Michael Jackson", foto: "https://i.scdn.co/image/ab67616100005174a1d2e2a6e481b34bb8e3a7e3" },
            { id: 4, nome: "Bob Dylan", foto: "https://i.scdn.co/image/ab67616100005174a1d2e2a6e481b34bb8e3a7e3" },
            { id: 5, nome: "Nirvana", foto: "https://i.scdn.co/image/ab67616100005174a1d2e2a6e481b34bb8e3a7e3" }
        ];

        let playlists = [
            { id: 1, nome: "Favoritas", musicas: [1, 3, 5] },
            { id: 2, nome: "Rock Clássico", musicas: [1, 4, 5, 8] }
        ];

        // Estado do aplicativo
        let estado = {
            musicaAtual: null,
            playlists: playlists,
            playlistsSidebar: playlists,
            playlistsModal: [],
            musicaParaAdicionar: null,
            isPlaying: false,
            progresso: 0,
            intervaloProgresso: null
        };

        // Elementos do DOM
        const elementos = {
            containerMusicas: document.getElementById('container-musicas'),
            containerArtistas: document.getElementById('container-artistas'),
            containerPlaylists: document.getElementById('container-playlists'),
            listaPlaylists: document.getElementById('lista-playlists'),
            listaPlaylistsModal: document.getElementById('lista-playlists-modal'),
            btnNovaPlaylist: document.getElementById('btn-nova-playlist'),
            modalPlaylist: document.getElementById('modal-playlist'),
            modalAdicionarPlaylist: document.getElementById('modal-adicionar-playlist'),
            nomePlaylist: document.getElementById('nome-playlist'),
            salvarPlaylist: document.getElementById('salvar-playlist'),
            cancelarPlaylist: document.getElementById('cancelar-playlist'),
            fecharModal: document.getElementById('fechar-modal'),
            fecharModalAdicionar: document.getElementById('fechar-modal-adicionar'),
            cancelarAdicionar: document.getElementById('cancelar-adicionar'),
            musicaSelecionada: document.getElementById('musica-selecionada'),
            campoBusca: document.getElementById('campo-busca'),
            nomeMusicaAtual: document.getElementById('nome-musica-atual'),
            artistaMusicaAtual: document.getElementById('artista-musica-atual'),
            capaMusicaAtual: document.getElementById('capa-musica-atual'),
            btnPlay: document.getElementById('btn-play'),
            barraProgresso: document.getElementById('barra-progresso'),
            tempoAtual: document.getElementById('tempo-atual'),
            tempoTotal: document.getElementById('tempo-total')
        };

        // Funções do aplicativo
        const funcoes = {
            renderizarMusicas: () => {
                elementos.containerMusicas.innerHTML = '';
                musicas.forEach(musica => {
                    const musicaElement = document.createElement('div');
                    musicaElement.className = 'card-musica bg-gray-800 p-4 rounded-lg cursor-pointer hover:bg-gray-700 transition-colors';
                    musicaElement.innerHTML = `
                        <div class="relative mb-4">
                            <img src="${musica.capa}" alt="${musica.nome}" class="w-full aspect-square object-cover rounded">
                            <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity play-btn" data-id="${musica.id}">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-black" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
                                </svg>
                            </button>
                            <button class="absolute top-2 right-2 bg-black bg-opacity-60 rounded-full p-1.5 adicionar-playlist-btn" data-id="${musica.id}">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
                                    <path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd" />
                                </svg>
                            </button>
                        </div>
                        <h3 class="texto-principal font-medium truncate">${musica.nome}</h3>
                        <p class="texto-secundario text-sm truncate">${musica.artista}</p>
                    `;
                    elementos.containerMusicas.appendChild(musicaElement);
                });
                
                // Adicionar eventos aos botões de play
                document.querySelectorAll('.play-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        const id = parseInt(btn.getAttribute('data-id'));
                        funcoes.tocarMusica(id);
                    });
                });
                
                // Adicionar eventos aos botões de adicionar à playlist
                document.querySelectorAll('.adicionar-playlist-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        e.stopPropagation();
                        const id = parseInt(btn.getAttribute('data-id'));
                        funcoes.abrirModalAdicionarPlaylist(id);
                    });
                });
                
                // Adicionar evento de clique nas músicas
                document.querySelectorAll('.card-musica').forEach(card => {
                    card.addEventListener('click', () => {
                        const id = parseInt(card.querySelector('.play-btn').getAttribute('data-id'));
                        funcoes.tocarMusica(id);
                    });
                });
            },
            
            renderizarArtistas: () => {
                elementos.containerArtistas.innerHTML = '';
                artistas.forEach(artista => {
                    const artistaElement = document.createElement('div');
                    artistaElement.className = 'bg-gray-800 p-4 rounded-full cursor-pointer hover:bg-gray-700 transition-colors text-center';
                    artistaElement.innerHTML = `
                        <div class="w-full aspect-square mb-3">
                            <img src="${artista.foto}" alt="${artista.nome}" class="w-full h-full rounded-full object-cover">
                        </div>
                        <h3 class="texto-principal font-medium">${artista.nome}</h3>
                        <p class="texto-secundario text-sm">Artista</p>
                    `;
                    elementos.containerArtistas.appendChild(artistaElement);
                });
            },
            
            renderizarPlaylists: () => {
                // Playlists na página principal
                elementos.containerPlaylists.innerHTML = '';
                estado.playlists.forEach(playlist => {
                    const playlistElement = document.createElement('div');
                    playlistElement.className = 'playlist-card p-4 rounded-lg cursor-pointer hover:opacity-90 transition-opacity';
                    playlistElement.innerHTML = `
                        <div class="mb-3">
                            <div class="w-full aspect-square bg-black bg-opacity-20 rounded flex items-center justify-center">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19V6l12-3v13M9 19c0 1.105-1.343 2-3 2s-3-.895-3-2 1.343-2 3-2 3 .895 3 2zm12-3c0 1.105-1.343 2-3 2s-3-.895-3-2 1.343-2 3-2 3 .895 3 2zM9 10l12-3" />
                                </svg>
                            </div>
                        </div>
                        <h3 class="texto-principal font-medium truncate">${playlist.nome}</h3>
                        <p class="texto-secundario text-sm">${playlist.musicas.length} músicas</p>
                    `;
                    elementos.containerPlaylists.appendChild(playlistElement);
                });
                
                // Playlists na sidebar
                elementos.listaPlaylists.innerHTML = '';
                estado.playlistsSidebar.forEach(playlist => {
                    const playlistElement = document.createElement('li');
                    playlistElement.className = 'texto-secundario hover:texto-principal cursor-pointer truncate';
                    playlistElement.textContent = playlist.nome;
                    elementos.listaPlaylists.appendChild(playlistElement);
                });
            },
            
            renderizarPlaylistsModal: () => {
                elementos.listaPlaylistsModal.innerHTML = '';
                estado.playlistsModal.forEach(playlist => {
                    const playlistElement = document.createElement('div');
                    playlistElement.className = 'flex items-center justify-between p-3 hover:bg-gray-700 rounded cursor-pointer';
                    playlistElement.innerHTML = `
                        <span class="texto-principal">${playlist.nome}</span>
                        <button class="adicionar-musica-btn px-3 py-1 bg-white bg-opacity-10 rounded-full texto-principal hover:bg-opacity-20" data-id="${playlist.id}">
                            Adicionar
                        </button>
                    `;
                    elementos.listaPlaylistsModal.appendChild(playlistElement);
                });
                
                // Adicionar eventos aos botões de adicionar música
                document.querySelectorAll('.adicionar-musica-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        const playlistId = parseInt(btn.getAttribute('data-id'));
                        funcoes.adicionarMusicaAPlaylist(playlistId, estado.musicaParaAdicionar);
                    });
                });
            },
            
            tocarMusica: (id) => {
                const musica = musicas.find(m => m.id === id);
                if (!musica) return;
                
                estado.musicaAtual = musica;
                estado.isPlaying = true;
                estado.progresso = 0;
                
                // Atualizar UI
                elementos.nomeMusicaAtual.textContent = musica.nome;
                elementos.artistaMusicaAtual.textContent = musica.artista;
                elementos.capaMusicaAtual.src = musica.capa;
                elementos.tempoTotal.textContent = musica.duracao;
                
                // Atualizar botão de play
                elementos.btnPlay.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zM7 8a1 1 0 012 0v4a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v4a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                    </svg>
                `;
                
                // Iniciar progresso da música
                if (estado.intervaloProgresso) {
                    clearInterval(estado.intervaloProgresso);
                }
                
                estado.intervaloProgresso = setInterval(() => {
                    if (estado.progresso >= 100) {
                        clearInterval(estado.intervaloProgresso);
                        return;
                    }
                    
                    estado.progresso += 0.5;
                    elementos.barraProgresso.value = estado.progresso;
                    
                    // Atualizar tempo atual (simulação)
                    const segundosTotais = 30; // Para simplificar, todas as músicas têm 30s
                    const segundosAtuais = Math.floor(segundosTotais * (estado.progresso / 100));
                    elementos.tempoAtual.textContent = `0:${segundosAtuais < 10 ? '0' + segundosAtuais : segundosAtuais}`;
                }, 1000);
            },
            
            pausarMusica: () => {
                estado.isPlaying = false;
                if (estado.intervaloProgresso) {
                    clearInterval(estado.intervaloProgresso);
                }
                
                // Atualizar botão de play
                elementos.btnPlay.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" viewBox="0 0 20 20" fill="currentColor">
                        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM9.555 7.168A1 1 0 008 8v4a1 1 0 001.555.832l3-2a1 1 0 000-1.664l-3-2z" clip-rule="evenodd" />
                    </svg>
                `;
            },
            
            abrirModalCriarPlaylist: () => {
                elementos.modalPlaylist.classList.remove('hidden');
                elementos.nomePlaylist.value = '';
            },
            
            fecharModalCriarPlaylist: () => {
                elementos.modalPlaylist.classList.add('hidden');
            },
            
            abrirModalAdicionarPlaylist: (musicaId) => {
                estado.musicaParaAdicionar = musicaId;
                estado.playlistsModal = [...estado.playlists];
                
                const musica = musicas.find(m => m.id === musicaId);
                elementos.musicaSelecionada.textContent = `Adicionar "${musica.nome}" à playlist:`;
                
                funcoes.renderizarPlaylistsModal();
                elementos.modalAdicionarPlaylist.classList.remove('hidden');
            },
            
            fecharModalAdicionarPlaylist: () => {
                elementos.modalAdicionarPlaylist.classList.add('hidden');
            },
            
            criarPlaylist: () => {
                const nome = elementos.nomePlaylist.value.trim();
                if (!nome) return;
                
                const novaPlaylist = {
                    id: estado.playlists.length + 1,
                    nome: nome,
                    musicas: []
                };
                
                estado.playlists.push(novaPlaylist);
                estado.playlistsSidebar.push(novaPlaylist);
                
                funcoes.renderizarPlaylists();
                funcoes.fecharModalCriarPlaylist();
            },
            
            adicionarMusicaAPlaylist: (playlistId, musicaId) => {
                const playlist = estado.playlists.find(p => p.id === playlistId);
                if (!playlist) return;
                
                if (!playlist.musicas.includes(musicaId)) {
                    playlist.musicas.push(musicaId);
                    
                    // Atualizar a exibição
                    funcoes.renderizarPlaylists();
                    funcoes.fecharModalAdicionarPlaylist();
                    
                    // Mostrar feedback visual
                    alert(`Música adicionada à playlist "${playlist.nome}"!`);
                } else {
                    alert('Esta música já está na playlist!');
                }
            },
            
            buscarMusicas: (termo) => {
                // Implementação simplificada de busca
                console.log('Buscando por:', termo);
                // Em uma implementação real, aqui você filtraria as músicas e atualizaria a UI
            },
            
            inicializar: () => {
                funcoes.renderizarMusicas();
                funcoes.renderizarArtistas();
                funcoes.renderizarPlaylists();
                
                // Event listeners
                elementos.btnNovaPlaylist.addEventListener('click', funcoes.abrirModalCriarPlaylist);
                elementos.fecharModal.addEventListener('click', funcoes.fecharModalCriarPlaylist);
                elementos.cancelarPlaylist.addEventListener('click', funcoes.fecharModalCriarPlaylist);
                elementos.salvarPlaylist.addEventListener('click', funcoes.criarPlaylist);
                elementos.fecharModalAdicionar.addEventListener('click', funcoes.fecharModalAdicionarPlaylist);
                elementos.cancelarAdicionar.addEventListener('click', funcoes.fecharModalAdicionarPlaylist);
                
                elementos.btnPlay.addEventListener('click', () => {
                    if (estado.isPlaying) {
                        funcoes.pausarMusica();
                    } else if (estado.musicaAtual) {
                        funcoes.tocarMusica(estado.musicaAtual.id);
                    }
                });
                
                elementos.campoBusca.addEventListener('input', (e) => {
                    funcoes.buscarMusicas(e.target.value);
                });
                
                // Permitir fechar modais com ESC
                document.addEventListener('keydown', (e) => {
                    if (e.key === 'Escape') {
                        funcoes.fecharModalCriarPlaylist();
                        funcoes.fecharModalAdicionarPlaylist();
                    }
                });
            }
        };

        // Inicializar o aplicativo
        document.addEventListener('DOMContentLoaded', funcoes.inicializar);
    </script>
</body>
</html>
