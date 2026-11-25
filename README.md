
```html
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>फेलवा (Felva)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
    <!-- Google Fonts: Noto Sans Devanagari & Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Noto+Sans+Devanagari:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Noto Sans Devanagari', 'Inter', sans-serif;
            background-color: #f0f2f5;
            -webkit-tap-highlight-color: transparent;
            user-select: none;
        }
        /* Hide scrollbars for horizontal story list */
        .no-scrollbar::-webkit-scrollbar {
            display: none;
        }
        .no-scrollbar {
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
        .animate-pop {
            animation: pop 0.25s ease-in-out;
        }
    </style>
</head>
<body class="bg-[#f0f2f5] text-gray-900 pb-16">

    <!-- Top App Header -->
    <header class="sticky top-0 z-40 bg-white shadow-sm">
        <div class="max-w-md mx-auto px-4 pt-3 pb-2 flex items-center justify-between">
            <div class="flex items-center space-x-2">
                <div class="w-9 h-9 rounded-full bg-[#1877F2] flex items-center justify-center text-white font-bold text-xl shadow-sm">
                    फे
                </div>
                <h1 class="text-2xl font-bold text-[#1877F2] tracking-tight">फेलवा</h1>
            </div>
            <div class="flex items-center space-x-2.5">
                <button onclick="openCreateModal()" class="w-9 h-9 rounded-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-gray-800 transition" title="नई पोस्ट">
                    <i class="fa-solid fa-plus text-lg"></i>
                </button>
                <button onclick="toggleSearch()" class="w-9 h-9 rounded-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-gray-800 transition" title="खोजें">
                    <i class="fa-solid fa-magnifying-glass text-base"></i>
                </button>
                <button onclick="showToast('मैसेज बॉक्स जल्द ही आ रहा है!')" class="w-9 h-9 rounded-full bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-gray-800 transition relative" title="मैसेज">
                    <i class="fa-brands fa-facebook-messenger text-lg"></i>
                    <span class="absolute -top-0.5 -right-0.5 w-4 h-4 bg-red-500 text-white text-[10px] font-bold rounded-full flex items-center justify-center">2</span>
                </button>
            </div>
        </div>

        <!-- Search Bar (Hidden by default) -->
        <div id="searchBar" class="hidden max-w-md mx-auto px-4 pb-2.5">
            <div class="relative">
                <input type="text" id="searchInput" oninput="filterPosts()" placeholder="फेलवा पर पोस्ट या दोस्त खोजें..." class="w-full bg-[#f0f2f5] text-sm rounded-full py-2 pl-9 pr-4 focus:outline-none focus:ring-2 focus:ring-[#1877F2]">
                <i class="fa-solid fa-magnifying-glass absolute left-3.5 top-2.5 text-gray-400 text-sm"></i>
            </div>
        </div>

        <!-- Top Navigation Tabs -->
        <nav class="max-w-md mx-auto flex border-t border-gray-100">
            <button onclick="switchTab('home')" id="tab-home" class="flex-1 py-2.5 flex justify-center items-center text-[#1877F2] border-b-[3px] border-[#1877F2] transition">
                <i class="fa-solid fa-house text-xl"></i>
            </button>
            <button onclick="switchTab('friends')" id="tab-friends" class="flex-1 py-2.5 flex justify-center items-center text-gray-500 border-b-[3px] border-transparent transition relative">
                <i class="fa-solid fa-user-group text-xl"></i>
                <span id="friendBadge" class="ml-1 bg-red-500 text-white text-[10px] font-bold px-1.5 py-0.2 rounded-full">3</span>
            </button>
            <button onclick="switchTab('notifications')" id="tab-notifications" class="flex-1 py-2.5 flex justify-center items-center text-gray-500 border-b-[3px] border-transparent transition relative">
                <i class="fa-solid fa-bell text-xl"></i>
                <span id="notifBadge" class="ml-1 bg-red-500 text-white text-[10px] font-bold px-1.5 py-0.2 rounded-full">4</span>
            </button>
            <button onclick="switchTab('profile')" id="tab-profile" class="flex-1 py-2.5 flex justify-center items-center text-gray-500 border-b-[3px] border-transparent transition">
                <i class="fa-solid fa-circle-user text-xl"></i>
            </button>
        </nav>
    </header>

    <!-- Main Content Container -->
    <main class="max-w-md mx-auto">

        <!-- ================= TAB 1: HOME FEED ================= -->
        <div id="view-home" class="space-y-2.5">
            
            <!-- Create Post Box -->
            <div class="bg-white p-3.5 shadow-sm">
                <div class="flex items-center space-x-2.5">
                    <img src="https://placehold.co/100x100/1877F2/ffffff?text=आप" alt="प्रोफाइल" class="w-10 h-10 rounded-full object-cover border border-gray-200">
                    <button onclick="openCreateModal()" class="flex-1 text-left bg-[#f0f2f5] hover:bg-gray-200 text-gray-600 text-sm py-2.5 px-4 rounded-full transition">
                        क्या सोच रहे हैं? कुछ लिखें...
                    </button>
                    <button onclick="openCreateModal(true)" class="p-2 text-green-600 hover:bg-green-50 rounded-full transition" title="फोटो जोड़ें">
                        <i class="fa-regular fa-images text-xl"></i>
                    </button>
                </div>
                <div class="grid grid-cols-3 border-t border-gray-100 mt-3 pt-2 text-xs font-semibold text-gray-600">
                    <button onclick="openCreateModal(false)" class="flex items-center justify-center space-x-1.5 py-1 hover:bg-gray-50 rounded-lg">
                        <i class="fa-solid fa-pen-to-square text-blue-500 text-sm"></i>
                        <span>स्टेटस</span>
                    </button>
                    <button onclick="openCreateModal(true)" class="flex items-center justify-center space-x-1.5 py-1 hover:bg-gray-50 rounded-lg border-x border-gray-100">
                        <i class="fa-solid fa-image text-green-500 text-sm"></i>
                        <span>फोटो</span>
                    </button>
                    <button onclick="openCreateModal(false, '😊 खुश महसूस कर रहे हैं')" class="flex items-center justify-center space-x-1.5 py-1 hover:bg-gray-50 rounded-lg">
                        <i class="fa-regular fa-face-smile text-yellow-500 text-sm"></i>
                        <span>फीलिंग</span>
                    </button>
                </div>
            </div>

            <!-- Stories Section -->
            <div class="bg-white py-3 pl-3.5 shadow-sm">
                <div class="flex space-x-2.5 overflow-x-auto no-scrollbar pr-3.5" id="storiesContainer">
                    <!-- Add Story Card -->
                    <div onclick="openStoryModal()" class="flex-shrink-0 w-24 h-40 rounded-xl overflow-hidden border border-gray-200 relative cursor-pointer bg-white shadow-xs group">
                        <img src="https://placehold.co/150x200/1877F2/ffffff?text=आपकी+फोटो" alt="स्टोरी" class="w-full h-28 object-cover group-hover:scale-105 transition">
                        <div class="absolute top-24 left-1/2 -translate-x-1/2 -translate-y-1/2 w-8 h-8 rounded-full bg-[#1877F2] border-2 border-white flex items-center justify-center text-white shadow">
                            <i class="fa-solid fa-plus text-sm"></i>
                        </div>
                        <div class="pt-4 px-1 text-center">
                            <p class="text-[11px] font-semibold text-gray-800 leading-tight">स्टोरी बनाएं</p>
                        </div>
                    </div>
                    <!-- Dynamic Stories injected by JS -->
                </div>
            </div>

            <!-- News Feed Posts Container -->
            <div id="feedContainer" class="space-y-2.5">
                <!-- Posts injected by JS -->
            </div>
        </div>

        <!-- ================= TAB 2: FRIENDS & REQUESTS ================= -->
        <div id="view-friends" class="hidden bg-white min-h-screen p-4 space-y-4">
            <div class="flex items-center justify-between">
                <h2 class="text-xl font-bold text-gray-900">दोस्त और रिक्वेस्ट</h2>
                <span class="text-xs font-semibold bg-blue-50 text-[#1877F2] px-2.5 py-1 rounded-full">फेलवा कम्युनिटी</span>
            </div>

            <!-- Friend Requests -->
            <div>
                <h3 class="text-sm font-bold text-gray-700 mb-3">फ्रेंड रिक्वेस्ट (<span id="reqCount">3</span>)</h3>
                <div id="friendRequestsList" class="space-y-3">
                    <!-- Injected via JS -->
                </div>
            </div>

            <hr class="border-gray-100">

            <!-- People You May Know -->
            <div>
                <h3 class="text-sm font-bold text-gray-700 mb-3">जिन्हें आप जानते होंगे</h3>
                <div id="suggestedFriendsList" class="space-y-3">
                    <!-- Injected via JS -->
                </div>
            </div>
        </div>

        <!-- ================= TAB 3: NOTIFICATIONS ================= -->
        <div id="view-notifications" class="hidden bg-white min-h-screen p-4 space-y-3">
            <div class="flex items-center justify-between mb-2">
                <h2 class="text-xl font-bold text-gray-900">नोटिफिकेशन</h2>
                <button onclick="markAllRead()" class="text-xs font-semibold text-[#1877F2] hover:underline">सभी पढ़ा हुआ मानें</button>
            </div>
            <div id="notificationsList" class="space-y-2">
                <!-- Injected via JS -->
            </div>
        </div>

        <!-- ================= TAB 4: PROFILE ================= -->
        <div id="view-profile" class="hidden bg-[#f0f2f5] min-h-screen space-y-2.5">
            <div class="bg-white pb-4 shadow-sm">
                <!-- Cover Photo -->
                <div class="h-36 bg-gradient-to-r from-[#1877F2] via-blue-500 to-indigo-600 relative">
                    <span class="absolute bottom-2 right-3 bg-black/40 text-white text-[10px] px-2 py-0.5 rounded-full">फेलवा क्रिएटर</span>
                </div>
                <!-- Profile Info -->
                <div class="px-4 relative">
                    <div class="-mt-12 mb-2 flex justify-between items-end">
                        <img src="https://placehold.co/150x150/1877F2/ffffff?text=क्रिएटर" alt="प्रोफाइल फोटो" class="w-24 h-24 rounded-full border-4 border-white shadow-md object-cover bg-white">
                        <button onclick="openCreateModal()" class="bg-[#1877F2] text-white text-xs font-semibold px-4 py-2 rounded-lg shadow-xs hover:bg-blue-600 transition">
                            <i class="fa-solid fa-plus mr-1"></i> स्टोरी / पोस्ट जोड़ें
                        </button>
                    </div>
                    <h2 class="text-xl font-bold text-gray-900">फेलवा यूज़र (क्रिएटर)</h2>
                    <p class="text-xs text-gray-500 mt-0.5">नए दोस्तों से जुड़ें और अपने विचार साझा करें। 🇮🇳</p>
                    
                    <!-- Stats -->
                    <div class="grid grid-cols-3 gap-2 mt-4 bg-[#f0f2f5] p-2.5 rounded-xl text-center">
                        <div>
                            <p id="statPosts" class="text-base font-bold text-gray-900">0</p>
                            <p class="text-[11px] text-gray-500">आपकी पोस्ट</p>
                        </div>
                        <div class="border-x border-gray-300">
                            <p id="statFriends" class="text-base font-bold text-gray-900">128</p>
                            <p class="text-[11px] text-gray-500">दोस्त</p>
                        </div>
                        <div>
                            <p id="statLikes" class="text-base font-bold text-gray-900">0</p>
                            <p class="text-[11px] text-gray-500">कुल लाइक्स</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- User's Own Posts -->
            <div class="px-3 pt-1">
                <h3 class="text-sm font-bold text-gray-700 mb-2">आपकी टाइमलाइन पोस्ट</h3>
                <div id="userPostsContainer" class="space-y-2.5">
                    <!-- User posts filtered here -->
                </div>
            </div>
        </div>

    </main>

    <!-- ================= MODAL: CREATE POST ================= -->
    <div id="createPostModal" class="fixed inset-0 z-50 bg-black/60 hidden flex items-end sm:items-center justify-center p-0 sm:p-4">
        <div class="bg-white w-full max-w-md rounded-t-2xl sm:rounded-2xl shadow-xl overflow-hidden animate-slide-up">
            <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
                <h3 class="font-bold text-gray-800 text-base">पोस्ट बनाएं</h3>
                <button onclick="closeCreateModal()" class="w-8 h-8 rounded-full bg-gray-100 flex items-center justify-center text-gray-600">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div class="p-4 space-y-3">
                <div class="flex items-center space-x-2.5">
                    <img src="https://placehold.co/100x100/1877F2/ffffff?text=आप" class="w-10 h-10 rounded-full">
                    <div>
                        <p class="text-sm font-bold text-gray-800">फेलवा यूज़र</p>
                        <span class="inline-flex items-center text-[11px] bg-gray-100 text-gray-600 px-2 py-0.5 rounded-md">
                            <i class="fa-solid fa-earth-asia mr-1 text-[10px]"></i> पब्लिक
                        </span>
                    </div>
                </div>

                <textarea id="postTextInput" rows="4" placeholder="आप क्या सोच रहे हैं? यहाँ लिखें..." class="w-full text-base text-gray-800 placeholder-gray-400 focus:outline-none resize-none"></textarea>

                <!-- Optional Photo Selector -->
                <div id="photoInputBox" class="hidden space-y-2 bg-gray-50 p-3 rounded-xl border border-gray-200">
                    <label class="block text-xs font-semibold text-gray-700">फोटो चुनें (गैलरी से या तैयार थीम):</label>
                    <input type="file" id="imageFileInput" accept="image/*" onchange="previewSelectedImage(event)" class="block w-full text-xs text-gray-500 file:mr-3 file:py-1.5 file:px-3 file:rounded-full file:border-0 file:text-xs file:font-semibold file:bg-blue-50 file:text-[#1877F2] hover:file:bg-blue-100">
                    
                    <div class="flex space-x-2 pt-1 overflow-x-auto no-scrollbar">
                        <button type="button" onclick="selectPresetImage('https://placehold.co/600x400/2563eb/ffffff?text=सुप्रभात+दोस्तो!+☀️')" class="flex-shrink-0 text-[11px] bg-blue-100 text-blue-800 px-2.5 py-1 rounded-lg font-medium">☀️ सुप्रभात कार्ड</button>
                        <button type="button" onclick="selectPresetImage('https://placehold.co/600x400/16a34a/ffffff?text=खूबसूरत+भारत+🇮🇳')" class="flex-shrink-0 text-[11px] bg-green-100 text-green-800 px-2.5 py-1 rounded-lg font-medium">🇮🇳 प्रकृति कार्ड</button>
                        <button type="button" onclick="selectPresetImage('https://placehold.co/600x400/ea580c/ffffff?text=चाय+और+चर्चा+☕')" class="flex-shrink-0 text-[11px] bg-orange-100 text-orange-800 px-2.5 py-1 rounded-lg font-medium">☕ चाय कार्ड</button>
                    </div>
                    <img id="postImagePreview" src="" alt="प्रीव्यू" class="hidden w-full h-40 object-cover rounded-lg mt-2 border border-gray-200">
                </div>

                <div class="flex items-center justify-between border border-gray-200 rounded-xl px-3 py-2">
                    <span class="text-xs font-semibold text-gray-600">अपनी पोस्ट में जोड़ें</span>
                    <div class="flex space-x-3">
                        <button type="button" onclick="togglePhotoBox()" class="text-green-600 hover:scale-110 transition" title="फोटो">
                            <i class="fa-solid fa-image text-lg"></i>
                        </button>
                        <button type="button" onclick="appendEmoji('❤️')" class="text-red-500 hover:scale-110 transition">❤️</button>
                        <button type="button" onclick="appendEmoji('😂')" class="text-yellow-500 hover:scale-110 transition">😂</button>
                        <button type="button" onclick="appendEmoji('🙏')" class="text-amber-600 hover:scale-110 transition">🙏</button>
                    </div>
                </div>

                <button onclick="publishPost()" class="w-full bg-[#1877F2] hover:bg-blue-600 text-white font-bold py-2.5 rounded-xl shadow-sm transition">
                    पोस्ट करें
                </button>
            </div>
        </div>
    </div>

    <!-- ================= MODAL: COMMENTS ================= -->
    <div id="commentModal" class="fixed inset-0 z-50 bg-black/60 hidden flex items-end sm:items-center justify-center">
        <div class="bg-white w-full max-w-md rounded-t-2xl sm:rounded-2xl shadow-xl flex flex-col max-h-[80vh]">
            <div class="flex items-center justify-between px-4 py-3 border-b border-gray-100">
                <h3 class="font-bold text-gray-800 text-sm">कमेंट्स</h3>
                <button onclick="closeCommentModal()" class="w-7 h-7 rounded-full bg-gray-100 flex items-center justify-center text-gray-600">
                    <i class="fa-solid fa-xmark text-sm"></i>
                </button>
            </div>
            <div id="commentsList" class="p-4 overflow-y-auto flex-1 space-y-3">
                <!-- Comments injected here -->
            </div>
            <div class="p-3 border-t border-gray-100 flex items-center space-x-2 bg-white">
                <input type="text" id="newCommentInput" placeholder="अपना कमेंट लिखें..." class="flex-1 bg-[#f0f2f5] text-sm rounded-full px-4 py-2 focus:outline-none focus:ring-1 focus:ring-[#1877F2]">
                <button onclick="submitComment()" class="w-9 h-9 rounded-full bg-[#1877F2] text-white flex items-center justify-center">
                    <i class="fa-solid fa-paper-plane text-xs"></i>
                </button>
            </div>
        </div>
    </div>

    <!-- ================= MODAL: STORY VIEWER / CREATOR ================= -->
    <div id="storyViewerModal" class="fixed inset-0 z-50 bg-black hidden flex flex-col justify-between p-4 text-white">
        <div class="max-w-md w-full mx-auto flex items-center justify-between pt-2">
            <div class="flex items-center space-x-2.5">
                <img id="storyViewerAvatar" src="" class="w-9 h-9 rounded-full border border-white">
                <div>
                    <p id="storyViewerName" class="text-sm font-bold"></p>
                    <p class="text-[10px] text-gray-300">अभी-अभी</p>
                </div>
            </div>
            <button onclick="closeStoryViewer()" class="w-8 h-8 rounded-full bg-white/20 flex items-center justify-center">
                <i class="fa-solid fa-xmark"></i>
            </button>
        </div>
        <div class="max-w-md w-full mx-auto my-auto text
