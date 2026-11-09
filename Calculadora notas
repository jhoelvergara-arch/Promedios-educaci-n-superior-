<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora de Notas - Educación Superior Chile</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom scrollbars */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }
    </style>
</head>
<body class="bg-slate-50 text-slate-800 min-h-screen flex flex-col antialiased selection:bg-blue-500 selection:text-white">

    <!-- Navbar / Header -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-gradient-to-tr from-blue-600 to-indigo-600 text-white p-2 rounded-xl shadow-md">
                    <i data-lucide="graduation-cap" class="w-6 h-6"></i>
                </div>
                <div>
                    <h1 class="font-bold text-lg leading-tight text-slate-900">Calculadora Académica</h1>
                    <p class="text-xs text-slate-500 font-medium">Escala Chilena 1.0 - 7.0</p>
                </div>
            </div>
            
            <div class="flex items-center space-x-2">
                <button id="btn-export-import" onclick="toggleModal('modal-data')" class="p-2 text-slate-600 hover:text-blue-600 hover:bg-slate-100 rounded-lg transition" title="Respaldar o Restaurar">
                    <i data-lucide="database" class="w-5 h-5"></i>
                </button>
                <button id="btn-reset-all" onclick="resetAllData()" class="p-2 text-slate-400 hover:text-red-600 hover:bg-red-50 rounded-lg transition" title="Reiniciar todo">
                    <i data-lucide="rotate-ccw" class="w-5 h-5"></i>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Layout Container -->
    <main class="flex-grow max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col md:flex-row gap-6">

        <!-- Sidebar: Resumen Semestral & Lista de Ramos -->
        <aside class="w-full md:w-80 flex-shrink-0 space-y-6">
            
            <!-- Global Stats Card -->
            <div class="bg-white rounded-2xl p-5 border border-slate-200 shadow-sm space-y-4">
                <div class="flex justify-between items-center">
                    <span class="text-xs font-semibold uppercase tracking-wider text-slate-400">Promedio Ponderado Global</span>
                    <span class="px-2 py-0.5 text-xs font-semibold rounded-full bg-slate-100 text-slate-600" id="ramo-count-badge">0 Ramos</span>
                </div>
                
                <div class="flex items-baseline justify-between">
                    <div id="promedio-global-display" class="text-4xl font-extrabold tracking-tight text-slate-900">
                        1.0
                    </div>
                    <div id="global-status-badge" class="px-3 py-1 text-xs font-bold rounded-full bg-slate-100 text-slate-500">
                        Sin datos
                    </div>
                </div>

                <div class="w-full bg-slate-100 h-2 rounded-full overflow-hidden">
                    <div id="global-progress-bar" class="bg-blue-600 h-full transition-all duration-500 rounded-full" style="width: 0%"></div>
                </div>

                <p class="text-xs text-slate-500 flex items-center gap-1">
                    <i data-lucide="info" class="w-3.5 h-3.5 text-slate-400 flex-shrink-0"></i>
                    Nota mínima de aprobación: <strong class="text-slate-700 font-semibold">4.0</strong>
                </p>
            </div>

            <!-- List of Subjects (Ramos) -->
            <div class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden flex flex-col">
                <div class="p-4 border-b border-slate-100 flex items-center justify-between bg-slate-50/50">
                    <h2 class="font-bold text-slate-800 text-sm flex items-center gap-2">
                        <i data-lucide="book-open" class="w-4 h-4 text-blue-600"></i>
                        Mis Asignaturas
                    </h2>
                    <button onclick="addSubject()" class="inline-flex items-center gap-1 bg-blue-600 hover:bg-blue-700 active:scale-95 text-white text-xs font-semibold px-2.5 py-1.5 rounded-lg shadow-sm transition">
                        <i data-lucide="plus" class="w-3.5 h-3.5"></i> Nuevo Ramo
                    </button>
                </div>

                <div id="subjects-list" class="divide-y divide-slate-100 max-h-[calc(100vh-380px)] overflow-y-auto">
                    <!-- Dynamic subjects item insertion -->
                </div>
            </div>
        </aside>

        <!-- Main Content Area: Selected Subject Detail -->
        <section class="flex-grow flex flex-col space-y-6">

            <div id="no-subject-selected" class="hidden bg-white rounded-2xl border border-slate-200 p-12 text-center my-auto shadow-sm">
                <div class="w-16 h-16 bg-blue-50 text-blue-500 rounded-full flex items-center justify-center mx-auto mb-4">
                    <i data-lucide="book-open" class="w-8 h-8"></i>
                </div>
                <h3 class="text-lg font-bold text-slate-800 mb-1">No hay asignaturas seleccionadas</h3>
                <p class="text-sm text-slate-500 max-w-sm mx-auto mb-6">Agrega un ramo desde el panel lateral para empezar a ingresar tus evaluaciones y calcular tus promedios.</p>
                <button onclick="addSubject()" class="inline-flex items-center gap-2 bg-blue-600 hover:bg-blue-700 text-white text-sm font-semibold px-4 py-2 rounded-xl shadow-md transition">
                    <i data-lucide="plus" class="w-4 h-4"></i> Crear primer ramo
                </button>
            </div>

            <div id="subject-detail-card" class="bg-white rounded-2xl border border-slate-200 shadow-sm overflow-hidden flex flex-col">
                
                <!-- Subject Header -->
                <div class="p-5 sm:p-6 border-b border-slate-100 flex flex-col sm:flex-row sm:items-center justify-between gap-4 bg-slate-50/40">
                    <div class="space-y-1 flex-grow">
                        <div class="flex items-center gap-2">
                            <input type="text" id="subject-title-input" onchange="updateSubjectTitle(this.value)" class="text-xl sm:text-2xl font-bold text-slate-900 bg-transparent border-b border-transparent hover:border-slate-300 focus:border-blue-500 focus:bg-white focus:outline-none rounded px-1 py-0.5 transition w-full sm:w-auto" placeholder="Nombre de la asignatura">
                        </div>
                        <div class="flex items-center gap-3 text-xs text-slate-500">
                            <span class="flex items-center gap-1">
                                Ponderación global: 
                                <input type="number" min="0" max="100" id="subject-global-weight-input" onchange="updateSubjectGlobalWeight(this.value)" class="w-14 font-semibold text-slate-700 border border-slate-200 rounded px-1.5 py-0.5 bg-white text-center focus:border-blue-500 focus:outline-none"> %
                            </span>
                        </div>
                    </div>

                    <!-- Subject Summary Pill -->
                    <div class="flex items-center gap-3 bg-white border border-slate-200 p-2.5 rounded-xl shadow-sm self-start sm:self-auto">
                        <div class="text-right">
                            <div class="text-xs text-slate-400 font-medium">Promedio Ramo</div>
                            <div id="subject-average-display" class="text-2xl font-black text-slate-800">
                                1.0
                            </div>
                        </div>
                        <div id="subject-status-badge" class="px-2.5 py-1 text-xs font-bold rounded-lg bg-slate-100 text-slate-600">
                            Pendiente
                        </div>
                    </div>
                </div>

                <!-- Evaluaciones & Calculadora -->
                <div class="p-5 sm:p-6 space-y-6">

                    <!-- Weight progress bar indicator -->
                    <div class="space-y-2">
                        <div class="flex justify-between text-xs font-medium">
                            <span class="text-slate-600 flex items-center gap-1.5">
                                Avance de Ponderación Evaluada
                                <span id="weight-alert-icon"></span>
                            </span>
                            <span id="weight-total-text" class="font-bold text-slate-800">0% de 100%</span>
                        </div>
                        <div class="w-full bg-slate-100 h-2.5 rounded-full overflow-hidden flex">
                            <div id="weight-progress-bar" class="bg-blue-600 h-full transition-all duration-300 rounded-full" style="width: 0%"></div>
                        </div>
                        <p id="weight-warning-msg" class="text-xs text-amber-600 font-medium hidden flex items-center gap-1">
                            <i data-lucide="alert-triangle" class="w-3.5 h-3.5"></i> La suma de las ponderaciones supera el 100%. Por favor ajústalas.
                        </p>
                    </div>

                    <!-- Evaluaciones Table / List -->
                    <div>
                        <div class="flex items-center justify-between mb-3">
                            <h3 class="text-sm font-bold text-slate-800 uppercase tracking-wider">Evaluaciones</h3>
                            <button onclick="addEvaluation()" class="inline-flex items-center gap-1 text-xs font-semibold text-blue-600 hover:text-blue-700 hover:bg-blue-50 px-2.5 py-1.5 rounded-lg transition">
                                <i data-lucide="plus-circle" class="w-4 h-4"></i> Agregar Nota
                            </button>
                        </div>

                        <!-- Table Header for desktop -->
                        <div class="hidden sm:grid sm:grid-cols-12 gap-3 text-xs font-semibold text-slate-400 uppercase tracking-wider px-3 py-2 bg-slate-50 rounded-lg">
                            <div class="col-span-5">Evaluación / Descripción</div>
                            <div class="col-span-3 text-center">Nota (1.0 - 7.0)</div>
                            <div class="col-span-3 text-center">Ponderación %</div>
                            <div class="col-span-1 text-center">Acción</div>
                        </div>

                        <!-- Evaluations List -->
                        <div id="evaluations-list" class="space-y-2 mt-2">
                            <!-- Dynamic evaluation rows -->
                        </div>
                    </div>

                    <!-- Target / Final Exam Calculator Card -->
                    <div id="target-calculator-box" class="bg-gradient-to-r from-slate-900 to-slate-800 text-white rounded-2xl p-5 shadow-lg space-y-4">
                        <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-3 border-b border-slate-700/60 pb-3">
                            <div class="flex items-center gap-2">
                                <div class="bg-blue-500/20 p-2 rounded-lg text-blue-400">
                                    <i data-lucide="calculator" class="w-5 h-5"></i>
                                </div>
                                <div>
                                    <h4 class="font-bold text-sm text-white">¿Qué nota necesito en lo que falta?</h4>
                                    <p class="text-xs text-slate-400">Cálculo proyectado para la ponderación restante (<span id="calc-remaining-weight">0%</span>)</p>
                                </div>
                            </div>
                            
                            <!-- Custom Target Grade Input -->
                            <div class="flex items-center gap-2 bg-slate-800/80 border border-slate-700 px-3 py-1.5 rounded-xl self-start sm:self-auto">
                                <label for="target-grade-input" class="text-xs text-slate-300 font-medium">Meta deseada:</label>
                                <input type="number" id="target-grade-input" step="0.1" min="1.0" max="7.0" value="4.0" onchange="updateTargetGrade(this.value)" class="w-14 bg-slate-900 border border-slate-600 rounded text-center text-sm font-bold text-white focus:outline-none focus:border-blue-400">
                            </div>
                        </div>

                        <!-- Result Display -->
                        <div id="target-result-container" class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4 pt-1">
                            <div class="space-y-1">
                                <div class="text-xs text-slate-400 font-medium">Nota requerida en el porcentaje restante:</div>
                                <div class="flex items-baseline gap-3">
                                    <span id="target-required-grade" class="text-3xl sm:text-4xl font-extrabold text-blue-400">--</span>
                                    <span id="target-status-tag" class="text-xs font-semibold px-2.5 py-1 rounded-full bg-slate-700 text-slate-300">Esperando notas</span>
                                </div>
                            </div>

                            <div id="target-advice-msg" class="text-xs text-slate-300 bg-slate-800/90 border border-slate-700/80 rounded-xl p-3 max-w-md">
                                Ingrese ponderaciones que no superen el 100% para proyectar la nota final requerida.
                            </div>
                        </div>
                    </div>

                    <!-- Action Bar -->
                    <div class="flex justify-between items-center pt-2">
                        <button onclick="deleteCurrentSubject()" class="text-xs font-semibold text-red-600 hover:text-red-700 hover:bg-red-50 px-3 py-2 rounded-lg transition flex items-center gap-1.5">
                            <i data-lucide="trash-2" class="w-4 h-4"></i> Eliminar este ramo
                        </button>
                    </div>

                </div>
            </div>

        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-white border-t border-slate-200 mt-auto py-4 text-center text-xs text-slate-400">
        <div class="max-w-7xl mx-auto px-4">
            Sistema optimizado para la Escala Académica Chilena (1.0 - 7.0) • Aprobar con 4.0
        </div>
    </footer>

    <!-- Modal Import / Export Data -->
    <div id="modal-data" class="fixed inset-0 bg-slate-900/40 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl max-w-md w-full p-6 shadow-xl space-y-4 border border-slate-100">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
                <h3 class="font-bold text-slate-800 text-base flex items-center gap-2">
                    <i data-lucide="database" class="w-5 h-5 text-blue-600"></i> Respaldar / Cargar Datos
                </h3>
                <button onclick="toggleModal('modal-data')" class="text-slate-400 hover:text-slate-600">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            
            <p class="text-xs text-slate-500">Puedes copiar este texto para guardar un respaldo o pegar un código guardado previamente.</p>
            
            <textarea id="json-data-area" rows="6" class="w-full text-xs font-mono p-3 bg-slate-50 border border-slate-200 rounded-xl focus:outline-none focus:border-blue-500" placeholder="Código JSON de respaldo..."></textarea>
            
            <div class="flex gap-2 pt-2">
                <button onclick="copyDataBackup()" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-semibold text-xs py-2.5 rounded-xl transition flex items-center justify-center gap-1.5">
                    <i data-lucide="copy" class="w-4 h-4"></i> Copiar Código
                </button>
                <button onclick="importDataBackup()" class="flex-1 bg-blue-600 hover:bg-blue-700 text-white font-semibold text-xs py-2.5 rounded-xl transition flex items-center justify-center gap-1.5">
                    <i data-lucide="download" class="w-4 h-4"></i> Cargar Datos
                </button>
            </div>
        </div>
    </div>

    <!-- Application Logic Script -->
    <script>
        // State Storage structure
        let appState = {
            activeSubjectId: null,
            subjects: []
        };

        const STORAGE_KEY = 'chile_academic_calc_v1';

        // Load data on startup
        window.onload = function() {
            loadStateFromStorage();
            if (appState.subjects.length === 0) {
                // Initial Default Data for Demo
                createDefaultData();
            } else if (!appState.activeSubjectId && appState.subjects.length > 0) {
                appState.activeSubjectId = appState.subjects[0].id;
            }
            renderApp();
            lucide.createIcons();
        };

        // Default Initial Demo
        function createDefaultData() {
            const defaultSubject = {
                id: 'sub_' + Date.now(),
                name: 'Cálculo I',
                globalWeight: 100,
                targetGrade: 4.0,
                evaluations: [
                    { id: 'eval_1', name: 'Certamen 1', grade: 4.5, weight: 30 },
                    { id: 'eval_2', name: 'Certamen 2', grade: 3.2, weight: 30 },
                    { id: 'eval_3', name: 'Tareas / Quizzes', grade: 5.8, weight: 15 }
                ]
            };
            appState.subjects.push(defaultSubject);
            appState.activeSubjectId = defaultSubject.id;
            saveStateToStorage();
        }

        // Local Storage Helpers
        function saveStateToStorage() {
            try {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(appState));
            } catch (e) {
                console.error('Error saving state:', e);
            }
        }

        function loadStateFromStorage() {
            try {
                const data = localStorage.getItem(STORAGE_KEY);
                if (data) {
                    appState = JSON.parse(data);
                }
            } catch (e) {
                console.error('Error loading state:', e);
            }
        }

        function resetAllData() {
            if (confirm('¿Estás seguro de que deseas eliminar todas las asignaturas y notas?')) {
                appState = { activeSubjectId: null, subjects: [] };
                saveStateToStorage();
                renderApp();
            }
        }

        // Chilean Rounding Rule: round to 1 decimal place standard
        function roundGrade(num) {
            if (num === null || num === undefined || isNaN(num)) return 0;
            return Math.round(num * 10) / 10;
        }

        // Color badge helper according to Chilean standard
        // Below 4.0: Red (Reprobado)
        // 4.0 - 4.9: Blue/Sky (Aprobado Suficiente)
        // 5.0 - 7.0: Emerald/Green (Buen Desempeño)
        function getGradeStyle(grade) {
            if (!grade || isNaN(grade)) {
                return {
                    textClass: 'text-slate-400',
                    bgClass: 'bg-slate-100 text-slate-600 border-slate-200',
                    label: 'Sin Notas'
                };
            }

            const rounded = roundGrade(grade);
            if (rounded < 4.0) {
                return {
                    textClass: 'text-red-600',
                    bgClass: 'bg-red-50 text-red-700 border-red-200',
                    label: 'Reprobando'
                };
            } else if (rounded >= 4.0 && rounded < 5.0) {
                return {
                    textClass: 'text-blue-600',
                    bgClass: 'bg-blue-50 text-blue-700 border-blue-200',
                    label: 'Aprobado'
                };
            } else {
                return {
                    textClass: 'text-emerald-600',
                    bgClass: 'bg-emerald-50 text-emerald-700 border-emerald-200',
                    label: 'Destacado'
                };
            }
        }

        // Compute Subject Average
        function calculateSubjectStats(subject) {
            if (!subject || !subject.evaluations || subject.evaluations.length === 0) {
                return { average: null, totalWeight: 0, pendingWeight: 100, earnedPoints: 0 };
            }

            let totalWeight = 0;
            let weightedSum = 0;

            subject.evaluations.forEach(ev => {
                const w = parseFloat(ev.weight) || 0;
                const g = parseFloat(ev.grade);
                totalWeight += w;

                if (!isNaN(g) && g > 0) {
                    weightedSum += g * (w / 100);
                }
            });

            const pendingWeight = Math.max(0, 100 - totalWeight);
            
            // Average calculated relative to current weighted sum if not 100% or absolute sum
            let currentAverage = totalWeight > 0 ? (weightedSum / (totalWeight / 100)) : 0;
            
            return {
                average: roundGrade(currentAverage),
                actualWeightedAverage: roundGrade(weightedSum), // raw weighted sum so far
                totalWeight: Math.round(totalWeight * 10) / 10,
                pendingWeight: Math.round(pendingWeight * 10) / 10,
                earnedPoints: weightedSum
            };
        }

        // Global Semester Average Calculation
        function calculateGlobalAverage() {
            if (appState.subjects.length === 0) return { globalAvg: 0, count: 0 };

            let totalGlobalWeight = 0;
            let sumWeightedGrades = 0;
            let validSubjectsCount = 0;

            appState.subjects.forEach(sub => {
                const stats = calculateSubjectStats(sub);
                const gw = parseFloat(sub.globalWeight) || 100;
                if (stats.average !== null && !isNaN(stats.average)) {
                    sumWeightedGrades += stats.average * gw;
                    totalGlobalWeight += gw;
                    validSubjectsCount++;
                }
            });

            if (totalGlobalWeight === 0) return { globalAvg: 0, count: 0 };

            const finalAvg = roundGrade(sumWeightedGrades / totalGlobalWeight);
            return { globalAvg: finalAvg, count: validSubjectsCount };
        }

        // Target Grade Calculator logic
        // Formula: (Target - EarnedPoints) / (RemainingWeight % / 100)
        function calculateNeededGrade(subject) {
            const stats = calculateSubjectStats(subject);
            const target = subject.targetGrade || 4.0;
            
            if (stats.totalWeight >= 100) {
                return { status: 'COMPLETE', gradeNeeded: null };
            }

            const remainingWeightFraction = (100 - stats.totalWeight) / 100;
            if (remainingWeightFraction <= 0) return { status: 'COMPLETE', gradeNeeded: null };

            // Required Grade formula
            const pointsNeeded = target - stats.earnedPoints;
            const requiredGrade = pointsNeeded / remainingWeightFraction;
            const roundedRequired = roundGrade(requiredGrade);

            if (requiredGrade > 7.0) {
                return { status: 'IMPOSSIBLE', gradeNeeded: roundedRequired, target };
            } else if (requiredGrade <= 1.0) {
                return { status: 'PASSED_ALREADY', gradeNeeded: 1.0, target };
            } else {
                return { status: 'POSSIBLE', gradeNeeded: roundedRequired, target };
            }
        }

        // UI RENDERERS
        function renderApp() {
            renderSidebar();
            renderSubjectDetail();
            renderGlobalStats();
            lucide.createIcons();
        }

        function renderGlobalStats() {
            const { globalAvg, count } = calculateGlobalAverage();
            const displayEl = document.getElementById('promedio-global-display');
            const badgeEl = document.getElementById('global-status-badge');
            const barEl = document.getElementById('global-progress-bar');
            const countBadge = document.getElementById('ramo-count-badge');

            countBadge.innerText = `${appState.subjects.length} Ramo${appState.subjects.length !== 1 ? 's' : ''}`;

            if (count === 0) {
                displayEl.innerText = '1.0';
                displayEl.className = 'text-4xl font-extrabold tracking-tight text-slate-300';
                badgeEl.innerText = 'Sin datos';
                badgeEl.className = 'px-3 py-1 text-xs font-bold rounded-full bg-slate-100 text-slate-500';
                barEl.style.width = '0%';
                return;
            }

            displayEl.innerText = globalAvg.toFixed(1);
            const style = getGradeStyle(globalAvg);
            
            displayEl.className = `text-4xl font-extrabold tracking-tight ${style.textClass}`;
            badgeEl.innerText = style.label;
            badgeEl.className = `px-3 py-1 text-xs font-bold rounded-full border ${style.bgClass}`;
            
            // Percentage bar calculation (scale 1 to 7)
            const percentage = Math.max(0, Math.min(100, ((globalAvg - 1) / 6) * 100));
            barEl.style.width = `${percentage}%`;
        }

        function renderSidebar() {
            const container = document.getElementById('subjects-list');
            container.innerHTML = '';

            if (appState.subjects.length === 0) {
                container.innerHTML = `
                    <div class="p-6 text-center text-xs text-slate-400">
                        No has registrado asignaturas aún.
                    </div>
                `;
                return;
            }

            appState.subjects.forEach(sub => {
                const stats = calculateSubjectStats(sub);
                const isActive = sub.id === appState.activeSubjectId;
                const style = getGradeStyle(stats.average);

                const item = document.createElement('div');
                item.className = `p-3.5 transition cursor-pointer flex items-center justify-between border-l-4 ${
                    isActive 
                        ? 'bg-blue-50/60 border-blue-600 font-semibold' 
                        : 'border-transparent hover:bg-slate-50 text-slate-700'
                }`;
                item.onclick = () => selectSubject(sub.id);

                item.innerHTML = `
                    <div class="overflow-hidden pr-2">
                        <div class="text-sm font-medium text-slate-900 truncate">${escapeHtml(sub.name || 'Sin Nombre')}</div>
                        <div class="text-xs text-slate-400 font-normal">Pond. ${sub.globalWeight || 100}% • ${stats.totalWeight}% eval.</div>
                    </div>
                    <div class="text-right flex-shrink-0">
                        <span class="text-base font-bold ${style.textClass}">${stats.average !== null ? stats.average.toFixed(1) : '-.-'}</span>
                    </div>
                `;
                container.appendChild(item);
            });
        }

        function renderSubjectDetail() {
            const noSubCard = document.getElementById('no-subject-selected');
            const subDetailCard = document.getElementById('subject-detail-card');

            const currentSub = appState.subjects.find(s => s.id === appState.activeSubjectId);

            if (!currentSub) {
                noSubCard.classList.remove('hidden');
                subDetailCard.classList.add('hidden');
                return;
            }

            noSubCard.classList.add('hidden');
            subDetailCard.classList.remove('hidden');

            // Header Inputs
            document.getElementById('subject-title-input').value = currentSub.name || '';
            document.getElementById('subject-global-weight-input').value = currentSub.globalWeight || 100;
            document.getElementById('target-grade-input').value = currentSub.targetGrade || 4.0;

            // Stats
            const stats = calculateSubjectStats(currentSub);
            const style = getGradeStyle(stats.average);

            const avgDisplay = document.getElementById('subject-average-display');
            avgDisplay.innerText = stats.average !== null ? stats.average.toFixed(1) : '1.0';
            avgDisplay.className = `text-2xl font-black ${style.textClass}`;

            const badgeDisplay = document.getElementById('subject-status-badge');
            badgeDisplay.innerText = style.label;
            badgeDisplay.className = `px-2.5 py-1 text-xs font-bold rounded-lg border ${style.bgClass}`;

            // Weight Progress
            const weightText = document.getElementById('weight-total-text');
            const weightBar = document.getElementById('weight-progress-bar');
            const weightWarning = document.getElementById('weight-warning-msg');
            const weightAlertIcon = document.getElementById('weight-alert-icon');

            weightText.innerText = `${stats.totalWeight}% de 100%`;
            weightBar.style.width = `${Math.min(100, stats.totalWeight)}%`;

            if (stats.totalWeight > 100) {
                weightBar.className = 'bg-red-500 h-full transition-all duration-300 rounded-full';
                weightWarning.classList.remove('hidden');
                weightAlertIcon.innerHTML = `<i data-lucide="alert-circle" class="w-4 h-4 text-red-500 inline"></i>`;
            } else if (stats.totalWeight === 100) {
                weightBar.className = 'bg-emerald-500 h-full transition-all duration-300 rounded-full';
                weightWarning.classList.add('hidden');
                weightAlertIcon.innerHTML = `<i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-500 inline"></i>`;
            } else {
                weightBar.className = 'bg-blue-600 h-full transition-all duration-300 rounded-full';
                weightWarning.classList.add('hidden');
                weightAlertIcon.innerHTML = ``;
            }

            // Render Evaluations Rows
            renderEvaluationsList(currentSub);

            // Render Target Calculator
            renderTargetCalculator(currentSub);
        }

        function renderEvaluationsList(subject) {
            const listContainer = document.getElementById('evaluations-list');
            listContainer.innerHTML = '';

            if (subject.evaluations.length === 0) {
                listContainer.innerHTML = `
                    <div class="text-center py-8 bg-slate-50 border border-dashed border-slate-200 rounded-xl">
                        <p class="text-xs text-slate-400">No has agregado evaluaciones a este ramo.</p>
                        <button onclick="addEvaluation()" class="mt-2 text-xs font-semibold text-blue-600 hover:underline">
                            + Agregar primera evaluación
                        </button>
                    </div>
                `;
                return;
            }

            subject.evaluations.forEach((ev, idx) => {
                const row = document.createElement('div');
                row.className = 'grid grid-cols-1 sm:grid-cols-12 gap-2 sm:gap-3 items-center p-2.5 sm:p-2 bg-white sm:bg-slate-50/50 hover:bg-slate-100/60 rounded-xl border border-slate-200/80 transition';

                const gradeStyle = getGradeStyle(parseFloat(ev.grade));

                row.innerHTML = `
                    <!-- Name -->
                    <div class="sm:col-span-5">
                        <input type="text" value="${escapeHtml(ev.name)}" onchange="updateEvaluation('${ev.id}', 'name', this.value)" placeholder="Ej: Certamen ${idx + 1}" class="w-full text-xs sm:text-sm font-medium text-slate-800 bg-transparent border-b sm:border-none border-slate-200 focus:outline-none focus:bg-white rounded px-2 py-1">
                    </div>

                    <!-- Grade & Weight Controls Container -->
                    <div class="grid grid-cols-2 sm:col-span-6 gap-2 items-center">
                        <!-- Grade -->
                        <div class="flex items-center justify-center">
                            <input type="number" step="0.1" min="1.0" max="7.0" value="${ev.grade !== null && ev.grade !== undefined ? ev.grade : ''}" onchange="updateEvaluation('${ev.id}', 'grade', this.value)" placeholder="1.0-7.0" class="w-20 text-center text-sm font-bold border rounded-lg px-2 py-1.5 focus:outline-none focus:ring-2 focus:ring-blue-500 ${gradeStyle.textClass} bg-white shadow-sm">
                        </div>

                        <!-- Weight -->
                        <div class="flex items-center justify-center gap-1">
                            <input type="number" min="0" max="100" value="${ev.weight !== null && ev.weight !== undefined ? ev.weight : ''}" onchange="updateEvaluation('${ev.id}', 'weight', this.value)" placeholder="%" class="w-16 text-center text-sm font-semibold text-slate-700 border border-slate-200 rounded-lg px-2 py-1.5 focus:outline-none focus:ring-2 focus:ring-blue-500 bg-white shadow-sm">
                            <span class="text-xs text-slate-400 font-bold">%</span>
                        </div>
                    </div>

                    <!-- Delete Button -->
                    <div class="sm:col-span-1 flex justify-end sm:justify-center">
                        <button onclick="deleteEvaluation('${ev.id}')" class="p-1.5 text-slate-400 hover:text-red-600 hover:bg-red-50 rounded-lg transition" title="Eliminar nota">
                            <i data-lucide="x" class="w-4 h-4"></i>
                        </button>
                    </div>
                `;
                listContainer.appendChild(row);
            });
        }

        function renderTargetCalculator(subject) {
            const stats = calculateSubjectStats(subject);
            const remainingWeight = Math.max(0, 100 - stats.totalWeight);
            
            document.getElementById('calc-remaining-weight').innerText = `${remainingWeight}%`;

            const calcResult = calculateNeededGrade(subject);
            const reqGradeEl = document.getElementById('target-required-grade');
            const statusTagEl = document.getElementById('target-status-tag');
            const adviceMsgEl = document.getElementById('target-advice-msg');

            if (stats.totalWeight >= 100) {
                reqGradeEl.innerText = '--';
                reqGradeEl.className = 'text-3xl sm:text-4xl font-extrabold text-slate-400';
                statusTagEl.innerText = '100% Completado';
                statusTagEl.className = 'text-xs font-semibold px-2.5 py-1 rounded-full bg-slate-700 text-slate-300';
                
                if (stats.average >= (subject.targetGrade || 4.0)) {
                    adviceMsgEl.innerHTML = `<span class="text-emerald-400 font-bold">¡Asignatura finalizada con éxito!</span> Has alcanzado un promedio final de <strong>${stats.average.toFixed(1)}</strong>.`;
                } else {
                    adviceMsgEl.innerHTML = `<span class="text-red-400 font-bold">Asignatura finalizada.</span> El promedio obtenido de <strong>${stats.average.toFixed(1)}</strong> no alcanzó la meta de ${subject.targetGrade || 4.0}.`;
                }
                return;
            }

            if (stats.totalWeight === 0) {
                reqGradeEl.innerText = (subject.targetGrade || 4.0).toFixed(1);
                reqGradeEl.className = 'text-3xl sm:text-4xl font-extrabold text-blue-400';
                statusTagEl.innerText = 'Pendiente';
                statusTagEl.className = 'text-xs font-semibold px-2.5 py-1 rounded-full bg-blue-900/60 text-blue-300 border border-blue-700/50';
                adviceMsgEl.innerText = `Ingresa tus primeras notas para proyectar el rendimiento requerido en el 100% restante.`;
                return;
            }

            switch (calcResult.status) {
                case 'POSSIBLE':
                    reqGradeEl.innerText = calcResult.gradeNeeded.toFixed(1);
                    const reqStyle = getGradeStyle(calcResult.gradeNeeded);
                    reqGradeEl.className = `text-3xl sm:text-4xl font-extrabold ${reqStyle.textClass.replace('text-red-600', 'text-red-400').replace('text-blue-600', 'text-blue-400').replace('text-emerald-600', 'text-emerald-400')}`;
                    statusTagEl.innerText = 'Alcanzable';
                    statusTagEl.className = 'text-xs font-semibold px-2.5 py-1 rounded-full bg-blue-900/60 text-blue-300 border border-blue-700/50';
                    adviceMsgEl.innerHTML = `Necesitas promediar un <strong>${calcResult.gradeNeeded.toFixed(1)}</strong> en el <strong>${remainingWeight}%</strong> restante para lograr tu meta de <strong>${calcResult.target.toFixed(1)}</strong>.`;
                    break;

                case 'PASSED_ALREADY':
                    reqGradeEl.innerText = '1.0';
                    reqGradeEl.className = 'text-3xl sm:text-4xl font-extrabold text-emerald-400';
                    statusTagEl.innerText = '¡Aprobado Asegurado!';
                    statusTagEl.className = 'text-xs font-semibold px-2.5 py-1 rounded-full bg-emerald-900/60 text-emerald-300 border border-emerald-700/50';
                    adviceMsgEl.innerHTML = `¡Felicidades! Ya acumulaste el puntaje suficiente para obtener al menos un <strong>${calcResult.target.toFixed(1)}</strong> incluso si obtienes un 1.0 en lo que falta.`;
                    break;

                case 'IMPOSSIBLE':
                    reqGradeEl.innerText = calcResult.gradeNeeded.toFixed(1);
                    reqGradeEl.className = 'text-3xl sm:text-4xl font-extrabold text-red-400';
                    statusTagEl.innerText = 'Fuera de Escala (>7.0)';
                    statusTagEl.className = 'text-xs font-semibold px-2.5 py-1 rounded-full bg-red-900/60 text-red-300 border border-red-700/50';
                    adviceMsgEl.innerHTML = `Matemáticamente requieres un <strong>${calcResult.gradeNeeded.toFixed(1)}</strong> en el <strong>${remainingWeight}%</strong> restante, lo cual supera la nota máxima (7.0).`;
                    break;
            }
        }

        // ACTION HANDLERS
        function selectSubject(id) {
            appState.activeSubjectId = id;
            saveStateToStorage();
            renderApp();
        }

        function addSubject() {
            const count = appState.subjects.length + 1;
            const newSub = {
                id: 'sub_' + Date.now(),
                name: `Asignatura ${count}`,
                globalWeight: 100,
                targetGrade: 4.0,
                evaluations: [
                    { id: 'eval_' + Date.now() + '_1', name: 'Certamen 1', grade: null, weight: 40 },
                    { id: 'eval_' + Date.now() + '_2', name: 'Certamen 2', grade: null, weight: 60 }
                ]
            };
            appState.subjects.push(newSub);
            appState.activeSubjectId = newSub.id;
            saveStateToStorage();
            renderApp();
        }

        function deleteCurrentSubject() {
            if (!appState.activeSubjectId) return;
            const currentSub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (confirm(`¿Deseas eliminar la asignatura "${currentSub.name}"?`)) {
                appState.subjects = appState.subjects.filter(s => s.id !== appState.activeSubjectId);
                appState.activeSubjectId = appState.subjects.length > 0 ? appState.subjects[0].id : null;
                saveStateToStorage();
                renderApp();
            }
        }

        function updateSubjectTitle(val) {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (sub) {
                sub.name = val;
                saveStateToStorage();
                renderSidebar();
            }
        }

        function updateSubjectGlobalWeight(val) {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (sub) {
                sub.globalWeight = Math.max(0, parseFloat(val) || 0);
                saveStateToStorage();
                renderApp();
            }
        }

        function updateTargetGrade(val) {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (sub) {
                let parsed = parseFloat(val);
                if (isNaN(parsed)) parsed = 4.0;
                sub.targetGrade = Math.max(1.0, Math.min(7.0, parsed));
                saveStateToStorage();
                renderSubjectDetail();
            }
        }

        function addEvaluation() {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (!sub) return;

            const stats = calculateSubjectStats(sub);
            const defaultWeight = Math.max(0, 100 - stats.totalWeight);

            const newEval = {
                id: 'eval_' + Date.now(),
                name: `Evaluación ${sub.evaluations.length + 1}`,
                grade: null,
                weight: defaultWeight > 0 ? defaultWeight : 10
            };

            sub.evaluations.push(newEval);
            saveStateToStorage();
            renderApp();
        }

        function updateEvaluation(evalId, key, value) {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (!sub) return;

            const targetEval = sub.evaluations.find(e => e.id === evalId);
            if (!targetEval) return;

            if (key === 'name') {
                targetEval.name = value;
            } else if (key === 'grade') {
                if (value === '' || value === null) {
                    targetEval.grade = null;
                } else {
                    let parsed = parseFloat(value);
                    if (!isNaN(parsed)) {
                        // Clamp between 1.0 and 7.0
                        parsed = Math.max(1.0, Math.min(7.0, parsed));
                        targetEval.grade = roundGrade(parsed);
                    }
                }
            } else if (key === 'weight') {
                let parsed = parseFloat(value);
                targetEval.weight = isNaN(parsed) ? 0 : Math.max(0, Math.min(100, parsed));
            }

            saveStateToStorage();
            renderApp();
        }

        function deleteEvaluation(evalId) {
            const sub = appState.subjects.find(s => s.id === appState.activeSubjectId);
            if (!sub) return;

            sub.evaluations = sub.evaluations.filter(e => e.id !== evalId);
            saveStateToStorage();
            renderApp();
        }

        // Backup Modal Helpers
        function toggleModal(modalId) {
            const modal = document.getElementById(modalId);
            if (modal.classList.contains('hidden')) {
                modal.classList.remove('hidden');
                if (modalId === 'modal-data') {
                    document.getElementById('json-data-area').value = JSON.stringify(appState, null, 2);
                }
            } else {
                modal.classList.add('hidden');
            }
        }

        function copyDataBackup() {
            const textarea = document.getElementById('json-data-area');
            textarea.select();
            document.execCommand('copy');
            alert('Código de respaldo copiado al portapapeles.');
        }

        function importDataBackup() {
            const textarea = document.getElementById('json-data-area');
            try {
                const parsed = JSON.parse(textarea.value);
                if (parsed && Array.isArray(parsed.subjects)) {
                    appState = parsed;
                    saveStateToStorage();
                    renderApp();
                    toggleModal('modal-data');
                    alert('Datos cargados correctamente.');
                } else {
                    alert('El formato del código introducido no es válido.');
                }
            } catch (e) {
                alert('Error al procesar el código JSON. Verifica el texto.');
            }
        }

        // Escape HTML Utility
        function escapeHtml(str) {
            return String(str)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;')
                .replace(/"/g, '&quot;')
                .replace(/'/g, '&#039;');
        }
    </script>
</body>
</html>
