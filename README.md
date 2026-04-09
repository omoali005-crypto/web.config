# web.config
if ((newScore) % 5 === 0) {
  setLevel((prev) => prev + 1);
}

<p>Level: {level}</p>


<div
  id="coin"
  onClick={handleClick}
  style={{
    left: position.x,
    top: position.y,
    width: 50 - level * 3,
    height: 50 - level * 3,
  }}
></div>


 width: Math.max(20, 50 - level * 3),
height: Math.max(20, 50 - level * 3),
style={{
  left: position.x + "px",
  top: position.y + "px",
  width: (50 - level * 3) + "px",
  height: (50 - level * 3) + "px",
}}



const resetLevel = () => {
  setLevel(1);
};

<button onClick={resetLevel}>Reset Level</button>

