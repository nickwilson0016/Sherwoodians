import React, { useState, useEffect } from 'react';

// URLs for your single, combined CSV files.
// You MUST replace these with the actual URLs for each published tab.
const dataUrls = {
  standings: 'https://docs.google.com/spreadsheets/d/e/2PACX-1vTXmw29UZh_a-p13chTl3EUiUx1ll9NGD014qj7tVC0snPjuHcvLL_SqUIisuCE9ysRPwigIrepqnJ-/pub?gid=0&single=true&output=csv',
  draft: 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQxG8wUhQIo6uXePQPQfmvZS-h0eOhWOWGV3TSerYYVVrWlaW59cdLe9rB_OqIalxkzuiDfNAa_5Gmu/pub?gid=763323686&single=true&output=csv',
  transactions: 'https://docs.google.com/spreadsheets/d/e/2PACX-1vRu0Gxeepf1R4Upz0NjdfIKlziTDimChyiK3nW7KiSFKj-iqux5b3gk_I88TGJppYvHoW5XwhJuPND7/pub?gid=0&single=true&output=csv',
  playoff: 'https://docs.google.com/spreadsheets/d/e/2PACX-1vSAf3ZlRSnJcgtKB1tQa_YaJqnkOVNQYRiEUiI92domLwNVqdIYNenzDWEouPYiNu98RJ7pVz9s9ggQ/pub?gid=0&single=true&output=csv'
};

const Header = ({ title }) => (
  <header className="text-center mb-12">
    <h1 className="text-4xl md:text-6xl font-black text-transparent bg-clip-text bg-gradient-to-r from-[#FF4E50] via-[#FC913A] to-[#F9D423]">
      {title}
    </h1>
  </header>
);

const Navbar = ({ currentPage, onNavigate, onYearChange, years }) => (
  <nav className="flex flex-col md:flex-row items-center justify-between mb-8 p-4 bg-gray-800 rounded-lg shadow-2xl">
    <div className="flex space-x-4">
      {['Dashboard', 'Standings', 'Draft', 'Transactions'].map(page => (
        <button
          key={page}
          onClick={() => onNavigate(page)}
          className={`px-4 py-2 rounded-md font-medium transition-colors duration-200 ${
            currentPage === page
              ? 'bg-[#FF4E50] text-white shadow-lg'
              : 'text-gray-300 hover:text-white hover:bg-gray-700'
          }`}
        >
          {page}
        </button>
      ))}
    </div>
    <div className="mt-4 md:mt-0">
      <label htmlFor="year-select" className="font-bold mr-2 text-gray-300">
        Season:
      </label>
      <select
        id="year-select"
        onChange={onYearChange}
        className="p-2 bg-gray-700 border border-gray-600 rounded-md shadow-sm text-gray-200"
      >
        {years.map(year => (
          <option key={year} value={year}>
            {year}
          </option>
        ))}
      </select>
    </div>
  </nav>
);

const LoadingSpinner = () => (
  <div className="text-center text-xl text-gray-400 mt-12">
    <svg className="animate-spin h-8 w-8 text-gray-400 mx-auto" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
      <circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4"></circle>
      <path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
    </svg>
    <p className="mt-2">Loading data...</p>
  </div>
);

const TableSection = ({ title, headers, data }) => {
  return (
    <section className="bg-gray-800 rounded-lg shadow-2xl p-6 mb-8">
      <h2 className="text-3xl font-bold mb-4 text-[#F9D423]">{title}</h2>
      <div className="overflow-x-auto">
        <table className="min-w-full text-left">
          <thead className="bg-gray-700 text-gray-300">
            <tr>
              {headers.map((header, i) => (
                <th key={i} className="p-3">{header}</th>
              ))}
            </tr>
          </thead>
          <tbody className="bg-gray-800">
            {data.length > 0 ? (
              data.map((row, i) => (
                <tr key={i} className="border-b border-gray-700">
                  {headers.map((header, j) => (
                    <td key={j} className="p-3">{row[header]}</td>
                  ))}
                </tr>
              ))
            ) : (
              <tr>
                <td colSpan={headers.length} className="p-4 text-center text-gray-500">
                  No data available for this season.
                </td>
              </tr>
            )}
          </tbody>
        </table>
      </div>
    </section>
  );
};

