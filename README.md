import React, { useState, useEffect } from 'react';

const DeveloperAnimationWithStats = () => {
  const [showAnimation, setShowAnimation] = useState(true);
  const [animationFrame, setAnimationFrame] = useState(0);
  
  // Developer animation frames (simplified for demonstration)
  const developerFrames = [
    { transform: 'translateY(0px)' },
    { transform: 'translateY(-5px)' },
    { transform: 'translateY(-10px)' },
    { transform: 'translateY(-5px)' },
  ];
  
  // GitHub streak data (sample data)
  const streakData = {
    currentStreak: 42,
    longestStreak: 67,
    totalContributions: 852,
    lastYear: 512,
    averagePerWeek: 16.4
  };
  
  // Animation effect
  useEffect(() => {
    const timer = setInterval(() => {
      setAnimationFrame((prev) => (prev + 1) % developerFrames.length);
    }, 500);
    
    return () => clearInterval(timer);
  }, []);
  
  // Toggle between animation and stats
  const toggleView = () => {
    setShowAnimation(!showAnimation);
  };
  
  return (
    <div className="w-full p-6 bg-gray-900 rounded-lg shadow-lg overflow-hidden">
      <div className="flex flex-col items-center">
        <h2 className="text-2xl font-bold text-yellow-400 mb-6 text-center">
          {showAnimation ? "Developer Animation" : "GitHub Streak Stats"}
        </h2>
        
        <div className="w-full mb-6">
          <button 
            onClick={toggleView}
            className="px-4 py-2 bg-pink-600 text-white rounded-md hover:bg-pink-700 transition-all duration-300 mx-auto block"
          >
            {showAnimation ? "Show Stats" : "Show Animation"}
          </button>
        </div>
        
        {showAnimation ? (
          <div className="relative w-full h-64 flex justify-center items-center">
            <div 
              className="w-48 h-48 bg-gray-800 rounded-full flex items-center justify-center shadow-lg transition-all duration-500"
              style={developerFrames[animationFrame]}
            >
              <div className="relative">
                <div className="absolute -top-16 -left-16 w-80 h-80 opacity-20 rounded-full bg-gradient-to-r from-pink-500 to-yellow-500 animate-pulse"></div>
                <div className="relative z-10">
                  <svg className="w-32 h-32" viewBox="0 0 24 24" fill="none">
                    <path d="M12 16C14.2091 16 16 14.2091 16 12C16 9.79086 14.2091 8 12 8C9.79086 8 8 9.79086 8 12C8 14.2091 9.79086 16 12 16Z" fill="#F7D747" />
                    <path d="M18.5 5C17.12 5 16 6.12 16 7.5C16 8.88 17.12 10 18.5 10C19.88 10 21 8.88 21 7.5C21 6.12 19.88 5 18.5 5Z" fill="#F75C7E" />
                    <path d="M19 3H5C3.9 3 3 3.9 3 5V19C3 20.1 3.9 21 5 21H19C20.1 21 21 20.1 21 19V5C21 3.9 20.1 3 19 3ZM15 17L12 15L9 17L10 13.5L7 11H10.5L12 7.5L13.5 11H17L14 13.5L15 17Z" fill="#F0DB4F" />
                  </svg>
                  <div className="absolute top-0 left-0 w-full h-full flex items-center justify-center">
                    <div className="w-5 h-5 bg-pink-500 rounded-full animate-ping"></div>
                  </div>
                </div>
              </div>
            </div>
            
            {/* Code particles */}
            {[...Array(12)].map((_, i) => (
              <div 
                key={i}
                className="absolute w-2 h-2 bg-yellow-400 rounded-full opacity-60 animate-float"
                style={{
                  top: `${Math.random() * 100}%`,
                  left: `${Math.random() * 100}%`,
                  animationDelay: `${Math.random() * 5}s`,
                  animationDuration: `${3 + Math.random() * 7}s`
                }}
              />
            ))}
          </div>
        ) : (
          <div className="w-full bg-gray-800 rounded-lg p-6 shadow-xl border border-pink-500">
            <div className="grid grid-cols-2 gap-4">
              <div className="bg-gray-900 rounded-lg p-4 transform hover:scale-105 transition-all duration-300">
                <div className="text-pink-500 text-xl font-bold mb-2">Current Streak</div>
                <div className="text-yellow-400 text-3xl font-bold flex items-center">
                  {streakData.currentStreak} days
                  <span className="ml-2 text-pink-500">🔥</span>
                </div>
              </div>
              
              <div className="bg-gray-900 rounded-lg p-4 transform hover:scale-105 transition-all duration-300">
                <div className="text-pink-500 text-xl font-bold mb-2">Longest Streak</div>
                <div className="text-yellow-400 text-3xl font-bold flex items-center">
                  {streakData.longestStreak} days
                  <span className="ml-2 text-pink-500">⚡</span>
                </div>
              </div>
              
              <div className="bg-gray-900 rounded-lg p-4 transform hover:scale-105 transition-all duration-300">
                <div className="text-pink-500 text-xl font-bold mb-2">Total Contributions</div>
                <div className="text-yellow-400 text-3xl font-bold flex items-center">
                  {streakData.totalContributions}
                  <span className="ml-2 text-pink-500">📊</span>
                </div>
              </div>
              
              <div className="bg-gray-900 rounded-lg p-4 transform hover:scale-105 transition-all duration-300">
                <div className="text-pink-500 text-xl font-bold mb-2">Average Per