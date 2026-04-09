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