const Dashboard = ({ data, year }) => (
  <div className="mt-8 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
    <div className="md:col-span-2 lg:col-span-3 bg-gray-800 rounded-lg shadow-2xl p-6">
      <h2 className="text-3xl font-bold mb-4 text-[#F9D423]">League Overview</h2>
      <p className="text-gray-300 mb-6">
        Welcome to the official league history! Explore the triumphs, heartbreaks, and legendary moments
        from each season. Use the navigation to dive into specific details.
      </p>
    </div>
    
    <div className="bg-gray-800 rounded-lg shadow-2xl p-6 text-center">
      <h3 className="font-bold text-lg mb-2 text-[#FC913A]">Total Teams</h3>
      <p className="text-5xl font-black text-white">{data.standings.length}</p>
    </div>

    {data.standings.length > 0 && (
      <div className="bg-gray-800 rounded-lg shadow-2xl p-6 text-center">
        <h3 className="font-bold text-lg mb-2 text-[#F9D423]">Season Champion</h3>
        <p className="text-2xl font-black text-white">{data.standings.find(s => s.Rank === '1')?.['Team Name']}</p>
        <p className="text-gray-400 mt-1">from the {year} season</p>
      </div>
    )}

    {data.standings.length > 0 && (
      <div className="bg-gray-800 rounded-lg shadow-2xl p-6 text-center">
        <h3 className="font-bold text-lg mb-2 text-[#FF4E50]">Highest Score</h3>
        <p className="text-2xl font-black text-white">{Math.max(...data.standings.map(s => parseFloat(s['Points For'])))}</p>
        <p className="text-gray-400 mt-1">Points For in {year}</p>
      </div>
    )}
  </div>
);

const StandingsPage = ({ data }) => (
  <TableSection title="Final Standings" headers={data.standings.headers} data={data.standings.data} />
);

const DraftPage = ({ data }) => (
  <TableSection title="Draft Results" headers={data.draft.headers} data={data.draft.data} />
);

const TransactionsPage = ({ data }) => (
  <TableSection title="Transactions" headers={data.transactions.headers} data={data.transactions.data} />
);

export default function App() {
  const [currentPage, setCurrentPage] = useState('Dashboard');
  const [selectedYear, setSelectedYear] = useState('2023');
  const [allData, setAllData] = useState({});
  const [loading, setLoading] = useState(true);

  const fetchAndParseCSV = async (url) => {
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error(`HTTP error! status: ${response.status}`);
      const text = await response.text();
      const rows = text.split('\n').map(row => row.split(','));
      const headers = rows[0].map(h => h.trim());
      const data = rows.slice(1).filter(row => row.length === headers.length && row.join('').trim() !== '').map(row => {
        const obj = {};
        headers.forEach((header, i) => {
          obj[header] = row[i]?.trim();
        });
        return obj;
      });
      return { headers, data };
    } catch (error) {
      console.error('Error fetching or parsing CSV:', error);
      return { headers: [], data: [] };
    }
  };

  useEffect(() => {
    const fetchData = async () => {
      setLoading(true);
      const [standingsResponse, draftResponse, transactionsResponse, playoffResponse] = await Promise.all([
        fetchAndParseCSV(dataUrls.standings),
        fetchAndParseCSV(dataUrls.draft),
        fetchAndParseCSV(dataUrls.transactions),
        fetchAndParseCSV(dataUrls.playoff)
      ]);
      setAllData({
        standings: standingsResponse.data,
        draft: draftResponse.data,
        transactions: transactionsResponse.data,
        playoff: playoffResponse.data,
        standingsHeaders: standingsResponse.headers,
        draftHeaders: draftResponse.headers,
        transactionsHeaders: transactionsResponse.headers,
        playoffHeaders: playoffResponse.headers,
      });
      setLoading(false);
    };
    fetchData();
  }, []);

  const years = Array.from(new Set(Object.values(allData).flatMap(arr => arr.map(item => item.Year)))).filter(Boolean).sort((a, b) => b - a);

  const renderContent = () => {
    if (loading) {
      return <LoadingSpinner />;
    }

    const filteredData = {
      standings: allData.standings.filter(row => row.Year === selectedYear),
      draft: allData.draft.filter(row => row.Year === selectedYear),
      transactions: allData.transactions.filter(row => row.Year === selectedYear),
      playoff: allData.playoff.filter(row => row.Year === selectedYear),
      standingsHeaders: allData.standingsHeaders,
      draftHeaders: allData.draftHeaders,
      transactionsHeaders: allData.transactionsHeaders,
      playoffHeaders: allData.playoffHeaders,
    };

    switch (currentPage) {
      case 'Standings':
        return <TableSection title="Final Standings" headers={filteredData.standingsHeaders} data={filteredData.standings} />;
      case 'Draft':
        return <TableSection title="Draft Results" headers={filteredData.draftHeaders} data={filteredData.draft} />;
      case 'Transactions':
        return <TableSection title="Transactions" headers={filteredData.transactionsHeaders} data={filteredData.transactions} />;
      case 'Dashboard':
      default:
        return <Dashboard data={filteredData} year={selectedYear} />;
    }
  };

  return (
    <div className="bg-gray-900 min-h-screen text-gray-200 p-4 sm:p-8">
      <div className="max-w-7xl mx-auto">
        <Header title="League Legacy Dashboard" />
        <Navbar 
          currentPage={currentPage}
          onNavigate={setCurrentPage}
          onYearChange={(e) => setSelectedYear(e.target.value)}
          years={years}
        />
        {renderContent()}
      </div>
    </div>
  );
}
