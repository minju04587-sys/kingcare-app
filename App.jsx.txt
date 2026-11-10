mport React, { useState } from 'react';
import { Wrench, ShieldCheck, Calendar, Phone, Star, User, MapPin, CheckCircle, Clock, FileText, Plus } from 'lucide-react';

export default function App() {
  const [view, setView] = useState('customer');
  const [selectedService, setSelectedService] = useState('cleaning');
  const [requestSubmitted, setRequestSubmitted] = useState(false);
  const [activeTab, setActiveTab] = useState('request');
  
  const [requests, setRequests] = useState([
    { id: 1, type: '천장형 시스템 에어컨 세척', customer: '김철수', area: '서울 강남구', status: '대기 중', price: '80,000원' },
    { id: 2, type: '가정용 벽걸이 설치', customer: '영희', area: '경기 성남시', status: '진행 중', price: '120,000원' }
  ]);

  return (
    <div className="min-h-screen bg-gray-50 text-gray-800 font-sans pb-12">
      <header className="bg-blue-600 text-white p-4 shadow-md flex justify-between items-center">
        <h1 className="text-xl font-bold flex items-center gap-2">
          <Wrench className="w-6 h-6" /> 킹케어 (KingCare)
        </h1>
        <div className="flex bg-blue-700 p-1 rounded-lg text-sm">
          <button 
            onClick={() => setView('customer')} 
            className={`px-3 py-1 rounded-md transition ${view === 'customer' ? 'bg-white text-blue-600 font-bold' : 'text-white'}`}>
            고객용
          </button>
          <button 
            onClick={() => setView('expert')} 
            className={`px-3 py-1 rounded-md transition ${view === 'expert' ? 'bg-white text-blue-600 font-bold' : 'text-white'}`}>
            기사님용
          </button>
        </div>
      </header>

      <main className="max-w-md mx-auto p-4">
        {view === 'customer' ? (
          <div className="space-y-4">
            <div className="bg-white p-4 rounded-xl shadow-sm border border-gray-100">
              <h2 className="text-lg font-bold mb-3 text-gray-900">어떤 서비스가 필요하세요?</h2>
              <div className="grid grid-cols-3 gap-2 mb-4">
                {['세척', '설치', 'A/S'].map((srv) => (
                  <button 
                    key={srv}
                    onClick={() => setSelectedService(srv)}
                    className={`p-3 rounded-lg border text-sm font-semibold transition ${selectedService === srv ? 'border-blue-600 bg-blue-50 text-blue-600' : 'border-gray-200 text-gray-600'}`}
                  >
                    {srv}
                  </button>
                ))}
              </div>

              <div className="space-y-3">
                <div>
                  <label className="text-xs font-bold text-gray-500">에어컨 종류</label>
                  <select className="w-full mt-1 p-2 border rounded-lg text-sm bg-white">
                    <option>가정용 벽걸이 / 스탠드</option>
                    <option>천장형 1WAY 시스템</option>
                    <option>천장형 4WAY 시스템</option>
                  </select>
                </div>
                <div>
                  <label className="text-xs font-bold text-gray-500">지역 선택</label>
                  <input type="text" placeholder="예: 서울시 강남구" className="w-full mt-1 p-2 border rounded-lg text-sm" defaultValue="서울시 강남구 역삼동" />
                </div>
              </div>

              <button 
                onClick={() => setRequestSubmitted(true)}
                className="w-full mt-4 bg-blue-600 text-white py-3 rounded-xl font-bold shadow-md hover:bg-blue-700 transition"
              >
                견적 요청 및 전문가 매칭하기
              </button>
            </div>

            {requestSubmitted && (
              <div className="bg-green-50 border border-green-200 p-4 rounded-xl text-center space-y-2">
                <CheckCircle className="w-8 h-8 text-green-600 mx-auto" />
                <h3 className="font-bold text-green-800">견적 요청이 완료되었습니다!</h3>
                <p className="text-xs text-green-600">주변 전문 기사님들이 실시간 견적을 비교하고 있습니다.</p>
              </div>
            )}
          </div>
        ) : (
          <div className="space-y-4">
            <div className="bg-white p-4 rounded-xl shadow-sm border border-gray-100 flex justify-between items-center">
              <div>
                <p className="text-xs text-gray-500">홍길동 기사님 환영합니다</p>
                <h2 className="text-lg font-bold text-gray-900">실시간 오더 마켓</h2>
              </div>
              <span className="bg-blue-100 text-blue-700 text-xs px-2 py-1 rounded-full font-bold">인증 파트너</span>
            </div>

            <div className="space-y-3">
              {requests.map((req) => (
                <div key={req.id} className="bg-white p-4 rounded-xl shadow-sm border border-gray-100 space-y-2">
                  <div className="flex justify-between items-start">
                    <span className="text-xs font-bold bg-gray-100 text-gray-600 px-2 py-0.5 rounded">{req.area}</span>
                    <span className="text-blue-600 font-bold text-sm">{req.price}</span>
                  </div>
                  <h3 className="font-bold text-gray-800">{req.type}</h3>
                  <p className="text-xs text-gray-500">고객명: {req.customer}</p>
                  <button 
                    onClick={() => alert('오더가 수락되었습니다! 고객님과 연락이 연결됩니다.')}
                    className="w-full mt-2 bg-slate-900 text-white py-2 rounded-lg text-sm font-bold hover:bg-slate-800 transition"
                  >
                    오더 수락하기
                  </button>
                </div>
              ))}
            </div>
          </div>
        )}
      </main>
    </div>
  );
}
