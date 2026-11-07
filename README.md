'use client';

import { useState } from 'react';

// 模擬寵物資料 (未來可替換為資料庫 API)
const mockPet = {
  name: '豆豆 (Bean)',
  species: '黃金獵犬',
  birthDate: '2014-05-20',
  passedDate: '2026-03-18',
  avatarUrl: 'https://images.unsplash.com/photo-1552053831-71594a27632d?auto=format&fit=crop&q=80&w=800',
  epitaph: '謝謝你用一生的時間陪伴我們，帶給我們無數的溫暖與快樂。你永遠是家裡最棒的孩子，彩虹橋上自由奔跑吧！',
  candleCount: 128,
  flowerCount: 64,
  timeline: [
    {
      date: '2026 年 3 月',
      title: '安詳地去往彩虹橋',
      description: '在溫暖的陽光下靜靜睡著了，全家人都陪在身邊。',
      image: 'https://images.unsplash.com/photo-1537151608828-ea2b11777ee8?auto=format&fit=crop&q=80&w=600',
    },
    {
      date: '2020 年 8 月',
      title: '第一次海邊大冒險',
      description: '興奮地在浪花裡踩水，踩得全身是沙，但笑得比誰都開心。',
      image: 'https://images.unsplash.com/photo-1507146426996-ef05306b995a?auto=format&fit=crop&q=80&w=600',
    },
    {
      date: '2014 年 5 月',
      title: '來到我們家的第一天',
      description: '那時候只有巴掌大，怯生生地躲在沙發底下。',
      image: 'https://images.unsplash.com/photo-1543466835-00a7907e9de1?auto=format&fit=crop&q=80&w=600',
    },
  ],
};

