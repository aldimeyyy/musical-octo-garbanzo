1. - ```
     index.html
     ```
To implement these changes on GitHub:
1. Copy the complete HTML from my previous response
2. Apply these diffs to update the images and audio
3. Save as `index.html` in your GitHub repository
4. Upload your `happy-birthday.mp3` file to the same directory

Would you like me to show the changes for the other puzzle images as well?Here is the updated HTML content after applying above edits:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Selamat Ulang Tahun Sabrina Azizah!</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #fff5f7;
            color: #333;
            transition: all 0.3s ease;
        }
        
        .puzzle-container {
            perspective: 1000px;
        }
        
        .puzzle-piece {
            transition: transform 0.5s, box-shadow 0.3s;
            transform-style: preserve-3d;
        }
        
        .puzzle-piece:hover {
            transform: scale(1.05) rotateY(10deg);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        
        .message-box {
            background: linear-gradient(135deg, #f9f0ff 0%, #e6f9ff 100%);
            border-left: 5px solid #a78bfa;
        }
        
        .hidden {
            display: none;
        }
        
        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-15px); }
            100% { transform: translateY(0px); }
        }
        
        .floating {
            animation: float 3s ease-in-out infinite;
        }
        
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f00;
            opacity: 0;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col items-center justify-center p-4">
    <div class="max-w-4xl w-full text-center">
        <h1 class="text-4xl md:text-5xl font-bold text-purple-600 mb-8">Teka-Teki Ulang Tahun</h1>
        
        <div id="game-intro" class="mb-12">
            <div class="floating mb-8">
                <img src="https://placehold.co/600x400/pink/white?text=Happy+Birthday+Sabrina" alt="Kartun hewan lucu sedang memegang balon ulang tahun" class="rounded-lg mx-auto" />
            </div>
            <p class="text-lg mb-6">Selamat datang di permainan teka-teki spesial untuk merayakan ulang tahun Sabrina Azizah!</p>
            <button onclick="startGame()" class="bg-purple-500 hover:bg-purple-600 text-white font-bold py-3 px-6 rounded-full text-lg transition-all transform hover:scale-105">
                Mulai Permainan
            </button>
        </div>
        
        <div id="game-container" class="hidden">
            <div class="puzzle-container grid grid-cols-2 md:grid-cols-3 gap-4 mb-8">
                <!-- Puzzle pieces will be inserted here -->
            </div>
            
            <div id="progress" class="bg-gray-200 rounded-full h-4 mb-6">
                <div id="progress-bar" class="bg-purple-500 h-4 rounded-full" style="width: 0%"></div>
            </div>
            
            <p id="hint" class="text-lg font-semibold mb-4">Tekateki 1: Hewan apa yang suka makan wortel dan melompat-lompat?</p>
        </div>
        
        <div id="completion-message" class="hidden">
            <div class="message-box p-8 rounded-lg shadow-lg mb-8">
                <h2 class="text-3xl font-bold text-purple-700 mb-6">Barakallah fi umrik Sabrina Azizah!</h2>
                
                <div class="mb-6">
                    <img src="https://placehold.co/600x400/pink/white?text=Barakallah+Fi+Umrik" alt="Ucapan ulang tahun islami dengan kaligrafi arab" class="rounded-lg mx-auto" />
                </div>
                
                <p class="text-lg mb-4">Maaf ya aku masih banyak kekurangan.</p>
                <p class="text-lg mb-6">Semoga di kemudian hari kita bisa saling melengkapi kekurangan masing-masing.</p>
                
                <p class="text-lg italic">Dan semoga kamu ga cuek, kesel, dan cuek lagi wleee~</p>
                
                <button id="playMusic" class="mt-8 bg-pink-500 hover:bg-pink-600 text-white font-bold py-3 px-6 rounded-full flex items-center mx-auto">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z" />
                    </svg>
                    Putar Lagu Selamat Ulang Tahun
                </button>
            </div>
        </div>
    </div>
    
    <audio id="birthdaySong" src="happy-birthday.mp3" preload="auto"></audio>
    <!-- Upload file happy-birthday.mp3 ke direktori yang sama -->
    
    <script>
        // Game state
        const gameState = {
            currentPuzzle: 0,
            completedPuzzles: 0,
            puzzles: [
                {
                    question: "Hewan apa yang suka makan wortel dan melompat-lompat?",
                    answer: "kelinci",
                    image: "https://placehold.co/300x200/ffc0cb/white?text=Kelinci&font=poppins"
                },
                {
                    question: "Hewan apa yang punya cangkang, jalan pelan, dan suka bawa rumahnya?",
                    answer: "kura-kura",
                    image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/1e1d4c93-0b57-4491-86a3-efb604a9ccbe.png"
                },
                {
                    question: "Hewan apa yang punya leher panjang dan suka makan daun?",
                    answer: "jerapah",
                    image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/25975efc-b553-45fc-b21b-01632abbab2a.png"
                },
                {
                    question: "Hewan apa yang berwarna hitam putih dan berasal dari China?",
                    answer: "panda",
                    image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/f5d5124d-19b4-4ec9-8877-ca48e8e2fa36.png"
                },
                {
                    question: "Hewan apa yang suka berenang dan mengeluarkan suara 'quack'?",
                    answer: "bebek",
                    image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b271dc66-fe32-48ed-ba2c-6747aa9f2e41.png"
                }
            ]
        };
        
        // DOM elements
        const gameIntro = document.getElementById('game-intro');
        const gameContainer = document.getElementById('game-container');
        const completionMessage = document.getElementById('completion-message');
        const puzzleContainer = document.querySelector('.puzzle-container');
        const hintElement = document.getElementById('hint');
        const progressBar = document.getElementById('progress-bar');
        const playMusicBtn = document.getElementById('playMusic');
        const birthdaySong = document.getElementById('birthdaySong');
        
        // Initialize the game
        function startGame() {
            gameIntro.classList.add('hidden');
            gameContainer.classList.remove('hidden');
            loadPuzzle(gameState.currentPuzzle);
            updateProgress();
        }
        
        // Load puzzle elements
        function loadPuzzle(index) {
            puzzleContainer.innerHTML = '';
            const puzzle = gameState.puzzles[index];
            
            hintElement.textContent = `Tekateki ${index + 1}: ${puzzle.question}`;
            
            // Create puzzle pieces (scrambled)
            const pieces = [
                {text: puzzle.answer.slice(0, Math.floor(puzzle.answer.length/2)), isCorrect: false},
                {text: puzzle.answer.slice(Math.floor(puzzle.answer.length/2)), isCorrect: false},
                {text: "❓", isCorrect: false},
                {text: "❓", isCorrect: false},
                {text: "❓", isCorrect: false},
                {text: "❓", isCorrect: false}
            ];
            
            // Randomly set one piece to be correct
            const correctIndex = Math.floor(Math.random() * pieces.length);
            pieces[correctIndex].isCorrect = true;
            pieces[correctIndex].text = puzzle.answer;
            
            // Shuffle pieces
            pieces.sort(() => Math.random() - 0.5);
            
            // Create puzzle piece elements
            pieces.forEach((piece, i) => {
                const pieceElement = document.createElement('div');
                pieceElement.className = 'puzzle-piece bg-white rounded-lg p-6 flex items-center justify-center text-2xl font-bold cursor-pointer shadow-md hover:shadow-lg';
                
                if (piece.isCorrect) {
                    pieceElement.classList.add('bg-purple-100');
                    pieceElement.textContent = piece.text;
                    pieceElement.addEventListener('click', () => correctPieceSelected(pieceElement));
                } else {
                    pieceElement.textContent = piece.text;
                    pieceElement.addEventListener('click', () => wrongPieceSelected(pieceElement));
                }
                
                puzzleContainer.appendChild(pieceElement);
            });
        }
        
        // Handle correct piece selection
        function correctPieceSelected(piece) {
            piece.classList.remove('bg-purple-100');
            piece.classList.add('bg-green-100', 'border-2', 'border-green-400');
            
            setTimeout(() => {
                piece.classList.add('transform', 'scale-0');
                
                setTimeout(() => {
                    gameState.completedPuzzles++;
                    updateProgress();
                    
                    if (gameState.currentPuzzle < gameState.puzzles.length - 1) {
                        gameState.currentPuzzle++;
                        loadPuzzle(gameState.currentPuzzle);
                    } else {
                        completeGame();
                    }
                }, 500);
            }, 800);
        }
        
        // Handle wrong piece selection
        function wrongPieceSelected(piece) {
            piece.classList.add('bg-red-100', 'border-2', 'border-red-400', 'animate-pulse');
            
            setTimeout(() => {
                piece.classList.remove('bg-red-100', 'border-2', 'border-red-400', 'animate-pulse');
            }, 1000);
        }
        
        // Update progress bar
        function updateProgress() {
            const progress = (gameState.completedPuzzles / gameState.puzzles.length) * 100;
            progressBar.style.width = `${progress}%`;
        }
        
        // Complete the game
        function completeGame() {
            gameContainer.classList.add('hidden');
            completionMessage.classList.remove('hidden');
            createConfetti();
        }
        
        // Create confetti effect
        function createConfetti() {
            const colors = ['#ef4444', '#f97316', '#f59e0b', '#84cc16', '#10b981', '#06b6d4', '#3b82f6', '#8b5cf6', '#ec4899'];
            
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.transform = `rotate(${Math.random() * 360}deg)`;
                
                document.body.appendChild(confetti);
                
                // Animate confetti
                const animation = confetti.animate(
                    [
                        { 
                            transform: `translate(0, 0) rotate(0)`, 
                            opacity: 1 
                        },
                        { 
                            transform: `translate(${Math.random() * 200 - 100}px, ${window.innerHeight}px) rotate(${Math.random() * 360}deg)`, 
                            opacity: 0 
                        }
                    ],
                    {
                        duration: 3000 + Math.random() * 3000,
                        easing: 'cubic-bezier(0.1, 0.2, 0.8, 1)'
                    }
                );
                
                animation.onfinish = () => confetti.remove();
            }
        }
        
        // Play birthday song
        playMusicBtn.addEventListener('click', function() {
            if (birthdaySong.paused) {
                birthdaySong.play();
                playMusicBtn.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h14M5 12a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v4a2 2 0 01-2 2M5 12a2 2 0 00-2 2v4a2 2 0 002 2h14a2 2 0 002-2v-4a2 2 0 00-2-2m-2-4h.01M17 16h.01" />
                    </svg>
                    Jeda Lagu
                `;
            } else {
                birthdaySong.pause();
                playMusicBtn.innerHTML = `
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 mr-2" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.536 8.464a5 5 0 010 7.072m2.828-9.9a9 9 0 010 12.728M5.586 15H4a1 1 0 01-1-1v-4a1 1 0 011-1h1.586l4.707-4.707C10.923 3.663 12 4.109 12 5v14c0 .891-1.077 1.337-1.707.707L5.586 15z" />
                    </svg>
                    Putar Lagu Selamat Ulang Tahun
                `;
            }
        });
    </script>
</body>
</html>
