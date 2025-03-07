'use client';
import { useState } from 'react';

export default function Home() {
    const [harga, setHarga] = useState('');
    const [output, setOutput] = useState('');

    const kiraSifatHarga = () => {
        let hargaValue = parseFloat(harga);
        let waveKecil, waveBesar, tp1, tp2, tp3;

        if (hargaValue >= 0.005 && hargaValue < 0.1) {
            waveKecil = 0.01; waveBesar = 0.02;
        } else if (hargaValue >= 0.1 && hargaValue <= 1.0) {
            waveKecil = 0.025; waveBesar = 0.05;
        } else {
            setOutput("Harga di luar julat yang disediakan.");
            return;
        }

        tp1 = hargaValue + waveBesar;
        tp2 = hargaValue + (2 * waveBesar);
        tp3 = hargaValue + (3 * waveBesar);

        setOutput(`1/2 Wave: RM${waveKecil.toFixed(3)}\n1 Wave: RM${waveBesar.toFixed(3)}\nTP1: RM${tp1.toFixed(3)}\nTP2: RM${tp2.toFixed(3)}\nTP3: RM${tp3.toFixed(3)}`);
    };

    return (
        <div className="flex flex-col items-center justify-center min-h-screen bg-gray-100 p-4">
            <div className="bg-white p-6 rounded-lg shadow-lg text-center max-w-md w-full">
                <h1 className="text-2xl font-bold mb-4">Kalkulator Sifat Harga</h1>
                <input
                    type="number"
                    className="w-full p-2 border border-gray-300 rounded-md mb-4"
                    placeholder="Masukkan Harga (contoh: 0.08)"
                    value={harga}
                    onChange={(e) => setHarga(e.target.value)}
                />
                <button 
                    className="w-full bg-green-500 text-white py-2 rounded-md hover:bg-green-600"
                    onClick={kiraSifatHarga}
                >
                    Kira
                </button>
                {output && <p className="mt-4 text-lg font-semibold whitespace-pre-line">{output}</p>}
            </div>
        </div>
    );
}
