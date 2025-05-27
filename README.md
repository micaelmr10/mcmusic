<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MCMusic - Seu player de música</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #121212;
            color: white;
        }
        
        .progress-bar {
            -webkit-appearance: none;
            height: 4px;
            background: #535353;
            border-radius: 2px;
            overflow: hidden;
        }
        
        .progress-bar::-webkit-progress-bar {
            background-color: #535353;
        }
        
        .progress-bar::-webkit-progress-value {
            background-color: #1db954;
        }
        
        .volume-bar {
            -webkit-appearance: none;
            height: 4px;
            background: #535353;
            border-radius: 2px;
            overflow: hidden;
        }
        
        .volume-bar::-webkit-progress-bar {
            background-color: #535353;
        }
        
        .volume-bar::-webkit-progress-value {
            background-color: #1db954;
        }
        
        .song-item:hover {
            background-color: rgba(255, 255, 255, 0.1);
            transition: background-color 0.2s ease;
        }
        
        .playlist-card:hover {
            transform: scale(1.02);
            transition: transform 0.2s ease;
        }
        
        .blur-bg {
            background: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(10px);
        }
        
        .gradient-bg {
            background: linear-gradient(180deg, rgba(18,18,18,0.8) 0%, rgba(18,18,18,1) 100%);
        }
    </style>
