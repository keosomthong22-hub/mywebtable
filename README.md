# <!DOCTYPE html>
<html lang="lo">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ລະບົບຕິດຕາມການຂຶ້ນຫ້ອງ-ລົງຫ້ອງຂອງຄູ (Admin Secure)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Phetsarath -->
    <link href="https://fonts.googleapis.com/css2?family=Phetsarath:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Phetsarath', sans-serif;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.95); }
            to { opacity: 1; transform: scale(1); }
        }
        .modal-animate {
            animation: fadeIn 0.25s ease-out forwards;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col">

    <!-- Navbar -->
    <header class="bg-gradient-to-r from-indigo-700 to-indigo-800 text-white shadow-md sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 py-3 flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <div class="bg-white/10 p-2.5 rounded-xl backdrop-blur-md shadow-inner">
                    <i class="fa-solid fa-school-flag text-xl text-indigo-200"></i>
                </div>
                <div>
                    <h1 class="text-base sm:text-lg font-bold">ລະບົບຕິດຕາມການຂຶ້ນຫ້ອງ-ລົງຫ້ອງຂອງຄູ</h1>
                    <p class="text-xs text-indigo-200">ອອກແບບ ແລະ ພັດທະນາໂດຍ: ອາຈານ ອາປຸ ແກ້ວສົມທອງ 020 22887795</p>
                </div>
            </div>
            <nav class="flex space-x-2">
                <button onclick="switchTab('home')" id="nav-home" class="px-4 py-2 rounded-xl bg-indigo-900/80 text-white text-sm font-medium transition flex items-center space-x-2 shadow-inner border border-indigo-600/50">
                    <i class="fa-solid fa-house"></i>
                    <span class="hidden sm:inline">ໜ້າທຳອິດ (ບັນທຶກ)</span>
                </button>
                <button onclick="tryAccessAdmin()" id="nav-admin" class="px-4 py-2 rounded-xl text-indigo-100 hover:bg-indigo-600/50 text-sm font-medium transition flex items-center space-x-2 border border-transparent">
                    <i class="fa-solid fa-lock" id="admin-lock-icon"></i>
                    <span class="hidden sm:inline">ໜ້າແອັດມິນ (ຈັດການ)</span>
                </button>
            </nav>
        </div>
    </header>

    <!-- Main Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto p-4 sm:p-6">

        <!-- ================= HOME TAB ================= -->
        <div id="tab-home" class="space-y-6">
            <!-- Header Banner -->
            <div class="bg-gradient-to-r from-indigo-600 via-blue-600 to-indigo-700 rounded-2xl p-6 text-white shadow-lg flex flex-col md:flex-row justify-between items-center relative overflow-hidden">
                <div class="absolute -right-10 -bottom-10 w-48 h-48 bg-white/10 rounded-full blur-2xl pointer-events-none"></div>
                <div class="mb-4 md:mb-0 z-10">
                    <h2 class="text-2xl font-bold">ບັນທຶກຂໍ້ມູນຄູບໍ່ໄດ້ຂຶ້ນຫ້ອງ</h2>
                    <p class="text-indigo-100 text-sm mt-1">ກະລຸນາປ້ອນຂໍ້ມູນໃຫ້ครบຖ້ວນ ເພື່ອຄວາມສະດວກໃນການຕິດຕາມກວດກາ (ໜ້ານີ້ເພີ່ມໄດ້ຢ່າງດຽວ)</p>
                </div>
                <div class="bg-white/10 backdrop-blur-md px-5 py-3 rounded-2xl border border-white/20 text-center z-10 shadow-lg">
                    <span class="block text-xs text-indigo-200">ວັນທີປັດຈຸບັນ</span>
                    <span class="text-base font-bold" id="current-date-display">--/--/----</span>
                </div>
            </div>

            <!-- Grid Layout -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Form Add (User can only ADD) -->
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100 lg:col-span-1">
                    <h3 class="text-lg font-bold text-slate-700 mb-4 flex items-center space-x-2">
                        <i class="fa-solid fa-circle-plus text-indigo-600"></i>
                        <span>ເພີ່ມລາຍການຄູຂາດສອນ</span>
                    </h3>
                    <form id="attendance-form" onsubmit="handleAddAttendance(event)" class="space-y-4">
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">ວັນທີ, ເດືອນ, ປີ</label>
                            <input type="date" id="record-date" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-slate-50/50">
                        </div>
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-xs font-semibold text-slate-600 mb-1">ຊັ້ນຮຽນ</label>
                                <select id="record-grade" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-white">
                                    <option value="">ເລືອກຊັ້ນ</option>
                                    <option value="ມ.1">ມ. 1</option>
                                    <option value="ມ.2">ມ. 2</option>
                                    <option value="ມ.3">ມ. 3</option>
                                    <option value="ມ.4">ມ. 4</option>
                                    <option value="ມ.5">ມ. 5</option>
                                    <option value="ມ.6">ມ. 6</option>
                                    <option value="ມ.7">ມ. 7</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-xs font-semibold text-slate-600 mb-1">ຫ້ອງ</label>
                                <input type="text" id="record-room" placeholder="ເຊັ່ນ: ມ.1/1" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                            </div>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">ຊົ່ວໂມງຮຽນ</label>
                            <select id="record-period" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-white">
                                <option value="">ເລືອກຊົ່ວໂມງ</option>
                                <option value="ຊົ່ວໂມງທີ 1">ຊົ່ວໂມງທີ 1</option>
                                <option value="ຊົ່ວໂມງທີ 2">ຊົ່ວໂມງທີ 2</option>
                                <option value="ຊົ່ວໂມງທີ 3">ຊົ່ວໂມງທີ 3</option>
                                <option value="ຊົ່ວໂມງທີ 4">ຊົ່ວໂມງທີ 4</option>
                                <option value="ຊົ່ວໂມງທີ 5">ຊົ່ວໂມງທີ 5</option>
                                <option value="ຊົ່ວໂມງທີ 6">ຊົ່ວໂມງທີ 6</option>
                                <option value="ຊົ່ວໂມງທີ 7">ຊົ່ວໂມງທີ 7</option>
                            </select>
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">ຊື່ ແລະ ນາມສະກຸນຄູ</label>
                            <input type="text" id="record-teacher" placeholder="ປ້ອນຊື່ຄູຜູ້ສອນ" required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-slate-600 mb-1">ສາເຫດທີ່ບໍ່ໄດ້ຂຶ້ນຫ້ອງ</label>
                            <textarea id="record-reason" rows="2" placeholder="ເຊັ່ນ: ເຈັບເປັນ, ຕິດພາລະກິດ..." required class="w-full px-3 py-2 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm"></textarea>
                        </div>
                        <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-medium py-2.5 rounded-xl shadow-md transition text-sm flex items-center justify-center space-x-2">
                            <i class="fa-solid fa-paper-plane"></i>
                            <span>ບັນທຶກຂໍ້ມູນ (ສົ່ງລາຍງານ)</span>
                        </button>
                    </form>
                </div>

                <!-- List View (Public Feed - Read Only) -->
                <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100 lg:col-span-2 flex flex-col">
                    <div class="flex justify-between items-center mb-4">
                        <h3 class="text-lg font-bold text-slate-700 flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-indigo-600"></i>
                            <span>ລາຍການຄູຂາດສອນລ່າສຸດ (ເບິ່ງຢ່າງດຽວ - ບໍ່ສາມາດແກ້ໄຂ/ລົບໄດ້)</span>
                        </h3>
                        <span class="bg-indigo-50 text-indigo-700 text-xs px-3 py-1 rounded-full font-semibold" id="total-count">0 ລາຍການ</span>
                    </div>
                    
                    <div class="overflow-x-auto flex-grow">
                        <table class="w-full text-left border-collapse">
                            <thead>
                                <tr class="border-b border-slate-100 text-slate-400 text-xs uppercase font-semibold">
                                    <th class="py-3 px-2">ວັນທີ</th>
                                    <th class="py-3 px-2">ຊັ້ນ/ຫ້ອງ</th>
                                    <th class="py-3 px-2">ຊົ່ວໂມງ</th>
                                    <th class="py-3 px-2">ຊື່ຄູ</th>
                                    <th class="py-3 px-2">ສາເຫດ</th>
                                </tr>
                            </thead>
                            <tbody id="public-table-body" class="divide-y divide-slate-50 text-sm text-slate-600">
                                <!-- Data populated by JS -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- ================= ADMIN TAB ================= -->
        <div id="tab-admin" class="hidden space-y-6">
            <div class="bg-gradient-to-r from-slate-800 to-slate-900 text-white rounded-2xl p-6 shadow-xl flex flex-col md:flex-row justify-between items-center gap-4">
                <div>
                    <div class="flex items-center space-x-2">
                        <span class="bg-amber-400/20 text-amber-300 border border-amber-400/30 text-xs px-2.5 py-1 rounded-full font-semibold flex items-center space-x-1">
                            <i class="fa-solid fa-shield-check"></i>
                            <span>Admin Mode Active</span>
                        </span>
                    </div>
                    <h2 class="text-2xl font-bold mt-2">ໜ້າຈັດການລະບົບສຳລັບແອັດມິນ</h2>
                    <p class="text-slate-300 text-sm mt-1">ສາມາດກວດສອບ, ແກ້ໄຂ (Edit), ລົບ (Delete) ຂໍ້ມູນ ແລະ ຈັດການລະຫັດຜ່ານໄດ້</p>
                </div>
                <div class="flex flex-wrap gap-2">
                    <button onclick="openChangePasswordModal()" class="bg-slate-700 hover:bg-slate-600 text-amber-300 border border-slate-600 px-4 py-2 rounded-xl text-sm font-medium transition flex items-center space-x-2 shadow">
                        <i class="fa-solid fa-key"></i>
                        <span>ປ່ຽນລະຫັດແອັດມິນ</span>
                    </button>
                    <button onclick="exportToCSV()" class="bg-emerald-600 hover:bg-emerald-700 text-white px-4 py-2 rounded-xl text-sm font-medium transition flex items-center space-x-2 shadow">
                        <i class="fa-solid fa-file-excel"></i>
                        <span>ສົ່ງອອກ Excel (CSV)</span>
                    </button>
                    <button onclick="adminLogout()" class="bg-rose-600/80 hover:bg-rose-600 text-white px-3 py-2 rounded-xl text-sm font-medium transition flex items-center space-x-1 shadow" title="ອອກຈາກລະບົບແອັດມິນ">
                        <i class="fa-solid fa-right-from-bracket"></i>
                    </button>
                </div>
            </div>

            <!-- Blocks Section for Each Grade (ມ.1 - ມ.7) -->
            <div class="space-y-3">
                <h3 class="text-lg font-bold text-slate-700 flex items-center space-x-2">
                    <i class="fa-solid fa-cubes text-indigo-600"></i>
                    <span>ລາຍງານແຍກຕາມຊັ້ນຮຽນ (ກົດເພື່ອເບິ່ງ/ກັ່ນກອງ)</span>
                </h3>
                <div class="grid grid-cols-2 sm:grid-cols-4 lg:grid-cols-8 gap-3" id="grade-blocks-container">
                    <!-- Dynamic Blocks Generated Here -->
                </div>
            </div>

            <!-- Filter and Search -->
            <div class="bg-white p-4 rounded-2xl shadow-sm border border-slate-100 flex flex-wrap gap-4 items-center justify-between">
                <div class="flex items-center space-x-2 w-full md:w-auto">
                    <input type="text" id="admin-search" onkeyup="renderAdminTable()" placeholder="ຄົ້ນຫາຊື່ຄູ, ຫ້ອງ, ສາເຫດ..." class="px-3 py-2 border border-slate-200 rounded-xl text-sm w-full md:w-80 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                </div>
                <div class="text-xs text-slate-500">
                    ທັງໝົດ: <span id="admin-total-count" class="font-bold text-indigo-600">0</span> ລາຍການ
                </div>
            </div>

            <!-- Admin Table -->
            <div class="bg-white rounded-2xl p-6 shadow-sm border border-slate-100 overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="border-b border-slate-100 text-slate-400 text-xs uppercase font-semibold">
                            <th class="py-3 px-3">ວັນທີ</th>
                            <th class="py-3 px-3">ຊັ້ນ/ຫ້ອງ</th>
                            <th class="py-3 px-3">ຊົ່ວໂມງ</th>
                            <th class="py-3 px-3">ຊື່ຄູ-ອາຈານ</th>
                            <th class="py-3 px-3">ສາເຫດ</th>
                            <th class="py-3 px-3 text-center">ຈັດການ (ແກ້ໄຂ / ລົບ)</th>
                        </tr>
                    </thead>
                    <tbody id="admin-table-body" class="divide-y divide-slate-50 text-sm text-slate-600">
                        <!-- Data populated by JS -->
                    </tbody>
                </table>
            </div>
        </div>

    </main>

    <!-- ================= PROFESSIONAL LOGIN MODAL ================= -->
    <div id="login-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-md hidden flex items-center justify-center z-50 p-4">
        <div class="bg-white rounded-3xl max-w-sm w-full p-8 shadow-2xl modal-animate border border-slate-100 relative overflow-hidden">
            <!-- Decorative gradient header inside modal -->
            <div class="absolute top-0 left-0 right-0 h-2 bg-gradient-to-r from-indigo-500 via-blue-500 to-indigo-600"></div>
            
            <div class="text-center mb-6">
                <div class="w-16 h-16 bg-indigo-50 text-indigo-600 rounded-2xl flex items-center justify-center mx-auto mb-3 shadow-inner border border-indigo-100">
                    <i class="fa-solid fa-shield-keyhole text-2xl"></i>
                </div>
                <h3 class="text-xl font-bold text-slate-800">ເຂົ້າສູ່ລະບົບແອັດມິນ</h3>
                <p class="text-xs text-slate-400 mt-1">ກະລຸນາປ້ອນລະຫັດຜ່ານເພື່ອຈັດການລະບົບ</p>
            </div>

            <form onsubmit="handleAdminLogin(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1.5">ລະຫັດຜ່ານແອັດມິນ</label>
                    <div class="relative">
                        <span class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-slate-400">
                            <i class="fa-solid fa-lock text-xs"></i>
                        </span>
                        <input type="password" id="login-password" placeholder="ປ້ອນລະຫັດຜ່ານ..." required class="w-full pl-9 pr-10 py-2.5 border border-slate-200 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-slate-50/50">
                        <button type="button" onclick="togglePasswordVisibility()" class="absolute inset-y-0 right-0 pr-3 flex items-center text-slate-400 hover:text-slate-600">
                            <i class="fa-solid fa-eye text-xs" id="toggle-icon"></i>
                        </button>
                    </div>
                    <p id="login-error" class="text-rose-500 text-xs mt-1.5 hidden font-medium text-center">ລະຫັດຜ່ານບໍ່ຖືກຕ້ອງ!</p>
                </div>

                <div class="flex space-x-2 pt-2">
                    <button type="button" onclick="closeLoginModal()" class="w-1/2 bg-slate-100 hover:bg-slate-200 text-slate-600 py-2.5 rounded-xl text-sm font-medium transition">ຍົກເລີກ</button>
                    <button type="submit" class="w-1/2 bg-indigo-600 hover:bg-indigo-700 text-white py-2.5 rounded-xl text-sm font-medium shadow-md transition flex items-center justify-center space-x-1.5">
                        <span>ເຂົ້າສູ່ລະບົບ</span>
                        <i class="fa-solid fa-arrow-right-to-bracket text-xs"></i>
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- ================= CHANGE PASSWORD MODAL ================= -->
    <div id="change-pass-modal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-md hidden flex items-center justify-center z-50 p-4">
        <div class="bg-white rounded-3xl max-w-sm w-full p-8 shadow-2xl modal-animate border border-slate-100">
            <div class="flex justify-between items-center mb-6 border-b pb-3">
                <h3 class="font-bold text-lg text-slate-800 flex items-center space-x-2">
                    <i class="fa-solid fa-key text-indigo-600"></i>
                    <span>ປ່ຽນລະຫັດຜ່ານແອັດມິນ</span>
                </h3>
                <button onclick="closeChangePasswordModal()" class="text-slate-400 hover:text-slate-600">
                    <i class="fa-solid fa-xmark text-lg"></i>
                </button>
            </div>
            <form onsubmit="handlePasswordChange(event)" class="space-y-4">
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ລະຫັດຜ່ານເກົ່າ</label>
                    <input type="password" id="old-pass" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm focus:ring-2 focus:ring-indigo-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ລະຫັດຜ່ານໃໝ່</label>
                    <input type="password" id="new-pass" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm focus:ring-2 focus:ring-indigo-500">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ຢືນຢັນລະຫັດຜ່ານໃໝ່</label>
                    <input type="password" id="confirm-pass" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm focus:ring-2 focus:ring-indigo-500">
                </div>
                <div class="flex space-x-2 pt-2">
                    <button type="button" onclick="closeChangePasswordModal()" class="w-1/2 bg-slate-100 hover:bg-slate-200 text-slate-600 py-2.5 rounded-xl text-sm font-medium">ຍົກເລີກ</button>
                    <button type="submit" class="w-1/2 bg-indigo-600 hover:bg-indigo-700 text-white py-2.5 rounded-xl text-sm font-medium shadow-md">ບັນທຶກລະຫັດໃໝ່</button>
                </div>
            </form>
        </div>
    </div>

    <!-- ================= EDIT ITEM MODAL ================= -->
    <div id="edit-modal" class="fixed inset-0 bg-slate-900/50 backdrop-blur-sm hidden flex items-center justify-center z-50 p-4">
        <div class="bg-white rounded-3xl max-w-md w-full p-6 shadow-xl space-y-4 modal-animate">
            <div class="flex justify-between items-center border-b pb-3">
                <h3 class="font-bold text-lg text-slate-700 flex items-center space-x-2">
                    <i class="fa-solid fa-pen-to-square text-indigo-600"></i>
                    <span>ແກ້ໄຂຂໍ້ມູນຄູຂາດສອນ</span>
                </h3>
                <button onclick="closeEditModal()" class="text-slate-400 hover:text-slate-600">
                    <i class="fa-solid fa-xmark text-xl"></i>
                </button>
            </div>
            <form id="edit-form" onsubmit="handleUpdateAttendance(event)" class="space-y-3">
                <input type="hidden" id="edit-id">
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ວັນທີ</label>
                    <input type="date" id="edit-date" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm">
                </div>
                <div class="grid grid-cols-2 gap-2">
                    <div>
                        <label class="block text-xs font-semibold text-slate-600 mb-1">ຊັ້ນຮຽນ</label>
                        <select id="edit-grade" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm bg-white">
                            <option value="ມ.1">ມ. 1</option>
                            <option value="ມ.2">ມ. 2</option>
                            <option value="ມ.3">ມ. 3</option>
                            <option value="ມ.4">ມ. 4</option>
                            <option value="ມ.5">ມ. 5</option>
                            <option value="ມ.6">ມ. 6</option>
                            <option value="ມ.7">ມ. 7</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-slate-600 mb-1">ຫ້ອງ</label>
                        <input type="text" id="edit-room" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm">
                    </div>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ຊົ່ວໂມງ</label>
                    <select id="edit-period" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm bg-white">
                        <option value="ຊົ່ວໂມງທີ 1">ຊົ່ວໂມງທີ 1</option>
                        <option value="ຊົ່ວໂມງທີ 2">ຊົ່ວໂມງທີ 2</option>
                        <option value="ຊົ່ວໂມງທີ 3">ຊົ່ວໂມງທີ 3</option>
                        <option value="ຊົ່ວໂມງທີ 4">ຊົ່ວໂມງທີ 4</option>
                        <option value="ຊົ່ວໂມງທີ 5">ຊົ່ວໂມງທີ 5</option>
                        <option value="ຊົ່ວໂມງທີ 6">ຊົ່ວໂມງທີ 6</option>
                        <option value="ຊົ່ວໂມງທີ 7">ຊົ່ວໂມງທີ 7</option>
                    </select>
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ຊື່ຄູ</label>
                    <input type="text" id="edit-teacher" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm">
                </div>
                <div>
                    <label class="block text-xs font-semibold text-slate-600 mb-1">ສາເຫດ</label>
                    <textarea id="edit-reason" rows="2" required class="w-full px-3 py-2 border border-slate-200 rounded-xl text-sm"></textarea>
                </div>
                <div class="flex space-x-2 pt-2">
                    <button type="button" onclick="closeEditModal()" class="w-1/2 bg-slate-100 hover:bg-slate-200 text-slate-700 py-2 rounded-xl text-sm font-medium">ຍົກເລີກ</button>
                    <button type="submit" class="w-1/2 bg-indigo-600 hover:bg-indigo-700 text-white py-2 rounded-xl text-sm font-medium shadow">ບັນທຶກການແກ້ໄຂ</button>
                </div>
            </form>
        </div>
    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // Initialize Data and Password
        let attendanceList = JSON.parse(localStorage.getItem('teacher_attendance')) || [
            { id: 1, date: '2026-10-02', grade: 'ມ.3', room: 'ມ.3/1', period: 'ຊົ່ວໂມງທີ 1', teacher: 'ອ.ຈ ສົມສີ ວົງສາ', reason: 'ເຈັບເປັນ (ເປັນໄຂ້ຫວັດ)' },
            { id: 2, date: '2026-10-02', grade: 'ມ.5', room: 'ມ.5/2', period: 'ຊົ່ວໂມງທີ 3', teacher: 'ອ.ຈ ບຸນມີ ສຸວັນນະລາດ', reason: 'ໄປລາຊະການດ່ວນ' }
        ];

        let adminPassword = localStorage.getItem('admin_password') || 'admin123';
        let isAdminLoggedIn = sessionStorage.getItem('is_admin_logged_in') === 'true';
        let selectedGradeFilter = 'ALL';

        // Set default date
        document.getElementById('record-date').valueAsDate = new Date();
        const optionsDate = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
        document.getElementById('current-date-display').innerText = new Date().toLocaleDateString('lo-LA', optionsDate);

        // Update Nav UI based on login status
        updateAdminNavState();

        function switchTab(tab) {
            const homeTab = document.getElementById('tab-home');
            const adminTab = document.getElementById('tab-admin');
            const navHome = document.getElementById('nav-home');
            const navAdmin = document.getElementById('nav-admin');

            if (tab === 'home') {
                homeTab.classList.remove('hidden');
                adminTab.classList.add('hidden');
                navHome.className = "px-4 py-2 rounded-xl bg-indigo-900/80 text-white text-sm font-medium transition flex items-center space-x-2 shadow-inner border border-indigo-600/50";
                navAdmin.className = "px-4 py-2 rounded-xl text-indigo-100 hover:bg-indigo-600/50 text-sm font-medium transition flex items-center space-x-2 border border-transparent";
                renderPublicTable();
            } else {
                if (!isAdminLoggedIn) {
                    openLoginModal();
                    return;
                }
                homeTab.classList.add('hidden');
                adminTab.classList.remove('hidden');
                navAdmin.className = "px-4 py-2 rounded-xl bg-slate-800 text-white text-sm font-medium transition flex items-center space-x-2 shadow-inner border border-slate-700";
                navHome.className = "px-4 py-2 rounded-xl text-indigo-100 hover:bg-indigo-600/50 text-sm font-medium transition flex items-center space-x-2 border border-transparent";
                renderGradeBlocks();
                renderAdminTable();
            }
        }

        function tryAccessAdmin() {
            if (isAdminLoggedIn) {
                switchTab('admin');
            } else {
                openLoginModal();
            }
        }

        function updateAdminNavState() {
            const icon = document.getElementById('admin-lock-icon');
            if (isAdminLoggedIn) {
                icon.className = "fa-solid fa-shield-check text-amber-300";
            } else {
                icon.className = "fa-solid fa-lock";
            }
        }

        // Login Modal Control
        function openLoginModal() {
            document.getElementById('login-modal').classList.remove('hidden');
            document.getElementById('login-password').value = '';
            document.getElementById('login-error').classList.add('hidden');
            document.getElementById('login-password').focus();
        }

        function closeLoginModal() {
            document.getElementById('login-modal').classList.add('hidden');
        }

        function togglePasswordVisibility() {
            const pwdInput = document.getElementById('login-password');
            const icon = document.getElementById('toggle-icon');
            if (pwdInput.type === 'password') {
                pwdInput.type = 'text';
                icon.className = "fa-solid fa-eye-slash text-xs";
            } else {
                pwdInput.type = 'password';
                icon.className = "fa-solid fa-eye text-xs";
            }
        }

        function handleAdminLogin(e) {
            e.preventDefault();
            const pass = document.getElementById('login-password').value;
            if (pass === adminPassword) {
                isAdminLoggedIn = true;
                sessionStorage.setItem('is_admin_logged_in', 'true');
                updateAdminNavState();
                closeLoginModal();
                switchTab('admin');
            } else {
                const err = document.getElementById('login-error');
                err.classList.remove('hidden');
                document.getElementById('login-password').focus();
            }
        }

        function adminLogout() {
            isAdminLoggedIn = false;
            sessionStorage.removeItem('is_admin_logged_in');
            updateAdminNavState();
            switchTab('home');
            alert('ອອກຈາກລະບົບແອັດມິນຮຽບຮ້ອຍແລ້ວ');
        }

        // Password Change Modal
        function openChangePasswordModal() {
            document.getElementById('change-pass-modal').classList.remove('hidden');
        }

        function closeChangePasswordModal() {
            document.getElementById('change-pass-modal').classList.add('hidden');
        }

        function handlePasswordChange(e) {
            e.preventDefault();
            const oldPass = document.getElementById('old-pass').value;
            const newPass = document.getElementById('new-pass').value;
            const confirmPass = document.getElementById('confirm-pass').value;

            if (oldPass !== adminPassword) {
                alert('ລະຫັດຜ່ານເກົ່າບໍ່ຖືກຕ້ອງ!');
                return;
            }
            if (newPass !== confirmPass) {
                alert('ລະຫັດຜ່ານໃໝ່ບໍ່ກົງກັນ!');
                return;
            }
            if (newPass.length < 4) {
                alert('ລະຫັດຜ່ານໃໝ່ຕ້ອງມີຢ່າງໜ້ອຍ 4 ຕົວອັກສອນ!');
                return;
            }

            adminPassword = newPass;
            localStorage.setItem('admin_password', adminPassword);
            closeChangePasswordModal();
            alert('ປ່ຽນລະຫັດຜ່ານແອັດມິນສຳເລັດແລ້ວ!');
            document.getElementById('old-pass').value = '';
            document.getElementById('new-pass').value = '';
            document.getElementById('confirm-pass').value = '';
        }

        // Save to LocalStorage
        function saveData() {
            localStorage.setItem('teacher_attendance', JSON.stringify(attendanceList));
        }

        // Handle Add (Home)
        function handleAddAttendance(e) {
            e.preventDefault();
            const newItem = {
                id: Date.now(),
                date: document.getElementById('record-date').value,
                grade: document.getElementById('record-grade').value,
                room: document.getElementById('record-room').value,
                period: document.getElementById('record-period').value,
                teacher: document.getElementById('record-teacher').value,
                reason: document.getElementById('record-reason').value
            };

            attendanceList.unshift(newItem);
            saveData();
            document.getElementById('attendance-form').reset();
            document.getElementById('record-date').valueAsDate = new Date();
            renderPublicTable();
            alert('ບັນທຶກຂໍ້ມູນສຳເລັດແລ້ວ!');
        }

        // Render Public Table
        function renderPublicTable() {
            const tbody = document.getElementById('public-table-body');
            tbody.innerHTML = '';
            document.getElementById('total-count').innerText = `${attendanceList.length} ລາຍການ`;

            if (attendanceList.length === 0) {
                tbody.innerHTML = `<tr><td colspan="5" class="text-center py-6 text-slate-400">ຍັງບໍ່ມີຂໍ້ມູນການຂາດສອນ</td></tr>`;
                return;
            }

            attendanceList.forEach(item => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/80 transition";
                tr.innerHTML = `
                    <td class="py-3 px-2 font-medium text-slate-700">${item.date}</td>
                    <td class="py-3 px-2"><span class="bg-slate-100 text-slate-700 px-2 py-0.5 rounded-lg text-xs font-semibold">${item.grade} (${item.room})</span></td>
                    <td class="py-3 px-2 text-indigo-600 font-medium">${item.period}</td>
                    <td class="py-3 px-2 text-slate-800 font-semibold">${item.teacher}</td>
                    <td class="py-3 px-2 text-slate-500">${item.reason}</td>
                `;
                tbody.appendChild(tr);
            });
        }

        // Render Grade Blocks
        function renderGradeBlocks() {
            const container = document.getElementById('grade-blocks-container');
            const grades = ['ALL', 'ມ.1', 'ມ.2', 'ມ.3', 'ມ.4', 'ມ.5', 'ມ.6', 'ມ.7'];
            container.innerHTML = '';

            grades.forEach(grade => {
                const count = grade === 'ALL' 
                    ? attendanceList.length 
                    : attendanceList.filter(i => i.grade === grade).length;

                const isSelected = selectedGradeFilter === grade;
                const activeClass = isSelected 
                    ? 'bg-indigo-600 text-white shadow-md ring-2 ring-indigo-400' 
                    : 'bg-white text-slate-700 border border-slate-200 hover:border-indigo-300 hover:bg-slate-50';

                const block = document.createElement('button');
                block.type = 'button';
                block.className = `p-3 rounded-2xl flex flex-col items-center justify-center transition cursor-pointer ${activeClass}`;
                block.onclick = () => filterByGrade(grade);

                block.innerHTML = `
                    <span class="text-xs font-bold">${grade === 'ALL' ? 'ທັງໝົດ' : grade}</span>
                    <span class="text-lg font-extrabold mt-1 ${isSelected ? 'text-white' : 'text-indigo-600'}">${count}</span>
                    <span class="text-[10px] opacity-80">ລາຍການ</span>
                `;
                container.appendChild(block);
            });
        }

        function filterByGrade(grade) {
            selectedGradeFilter = grade;
            renderGradeBlocks();
            renderAdminTable();
        }

        // Render Admin Table
        function renderAdminTable() {
            const tbody = document.getElementById('admin-table-body');
            const searchKeyword = document.getElementById('admin-search').value.toLowerCase();
            tbody.innerHTML = '';

            const filteredList = attendanceList.filter(item => {
                const matchesGrade = selectedGradeFilter === 'ALL' || item.grade === selectedGradeFilter;
                const matchesSearch = item.teacher.toLowerCase().includes(searchKeyword) ||
                    item.room.toLowerCase().includes(searchKeyword) ||
                    item.reason.toLowerCase().includes(searchKeyword) ||
                    item.date.includes(searchKeyword) ||
                    item.grade.toLowerCase().includes(searchKeyword);
                return matchesGrade && matchesSearch;
            });

            document.getElementById('admin-total-count').innerText = filteredList.length;

            if (filteredList.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="text-center py-6 text-slate-400">ບໍ່ພົບຂໍ້ມູນທີ່ຄົ້ນຫາ</td></tr>`;
                return;
            }

            filteredList.forEach(item => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-slate-50/80 transition";
                tr.innerHTML = `
                    <td class="py-3 px-3 font-medium text-slate-700">${item.date}</td>
                    <td class="py-3 px-3"><span class="bg-indigo-50 text-indigo-700 px-2.5 py-1 rounded-xl text-xs font-semibold">${item.grade} (${item.room})</span></td>
                    <td class="py-3 px-3 text-indigo-600 font-medium">${item.period}</td>
                    <td class="py-3 px-3 text-slate-800 font-semibold">${item.teacher}</td>
                    <td class="py-3 px-3 text-slate-500">${item.reason}</td>
                    <td class="py-3 px-3 text-center space-x-1.5">
                        <button onclick="openEditModal(${item.id})" class="bg-amber-100 text-amber-700 hover:bg-amber-200 p-2 rounded-xl transition" title="ແກ້ໄຂ">
                            <i class="fa-solid fa-pen text-xs"></i>
                        </button>
                        <button onclick="deleteItem(${item.id})" class="bg-rose-100 text-rose-700 hover:bg-rose-200 p-2 rounded-xl transition" title="ລົບ">
                            <i class="fa-solid fa-trash text-xs"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        // Delete Item
        function deleteItem(id) {
            if (confirm('ທ່ານຕ້ອງການລົບຂໍ້ມູນລາຍການນີ້ແທ້ບໍ?')) {
                attendanceList = attendanceList.filter(item => item.id !== id);
                saveData();
                renderGradeBlocks();
                renderAdminTable();
            }
        }

        // Edit Modal
        function openEditModal(id) {
            const item = attendanceList.find(i => i.id === id);
            if (!item) return;

            document.getElementById('edit-id').value = item.id;
            document.getElementById('edit-date').value = item.date;
            document.getElementById('edit-grade').value = item.grade;
            document.getElementById('edit-room').value = item.room;
            document.getElementById('edit-period').value = item.period;
            document.getElementById('edit-teacher').value = item.teacher;
            document.getElementById('edit-reason').value = item.reason;

            document.getElementById('edit-modal').classList.remove('hidden');
        }

        function closeEditModal() {
            document.getElementById('edit-modal').classList.add('hidden');
        }

        function handleUpdateAttendance(e) {
            e.preventDefault();
            const id = Number(document.getElementById('edit-id').value);
            const index = attendanceList.findIndex(i => i.id === id);

            if (index !== -1) {
                attendanceList[index] = {
                    id: id,
                    date: document.getElementById('edit-date').value,
                    grade: document.getElementById('edit-grade').value,
                    room: document.getElementById('edit-room').value,
                    period: document.getElementById('edit-period').value,
                    teacher: document.getElementById('edit-teacher').value,
                    reason: document.getElementById('edit-reason').value
                };
                saveData();
                closeEditModal();
                renderGradeBlocks();
                renderAdminTable();
                alert('ອັບເດດຂໍ້ມູນສຳເລັດແລ້ວ!');
            }
        }

        // Export CSV
        function exportToCSV() {
            let csvContent = "\uFEFFວັນທີ,ຊັ້ນ,ຫ້ອງ,ຊົ່ວໂມງ,ຊື່ຄູ,ສາເຫດ\n";
            attendanceList.forEach(item => {
                csvContent += `"${item.date}","${item.grade}","${item.room}","${item.period}","${item.teacher}","${item.reason}"\n`;
            });
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `teacher_attendance_${new Date().toISOString().slice(0,10)}.csv`;
            a.click();
        }

        // Initial Load
        renderPublicTable();
    </script>
</body>
</html>
