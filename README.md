


body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #1c1ce7;
    color: white;
}

#game-area {
    width: 400px;
    height: 400px;
    background-color: #2c2c44;
    margin: 20px auto;
    position: relative;
    border-radius: 10px;
}

#coin {
   
    background-color: gold;
    border-radius: 50%;
    position: absolute;
    cursor: pointer;
    transition: all 0.2s;
}

button {
    padding: 10px 20px;
    font-size: 16px;
    margin-top: 10px;
    border: none;
    border-radius: 5px;
    background-color: gold;
    cursor: pointer;
}




   import { useState, useEffect } from "react";
import "./App.css";

function App() {
  const [score, setScore] = useState(0);
  const [started, setStarted] = useState(false);
  const [level, setLevel] = useState(1);
  const [time, setTime] = useState(30);
  const [position, setPosition] = useState({ x: 0, y: 0 });
  const [gameOver, setGameOver] = useState(false);
  const [highscore, setHighscore] = useState(0);

  const moveCoin = () => {
    const maxX = 350;
    const maxY = 350;

    const randomX = Math.floor(Math.random() * maxX);
    const randomY = Math.floor(Math.random() * maxY);

    setPosition({ x: randomX, y: randomY });
  };

  const handleClick = () => {
    if (gameOver) return;

    const newScore = score + 1;
    setScore(newScore);

    if (newScore > highscore) {
      setHighscore(newScore);
    }

    if ((newScore) % 5 === 0) 
  setLevel((prev) => prev + 1);

    moveCoin();
  };

  useEffect(() => {
    if (gameOver) return;

    if (time === 0) {
      setGameOver(true);
      return;
    }

    const timer = setInterval(() => {
      setTime((prev) => prev - 1);
    }, 1000);

    return () => clearInterval(timer);
  }, [time, gameOver]);

  useEffect(() => {
    moveCoin();
  }, []);

const resetLevel = () => {
  setLevel(1);
};

const restartGame = () => {
  setScore(0);
  setTime(30);
  setGameOver(false);
  moveCoin();
};

  return (
    <div>
      <h1>🪙 Coin Clicker</h1>
      <p>Poeng: {score}</p>
      <p>Level: {level}</p>
      <p>Highscore: {highscore}</p>
      <p>Tid igjen: {time} sek</p>
    {!started && (
      <button onClick={() => setStarted(true)}>Start Game</button>
)}


      <div id="game-area">
        {started && !gameOver && (

          <div
            id="coin"
            onClick={handleClick}
            style={{
              left: position.x + "px",
              top: position.y + "px",
              width: `${Math.max(20, 50 - score * 3)}px`,
              height: `${Math.max(20, 50 - score * 3)}px`,
                backgroundColor: "red",



            }}
          ></div>
        )}
      </div>

      {gameOver && (
        <div>
          <h2>Game Over!</h2>
          <button onClick={restartGame}>Spill igjen</button>
        </div>
      )}
    </div>
  );
}

export default App;