</head>
<body class="h-screen flex flex-col">
    <!-- Main Container -->
    <div class="flex flex-1 overflow-hidden">
        <!-- Sidebar -->
        <div class="w-64 bg-black p-6 flex flex-col hidden md:flex">
            <div class="mb-8">
                <h1 class="text-2xl font-bold text-white flex items-center">
                    <i class="fas fa-music mr-2 text-green-500"></i> MCMusic
                </h1>
            </div>
            
            <nav class="mb-8">
                <ul class="space-y-4">
                    <li>
                        <a href="#" class="flex items-center text-white hover:text-green-500">
                            <i class="fas fa-home mr-4"></i> Início
                        </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center text-gray-400 hover:text-white">
                            <i class="fas fa-search mr-4"></i> Buscar
                        </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center text-gray-400 hover:text-white">
                            <i class="fas fa-book mr-4"></i> Sua Biblioteca
                        </a>
                    </li>
                </ul>
            </nav>
            
            <div class="mt-auto">
                <div class="bg-gray-800 p-4 rounded-lg">
                    <p class="text-sm text-gray-400 mb-2">Faça upgrade para o Premium</p>
                    <button class="bg-white text-black text-sm font-bold py-1 px-4 rounded-full hover:scale-105 transition-transform">
                        Upgrade
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Main Content -->
        <div class="flex-1 overflow-y-auto">
            <!-- Header -->
            <header class="sticky top-0 z-10 blur-bg p-4 flex justify-between items-center">
                <div class="flex items-center space-x-4">
                    <button class="rounded-full bg-black p-2 md:hidden">
                        <i class="fas fa-bars"></i>
                    </button>
                    <h2 class="text-xl font-bold">Bem-vindo de volta</h2>
                </div>
                <div class="flex items-center space-x-4">
                    <button class="rounded-full bg-black p-2">
                        <i class="fas fa-bell"></i>
                    </button>
                    <div class="flex items-center space-x-2">
                        <div class="w-8 h-8 rounded-full bg-green-500 flex items-center justify-center">
                            <span class="font-bold">MC</span>
                        </div>
                        <span class="hidden md:inline">Meu Perfil</span>
                    </div>
                </div>
            </header>
            
            <!-- Content -->
            <main class="p-6">
                <!-- Recently Played -->
                <section class="mb-8">
                    <h2 class="text-2xl font-bold mb-4">Tocados recentemente</h2>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-4">
                        <!-- Playlist Cards -->
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Hits do Momento</h3>
                            <p class="text-sm text-gray-400">As músicas mais tocadas agora</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Top Brasil</h3>
                            <p class="text-sm text-gray-400">As mais tocadas no Brasil</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Rock Classics</h3>
                            <p class="text-sm text-gray-400">As melhores do rock</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Sertanejo</h3>
                            <p class="text-sm text-gray-400">As melhores do sertanejo</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Funk Hits</h3>
                            <p class="text-sm text-gray-400">Os maiores hits do funk</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">MPB</h3>
                            <p class="text-sm text-gray-400">Música Popular Brasileira</p>
                        </div>
                    </div>
                </section>
                
                <!-- Your Playlists -->
                <section class="mb-8">
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-2xl font-bold">Suas playlists</h2>
                        <button class="text-gray-400 hover:text-white">Mostrar tudo</button>
                    </div>
                    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-4">
                        <!-- Playlist Cards -->
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Minhas Favoritas</h3>
                            <p class="text-sm text-gray-400">Por você</p>
                        </div>
                        
                        <div class="bg-gray-800 p-4 rounded-lg playlist-card cursor-pointer">
                            <div class="relative mb-4">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Playlist" class="w-full rounded">
                                <button class="absolute bottom-2 right-2 bg-green-500 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity">
                                    <i class="fas fa-play text-black"></i>
                                </button>
                            </div>
                            <h3 class="font-bold">Treino</h3>
                            <p class="text-sm text-gray-400">Para malhar</p>
                        </div>
                    </div>
                </section>
                
                <!-- Made For You -->
                <section>
                    <h2 class="text-2xl font-bold mb-4">Feito para você</h2>
                    <div class="bg-gradient-to-r from-purple-900 to-blue-900 rounded-lg p-6 mb-6">
                        <div class="flex flex-col md:flex-row items-center">
                            <div class="mb-4 md:mb-0 md:mr-6">
                                <img src="https://i.scdn.co/image/ab67706f00000002ca5a7517156021292e5663a6" alt="Daily Mix" class="w-40 h-40 rounded shadow-lg">
                            </div>
                            <div>
                                <p class="text-sm font-bold mb-2">PLAYLIST</p>
                                <h3 class="text-4xl font-bold mb-4">Daily Mix 1</h3>
                                <p class="text-gray-300 mb-4">Mistura perfeita de músicas que você ama e novas descobertas, atualizada diariamente.</p>
                                <div class="flex space-x-4">
                                    <button class="bg-green-500 text-black font-bold py-2 px-6 rounded-full hover:bg-green-400 transition-colors">
                                        <i class="fas fa-play mr-2"></i> Reproduzir
                                    </button>
                                    <button class="border border-gray-300 text-white font-bold py-2 px-6 rounded-full hover:border-white transition-colors">
                                        Seguir
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Songs List -->
                    <div class="bg-gray-800 bg-opacity-40 rounded-lg overflow-hidden">
                        <div class="p-4 border-b border-gray-700 hidden md:grid grid-cols-12 text-gray-400 text-sm">
                            <div class="col-span-1">#</div>
                            <div class="col-span-5">TÍTULO</div>
                            <div class="col-span-4">ÁLBUM</div>
                            <div class="col-span-2 text-right">DURAÇÃO</div>
                        </div>
                        
                        <!-- Song Items -->
                        <div class="song-item p-4 grid grid-cols-2 md:grid-cols-12 items-center border-b border-gray-700 cursor-pointer hover:bg-gray-700">
                            <div class="col-span-1 hidden md:block">1</div>
                            <div class="col-span-5 flex items-center">
                                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Song" class="w-10 h-10 mr-3">
                                <div>
                                    <p class="font-medium">Bohemian Rhapsody</p>
                                    <p class="text-sm text-gray-400">Queen</p>
                                </div>
                            </div>
                            <div class="col-span-4 hidden md:block">
                                <p class="text-gray-400">A Night at the Opera</p>
                            </div>
                            <div class="col-span-2 text-right">
                                <p class="text-gray-400">5:55</p>
                            </div>
                        </div>
                        
                        <div class="song-item p-4 grid grid-cols-2 md:grid-cols-12 items-center border-b border-gray-700 cursor-pointer hover:bg-gray-700">
                            <div class="col-span-1 hidden md:block">2</div>
                            <div class="col-span-5 flex items-center">
                                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Song" class="w-10 h-10 mr-3">
                                <div>
                                    <p class="font-medium">Sweet Child O' Mine</p>
                                    <p class="text-sm text-gray-400">Guns N' Roses</p>
                                </div>
                            </div>
                            <div class="col-span-4 hidden md:block">
                                <p class="text-gray-400">Appetite for Destruction</p>
                            </div>
                            <div class="col-span-2 text-right">
                                <p class="text-gray-400">5:56</p>
                            </div>
                        </div>
                        
                        <div class="song-item p-4 grid grid-cols-2 md:grid-cols-12 items-center border-b border-gray-700 cursor-pointer hover:bg-gray-700">
                            <div class="col-span-1 hidden md:block">3</div>
                            <div class="col-span-5 flex items-center">
                                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Song" class="w-10 h-10 mr-3">
                                <div>
                                    <p class="font-medium">Hotel California</p>
                                    <p class="text-sm text-gray-400">Eagles</p>
                                </div>
                            </div>
                            <div class="col-span-4 hidden md:block">
                                <p class="text-gray-400">Hotel California</p>
                            </div>
                            <div class="col-span-2 text-right">
                                <p class="text-gray-400">6:30</p>
                            </div>
                        </div>
                        
                        <div class="song-item p-4 grid grid-cols-2 md:grid-cols-12 items-center border-b border-gray-700 cursor-pointer hover:bg-gray-700">
                            <div class="col-span-1 hidden md:block">4</div>
                            <div class="col-span-5 flex items-center">
                                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Song" class="w-10 h-10 mr-3">
                                <div>
                                    <p class="font-medium">Stairway to Heaven</p>
                                    <p class="text-sm text-gray-400">Led Zeppelin</p>
                                </div>
                            </div>
                            <div class="col-span-4 hidden md:block">
                                <p class="text-gray-400">Led Zeppelin IV</p>
                            </div>
                            <div class="col-span-2 text-right">
                                <p class="text-gray-400">8:02</p>
                            </div>
                        </div>
                        
                        <div class="song-item p-4 grid grid-cols-2 md:grid-cols-12 items-center cursor-pointer hover:bg-gray-700">
                            <div class="col-span-1 hidden md:block">5</div>
                            <div class="col-span-5 flex items-center">
                                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Song" class="w-10 h-10 mr-3">
                                <div>
                                    <p class="font-medium">Smells Like Teen Spirit</p>
                                    <p class="text-sm text-gray-400">Nirvana</p>
                                </div>
                            </div>
                            <div class="col-span-4 hidden md:block">
                                <p class="text-gray-400">Nevermind</p>
                            </div>
                            <div class="col-span-2 text-right">
                                <p class="text-gray-400">5:01</p>
                            </div>
                        </div>
                    </div>
                </section>
            </main>
        </div>
    </div>
    
    <!-- Player Bar -->
    <div class="h-20 bg-gray-900 border-t border-gray-800 flex items-center px-4">
        <div class="w-full grid grid-cols-3 gap-4">
            <!-- Song Info -->
            <div class="flex items-center">
                <img src="https://i.scdn.co/image/ab67616d00001e02ff9ca10b55ce82ae553c8228" alt="Now Playing" class="w-14 h-14 mr-3">
                <div>
                    <p class="font-medium text-sm">Bohemian Rhapsody</p>
                    <p class="text-xs text-gray-400">Queen</p>
                </div>
                <button class="ml-4 text-gray-400 hover:text-white">
                    <i class="far fa-heart"></i>
                </button>
            </div>
            
            <!-- Player Controls -->
            <div class="flex flex-col items-center justify-center">
                <div class="flex items-center space-x-4 mb-2">
                    <button class="text-gray-400 hover:text-white">
                        <i class="fas fa-random"></i>
                    </button>
                    <button class="text-gray-400 hover:text-white">
                        <i class="fas fa-step-backward"></i>
                    </button>
                    <button class="bg-white rounded-full w-8 h-8 flex items-center justify-center hover:scale-105 transition-transform">
                        <i class="fas fa-play text-black"></i>
                    </button>
                    <button class="text-gray-400 hover:text-white">
                        <i class="fas fa-step-forward"></i>
                    </button>
                    <button class="text-gray-400 hover:text-white">
                        <i class="fas fa-redo"></i>
                    </button>
                </div>
                <div class="w-full flex items-center space-x-2">
                    <span class="text-xs text-gray-400">2:34</span>
                    <progress class="progress-bar w-full" value="45" max="100"></progress>
                    <span class="text-xs text-gray-400">5:55</span>
                </div>
            </div>
            
            <!-- Volume Controls -->
            <div class="flex items-center justify-end space-x-2">
                <button class="text-gray-400 hover:text-white">
                    <i class="fas fa-list-ul"></i>
                </button>
                <button class="text-gray-400 hover:text-white">
                    <i class="fas fa-laptop"></i>
                </button>
                <button class="text-gray-400 hover:text-white">
                    <i class="fas fa-volume-up"></i>
                </button>
                <progress class="volume-bar w-24" value="70" max="100"></progress>
            </div>
        </div>
    </div>

    <script>
        // Player functionality
        document.addEventListener('DOMContentLoaded', function() {
            const playButtons = document.querySelectorAll('.play-button, .song-item');
            const mainPlayButton = document.querySelector('.player-bar .fa-play').parentElement;
            let isPlaying = false;
            
            // Play button functionality
            playButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const songItem = this.closest('.song-item');
                    if (songItem) {
                        const songTitle = songItem.querySelector('p.font-medium').textContent;
                        const artist = songItem.querySelector('p.text-gray-400').textContent;
                        
                        // Update player bar
                        document.querySelector('.player-bar p.font-medium').textContent = songTitle;
                        document.querySelector('.player-bar p.text-gray-400').textContent = artist;
                    }
                    
                    // Toggle play state
                    isPlaying = !isPlaying;
                    const playIcon = mainPlayButton.querySelector('i');
                    playIcon.classList.toggle('fa-play', !isPlaying);
                    playIcon.classList.toggle('fa-pause', isPlaying);
                    
                    // Update progress bar animation
                    if (isPlaying) {
                        animateProgressBar();
                    }
                });
            });
            
            // Progress bar animation
            function animateProgressBar() {
                const progressBar = document.querySelector('.progress-bar');
                let progress = parseInt(progressBar.value);
                const max = parseInt(progressBar.max);
                
                const interval = setInterval(() => {
                    if (!isPlaying) {
                        clearInterval(interval);
                        return;
                    }
                    
                    progress += 1;
                    progressBar.value = progress;
                    
                    if (progress >= max) {
                        clearInterval(interval);
                        isPlaying = false;
                        const playIcon = mainPlayButton.querySelector('i');
                        playIcon.classList.toggle('fa-play', !isPlaying);
                        playIcon.classList.toggle('fa-pause', isPlaying);
                    }
                }, 1000);
            }
            
            // Volume control
            const volumeBar = document.querySelector('.volume-bar');
            const volumeIcon = document.querySelector('.fa-volume-up');
            
            volumeBar.addEventListener('input', function() {
                const volume = this.value;
                
                if (volume > 50) {
                    volumeIcon.className = 'fas fa-volume-up';
                } else if (volume > 0) {
                    volumeIcon.className = 'fas fa-volume-down';
                } else {
                    volumeIcon.className = 'fas fa-volume-mute';
                }
            });
            
            // Mobile menu toggle
            const mobileMenuButton = document.querySelector('.md\\:hidden button');
            const sidebar = document.querySelector('.bg-black');
            
            if (mobileMenuButton && sidebar) {
                mobileMenuButton.addEventListener('click', function() {
                    sidebar.classList.toggle('hidden');
                });
            }
        });
    </script>
</body>
</html>
