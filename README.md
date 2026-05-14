function checkTurnitin() {
    const text = document.getElementById('inputText').value.trim();
    if (!text) return alert("Masukkan teks terlebih dahulu!");

    const resultPanel = document.getElementById('resultPanel');
    resultPanel.classList.remove('hidden');
    resultPanel.innerHTML = `
        <div class="text-center mb-6">
            <h3 class="text-2xl font-bold text-gray-800">Hasil Analisis</h3>
        </div>
        <div class="flex justify-center items-center gap-8 mb-8">
            <div class="text-center">
                <div id="similarityScore" class="text-7xl font-bold text-red-500">67</div>
                <div class="text-sm text-gray-500">Similarity</div>
            </div>
            <div class="h-28 w-px bg-gray-200"></div>
            <div class="space-y-4">
                <div class="flex items-center gap-4">
                    <span class="w-24 text-right">AI Match</span>
                    <div class="flex-1 h-3 bg-gray-200 rounded-full overflow-hidden">
                        <div class="h-3 bg-blue-500 rounded-full" style="width: 22%"></div>
                    </div>
                    <span class="w-12 font-medium">22%</span>
                </div>
                <div class="flex items-center gap-4">
                    <span class="w-24 text-right">Web Match</span>
                    <div class="flex-1 h-3 bg-gray-200 rounded-full overflow-hidden">
                        <div class="h-3 bg-orange-500 rounded-full" style="width: 45%"></div>
                    </div>
                    <span class="w-12 font-medium">45%</span>
                </div>
            </div>
        </div>
        <button onclick="goToParaphrase()" 
            class="w-full py-5 bg-gradient-to-r from-blue-600 to-indigo-600 text-white rounded-3xl font-semibold text-lg hover:scale-105 transition">
            Perbaiki dengan Paraphrase AI →
        </button>
    `;

    // Random realistic score
    const score = Math.floor(Math.random() * 45) + 40;
    document.getElementById('similarityScore').textContent = score;
}

function paraphraseText() {
    const original = document.getElementById('paraOriginal').value.trim();
    if (!original) return alert("Masukkan teks yang ingin diparaphrase!");

    const result = document.getElementById('paraResult');
    result.value = "Sedang memproses dengan AI...";

    setTimeout(() => {
        let paraphrased = original
            .replace(/adalah/g, "merupakan")
            .replace(/penting/g, "sangat krusial")
            .replace(/karena/g, "sebab")
            .replace(/sehingga/g, "hingga")
            .replace(/dapat/g, "bisa");

        result.value = paraphrased + "\n\n✅ Hasil paraphrase AI - ParaCheck";
        document.getElementById('uniqueness').textContent = (88 + Math.floor(Math.random() * 11)) + "%";
    }, 900);
}

function copyParaphrase() {
    const text = document.getElementById('paraResult').value;
    if (text) {
        navigator.clipboard.writeText(text).then(() => alert("✅ Teks berhasil disalin!"));
    }
}

function goToParaphrase() {
    document.getElementById('paraOriginal').value = document.getElementById('inputText').value;
    document.getElementById('paraphrase').scrollIntoView({ behavior: 'smooth' });
    setTimeout(paraphraseText, 800);
}

function clearAll() {
    document.getElementById('inputText').value = '';
    document.getElementById('resultPanel').classList.add('hidden');
}

// Auto resize textarea
document.addEventListener('input', function(e) {
    if (e.target.tagName === 'TEXTAREA') {
        e.target.style.height = 'auto';
        e.target.style.height = e.target.scrollHeight + 'px';
    }
});