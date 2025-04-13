import React, { useState } from "react";

const getRandomNumber = () => Math.floor(Math.random() * 9) + 1;

const getColor = (num) => (num % 2 === 0 ? "Green" : "Red");
const getSize = (num) => (num > 5 ? "Big" : num < 5 ? "Small" : "Neutral");

export default function SabAmirGame() {
  const [number, setNumber] = useState(null);
  const [history, setHistory] = useState([]);
  const [result, setResult] = useState({ size: "", color: "" });

  const handlePlay = () => {
    const newNumber = getRandomNumber();
    const newSize = getSize(newNumber);
    const newColor = getColor(newNumber);
    setNumber(newNumber);
    setResult({ size: newSize, color: newColor });
    setHistory([{ number: newNumber, size: newSize, color: newColor }, ...history]);
  };

  return (
    <div className="min-h-screen bg-gray-100 flex flex-col items-center p-4">
      <h1 className="text-3xl font-bold mb-4">Sab Amir - Colour Trading Game</h1>
      <button
        onClick={handlePlay}
        className="px-6 py-2 bg-blue-600 text-white rounded-2xl shadow-lg hover:bg-blue-700"
      >
        Play Round
      </button>

      {number && (
        <div className="mt-6 text-center">
          <p className="text-xl">Number: <strong>{number}</strong></p>
          <p className="text-lg">Size: <strong>{result.size}</strong></p>
          <p className="text-lg">Color: <strong>{result.color}</strong></p>
        </div>
      )}

      <div className="mt-10 w-full max-w-md">
        <h2 className="text-xl font-semibold mb-2">History</h2>
        <ul className="bg-white rounded-xl shadow-md p-4 space-y-2">
          {history.map((entry, index) => (
            <li key={index} className="border-b last:border-none pb-2">
              #{index + 1} - Number: <strong>{entry.number}</strong>,
              Size: <span className="font-medium">{entry.size}</span>,
              Color: <span className="font-medium">{entry.color}</span>
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
}