export default function PetMemorialPage() {
  const [candles, setCandles] = useState(mockPet.candleCount);
  const [flowers, setFlowers] = useState(mockPet.flowerCount);
  const [hasLit, setHasLit] = useState(false);
  const [hasGivenFlower, setHasGivenFlower] = useState(false);

  // 計算陪伴天數
  const calculateDays = (start: string, end: string) => {
    const startDate = new Date(start);
    const endDate = new Date(end);
    const diffTime = Math.abs(endDate.getTime() - startDate.getTime());
    return Math.ceil(diffTime / (1000 * 60 * 60 * 24));
  };

  const daysTogether = calculateDays(mockPet.birthDate, mockPet.passedDate);

  return (
    <div className="min-h-screen bg-[#FAF6F0] text-[#5A4D41] pb-16 font-sans">
      {/* 頂部導覽列 */}
      <header className="flex justify-between items-center px-6 py-4 max-w-2xl mx-auto">
        <span className="text-sm tracking-widest text-[#8C7A6B] font-medium">PET MEMORIAL</span>
        <button 
          onClick={() => alert('已複製紀念頁面連結！')}
          className="text-xs bg-[#EADBC8] hover:bg-[#DBCAB5] text-[#5A4D41] px-3 py-1.5 rounded-full transition"
        >
          分享連結 🔗
        </button>
      </header>

      <main className="max-w-2xl mx-auto px-4">
        {/* 寵物主資訊卡片 */}
        <div className="bg-white/80 backdrop-blur-sm rounded-3xl p-6 shadow-sm border border-[#F0E5D8] text-center my-4">
          <div className="relative w-32 h-32 mx-auto mb-4">
            <img
              src={mockPet.avatarUrl}
              alt={mockPet.name}
              className="w-full h-full object-cover rounded-full shadow-md border-4 border-white"
            />
            <span className="absolute bottom-0 right-1 bg-[#EADBC8] text-xs px-2 py-0.5 rounded-full shadow">
              🐾
            </span>
          </div>

          <h1 className="text-2xl font-bold text-[#4A3E3D] mb-1">{mockPet.name}</h1>
          <p className="text-xs text-[#8C7A6B] tracking-wide mb-3">
            {mockPet.birthDate} — {mockPet.passedDate}
          </p>

          <div className="inline-block bg-[#F5EBE0] text-[#795239] text-xs px-4 py-1.5 rounded-full font-medium mb-4">
            溫馨陪伴了 <span className="font-bold text-[#A75D5D]">{daysTogether.toLocaleString()}</span> 個日夜
          </div>

          <p className="text-sm leading-relaxed text-[#6E5D4F] italic px-4">
            「{mockPet.epitaph}」
          </p>
        </div>

        {/* 虛擬追思互動區 */}
        <div className="flex gap-4 my-6">
          <button
            onClick={() => {
              if (!hasLit) {
                setCandles(candles + 1);
                setHasLit(true);
              }
            }}
            className={`flex-1 py-3 px-4 rounded-2xl flex items-center justify-center gap-2 transition shadow-sm font-medium text-sm ${
              hasLit 
                ? 'bg-[#EADBC8] text-[#5A4D41] cursor-default' 
                : 'bg-white hover:bg-[#F5EBE0] text-[#5A4D41] border border-[#F0E5D8]'
            }`}
          >
            <span>🕯️</span>
            <span>{hasLit ? '已點燃蠟燭' : '點燃蠟燭'}</span>
            <span className="bg-[#FAF6F0] px-2 py-0.5 rounded-full text-xs text-[#8C7A6B]">
              {candles}
            </span>
          </button>

          <button
            onClick={() => {
              if (!hasGivenFlower) {
                setFlowers(flowers + 1);
                setHasGivenFlower(true);
              }
            }}
            className={`flex-1 py-3 px-4 rounded-2xl flex items-center justify-center gap-2 transition shadow-sm font-medium text-sm ${
              hasGivenFlower 
                ? 'bg-[#EADBC8] text-[#5A4D41] cursor-default' 
                : 'bg-white hover:bg-[#F5EBE0] text-[#5A4D41] border border-[#F0E5D8]'
            }`}
          >
            <span>🌸</span>
            <span>{hasGivenFlower ? '已獻上鮮花' : '獻上鮮花'}</span>
            <span className="bg-[#FAF6F0] px-2 py-0.5 rounded-full text-xs text-[#8C7A6B]">
              {flowers}
            </span>
          </button>
        </div>

        {/* 時光軸內容區 */}
        <div className="bg-white/80 backdrop-blur-sm rounded-3xl p-6 shadow-sm border border-[#F0E5D8] mb-6">
          <h2 className="text-base font-bold text-[#4A3E3D] mb-6 flex items-center gap-2">
            <span>✨</span> 時光回憶錄
          </h2>

          <div className="space-y-8 relative before:absolute before:inset-0 before:left-3 before:w-0.5 before:bg-[#EADBC8]">
            {mockPet.timeline.map((item, index) => (
              <div key={index} className="relative pl-8">
                {/* 節點圓點 */}
                <div className="absolute left-1.5 top-1.5 -translate-x-1/2 w-3 h-3 rounded-full bg-[#C8AE7D] border-2 border-white"></div>
                
                <span className="text-xs text-[#8C7A6B] font-medium block mb-1">
                  {item.date}
                </span>
                <h3 className="text-sm font-bold text-[#4A3E3D] mb-1">
                  {item.title}
                </h3>
                <p className="text-xs leading-relaxed text-[#6E5D4F] mb-3">
                  {item.description}
                </p>
                {item.image && (
                  <img
                    src={item.image}
                    alt={item.title}
                    className="w-full h-44 object-cover rounded-xl border border-[#F0E5D8]"
                  />
                )}
              </div>
            ))}
          </div>
        </div>

        {/* 追思留言區 */}
        <div className="bg-white/80 backdrop-blur-sm rounded-3xl p-6 shadow-sm border border-[#F0E5D8]">
          <h2 className="text-base font-bold text-[#4A3E3D] mb-4 flex items-center gap-2">
            <span>💬</span> 寫下追思祝福
          </h2>
          <textarea
            placeholder={`寫下想對 ${mockPet.name} 說的話...`}
            rows={3}
            className="w-full p-3 text-xs rounded-xl bg-[#FAF6F0] border border-[#EADBC8] focus:outline-none focus:ring-1 focus:ring-[#C8AE7D] text-[#5A4D41]"
          />
          <button className="mt-2 w-full py-2.5 bg-[#C8AE7D] hover:bg-[#B69A67] text-white text-xs font-medium rounded-xl transition">
            送出留言
          </button>
        </div>
      </main>
    </div>
  );
}
